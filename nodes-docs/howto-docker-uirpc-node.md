### Commands to start a UI/RPC node using the Totem Parachain Collator docker image.

Add the following commands to your `start.sh` file. 

_Do not forget to replace the name placeholders where appropriate!_

This type of node supports relaying transactions to the network as well as reading blockchain storage. It is generally used by applications, and exchanges. 

We recommend that you use a [reverse proxy](nodes-docs/howto-nginx-uirpcnodes) to route traffic to this node, so that certificates can be served, which is a requirement of both the Polkadotjs libraries and the PolkadotJS Apps front-end.

#### Start commands for a UI/RPC Node

```shell
docker run \
-it \
-p 0.0.0.0:30333:30333 \
-p 0.0.0.0:40333:40333 \
-p 127.0.0.1:9944:9944 \ # this is for reverse proxy use
# -p 0.0.0.0:9944:9944 \ # this is for direct use
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
--ws-external \
--rpc-cors=all \
--prometheus-external \ # optional
--prometheus-port 9615 \ # optional
-- \
--chain polkadot \
--port 40333 \
--prometheus-external \ # optional
--prometheus-port 9616 # optional
```

Using [Polkadotjs apps live application](https://polkadot.js.org/apps) or the PolkadotJS libraries in your code you should be able to connect to your node using a connection string as follows. It assumes the use of a reverse proxy and that the host port will listen on `port 443`. For example our end point is: 

    wss://k-ui.kapex.network

Using [Polkadotjs apps running on your own machine](https://github.com/polkadot-js/apps) (i.e. at localhost), you should be able to connect directly to your ui/rpc node using a connection string as follows:

    ws://your-ui-rpc-node-ip-address:9944