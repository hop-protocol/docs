---
description: Instructions for running a Hop Node.
---

# Running a Hop Bonder

_**Notice:** Currently Bonders must be allowed by the Hop Bridge smart contract governed by the Hop team. We are working on decentralizing the Bonder role completely. Reach out to the Hop team on discord if you are interested on becoming a bonder._

Welcome to the guide for setting up and running a Hop bonder! By sequentially following these steps, you should be up and running with your own bonder in no time! Click "Next" below to move onto the next step.

## Getting started

Before getting started, read through the requirements listed below:

{% content-ref url="requirements.md" %}
[requirements.md](requirements.md)
{% endcontent-ref %}

The first step is to set up a configuration file to specify which network to use and which tokens to bond.

Create a new directory under your home directory for the Hop Node configuration:

```bash
mkdir ~/.hop-node
```

The configuration file should be a JSON file under the Hop Node configuration directory:

```bash
touch ~/.hop-node/config.json
```

Open up this file now with your favorite editor and add the following example config:

{% content-ref url="configuration.md" %}
[configuration.md](configuration.md)
{% endcontent-ref %}

For more configuration examples and information, see the [Hop Node Configuration](configuration.md) page.

The next step is to run the Hop Node using our configuration.

## Using Docker (recommended)

Make sure docker daemon is running if not already.

{% content-ref url="installing-docker.md" %}
[installing-docker.md](installing-docker.md)
{% endcontent-ref %}

The Hop Node docker image is hosted on [Docker Hub](https://hub.docker.com/r/hopprotocol/hop-node).

Pull the Hop Node docker image:

```bash
docker pull hopprotocol/hop-node
```

{% content-ref url="docker.md" %}
[docker.md](docker.md)
{% endcontent-ref %}

Create a new file `docker.env` with the private key to use for signing transactions (note: you may also use an [encrypted keystore](keystore.md) which is the recommended way):

```bash
BONDER_PRIVATE_KEY=<YOUR_PRIVATE_KEY>
```

In order for docker to be aware of the configuration file, we'll need to mount a volume with the location of the directory containing the config file.

Run the docker image with the `--env-file` argument and with the `-v` volume argument to mount the host directory `~/.hop-node` to the `/root` directory on the container, and also specify to use the config with `--config /root/config.json` command argument:

```bash
docker run --env-file docker.env -v ~/.hop-node:/root hopprotocol/hop-node --config /root/config.json
```

This should be the bare minimum to get up and running. Check out the rest of the articles in the sidebar.

{% content-ref url="keystore.md" %}
[keystore.md](keystore.md)
{% endcontent-ref %}

{% content-ref url="configuration.md" %}
[configuration.md](configuration.md)
{% endcontent-ref %}

{% content-ref url="monitoring.md" %}
[monitoring.md](monitoring.md)
{% endcontent-ref %}

## Using NPM

_Note: Using **docker instead is highly recommended** instead of using NPM package._

Install `@hop-protocol/hop-node` package globally:

```bash
npm install --global @hop-protocol/hop-node
```

Setup the private key to use for signing transactions:

```bash
export BONDER_PRIVATE_KEY=<YOUR_PRIVATE_KEY>
```

Run Hop Node with configuration file:

```bash
hop-node --config ~/.hop-node/config.json
```
