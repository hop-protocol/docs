---
description: Running the Bonder as a Docker Container Options
---

The following are some options you can consider when running the bonder client.

#### Running as daemon

Use the `--detach` docker flag to run container as daemon.

```bash
docker run --detach -v ~/.hop:/root hopprotocol/hop-node:mainnet
```

Note: If you're keystore requires a passphrase and you're not using a password file, you'll need to pass the passpharse via the `KEYSTORE_PASS` environment variable.

```bash
export KEYSTORE_PASS=mysecretpassword
docker run --detach -e KEYSTORE_PASS=$KEYSTORE_PASS -v ~/.hop:/root/.hop hopprotocol/hop-node:mainnet
```

## Docker Compose

Docker compose example for Hop Node: `docker-compose.yml`

```yaml
version: '3.9'

  bonder:
    image: hopprotocol/hop:mainnet
    env_file:
      - docker.env
    restart: unless-stopped
    volumes:
        - /home/ubuntu/.hop:/root/.hop
```

Start docker container:

```bash
docker-compose -f docker-compose.yml up bonder
```

Start docker container as daemon:

```bash
docker-compose -f docker-compose.yml up --detach bonder
```

## Stopping docker container

```bash
docker stop hop-node
docker rm hop-node
```
