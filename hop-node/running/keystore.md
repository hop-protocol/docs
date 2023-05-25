---
description: Hop Node keystore documentation
---

# Keystore

## Generate Keystore

Use the `keystore generate` command to generate an encrypted keystore:

{% tabs %}
{% tab title="Docker" %}
```bash
hop keystore generate --path /root/keystore.json
```
{% endtab %}

{% tab title="Node" %}
```bash
hop-node keystore generate
```
{% endtab %}
{% endtabs %}

It will prompt you for a passphrase:

```bash
Enter new keystore encryption passphrase: ********
Confirm passphrase: ********
```

Then it will display your seed phrase. This only displayed once here so make sure to copy it.

```bash
This is your seed phrase. Write it down and store it safely.

inquiry leisure hurry trade leave gown add sad feel salad seat west scare filter swear siege buyer funny detect noble scene index traffic extend

Press [Enter] when you have written down your mnemonic.
```

Next you will have to paste in the mnemonic you copied to confirm:

```bash
Please type mnemonic (separated by spaces) to confirm you have written it down

: nice grow shine drift recycle survey piano rifle soccer business evidence stand pave belt room size neither volume odor sorry ten flash deliver rack
```

Your keystore should now be generated and stored in the default location`~/.hop-node/keystore.json`

```bash
Creating your keys
Creating your keystore
Public address: 0x2c2c2420128945403197a768a39fe5a8fda60f39
Your keys can be found at: /home/ubuntu/.hop-node/keystore.json

Keystore generation is complete.
Press [Enter] to exit.
```

## Keystore passphrase storage

You have a few options to store the keystore passphrase. Two options that are shown below are to use AWS Parameter Store (recommended) or storing it on the server itself. Either option is acceptable, as is anything else you are comfortable with.

{% content-ref url="keystore-aws-parameter-store.md" %}
[keystore-aws-parameter-store.md](keystore-aws-parameter-store.md)
{% endcontent-ref %}

{% content-ref url="keystore-local-passphrase.md" %}
[keystore-local-passphrase.md](keystore-local-passphrase.md)
{% endcontent-ref %}