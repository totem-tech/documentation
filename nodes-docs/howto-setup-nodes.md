# Setup Totem KAPEX Nodes on VPS

The setup was performed on Linux Ubuntu 22.04 and can be used on VPS/droplets from various service providers.

### Support

If you come across issues or need help, please reach out to us on [Telegram](https://t.me/totemchat), [Discord](https://discord.gg/TXPKJTAGvt) or <a href="mailto:support@totemaccounting.com?subject=Totem Docs: Help running my Node">email</a>.

## Scope of the document

In this document we will go through the various node types that exist for KAPEX and how to configure them. The intended audience are Exchanges, Validators (Collators), Archivists, Blockchain Indexers (block explorers etc...) and all other parties interested in supporting the KAPEX Parachain Network.

The node types are:

* Boot Node

* UI/RPC Node. 

    * _This node type is also useful for centralised exchanges in order to setup API endpoints._

* Collator Node

* Archive Node

* Vanilla Full Node

**We will be using our [totem-parachain-collator](https://hub.docker.com/r/totemlive/totem-parachain-collator/tags) from the dockerhub repository in all the examples.**

* If you wish to compile a node from scratch some of the settings apply, but obviously the docker-specific settings do not apply. We highly recommend the docker image is used to avoid issues.

### Fail2Ban

This utility attempts to reduce some aspects of Denial of Service (DoS) attacks, but is somewhat complex to manage and maintain. See at the [end of this page](/nodes-docs/howto-setup-nodes?id=install-fail2ban) for the installation details. 

_Fail2Ban should not be seen as the only requirement to secure your server, but should be seen as part of an overall attack mitigation strategy including but not limited to:_ 

* ssh login

    * not permitting password login

    * root user login not allowed

* use of a firewall with only certain ports open

* nginx request rate limiting

* other...

_This document is not designed to address the entire scope of possible server attack vectors by any means nor do we provide any guarantees that implementing all of the steps here would be sufficient to prevent your server from being attacked. It is a best efforts approach, but for specific security requirements, we highly recommend that you contact the relevant indiustry professionals in order to conduct and audit of your setups._

## Preliminary configuration

#### User ID conflict with Docker

Upon initial creation of the droplet/server you must remove any user with the `UID=1000` as this conflicts with the KAPEX Docker image permissions which we will be using here.

For example on a fresh Ubuntu install there may be a user called `ubuntu` with this `UID`. Follow these steps to remove this user and create a fresh one. 

```shell
# check for user with UID 1000
nano /etc/passwd

# delete ubuntu guest user if necessary
deluser --remove-home ubuntu

# create a new user
# skip entering details, and add initial password when prompted
adduser <a-username>

# make the user a admin (optional)
usermod -aG sudo <a-username>

```

## Install other components

### Firewall

Create a firewall to specify which ports you require to be open

```shell
# update package manager
apt update

#Install UFW Firewall
apt-get install ufw

#start the firewall
ufw enable

# allow ssh login (port 22)
ufw allow ssh
```

Refer to the ports needed to be opened for the specific node type [here](nodes-docs/ports.md) or by following the specific links:

* [Bootnode with domain name and nginx reverse proxy](nodes-docs/ports?id=bootnode-with-domain-name-and-nginx-reverse-proxy)

* [Bootnode without domain name](nodes-docs/ports?id=bootnode-without-domain-name)

* [UI node with domain name and nginx reverse proxy, but not RPC](nodes-docs/ports?id=ui-node-with-domain-name-and-nginx-reverse-proxy-but-not-rpc)

* [Collator Node](nodes-docs/ports?id=collator-node)

* [Collator Node with UI and RPC access](nodes-docs/ports?id=collator-node-with-ui-and-rpc-access)

* [Vanilla Full node or Archive node](nodes-docs/ports?id=vanilla-full-node-or-archive-node)

```
# check the setup
ufw status numbered
```

### Nginx

> If you are not creating either of these node types you will not need to use nginx.

Two different use cases exist for using nginx as a reverse proxy. The following links provide that information:

[nginx for bootnodes](nodes-docs/howto-nginx-bootnodes.md)

[nginx for ui/rpc](nodes-docs/howto-nginx-uirpcnodes.md)


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