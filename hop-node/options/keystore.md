---
description: Options when Using your Keystore
---

# Keystore Options

### Use a custom keystore location

To use a custom keystore location, use the `-path`  flag:

{% tabs %}
{% tab title="Docker" %}
```bash
hop keystore generate --path /my/path/keystore.json
```
{% endtab %}

{% tab title="Node" %}
```bash
hop-node keystore generate --path ~/my/path/keystore.json
```
{% endtab %}
{% endtabs %}

The default location is `~/.hop/keystore.json`

### Use an existing private key

You may generate an encrypted keystore using an existing private key by using the `--private-key` flag:

{% tabs %}
{% tab title="Docker" %}
```bash
hop keystore generate --private-key=0x4f3edf983ac636a65a842ce7c78d9aa706d3b113bce9c46f30d7d21715b23b1d
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
hop keystore decrypt
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
hop keystore reencrypt
```
{% endtab %}

{% tab title="Node" %}
```
hop-node keystore reencrypt
```
{% endtab %}
{% endtabs %}

### View keystore address

Use the `keystore address` command to print the keystore public address:

{% tabs %}
{% tab title="Docker" %}
```bash
hop keystore address
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
