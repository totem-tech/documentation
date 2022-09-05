# Nginx setup for UI/RPC Nodes using DNS

### Nginx is used with UI/RPC node types for managing API endpoints supporting an application in order to read the state of the network, and to relay transactions. 

* In general this type of node will be used by Centralised Exchanges and application developers.

    * You can also run your own UI/RPC node to interact with the Kapex application front-end, instead of using the public endpoints available in the application. See the application documentation for information on this.

* Nginx will handle serving the certificates for the domain. 

    * When using Fully Qualified Domain Names (FQDN) in conjuntion with Polkadotjs Libraries connections are generally only allowed the Secure Websocket Protocol `wss://your.domain.name`.

    * Although technically these certificates can be self-signed, we recommend that you use [Let's Encrypt](https://letsencrypt.org/) and [Certbot](https://certbot.eff.org/) to generate and maintain the certificates. 

        * Certbot can also configure your `nginx` files for you and handle automatic renewals for the certificates which is very useful.

Since we are setting up a UI RPC node that uses a FQDN it will expose your node to additional traffic over and above the peer-to-peer networking traffic, and so you should consider the available CPU, memory, disk swapping capacity of your node. This should be monitored regularly and adjusted according to the demands of your node.

* This may include load balancing activities, but this document will not cover that configuration setup.

## Installing Nginx for a UI/RPC Node

```shell
# Install nginx
apt install nginx
````

The default settings for the nginx.conf should be sufficient, but you will need to edit the `default` file in `/sites-available` directory.

```
cd /etc/nginx
cd sites-available
nano default
```

Add the following into the file and save.

```
# Place this in the sites-available default file

limit_req_zone              $binary_remote_addr zone=yourzonename:10m rate=5r/s;
map $http_upgrade $connection_upgrade {
    default                  upgrade;
    ''                       close;
}
# upstream websocket parachain
upstream websocket-parachain-ui {
    server                   127.0.0.1:9944;
}

server {
#   Http Config
    server_name "your.domain.name";

#   SSL Configuration managed by Certbot!
    listen [::]:443 ssl ipv6only=on http2 default_server; # managed by Certbot
    listen 443 ssl http2 default_server; # managed by Certbot

    ssl_certificate /etc/letsencrypt/live/your.domain.name/fullchain.pem; # managed by Certbot
    ssl_certificate_key /etc/letsencrypt/live/your.domain.name/privkey.pem; # managed by Certbot

    include /etc/letsencrypt/options-ssl-nginx.conf; # managed by Certbot
    ssl_dhparam /etc/letsencrypt/ssl-dhparams.pem; # managed by Certbot

    location / {
        limit_req            zone=yourzonename burst=20 nodelay;
        limit_req_status     444;
        proxy_pass           http://websocket-parachain-ui;
        proxy_http_version   1.1;
        proxy_set_header     X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header     Upgrade $http_upgrade;
        proxy_set_header     Connection "Upgrade";
        proxy_set_header     Proxy "";
        proxy_set_header     Host $server_name;
        proxy_set_header     X-Real-IP $remote_addr;
        proxy_set_header     X-Forwarded-Proto $scheme;
    }
}
```

This code listens for api connections on port `443` the default secure websocket port on the `host`, and forwards to port `9944` on `localhost`. 

Later we will configure the docker container to listen to port `9944` on `localhost` and forward to the same port inside the container. The default port for the UI/RPC websocket on the parachain is `9944`.

Check that nginx has been configured properly
    
    nginx -t

Start nginx
    
    service nginx start