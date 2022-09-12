---
description: Install Docker service on server
---

# Installing Docker

Official Docker install [Instructions here](https://docs.docker.com/config/daemon/systemd/).

Instructions on installing docker on an Ubuntu server:

```bash
sudo apt-get update
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable"
sudo apt-get install docker-ce -y
sudo usermod -aG docker $USER
newgrp docker
docker info
```
