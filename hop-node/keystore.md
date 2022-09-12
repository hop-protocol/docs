---
description: Hop Node keystore documentation
---

# Keystore

## Generate Keystore

Use the `keystore generate` command to generate an encrypted keystore:

{% tabs %}
{% tab title="Docker" %}
```bash
docker run -it -v ~/.hop-node:/root hopprotocol/hop-node keystore generate --path /root/keystore.json
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
Your keys can be found at: /home/mota/.hop-node/keystore.json

Keystore generation is complete.
Press [Enter] to exit.
```

### Use a custom keystore location

To use a custom keystore location, use the `-path`  flag:

{% tabs %}
{% tab title="Docker" %}
```bash
docker run -it -v ~/.hop-node:/root hopprotocol/hop-node keystore generate --path /root/keystore.json
```
{% endtab %}

{% tab title="Node" %}
```bash
hop-node keystore generate --path ~/.hop-node/keystore.json
```
{% endtab %}
{% endtabs %}

The default location is `~/.hop-node/keystore.json`

### Use an existing private key

You may generate an encrypted keystore using an existing private key by using the `--private-key` flag:

{% tabs %}
{% tab title="Docker" %}
```bash
docker run -it -v ~/.hop-node:/root hopprotocol/hop-node keystore generate --path /root/keystore.json --private-key=0x4f3edf983ac636a65a842ce7c78d9aa706d3b113bce9c46f30d7d21715b23b1d
```
{% endtab %}

{% tab title="Node" %}
```bash
hop-node keystore generate --private-key=0x4f3edf983ac636a65a842ce7c78d9aa706d3b113bce9c46f30d7d21715b23b1d
```
{% endtab %}
{% endtabs %}

Note that you will no be prompted with the mnemonic in this case.

### Decrypt keystore

Use the `keystore decrypt` command to decrypt an encrypted keystore:

{% tabs %}
{% tab title="Docker" %}
```bash
docker run -it -v ~/.hop-node:/root hopprotocol/hop-node keystore decrypt --path /root/keystore.json
```
{% endtab %}

{% tab title="Node" %}
```bash
hop-node keystore decrypt
```
{% endtab %}
{% endtabs %}

It will prompt you for the passphrase required to decrypt it:

```bash
keystore passphrase: ********
```

It will display the private key if the passphrase is correct:

```bash
4f3edf983ac636a65a842ce7c78d9aa706d3b113bce9c46f30d7d21715b23b1d
```

### Re-encrypt keystore with a new passphrase

Use the `keystore reencrypt` command to re-encrypt an encrypted keystore with a new passphrase:

{% tabs %}
{% tab title="Docker" %}
```bash
docker run -it -v ~/.hop-node:/root hopprotocol/hop-node keystore reencrypt --path /root/keystore.json
```
{% endtab %}

{% tab title="Node" %}
```
hop-node keystore reencrypt
```
{% endtab %}
{% endtabs %}

asdf

### View keystore address

Use the `keystore address` command to print the keystore public address:

{% tabs %}
{% tab title="Docker" %}
```bash
docker run -v ~/.hop-node:/root hopprotocol/hop-node keystore address --path /root/keystore.json
```
{% endtab %}

{% tab title="Node" %}
```bash
hop-node keystore address
```
{% endtab %}
{% endtabs %}

Example output:

```bash
0x90f8bf6a479f320ead074411a4b0e7944ea8c9c1
```
