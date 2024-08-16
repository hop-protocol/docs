---
description: Set up SSH 2FA with Google Authenticator
---

# Add SSH 2FA

This article goes over installing google authenticator on an Ubuntu server to enable 2FA authentication when performing SSH.

Note: It's recommended that you try setting up 2FA on a test server first, so you are not locked out of your server in case something goes wrong. It's also important to fully test the authentication before going live since a misconfiguration could leave your server less secure.

## Install Google Authenticator

```bash
sudo apt install libpam-google-authenticator -y
```

Run the `google-authenticator` command and follow the on-screen prompts

```bash
google-authenticator
```

First, it will ask you about time-based tokens. Say `y` to this question:

```
Do you want authentication tokens to be time-based: y
```

You will now see a big QR code on your screen, scan it with your Google Authenticator app to add it. You will also see your secret and a few backup codes looking like this:

```
Your new secret key is: IRG2TALMR5U2LK5VQ5AQIG3HA4
Your verification code is 282436
Your emergency scratch codes are:
  29778030
  86888537
  50553659
  41403052
  82649596
 
```

{% hint style="info" %}
Record the emergency scratch codes somewhere safe in case you need to log into the machine but don't have your 2FA app handy. Without the app, you will no longer be able to SSH into the machine!
{% endhint %}

Finally, it will ask you for some more parameters; the recommended defaults are as follows:

```
Do you want me to update your "/<username>/.google_authenticator" file: y
Do you want to disallow multiple uses of the same authentication token: y
By default... < long story about time skew > ... Do you want to do so: n
Do you want to enable rate-limiting: y
```

### Configure OpenSSH

```bash
sudo vim /etc/pam.d/sshd
```

Add to bottom of pam sshd file

```bash
auth required pam_google_authenticator.so
```

Update SSH

```bash
sudo vim /etc/ssh/sshd_config
```

Make sure to have these settings enabled

```bash
KbdInteractiveAuthentication yes # This is called `ChallengeResponseAuthentication` in versions prior to Ubuntu 22.04
UsePAM yes
```

At the bottom of the file, add a new line to require both the SSH key as well as the 2FA code when accessing the server.

```bash
AuthenticationMethods publickey,keyboard-interactive:pam
```

Restart SSH service

```bash
sudo service ssh reload
```

Google Authenticator setup is now compete! If you want to disable it at a later time, undo the steps above that modify the `/etc/pam.d/sshd` and `/etc/ssh/sshd_config` files. Ensure you reload the `ssh` service after modification.