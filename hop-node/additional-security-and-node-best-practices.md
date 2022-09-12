---
description: Quick steps to secure your node
---

# Additional Security & Node Best Practices

## Additional Security

[This guide](https://www.coincashew.com/coins/overview-eth/guide-or-security-best-practices-for-a-eth2-validator-beaconchain-node) shows you how to take additional steps to secure your server. Each security item is enumerated below.

{% hint style="info" %}
Please note that any ports listed in the guide are not specific to the Hop Node.
{% endhint %}

1. ****[**Create a non-root user with sudo privileges**](https://www.coincashew.com/coins/overview-eth/guide-or-security-best-practices-for-a-eth2-validator-beaconchain-node#create-a-non-root-user-with-sudo-privileges)
2. ****[**Disable SSH password Authentication and Use SSH Keys only**](https://www.coincashew.com/coins/overview-eth/guide-or-security-best-practices-for-a-eth2-validator-beaconchain-node#disable-ssh-password-authentication-and-use-ssh-keys-only)
3. ****[**Update your system**](https://www.coincashew.com/coins/overview-eth/guide-or-security-best-practices-for-a-eth2-validator-beaconchain-node#update-your-system)****
4. ****[**Setup Two Factor Authentication for SSH \[Optional\]**](https://www.coincashew.com/coins/overview-eth/guide-or-security-best-practices-for-a-eth2-validator-beaconchain-node#setup-two-factor-authentication-for-ssh-optional)****
5. ****[**Secure Shared Memory**](https://www.coincashew.com/coins/overview-eth/guide-or-security-best-practices-for-a-eth2-validator-beaconchain-node#secure-shared-memory)****
6. ****[**Install Fail2ban \[Optional\]**](https://www.coincashew.com/coins/overview-eth/guide-or-security-best-practices-for-a-eth2-validator-beaconchain-node#install-fail-2-ban)****
7. ****[**Configure your Firewall**](https://www.coincashew.com/coins/overview-eth/guide-or-security-best-practices-for-a-eth2-validator-beaconchain-node#configure-your-firewall)****
8. ****[ **Verify Listening Ports**](https://www.coincashew.com/coins/overview-eth/guide-or-security-best-practices-for-a-eth2-validator-beaconchain-node#verify-listening-ports)
9.  ****[ **Use system user accounts - Principle of Least Privilege \[Advanced Users / Optional\]**](https://www.coincashew.com/coins/overview-eth/guide-or-security-best-practices-for-a-eth2-validator-beaconchain-node#use-system-user-accounts-principle-of-least-privilege-advanced-users-optional)



## Instance Best Practices

The following are best practices when running a node.

| Type                   | Best Practice                                                                                                                                                                                                                                                               |
| ---------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Networking             | Assign static internal IPs to both your validator node and daily laptop/PC. This is useful in conjunction with ufw and Fail2ban's whitelisting feature. Typically, this can be configured in your router's settings. Consult your router's manual for instructions.         |
| Power Outage           | In case of power outage, you want your validator machine to restart as soon as power is available. In the BIOS settings, change the **Restore on AC / Power Loss** or **After Power Loss** setting to always on. Better yet, install an Uninterruptible Power Supply (UPS). |
| Clear the bash history | <p>When pressing the up-arrow key, you can see prior commands which may contain sensitive data. To clear this, run the following:</p><p><code>shred -u ~/.bash_history &#x26;&#x26; touch ~/.bash_history</code></p>                                                        |
