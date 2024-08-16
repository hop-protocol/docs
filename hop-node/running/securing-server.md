---
description: Things you can do to secure your server running the Bonder
---

{% hint style="info" %}
Please note that this guide is written for Ubuntu 24.04. It also applies to all of the currently maintained Ubuntu releases.
{% endhint %}

# Securing your Server

These are a number of things you can do to secure an Ubuntu server.

{% hint style="info" %}
**These are examples and it's recommended that do your own research to know what's best for your own server.**
{% endhint %}

### Update your system

Keep the system up-to-date with the latest patches

```bash
sudo apt update -y && sudo apt full-upgrade -y
sudo apt autoremove -y && sudo apt autoclean
```

### Set up user configs

Disable the `root` user account and set a password for your account
```bash
sudo passwd -l root
sudo passwd ubuntu
```

### Harden SSH config

Edit SSH configuration

```bash
sudo vim /etc/ssh/sshd_config
```

In `sshd_config` file, update the values below or ensure that they are already set to these values.

```bash
PermitRootLogin no
PubkeyAuthentication yes
PasswordAuthentication no
PermitEmptyPasswords no
KbdInteractiveAuthentication no # In versions prior to Ubuntu 22.04, this is called `ChallengeResponseAuthentication`
X11Forwarding no
```

At the bottom of the file, add a new line to allow only your user to access the server.

```bash
AllowUsers ubuntu
```

Verify changes and reload service

```bash
sudo systemctl restart ssh.socket # If you are on a version prior to 24.04, run `sudo service ssh reload` instead
```

### Install fail2ban

Installing fail2ban will block out anyone who fails to repeatedly log in

```bash
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
sudo ufw default deny incoming
sudo ufw allow 22 comment "Allow SSH"
sudo systemctl restart ufw.service
sudo systemctl enable ufw.service
```

### Reset the server

The base configuration is now set up and enabled. Restart the server now to complete the update and upgrade of packages and associated config.

```bash
sudo reboot
```

### Add SSH 2FA

Check out the link below

{% content-ref url="ssh-2fa.md" %}
[ssh-2fa.md](ssh-2fa.md)
{% endcontent-ref %}
