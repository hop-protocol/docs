# Keystore Local Passphrase 

Storing the keystore passphrase locally is as simple as adding it to the config file.

_**Note**: The entirety of the config file will be explained in the next section, so feel free to move on and return here when you need to add the keystore config._

Update your config `~/.hop-node/config.json` to use the passphrase:

```json
{
  "keystore": {
    "location": "~/.hop-node/keystore.json",
    "pass": "myPassword"
  }
}
```
