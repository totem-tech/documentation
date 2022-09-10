# Open Ports for Totem KAPEX parachain nodes

### The following tables relate to the ports to be opened on the host for the specific configuration of your selected parachain node type. 

Each parachain node type opens at least one parachain port and one relaychain port. The configuration covers the usual scenarios and it should be noted that you may mix-and-match settings to configure your node for your own use cases.


> This page does not cover the port mappings from the host to the docker container which is covered in the [docker configuration section](nodes-docs/howto-setup-nodes?id=docker-configuration).

> Prometheus allows health monitoring for your nodes. Although we recommend its use and have listed the ports here, it is optional.

---

### Bootnode with domain name and nginx reverse proxy

In this configuration the host port for the Parachain connection will be a different port than the one exposed in the docker container. You only need to ensure that the host port is configured to allow traffic through your firewall. 

The configuration will map the ports similar to this, although you can choose your own port numbers.

> `host port 31333` -> `localhost port 30333` -> `container port 30333`.

Ports to open on the host.

|Relating to chain...	|p2p port	|UI port	|rpc port | Prometheus* port |
|----|----|----|----|----|
|Parachain	|31333	|n/a	|n/a |9615	|
|Polkadot	|40333	|n/a	|n/a |9616	|

---

### Bootnode without domain name

Ports to open on the host.

|Relating to chain...	|p2p port	|UI port	|rpc port | Prometheus* port |
|----|----|----|----|----|
|Parachain	|30333	|n/a	|n/a |9615	|
|Polkadot	|40333	|n/a	|n/a |9616	|

---

### UI node with domain name and nginx reverse proxy, but not RPC

In this configuration the host port for the Parachain connection will be a different port than the one exposed in the docker container. You only need to ensure that the host port is configured to allow traffic through your firewall. 

The configuration will map the ports similar to this, although you can choose your own port numbers.

> `host port 31333` -> `localhost port 30333` -> `container port 30333`.

Also this configuration will require a secure websocket connection. It is recommended that you use [Certbot](https://certbot.eff.org/instructions?ws=nginx&os=ubuntufocal) to automatically configure `nginx`.

Again the configuration will map the ports similar to this, although you can choose your own port numbers.

> `host port 443` -> `localhost port 9944` -> `container port 9944`.

Ports to open on the host.

|Relating to chain...	|p2p port	|UI port	|rpc port | Prometheus* port |
|----|----|----|----|----|
|Parachain	|31333	|443	|n/a |9615	|
|Polkadot	|40333	|n/a	|n/a |9616	|

---

### Collator node

Ports to open on the host.

|Relating to chain...	|p2p port	|UI port	|rpc port | Prometheus* port |
|----|----|----|----|----|
|Parachain	|30333	|n/a	|n/a |9615	|
|Polkadot	|40333	|n/a	|n/a |9616	|

---

### Collator Node with UI and RPC access

> RPC access should only be used/opened temporarily to access certain restricted services on your collator

Ports to open on the host.

|Relating to chain...	|p2p port	|UI port	|rpc port | Prometheus* port |
|----|----|----|----|----|
|Parachain	|30333	|9944	|9933 |9615	|
|Polkadot	|40333	|n/a	|n/a  |9616	|

---

### Vanilla Full node or Archive node

Ports to open on the host.

|Relating to chain...	|p2p port	|UI port	|rpc port | Prometheus* port |
|----|----|----|----|----|
|Parachain	|30333	|n/a	|n/a |9615	|
|Polkadot	|40333	|n/a	|n/a |9616	|