---
description: Things you can do to secure your server running the Hop Node
---

# Securing Server

These are some things you can do to secure an Ubuntu server.

**These are examples and it's recommended that do your own research to know what's best for your own server.**

### Update your system

Keep the system up-to-date with the latest patches

```bash
sudo apt update -y && sudo apt full-upgrade -y
sudo apt autoremove -y && sudo apt autoclean
```

### Create new user instead of using default user

Create a non-root user with sudo privileges

```bash
sudo useradd -m -s /bin/bash alice
sudo passwd alice
sudo usermod -aG sudo alice
```

Copy authorized SSH hosts to new user

```bash
su - alice
sudo cp -r /home/ubuntu/.ssh .ssh
sudo chown -R alice:alice .ssh
```

Delete default user

```bash
sudo userdel -r -f ubuntu
```

### Harden SSH config

Edit SSH configuration

```bash
sudo vim /etc/ssh/sshd_config
```

In `sshd_config` file, make sure to have the following settings:

```bash
PermitRootLogin no
PasswordAuthentication no
PermitEmptyPasswords no
ChallengeResponseAuthentication no # This has been replaced by KbdInteractiveAuthentication in Ubuntu 22.04 and later
X11Forwarding no
```

**Optional**: Locate Port and customize it your random port. Use a random port # from 1024 thru 49141. [Check for possible conflicts](https://en.wikipedia.org/wiki/List_of_TCP_and_UDP_port_numbers).

```bash
Port <port number>
```

Verify changes and reload service

```bash
sudo sshd -t
sudo service ssh reload
```

### Only allow specific users for SSH

Edit SSH configuration

```bash
sudo vim /etc/ssh/sshd_config
```

Edit or add `AllowUsers` with space separated usernames

```
AllowUsers alice
```

Reload SSH service

```
sudo service ssh reload
```

### Disable root account

Disabling the `root` user account is a good idea

```bash
sudo passwd -l root
```

### Install fail2ban

Installing fail2ban will block out anyone who fails to repeatedly log in

```bash
sudo apt update
sudo apt install fail2ban -y
```

Create a local configuration file

```bash
sudo vim /etc/fail2ban/jail.local
```

Add the following config

```
[sshd]
enabled = true
port = <22 or your random port number>
filter = sshd
logpath = /var/log/auth.log
maxretry = 3
```

Restart services and show status

```bash
sudo service fail2ban restart
sudo service fail2ban status
```

### Firewall

All incoming connections can be disallowed. Only outgoing connections need to be allowed.

For example, if using [UFW](securing-server.md#create-new-user-instead-of-using-default-user)

```bash
systemctl start ufw.service
systemctl enable ufw.service

sudo ufw default deny
sudo ufw allow "22/tcp" # allow SSH port
sudo ufw disable # must disable and enable to apply changes
sudo ufw enable
sudo ufw status
```

### Add SSH 2FA

Check out the link below

{% content-ref url="ssh-2fa.md" %}
[ssh-2fa.md](ssh-2fa.md)
{% endcontent-ref %}
