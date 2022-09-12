---
description: Set up a Hop Node on EC2. ⚠️ Hope Node is in beta. Use at your own risk!
---

# EC2 Setup

## Node Creation

Create an EC2 instance to run your Hop Node

#### On the AWS website

1. Go to [https://console.aws.amazon.com/](https://console.aws.amazon.com/)
2. Sign into your AWS account
3. In the "_services_" search bar, type "EC2" and click on the first result
4. Click "Launch Instance"
5. Select "_Ubuntu Server 20.04 LTS (HVM), SSD Volume Type_"
6. Search for the instance type "m5.large" and select this instance
7. Click "_Next: Configure Instance Details"_
8. Click "_Next: Add Storage"_
9. In the "_Size (GiB)"_ column, use "100" instead of the default "8"
10. Click "_Review and Launch_"
11. Click "_Launch_"
12. Select "_Create a new key pair_" and name it "hop-node"
13. Click "_Download Key Pair_" and save the _.pem_ file on your machine
14. Click "_Launch Instances_"

#### In the Terminal on your local machine

1. Navigate to the directory where you downloaded your _.pem_ file (for example, try `cd ~/Downloads`)
2. Run the following commands to set up your Hop Node directory and server access.

i. Create _.ssh_ directory if not existing already:

```
mkdir ~/.ssh
```

ii. Move _.pem_ file to the ssh directory:

```bash
mv ~/Downloads/hop-node.pem ~/.ssh
```

iii: Change the permission of the _.pem_ file for SSH:

```
chmod 400 ~/.ssh/hop-node.pem
```

#### On the AWS website

1. Navigate to your EC2 instances (this should be the page you were on last)
2. Select your instance and click the "_Connect_" button
3. Choose "_SSH client_"
4. Copy the last line labeled "_Example_"

**In the Terminal on your local machine**

1. Paste the command you copied and run it
2. When prompted, type "_yes_" and click enter

## Docker Installation and Node Set up

On your new EC2 Ubuntu instance, install Docker and pull the latest Hop Node:

```
sudo apt-get update
```

```
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```

```
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable"
```

```
sudo apt-get install docker-ce -y
```

```
sudo usermod -aG docker $USER
```

```
newgrp docker
```

```
docker pull hopprotocol/hop-node
```

Set up the Hop Node configuration:

```
mkdir ~/.hop-node
```

```
vim ~/.hop-node/config.json
```

In this file, paste the default configuration example:

{% content-ref url="configuration.md" %}
[configuration.md](configuration.md)
{% endcontent-ref %}

## Keystore Generation and Funding

Generate the Keystore that will be the Hop Bonder.

```
docker run -v ~/.hop-node:/root -it hopprotocol/hop-node keystore generate --path /root/keystore.json
```

Follow the instructions in your terminal and return to this page upon completion.

The command ends by printing the public key associated with your Hop Bonder. You may now send funds to that address.

## Running the Bonder

Run the following command to run the Hop Bonder

```
docker run -d hop-bonder -v ~/.hop-node:/root -it hopprotocol/hop-node --config /root/config.json
```
