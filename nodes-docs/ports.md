# Ports for the Totem KAPEX parachain nodes

The following tables relates to the ports needed to be open to run the KAPEX parachain. 

It is assumed that you only open the ports that you need for the configuration of your node type.

*_Prometheus allows health monitoring for your nodes. It is optional in all cases._

#### Bootnode with domain name and nginx reverse proxy

|Chain Config.	|p2p	|UI	|rpc| Prometheus*|
|----|----|----|----|----|
|Parachain	|41333	|n/a	|n/a |9615	|
|Polkadot	|40333	|n/a	|n/a |9616	|

#### Bootnode without domain name

|Chain Config.	|p2p	|UI	|rpc| Prometheus*|
|----|----|----|----|----|
|Parachain	|30333	|n/a	|n/a |9615	|
|Polkadot	|40333	|n/a	|n/a |9616	|

#### UI node with domain name and nginx reverse proxy, but not RPC

|Chain Config.	|p2p	|UI	|rpc| Prometheus*|
|----|----|----|----|----|
|Parachain	|41333	|9944	|n/a |9615	|
|Polkadot	|40333	|9945	|n/a |9616	|

#### Collator node

|Chain Config.	|p2p	|UI	|rpc| Prometheus*|
|----|----|----|----|----|
|Parachain	|30333	|n/a	|n/a |9615	|
|Polkadot	|40333	|n/a	|n/a |9616	|

#### Collator Node with UI and RPC access

**RPC access should only be used/opened temporarily to access certain restricted services on your collator**

|Chain Config.	|p2p	|UI	|rpc| Prometheus*|
|----|----|----|----|----|
|Parachain	|30333	|9944	|9933 |9615	|
|Polkadot	|40333	|9945	|9934 |9616	|

#### Vanilla Full node or Archive node

|Chain Config.	|p2p	|UI	|rpc| Prometheus*|
|----|----|----|----|----|
|Parachain	|30333	|n/a	|n/a |9615	|
|Polkadot	|40333	|n/a	|n/a |9616	|