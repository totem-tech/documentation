### Commands to start a Archive node using the Totem Parachain Collator docker image.

Add the following commands to your `start.sh` file. 

_Do not forget to replace the name placeholders where appropriate!_

An archive node stores the entire blockchain history, rather than the pruned state of the chain. All nodes except archival and collator nodes store just the latest pruned state of the blockchain database and the storage requirements are significantly lower than an archive or collator. Therefore when running an archive node you should monitor the available disk space carefully.

The use case for an Archive Node is to support the network by retaining a full copy of all transactions and data that has been seen by the network. It is useful for indexers and as a potential fall-back for a non-functioning collator node.

#### Start commands for a Archive Node

```shell
docker run \
-it \
-p 0.0.0.0:30333:30333 \
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
--state-pruning="archive" \
--name "name-to-identify-on-telemetry" \
--port 30333 \
--prometheus-external \ # optional
--prometheus-port 9615 \ # optional
-- \
--chain polkadot \
--port 40333 \
--prometheus-external \ # optional
--prometheus-port 9616 # optional
```