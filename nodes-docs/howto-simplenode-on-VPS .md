# Setup Bootnode on VPS

The setup was performed on Linux Ubuntu 22.04

Upon initial creation of the droplet/server you must remove any user with the `UID=1000` as this conflicts with the Docker container permissions. Usually if one exists it is a user called `ubuntu` with this `UID`.

It is assumed that as this is a fresh system creation and you are already loged in as a root user. If not then switch to the root user with `sudo su`. 

```shell
# check for user with UID 1000
nano /etc/passwd

# delete ubuntu guest user if necessary
deluser --remove-home ubuntu

# create a new user
adduser <a-username>

# skip entering details, and add initial password when prompted
# make the user a admin
usermod -aG sudo <a-username>

```

## Install other components

### Firewall

```shell
# update package manager
apt update

#Install UFW Firewall
apt-get install ufw

#start the firewall
ufw enable

# allow ssh login (port 22)
ufw allow ssh

# allow p2p on the parachain node (do not use port 30333!)
ufw allow 41333

# allow p2p on the relaychain node
ufw allow 4O333

# you can add other optional ports:
#prometheus on the parachain node
ufw allow 9615
#prometheus on the relachain node
ufw allow 9616

# check the setup
ufw status numbered
```

### nginx

Nginx has several important features in this context, but it is not used in this setup "everywhere".

It is required because we are setting up a bootnode that uses a FQDN in it's `Multiaddr` as specified in the parachain `chain_spec.json` file.

    /dns4/k-boot-1.kapex.network/tcp/41333/ws/p2p/12D3KooWAyVMvqR9zpu3ri6SAFQewfQegrQ2iMSx8UsmXeixxCZo

These are the features that will apply only to the Parachain section of the parachain node:

1) Allows by-directional communication in libp2p

    * see [Libp2p Hole Punching Max Inden @ FOSDEM](https://youtu.be/pSXlpKlZX7I)

    * also worth seeing [Explainer on UDP/Quic used by Libp2p](https://youtu.be/cdb7M37o9sU)

2) It speeds up the node discovery process

3) Allows for persistant connections between peers

4) prevents sudden node disconnection when dialing

5) Allows information about other nodes to be shared with connecting nodes

```shell
# Install nginx - this is only partially used
apt install nginx
````

Create a `streams-enabled` directory and add a config file
```
cd /etc/nginx
mkdir -p streams-enabled
cd streams-enabled
nano your-config-filename.conf
```
Add the following into the file and save.
This code listens for parachain connections on port `41333` on the `host`, and forwards to port `30333` on `localhost`. Later we will configure the docker container to listen to port `30333` on `localhost` and forward to the parachain port inside the container.
```
server {
    listen               0.0.0.0:41333;
    proxy_pass           127.0.0.1:30333;
}
```
Edit the nginx config file to use the config

    cd ../
    nano nginx.conf

The following is the minimal configuration that is needed inside `nginx.conf`file. 

**IMPORTANT NOTE:** the `stream` directive is used, and `http` is not used because we recommend that the server is not used for any other services for example like a web server.

You should comment the `http` directive in the default `nginx.conf` file. 
```
user www-data;
worker_processes auto;
pid /run/nginx.pid;
include /etc/nginx/modules-enabled/*.conf;

stream {
  include streams-enabled/*;
}

events {
        worker_connections 768;
        # multi_accept on;
}
```
Check that nginx has been configured properly
    
    nginx -t

Start nginx
    
    service nginx start

### Docker installation 
In the this section we install docker. 

Although it can be installed from SNAP in Ubuntu 22.04, we recommend doing this manually to cover all the steps.

```shell
# this script can be run at once
sudo apt-get remove docker docker-engine docker.io containerd runc && \
sudo apt-get update && \
sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg \
lsb-release && \
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg && \
echo \
"deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
$(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null && \
sudo apt-get update && \
sudo apt-get install docker-ce docker-ce-cli containerd.io && \
docker run hello-world
```

There are some follow-up steps:
```shell
# create the docker group
sudo groupadd docker
# apply it to the user you created
sudo usermod -aG docker <a-username>
newgrp docker
# check all is running well
docker run hello-world
```

At this point the server should be shutdown and restarted:

    shutdown -r now

You can now login as the user you created earlier.

### Setting up and running the node


```shell
# Create a directory to hold your chain data:
mkdir -p data
cd data

nano node-key
# paste your node key in hex format here. note do not have a new line and do not prefix the hex value with `0x`
# save and close
```
Create a file to start your chain

    nano start.sh

Add the following commands
```
docker run \
-it \
-p 127.0.0.1:30333:30333 \
-p 0.0.0.0:40333:40333 \
-p 0.0.0.0:9615:9615 \
-p 0.0.0.0:9616:9616 \
--rm \
--name k-boot-1 \
--pull=always \
-v="/$(pwd)/data:/data" \
totemlive/totem-parachain-collator:v1.1.0-release \
--chain kapex \
--execution=wasm \
--state-cache-size=1 \
--name "k-boot-1" \
--port 30333 \
--node-key-file /data/node-key \
--node-key-type "ed25519" \
--prometheus-external \
--prometheus-port 9615 \
-- \
--chain polkadot \
--port 40333 \
--prometheus-external \
--prometheus-port 9616
```
Note that the use of `--rm` argument is optional, and could be replaced by `--restart unless-stopped`, however the downside of this command is that the container must be manually stoped and removed even if the script is stopped - in other words after each time that the container is stopped. Wherease `--rm` will remove it automatically.



Make the `start.sh` file executable

    chmod u+x start.sh

#### Errors
If you get the error when trying to stop a container `Error response from daemon: cannot stop container:` execute the following command from the user that is running the container

    sudo aa-remove-unknown

### Crontab

Crontab ensures that your image restarts after VPS maintenance where your provider shuts down your instance for example.

    crontab -e

Add the following line using the `username` you created earlier to define the directory path. 

```
    # Note crontab is user specific!
    @reboot cd /home/<a-username>; screen -dmS parachain ./start.sh
```

This will start the node in a screen instance call `parachain`.