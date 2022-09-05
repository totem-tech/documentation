# Nginx setup for Bootnodes

### Nginx is used with the bootnode type for introducing new nodes to the Kapex parachain network when you want to identify the node by DNS. 

Bootnodes work with the underlying `libp2p` protocol to provide an initial set of well-known nodes that new nodes can reach when starting. Each node will gossip information about their peers on the network, and bootnodes provide lists of known peers to new nodes to bootstrap the peer-to-peer network. 

However in order to acheive this certain aspects are handled by the process automatically. In most cases you will not have to worry about handling these aspects, but it is informative to know about them for troubleshooting.

1) Allowing multiplex communication in libp2p

    * see [Libp2p Hole Punching Max Inden @ FOSDEM](https://youtu.be/pSXlpKlZX7I)

    * also worth seeing [Explainer on UDP/Quic used by Libp2p](https://youtu.be/cdb7M37o9sU)

2) Speeds up the node discovery process

3) Allowing for persistant connections between peers, i.e. prevents sudden node disconnection when dialing

5) Allows information about other nodes to be shared with connecting nodes

If you are setting up a bootnode, please create an issue and a pull request on the totem-parachains Github repo to have your bootnode added to the [Kapex chain specification file](https://github.com/totem-tech/totem-parachains/blob/main/res/kapex/kapex-parachain-readable.json).

## Setup

There are two options for setting up a boot node, but only the one that uses a Fully Qualified Domain Name (FQDN) in its `Multiaddr` needs to have a reverse proxy such as `nginx` to route communication to the node.

This is an example of a boot node identity using a FQDN as specified in the Kapex parachain `chain_spec.json`:

    /dns4/k-boot-1.kapex.network/tcp/31333/ws/p2p/12D3KooWAyVMvqR9zpu3ri6SAFQewfQegrQ2iMSx8UsmXeixxCZo

This `Multiaddr` format need not be used if your boot node is going to be identified by its `IP` address in which case it would look something like this:

    /ip4/host-ip-address/tcp/host-port/ws/p2p/ed25519-node-identity

### Key generation for the node identity

You will need to create a Ed25519 key type for your node so that it can be identified on the p2p network.

The easiest way to generate a get is to use Parity Technology's Subkey tool as follows:

> Keep this file private. **DO NOT STORE THIS SECRET IN ANY PUBLIC DIRECTORY/REPOSITORY**

    # Generate Node Key type ED25519
    docker run --platform linux/amd64 --rm parity/subkey:latest generate-node-key > ./node-key-for-boot-node

The resulting file will contain the node's secret key and the output will in fact be the node's identity for use in the `Multiaddr` for the boot node. 




### Install & configure nginx

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