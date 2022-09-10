### Commands to start a Collator node using the Totem Parachain Collator docker image.

Add the following commands to your `start.sh` file. 

_Do not forget to replace the name placeholders where appropriate!_

A collator node collects and validates transactions for the Kapex Parachain as well as authoring blocks. It plays an important part in the relationship to the Polkadot relaychain by providing validated block headers for inclusion in the Polkadot Relaychain.

Although collators are not currently incentivised in the event that the transaction fee burn is considered an excessive on the total supply, it may be introduced.

If you are considering running a collator node, best practice is to also run a fall-back [archival node](nodes-docs/howto-docker-archivenode).

#### Start commands for a Collator Node

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
--collator \
--keystore-path /data/auth-key \
--prometheus-external \ # optional
--prometheus-port 9615 \ # optional
-- \
--chain polkadot \
--port 40333 \
--prometheus-external \ # optional
--prometheus-port 9616 # optional
```

The commands provided above are the usual commands for a Collator node. The node does not expose the UI/RPC ports which is the recommended state. However in certain speecific use cases - for example when you need to rotate the signing keys - a second set of commands is necessary and the UI/RPC ports are required to be [temporarily opened](nodes-docs/ports?id=collator-node-with-ui-and-rpc-access) so that you can connect to the node directly. The following commands should only be used for a limited time before reverting to the above set of commands.

We recommend that you create a new temporary start file:

```shell
nano  start-temporary.sh
chmod u+x start-temporary.sh
```
Add the following into the `start-temporary.sh` file. **Do not forget to change the placeholder texts and remove the comments**

```shell
docker run \
-it \
-p 0.0.0.0:30333:30333 \
-p 0.0.0.0:40333:40333 \
-p 0.0.0.0:9944:9944 \ # temporary
-p 0.0.0.0:9933:9933 \ # temporary
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
--pruning=archive \ # temporary
--ws-external \  # temporary
--unsafe-ws-external \  # temporary
--rpc-cors=all \  # temporary
--rpc-methods=unsafe \  # temporary
--prometheus-external \ # optional
--prometheus-port 9615 \ # optional
-- \
--chain polkadot \
--port 40333 \
--prometheus-external \ # optional
--prometheus-port 9616 # optional
```

Using [Polkadotjs apps](https://github.com/polkadot-js/apps) running on your own machine (i.e. at localhost), you should be able to connect directly to your collator node and execute RPC commands.

The connection string is in the format `ws://your-collator-node-ip-address:9944`.

Setting the keys for the collator node using the PolkadotJS Apps UI is identical to that of setting keys for a Polkadot Validator. Follow the instructions [here](https://wiki.polkadot.network/docs/maintain-guides-how-to-validate-polkadot#generating-the-session-keys).