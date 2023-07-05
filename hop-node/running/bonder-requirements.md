# Bonder Requirements

First, you must ensure you meet the minimum requirements to run the bonder. Relatively speaking, the process is not very intensive on any resource, so most modern machines should have no problem running the bonder client.

### Hardware Resources

The **recommended** requirements for Hop Node are:

* 100GB of storage or greater
* 8GB of memory or greater
* Intel i5 processor or newer

The minimum requirements for Hop Node are:

* 10GB of storage or greater
* 1GB of memory or greater
* Intel i3 processor or newer

### Operating system

Hop runs on any operating system as long as Node.js or Docker is supported. Ubuntu is a popular choice. Using Docker is recommended.

### Logging

The Hop Node does put out a lot of logs so it's recommended to use a log management service like [CloudWatch](https://aws.amazon.com/cloudwatch/), [Loggly](https://www.loggly.com/), [Splunk](https://www.splunk.com/), or simply rotate the logs so your node doesn't run out of storage.

#### RPC Provider

It is not a requirement to run your own RPC server on chain supported chain but you can use an existing RPC provider like [Infura](https://infura.io/), [Alchemy](https://www.alchemy.com/), or [Pokt](https://www.pokt.network/) when running the Hop node.

Ensure you have access to at least one endpoint per chain your bonder supports.

#### Exposed ports

No ports need to be exposed. Hop is not P2P based so all inbound ports may be closed.

#### Becoming an authorized bonder

Currently, bonders must be allowed by the Hop Bridge smart contract. Hop V2 will decentralize the Bonder role completely. Reach out to the Hop community on Discord if you are interested on becoming a bonder.