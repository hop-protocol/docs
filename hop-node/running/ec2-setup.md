---
description: Set up a Hop Node on EC2
---

# EC2 Setup

## Node Creation

Create an EC2 instance to run your Hop Node

#### On the AWS website

1. Go to [https://console.aws.amazon.com/](https://console.aws.amazon.com/)
2. Sign into your AWS account
3. In the "_services_" search bar, type "EC2" and click on the first result
4. Click "Launch Instance"
5. Select "_Ubuntu Server 22.04 LTS (HVM), SSD Volume Type_"
6. Search for the instance type "m5.large" and select this instance
7. In "_Key pair (login)_" specify the key you want to use for SSH
8. In "_Configure Storage_", use 100GB and choose `gp3`.
9. Click "_Launch instance_"
10. Click "_Launch Instances_"

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
