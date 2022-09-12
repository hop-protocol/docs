---
description: Hop Node configuration examples
---

# Configuration

_Note: The configuration requirements are evolving so documentation may not be up-to-date. Please let us know if there are issues setting up the Hop Node._

**Please ask the Hop team for an configuration specific to your Hop Node if you are going to be a whitelisted bonder.**

## Configuration example

```javascript
{
  "network": "mainnet",
  "chains": {
    "ethereum": {
      "rpcUrl": "https://mainnet.infura.io/v3/84842078b09946638c03157f83405213",
      "maxGasPrice": 500
    },
    "gnosis": {
      "rpcUrl": "https://rpc.gnosischain.com",
      "maxGasPrice": 90
    },
    "polygon": {
      "rpcUrl": "https://polygon-rpc.com",
      "maxGasPrice": 5000
    },
    "optimism": {
      "rpcUrl": "https://mainnet.optimism.io",
      "maxGasPrice": 500
    },
    "arbitrum": {
      "rpcUrl": "https://arb1.arbitrum.io/rpc",
      "maxGasPrice": 500
    }
  },
  "tokens": {
    "USDC": true
  },
  "routes": {
    "ethereum": {
      "polygon": true,
      "gnosis": true,
      "arbitrum": true,
      "optimism": true
    },
    "polygon": {
      "ethereum": true,
      "gnosis": true,
      "arbitrum": true,
      "optimism": true
    },
    "gnosis": {
      "ethereum": true,
      "polygon": true,
      "arbitrum": true,
      "optimism": true
    },
    "arbitrum": {
      "ethereum": true,
      "polygon": true,
      "gnosis": true,
      "optimism": true
    },
    "optimism": {
      "ethereum": true,
      "polygon": true,
      "gnosis": true,
      "arbitrum": true
    }
  },
  "db": {
    "location": "/root/db"
  },
  "logging": {
    "level": "debug"
  },
  "keystore": {
    "location": "/root/keystore.json",
    "parameterStore": "/Hop/Bonder/Keystore/Pass",
    "awsRegion": "us-east-1"
  },
  "watchers": {
    "bondTransferRoot": true,
    "bondWithdrawal": true,
    "commitTransfers": true,
    "settleBondedWithdrawals": true,
    "xDomainMessageRelay": true,
    "L1ToL2Relay": true
  },
  "commitTransfers": {
    "minThresholdAmount": {
      "USDC": {
        "polygon": {
          "ethereum": 170000,
          "gnosis": 50000,
          "optimism": 130000,
          "arbitrum": 130000
        },
        "gnosis": {
          "ethereum": 170000,
          "polygon": 130000,
          "optimism": 130000,
          "arbitrum": 130000
        },
        "optimism": {
          "ethereum": 170000,
          "polygon": 130000,
          "gnosis": 50000,
          "arbitrum": 130000
        },
        "arbitrum": {
          "ethereum": 170000,
          "polygon": 130000,
          "gnosis": 50000,
          "optimism": 130000
        }
      }
    }
  },
  "fees": {
    "USDC": {
      "ethereum": 14,
      "polygon": 14,
      "gnosis": 25,
      "optimism": 14,
      "arbitrum": 14
    }
  }
}
```

### Properties

| Key               | Value                                                                                                                 |
| ----------------- | --------------------------------------------------------------------------------------------------------------------- |
| `network`         | The Ethereum network to use. (e.g. "_mainnet_', "_kovan_", "_goerli_")                                                |
| `chains`          | Chain configuration such as RPC URLs and max gas prices to use. See chains section below for details.                 |
| `tokens`          | List of tokens and their bridges that bonder will interact with. See tokens section below for details.                |
| `routes`          | Desired routes to bond withdrawals.                                                                                   |
| `db`              | Cache db options. See db section below for details.                                                                   |
| `logging`         | Logging options. See logging section below for details.                                                               |
| `keystore`        | Keystore options. See keystores section below for details.                                                            |
| `watchers`        | List of watchers.                                                                                                     |
| `commitTransfers` | Configuration for committing transfers.                                                                               |
| `fees`            | Set bonder fees for each asset in terms of basis points ([BPS](https://www.investopedia.com/terms/b/basispoint.asp)). |
| `bonders`         | List of other bonders, used for calculating total available liquidity. See bonders section below for details.         |

### `chains`

Specify configuration options for each chain:

```javascript
"chains": {
  "<chain-slug>": {
    "rpcUrl": "<chain-rpc-url>",
    "maxGasPrice": <max-gas-price>
  },
  ...
}
```

Chain slug options:

| Chain slug | Description                  |
| ---------- | ---------------------------- |
| `ethereum` | Ethereum                     |
| `gnosis`   | Gnosis Chain (formerly xDai) |
| `arbitrum` | Arbitrum                     |
| `optimism` | Optimism                     |
| `polygon`  | Polygon (formerly Matic)     |

_Note: The RPC URL is optional and a default will be used if not specified._

_Note: If the selected network doesn't support a chain, it will be ignored._&#x20;

### `tokens`

Specify which tokens and their token bridges to interactive with:

```javascript
"tokens": {
  "USDC": true,
  ...
}
```

### `routes`

Specify which routes to bond:

```json
"routes": {
  "ethereum": {
    "polygon": true,
    "gnosis": true,
    "arbitrum": true,
    "optimism": true
  },
  "polygon": {
    "ethereum": true,
    "gnosis": true,
    "arbitrum": true,
    "optimism": true
  },
  ...
}
```

The structure is `source` -> `destination`, for example:

```
"routes": {
  "polygon": {
    "gnosis": true
  },
  ...
}
```

The above example means that the bonder will bond transfers at the destination sent from `polygon`->`gnosis`.

### `db`

Configure options for leveldb database used for caching:

| Key        | Default value    | Description            |
| ---------- | ---------------- | ---------------------- |
| `location` | `~/.hop-node/db` | Location for cache db. |

### `logging`

Configure logging levels:

| Key     | Default value | Description                                                         |
| ------- | ------------- | ------------------------------------------------------------------- |
| `level` | `debug`       | Logging level. Options are "_debug_", "_info_", "_warn_", "_error_" |

### `keystore`

Configure options for keystore:

| Key              | Default value               | Example                     | Description                                        |
| ---------------- | --------------------------- | --------------------------- | -------------------------------------------------- |
| `location`       | `~/.hop-node/keystore.json` | `~/.hop-node/keystore.json` | Location of keystore to use.                       |
| `pass`           |                             | mysecret                    | Passphrase for encrypted keystore.                 |
| `parameterStore` |                             | /Hop/Bonder/Keystore/Pass   | Use AWS SSM Parameter Store for keystore password. |
| `awsRegion`      | `us-east-1`                 | `us-east-1`                 | AWS region to use when using SSM Parameter Store.  |

{% content-ref url="keystore.md" %}
[keystore.md](keystore.md)
{% endcontent-ref %}

### `watchers`

Watchers are like services in the Hop Node.&#x20;

| Watcher                   | Description                                 |
| ------------------------- | ------------------------------------------- |
| `bondTransferRoot`        | Bond transfer roots leaving ORUs            |
| `bondWithdrawal`          | Bond withdrawals sent across chains         |
| `commitTransfers`         | Commit transfers to create a transfer root  |
| `settleBondedWithdrawals` | Settle individual transfers                 |
| `xDomainMessageRelay`     | Exit transfer roots form their source chain |
| `L1ToL2Relay`             | Relay messages sent from L1 to L2           |

They should all be enabled unless there's a specific reason not to enable certain watchers.

### `commitTransfers`

The `minThresholdAmount` is used to determine when to commit the bundle of transfers.

The format is `token: { source: { destination: amount } }`

This example will commit transfers when a total of at least 20,000 MATIC are pending commit in the bundle, going either from gnosis->ethereum or polygon->ethereum, and a 10,000 threshold for the direction gnosis->polygon or polygon->gnosis.

```javascript
"commitTransfers": {
  "minThresholdAmount": {
    "USDC": {
      "gnosis": {
        "ethereum": 20000,
        "polygon": 10000
      },
      "polygon": {
        "ethereum": 20000,
        "gnosis": 10000
      }
    }
  }
}
```

### `fees`

Configure fee options. The fees are in basis points:

```json
"fees": {
  "USDC": {
    "ethereum": 14,
    "polygon": 14,
    "gnosis": 25,
    "optimism": 14,
    "arbitrum": 14
  },
    ...
}
```

### `bonders`

List of bonders, used for calculating total available liquidity.

The format is &#x20;

```json
"[TOKEN]": {
  "[SOURCE_CHAIN]": {
    "[DESTINATION_CHAIN]": "[BONDER_ADDRESS]"
  }
}
```

Full example:

```json
  "bonders": {
    "ETH": {
      "ethereum": {
        "optimism": "0x710bDa329b2a6224E4B44833DE30F38E7f81d564",
        "arbitrum": "0x710bDa329b2a6224E4B44833DE30F38E7f81d564",
        "gnosis": "0x710bDa329b2a6224E4B44833DE30F38E7f81d564",
        "polygon": "0x710bDa329b2a6224E4B44833DE30F38E7f81d564"
      },
      "optimism": {
        "ethereum": "0x710bDa329b2a6224E4B44833DE30F38E7f81d564",
        "arbitrum": "0x710bDa329b2a6224E4B44833DE30F38E7f81d564",
        "gnosis": "0x710bDa329b2a6224E4B44833DE30F38E7f81d564",
        "polygon": "0x710bDa329b2a6224E4B44833DE30F38E7f81d564"
      },
      "arbitrum": {
        "ethereum": "0x710bDa329b2a6224E4B44833DE30F38E7f81d564",
        "optimism": "0x710bDa329b2a6224E4B44833DE30F38E7f81d564",
        "gnosis": "0x710bDa329b2a6224E4B44833DE30F38E7f81d564",
        "polygon": "0x710bDa329b2a6224E4B44833DE30F38E7f81d564"
      },
      "gnosis": {
        "ethereum": "0x710bDa329b2a6224E4B44833DE30F38E7f81d564",
        "arbitrum": "0x710bDa329b2a6224E4B44833DE30F38E7f81d564",
        "optimism": "0x710bDa329b2a6224E4B44833DE30F38E7f81d564",
        "polygon": "0x710bDa329b2a6224E4B44833DE30F38E7f81d564"
      },
      "polygon": {
        "ethereum": "0x710bDa329b2a6224E4B44833DE30F38E7f81d564",
        "arbitrum": "0x710bDa329b2a6224E4B44833DE30F38E7f81d564",
        "gnosis": "0x710bDa329b2a6224E4B44833DE30F38E7f81d564",
        "optimism": "0x710bDa329b2a6224E4B44833DE30F38E7f81d564"
      }
    },
    ...
  }

```

### `blocklist`

Configure a blocklist of addresses for bonder to not bond transfers.



Using local blocklist file of addresses:

```json
"blocklist": {
  "path": "/root/blocklist.txt"
}
```

Using remote blocklist file of adddresses:

```json
"blocklist": {
  "path": "https://example.com/blocklist.txt"
}
```

Using inline list of blocklisted addresses:

```json
"blocklist": {
  "addresses": {
    "0x123...": true,
    "0xabc...": true
  }
}
```

Note: The Hop Node will need to be restarted whenever updating local, remote, or inline blocklist of addresses.

OFAC list: [https://www.treasury.gov/ofac/downloads/sdnlist.txt](https://www.treasury.gov/ofac/downloads/sdnlist.txt)

### Environment variables

| Key                  | Value                                                                                                      |
| -------------------- | ---------------------------------------------------------------------------------------------------------- |
| `BONDER_PRIVATE_KEY` | Private key to use for signing transactions if not using an encrypted keystore.                            |
| `KEYSTORE_PASS`      | Keystore passphrase if using encrypted keystore and not using password file or AWS Parameter Store option. |



### Notifications



### Slack

The Hop Node can post to Slack when an error occurs or when it sends transactions.

To set it up, configure the following environment variables:

| Key                | Example Value    | Description                   |
| ------------------ | ---------------- | ----------------------------- |
| `SLACK_AUTH_TOKEN` | _xoxb-123...890_ | Slack Bot Auth Token          |
| `SLACK_CHANNEL`    | _mychannel_      | Channel ID or name to post to |
| `SLACK_USERNAME`   | _"Hop Node"_     | Username to give to bot       |

More granular options for Slack channels:

| Key                             | Example Value           | Description                                       |
| ------------------------------- | ----------------------- | ------------------------------------------------- |
| `SLACK_WARN_CHANNEL`            | _warning-logs_          | (optional) Channel for posting warning logs       |
| `SLACK_ERROR_CHANNEL`           | _error-logs_            | (optional) Channel for posting error logs         |
| `SLACK_INFO_CHANNEL`            | _info-logs_             | (optional) Channel for posting info logs          |
| `SLACK_LOG_CHANNEL`             | _debug-logs_            | (optional) Channel for posting debug logs         |
| `SLACK_SUCCESS_CHANNEL`         | _success-logs_          | (optional) Channel for posting success logs       |
| `GAS_BOOST_WARN_SLACK_CHANNEL`  | _gasboost-warning-logs_ | (optional) Channel for wallet signer warning logs |
| `GAS_BOOST_ERROR_SLACK_CHANNEL` | _gasboost-error-logs_   | (optional) Channel for wallet signer error logs   |
