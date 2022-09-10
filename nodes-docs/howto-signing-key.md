# Generating a signing key for a collator

These are the steps to create a signing key for your collator node. There are other ways to create this key, and in fact to inject the key into your node, but this tutorial only uses the Subkey tool.

You will need to create an `Sr25519` key type for your collator node so that it can sign blocks that it proposes.

The easiest way to generate a get is to use [Parity Technology's Subkey](https://hub.docker.com/r/parity/subkey/tags) as follows:

>**DO NOT STORE SECRET KEYS IN ANY PUBLIC DIRECTORY OR REPOSITORY**
> 
>**USE THIS TOOL OFFLINE**
>
> Keep the output file private! 

    # Generate Node Key type sR25519
    docker run --platform linux/amd64 --rm parity/subkey:latest generate > ./signing-key-for-collator-node

The resulting file will contain a secret seed phrase, the hex equivalen secret key, the hex public key, and the generic Polkadot Public Address for that key. **Make sure you back-up and securely store this file**

#### Creating this signing key file

You will need to use:

* the Seed Phrase

* the hex public key

The file that will be used for the signing key **_must use a specific naming convention_** as follows:

Name the file by concatenating `617526`* with the `hex public key`. You must drop the `0x` prefix of the public key when construction this file name.

*_the number `617526` is the hex representation of the name `aura` which is the name of the Authority Round consensus algorithm for Parachains._

>**DO NOT STORE SECRET KEYS IN ANY PUBLIC DIRECTORY OR REPOSITORY**

```shell
# create and edit the collator key file using the correct naming convention
nano 617526some-public-key-hex
```

Paste the secret seed phrase into this file in inverted commas, and save. 

**This new file is your collator key file.**
