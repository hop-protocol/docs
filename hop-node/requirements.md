---
description: Requirements for running a Hop Node
---

# Requirements

#### Resources

The **recommended** requirements for Hop Node are:

* 100GB of storage or greater
* 8GB of memory or greater
* Intel i5 processor or newer

The minimum requirements for Hop Node are:

* 10GB of storage or greater
* 1GB of memory or greater
* Intel i3 processor or newer

#### Operating system

Hop runs on any operating system as long as Node.js or Docker is supported. Ubuntu is a popular choice. Using Docker is recommended.

#### Logging

The Hop Node does put out a lot of logs so it's recommended to use a log managment service like [CloudWatch](https://aws.amazon.com/cloudwatch/), [Loggly](https://www.loggly.com/), [Splunk](https://www.splunk.com/), or simply rotate the logs so your node doesn't run out of storage.

#### RPC Provider

It is not a requirement to run your own RPC server on chain supported chain but you can use an existing RPC provider like [Infura](https://infura.io/), [Alchemy](https://www.alchemy.com/), or [Pokt](https://www.pokt.network/) when running the Hop node.

To override the default providers, update your Hop node `config.json`

```json
{
  ...
  "chains": {
    "ethereum": {
      "rpcUrl": "https://mainnet.infura.io/v3/84842078b09946638c03157f83405213"
    },
    "gnosis": {
      "rpcUrl": "https://rpc.gnosischain.com"
    },
    "polygon": {
      "rpcUrl": "https://polygon-rpc.com"
    },
    "optimism": {
      "rpcUrl": "https://mainnet.optimism.io"
    },
    "arbitrum": {
      "rpcUrl": "https://arb1.arbitrum.io/rpc"
    }
  }
}
```

{% content-ref url="docker-cloudwatch-logs.md" %}
[docker-cloudwatch-logs.md](docker-cloudwatch-logs.md)
{% endcontent-ref %}

#### Exposed ports

No ports need to be exposed. Hop is not P2P based so all inbound ports may be closed.

#### Becoming an authorized bonder

Currently Bonders must be allowed by the Hop Bridge smart contract governed by the Hop team. We are working on decentralizing the Bonder role completely and eventually bonders will be admitted by governance. Reach out to the Hop team on discord if you are interested on becoming a Bonder.
