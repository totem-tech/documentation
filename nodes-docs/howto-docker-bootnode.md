### Commands to start a bootnode using the Totem Parachain Collator docker image.

Add the following commands to your `start.sh` file. 

_Do not forget to replace the name placeholders where appropriate!_

Bootnodes help the network decentralisation by providing an initial set of _well known_ nodes on the network, from which new nodes can obtain information about potential peers. Running a Bootnode helps with decentralisation of the network.

> When the bootnode starts the log should display the expected “identity” for this node, i.e. the one that is associated with your node-key when it was generated. If it does not check the permissions, the location and/or name of the file.

#### Start commands for a Bootnode

```shell
docker run \
-it \
-p 127.0.0.1:30333:30333 \
-p 0.0.0.0:40333:40333 \
-p 0.0.0.0:9615:9615 \ # optional
-p 0.0.0.0:9616:9616 \ # optional
--rm \
--name your-container-name \
--pull=always \
-v="/$(pwd)/data:/data" \
totemlive/totem-parachain-collator:production \
--chain=kapex \
--execution=wasm \
--state-cache-size=1 \
--name "name-to-identify-on-telemetry" \
--port 30333 \
--node-key-file /data/node-key/name-of-your-node-key-file \
--node-key-type "ed25519" \
--prometheus-external \ # optional
--prometheus-port 9615 \ # optional
-- \
--chain polkadot \
--port 40333 \
--prometheus-external \ # optional
--prometheus-port 9616 # optional
```