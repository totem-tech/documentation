### Commands to start a Full node using the Totem Parachain Collator docker image.

Add the following commands to your `start.sh` file. 

_Do not forget to replace the name placeholders where appropriate!_

A Full Node running on the network mainly supports decentralisation, but does not perform any specific duties. 

#### Start commands for a Full Node

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
--state-cache-size=1 \
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