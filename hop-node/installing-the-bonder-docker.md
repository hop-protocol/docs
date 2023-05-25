---
description: Installing the bonder with Docker
---

## Installing Docker

The first step is to install Docker on your server. The official Docker install [Instructions are here](https://docs.docker.com/config/daemon/systemd/). A concise version of the instructions for installing Docker on an Ubuntu server are below:

```bash
sudo apt-get update
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable"
sudo apt-get install docker-ce -y
sudo usermod -aG docker $USER
newgrp docker
docker info
```

## Pulling the image

Next, you need to pull the bonder image.

```bash
docker pull hopprotocol/hop-node:mainnet
```
