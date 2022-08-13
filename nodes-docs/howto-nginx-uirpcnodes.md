# Nginx setup for UI/RPC Nodes

Nginx has several important features in this context, but it is only used with this UI/RPC node types for managing API endpoints for the network, but more specifically so that an app can relay transactions to the parachain network. 

This is mandatory however if the node is to be used with the Polkadotjs Libraries because nginx will also be required to handle the certificates for the domain. Although these can be self-signed it is recommended that yoou use [Let's Encrypt](https://letsencrypt.org/) and [Certbot](https://certbot.eff.org/) to generate and maintain the certificates. Certbot can also configuree your `nginx` files for you, if it is already installed.

Since we are setting up a UI RPC node that uses a FQDN it will expose your node to additional traffic over and above the peer-to-peer networking traffic, and so you should consider the available CPU, memory, disk swapping capacity etc.

```shell
# Install nginx - this is only partially used
apt install nginx
````

The default settings for the nginx.conf should be sufficient, but you will need to edit the default sites-available file.

```
cd /etc/nginx
cd sites-enabled
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
# 10246 websocket-polkadot-ui
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

Later we will configure the docker container to listen to port `9944` on `localhost` and forward to the parachain port inside the container.

Check that nginx has been configured properly
    
    nginx -t

Start nginx
    
    service nginx start