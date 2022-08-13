# Nginx setup for Bootnodes

Nginx has several important features in this context, but it is only used with this bootnode type for directing connections to the parachain using a domain name. This is optional however and it need not be used if your boot node is going to be identified by its `IP` address.

Since we are setting up a bootnode that uses a FQDN its `Multiaddr` as specified in the parachain `chain_spec.json` file will look something like this:

    /dns4/k-boot-1.kapex.network/tcp/41333/ws/p2p/12D3KooWAyVMvqR9zpu3ri6SAFQewfQegrQ2iMSx8UsmXeixxCZo

To add your bootnode to the `chain_spec.json` file create an issue in this repo and a pull request.

The bootnode networking features will apply only to the Parachain section of the parachain node because the relaychain section is already configured. These are:

1) Allowing multiplex communication in libp2p

    * see [Libp2p Hole Punching Max Inden @ FOSDEM](https://youtu.be/pSXlpKlZX7I)

    * also worth seeing [Explainer on UDP/Quic used by Libp2p](https://youtu.be/cdb7M37o9sU)

2) Speeds up the node discovery process

3) Allowing for persistant connections between peers, i.e. prevents sudden node disconnection when dialing

5) Allows information about other nodes to be shared with connecting nodes

```shell
# Install nginx - this is only partially used
apt install nginx
````

Create a `streams-enabled` directory and add a config file:

```
cd /etc/nginx
mkdir -p streams-enabled
cd streams-enabled
nano your-config-filename.conf
```

Add the following into the file and save.

```
server {
    listen               0.0.0.0:41333;
    proxy_pass           127.0.0.1:30333;
}
```

This code listens for parachain connections on port `41333` on the `host`, and forwards to port `30333` on `localhost`. 

Later we will configure the docker container to listen to port `30333` on `localhost` and forward to the parachain port inside the container.

Edit the nginx config file to use the config

    cd ../
    nano nginx.conf

The following is the minimal configuration that is needed inside `nginx.conf`file. 

**IMPORTANT NOTE:** the `stream` directive is used, and `http` is not used because we recommend that the server is not used for any other services (for example a web server).

You should comment the `http` directive in the default `nginx.conf` file or just delete it altogether.

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