# Nginx setup for Bootnodes

### Nginx is used with this bootnode type for directing connections to the parachain using a domain name. 

The bootnode networking features will apply only to the Parachain section of the parachain node because the relaychain section is pre-configured. The features are:

1) Allowing multiplex communication in libp2p

    * see [Libp2p Hole Punching Max Inden @ FOSDEM](https://youtu.be/pSXlpKlZX7I)

    * also worth seeing [Explainer on UDP/Quic used by Libp2p](https://youtu.be/cdb7M37o9sU)

2) Speeds up the node discovery process

3) Allowing for persistant connections between peers, i.e. prevents sudden node disconnection when dialing

5) Allows information about other nodes to be shared with connecting nodes

If you are setting up a bootnode, please create an issue and a pull request on the [totem-parachains Github repo](https://github.com/totem-tech/totem-parachains) to have your bootnode added to the [Kapex chain specification file](https://github.com/totem-tech/totem-parachains/blob/main/res/kapex/kapex-parachain-readable.json).

## Setup

Since we are setting up a bootnode that uses a Fully Qualified Domain Name (FQDN) its `Multiaddr` as specified in the parachain `chain_spec.json` file will look something like this:

    /dns4/k-boot-1.kapex.network/tcp/31333/ws/p2p/12D3KooWAyVMvqR9zpu3ri6SAFQewfQegrQ2iMSx8UsmXeixxCZo

**_This is optional_** and it need not be used if your boot node is going to be identified by its `IP` address.

### Instal nginx

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
    listen               0.0.0.0:31333;
    proxy_pass           127.0.0.1:30333;
}
```

This code listens for parachain connections on port `31333` on the `host`, and forwards to port `30333` on `localhost`. 

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