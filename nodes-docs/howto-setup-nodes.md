# Setup Totem KAPEX Nodes

The setup was performed on Linux Ubuntu 22.04 and can be used on VPS/droplets from various service providers, or any machine that supports Docker.

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

_This document is not designed to address the entire scope of possible server attack vectors by any means **nor do we provide any guarantees** that implementing all of the steps here would be sufficient to mitigate an attack on your server. It is a best efforts approach, but for specific security requirements, we highly recommend that you consult an opsec industry professional in order to conduct and audit of your setups._

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

To validate the ports that have been opened use this command:

```
# check the setup
ufw status numbered
```

### Nginx

Two different use cases exist for using nginx as a reverse proxy. The following links provide that information:

> If you are not creating either of these node types you will not need to use nginx.

[nginx for bootnodes](nodes-docs/howto-nginx-bootnodes.md)

[nginx for ui/rpc](nodes-docs/howto-nginx-uirpcnodes.md)

### Docker installation

In the this section we install docker. 

Although it can be installed from SNAP in Ubuntu 22.04, we recommend doing this manually to cover all the steps.

```shell
# run this if docker is already installed on your server, to update with latest version
sudo apt-get remove docker docker-engine docker.io containerd runc

# this script can be run at once
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

### Node data storage

Each node will require writeable directory to store block data, network data and keys. You can create this directory on your host or on a mounted volume, as long as it has the correct permissions it will be recognised by the container.

```shell
# Create a directory to hold your chain data... 
mkdir -p data
# ...and ensure that it is owned by the correct user:
chown 1000:1000 data
```

### Bootnode key location

If you are running a boot node (or for that matter if you want to specifically identify your node by identity), you will need to store the key to your node in a specific place that can be referenced by docker. Refer to the [node key generation](nodes-docs/howto-nginx-bootnodes?id=key-generation-for-the-node-identity) documentation to create the correct type of key.

```shell
cd data
mkdir -p keys
cd keys
mkdir -p node-key
```

Place the node key file inside the directory `/node-key`. This location will be referenced in the docker commands.

### Collator node signing key location

There are several ways to store the key for your collator, in this example we are storing a [previously generated signing key](nodes-docs/howto-signing-key) for our collator in a specific directory to be referenced by the node.

If you are running a collator ensure that the the key for your collator is named correctly and stored in this location.

```shell
cd data
mkdir -p keys
cd keys
mkdir -p auth-key
```
Place the collator signing key file inside the directory `/auth-key`. This location will be referenced in the docker commands.

## Starting your Kapex node

Create a file to start your chain

    nano start.sh

Choose the commands to add into this file dependent on the type of node you are creating. In these links you will find templates for docker start commands. Copy these commands and edit to replace the placeholder texts where needed.

[Docker commands for a Bootnode](nodes-docs/howto-docker-bootnode.md)

[Docker commands for a UI RPC node](nodes-docs/howto-docker-uirpc-node.md)

[Docker commands for a Collator node](nodes-docs/howto-docker-collatornode.md)

[Docker commands for a Archival node](nodes-docs/howto-docker-archivenode.md)

[Docker commands for a Simple Full node](nodes-docs/howto-docker-full-node.md)

Make the `start.sh` file executable

    sudo chmod u+x start.sh

### Notes on the Docker commands

#### Auto-remove running containers

The use of `--rm` argument is optional, and could be replaced by `--restart unless-stopped`, however the downside of this command is that the container must be manually stopped and removed even if the script is stopped - in other words after each time that the container is stopped, wherease `--rm` will remove it automatically. 

Configuring [Crontab](nodes-docs/howto-setup-nodes?id=crontab) is useful to maintain minimal down-time on your node, even when your VPs service provider conducts maintenance, and whden combined with `-rm` no cleanup is required.

#### Docker startup error

If you get the error when trying to stop a container `Error response from daemon: cannot stop container:` execute the following command from the user that is running the container:

    sudo aa-remove-unknown

### Crontab

Crontab ensures that your image restarts after your server is restarted. This can also happen if your VPS service provider shuts down your instance for maintenance.

    crontab -e

Add the following line using the `username` you created earlier to define the directory path. 

```
    # Note crontab is user specific!
    @reboot cd /home/<a-username>; screen -dmS parachain ./start.sh
```

This will start the node in a `screen` instance call `parachain`. Executing the start instruction in a screen session is useful to provide persistant execution whilst the user is logged out. To return to the session type `screen -x parachain` and to leave without closing the session type `ctrl a+d`.

### Final consideration

It is possible that your node comes under DOS attack. There are no easy ways to prevent this, however a combination of firewall, and Fail2Ban may help.

#### Install Fail2ban

    sudo apt-get update && \
    sudo apt-get upgrade && \
    sudo apt-get install -y fail2ban && \
    sudo systemctl start fail2ban && \
    sudo systemctl enable fail2ban && \
    sudo nano /etc/fail2ban/jail.local

add the following lines, but please note that using the default `ssh` port `22` is **not** recommended. To change this you must first change the default `ssh` port on your server.

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