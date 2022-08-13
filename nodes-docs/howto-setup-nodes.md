# Setup Totem KAPEX Nodes on VPS

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
# * prometheus port on the parachain node
ufw allow 9615
# * prometheus port on the relachain node
ufw allow 9616

# check the setup
ufw status numbered
```

### Nginx

Two different use cases exist for using nginx as a reverse proxy. The following links provide that information:

[nginx for bootnodes](node-docs/howto-nginx-bootnodes.md)

[nginx for ui/rpc](node-docs/howto-nginx-uirpcnodes.md)

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
# apply it to the user you created earlier
sudo usermod -aG docker <a-username>
newgrp docker
# check all is running well
docker run hello-world
```

At this point the server should be shutdown and restarted:

    shutdown -r now

You can now login as the user you created earlier using `ssh`. 

> **Note** you may be prompted for a password, but this option should be switched off, once you are certain your config is completed. See this article for [Linux passwordless login](https://linuxize.com/post/how-to-setup-passwordless-ssh-login/)

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

Choose the commands to add into this file dependent on the type of node you are creating:

[Commands for docker Bootnode](nodes.docs/howto-docker-bootnode.md)
[Commands for docker UI RPC node](nodes.docs/howto-docker-uirpcnode.md)
[Commands for docker Collator node](nodes.docs/howto-docker-collatornode.md)
[Commands for docker Archival node](nodes.docs/howto-docker-archivenode.md)
[Commands for docker Simple Full node](nodes.docs/howto-docker-simplenode.md)

### Crontab

Crontab ensures that your image restarts after your server is restarted. This can also happen if your VPS provider shuts down your instance for maintenance.

    crontab -e

Add the following line using the `username` you created earlier to define the directory path. 

```
    # Note crontab is user specific!
    @reboot cd /home/<a-username>; screen -dmS parachain ./start.sh
```

This will start the node in a `screen` instance call `parachain`.

### Final consideration

It is possible that your node comes under DOS attack. There are no easy ways to prevent this, however a combination of firewall, and Fail2Ban may help.

#### Install Fail2ban

`Fail2ban` is a common way to limit the impact of attacks on your server. This is not the most friendly utility to use of manage.

    sudo apt-get update && \
    sudo apt-get upgrade && \
    sudo apt-get install -y fail2ban && \
    sudo systemctl start fail2ban && \
    sudo systemctl enable fail2ban && \
    sudo nano /etc/fail2ban/jail.local

add the following lines

```shell 
    [sshd]
    enabled = true
    port = 22
    filter = sshd
    logpath = /var/log/auth.log
    maxretry = 3
```

    sudo systemctl restart fail2ban

#### Fail2ban Commands

https://www.fail2ban.org/wiki/index.php/Commands

    fail2ban-client <commands>
    fail2ban-client help
    fail2ban-client reload
    fail2ban-client start
    fail2ban-client stop
    fail2ban-client status

#### view logs
    tail /etc/fail2ban/jail.local
    tail /var/log/auth.log

#### Monitoring Fail2ban

https://www.the-art-of-web.com/system/fail2ban-log/

For this you will need to install logresolve

    apt install apache2-utils

https://askubuntu.com/questions/1080056/is-my-server-under-attack
    
#### Reset Banned IP

https://serverfault.com/questions/285256/how-to-unban-an-ip-properly-with-fail2ban