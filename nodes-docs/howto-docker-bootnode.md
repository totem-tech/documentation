### Running a bootnode using docker

```shell
# Create a directory to hold your chain data:
mkdir -p data
cd data
nano node-key
```
Paste your node key in hex format this file. 

**Note** do not have a new line at the end of the file and do not prefix the hex value with `0x`.

Create a file to start your chain

    nano start.sh

Add the following commands. You can change the names accordingly.

```
docker run \
-it \
-p 127.0.0.1:30333:30333 \
-p 0.0.0.0:40333:40333 \
-p 0.0.0.0:9615:9615 \
-p 0.0.0.0:9616:9616 \
--rm \
--name your-docker-name \
--pull=always \
-v="/$(pwd)/data:/data" \
totemlive/totem-parachain-collator:v1.1.0-release \
--chain kapex \
--execution=wasm \
--state-cache-size=1 \
--name "name-to-identify-on-telemetry" \
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
If you get the error when trying to stop a container `Error response from daemon: cannot stop container:` execute the following command from the user that is running the container:

    sudo aa-remove-unknown

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