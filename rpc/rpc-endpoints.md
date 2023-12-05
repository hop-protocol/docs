---
description: List of RPC endpoint URLs
---

# RPC Endpoints

**These are public RPC URLs available on each network.**

It's important to note that public RPC URLs generally have rate limits, so they may not be reliable 100% of the time.

For the Hop Node, it is highly recommmend to use custom RPC endpoints from an RPC provider service such as [Infura](https://infura.io/) or [Alchemy](https://www.alchemy.com/).

Check out [https://chainlist.org/](https://chainlist.org/) as an easy way to connect wallet and add network to your wallet.

Note: the Infura project ID in the examples below is the default that [ethersjs](https://github.com/ethers-io/ethers.js/blob/0d40156fcba5be155aa5def71bcdb95b9c11d889/packages/providers/src.ts/infura-provider.ts#L17) uses.

## Mainnet

### Ethereum

Chain ID: `1`

| URL                                                             |
| --------------------------------------------------------------- |
| `https://mainnet.infura.io/v3/84842078b09946638c03157f83405213` |
| `https://cloudflare-eth.com`                                    |
| `https://rpc.ankr.com/eth`                                      |
| `https://1rpc.io/eth`                                           |

### Polygon

Chain ID: `137`

| URL                                      |
| ---------------------------------------- |
| `https://polygon-rpc.com` (recommended)  |
| `https://rpc-mainnet.matic.network`      |
| `https://rpc-mainnet.maticvigil.com`     |
| `https://rpc-mainnet.matic.quiknode.pro` |
| `https://rpc.ankr.com/polygon`           |
| `https://1rpc.io/matic`                  |

### Gnosis Chain (formerly xDai)

Chain ID: `100`

| URL                                            |
| ---------------------------------------------- |
| `https://rpc.gnosis.gateway.fm` (recommended)  |
| `https://rpc.gnosischain.com`                  |
| `https://xdai-archive.blockscout.com`          |
| `https://rpc.ankr.com/gnosis`                  |
| `https://gnosischain-rpc.gateway.pokt.network` |
| `https://gnosis-mainnet.public.blastapi.io`    |

### Optimism

Chain ID: `10`

| URL                            |
| ------------------------------ |
| `https://rpc.ankr.com/optimism`|
| `https://1rpc.io/op`           |
| `https://optimism-mainnet.infura.io/v3/84842078b09946638c03157f83405213` |
| `https://mainnet.optimism.io` (not reliable due to rate limits) |

Using an [Alchemy](https://www.alchemy.com/) RPC url is recommended instead of the public url. [Set up here](https://dashboard.alchemyapi.io/).

### Arbitrum

Chain ID: `42161`

| URL                             |
| ------------------------------- |
| `https://arb1.arbitrum.io/rpc`  |
| `https://rpc.ankr.com/arbitrum` |
| `https://1rpc.io/arb`           |

Using an [Alchemy](https://www.alchemy.com/) RPC url is recommended instead of the public url. [Set up here](https://dashboard.alchemyapi.io/).

### Nova

Chain ID: `42170`

| URL                                          |
| -------------------------------------------- |
| `https://nova.arbitrum.io/rpc`              |
| `https://arbitrum-nova.public.blastapi.io `  |

Using an [Alchemy](https://www.alchemy.com/) RPC url is recommended instead of the public url. [Set up here](https://dashboard.alchemyapi.io/).

### Base

Chain ID: `8453`

| URL                        |
| -------------------------- |
| `https://mainnet.base.org` |

Using an [Alchemy](https://www.alchemy.com/) RPC url is recommended instead of the public url. [Set up here](https://dashboard.alchemyapi.io/).

### Linea

Chain ID: `59144`

| URL                        |
| -------------------------- |
| `https://rpc.linea.build`  |

Using an [Infura](https://www.infura.io/) RPC url is recommended instead of the public url. [Set up here](https://app.infura.io/register).

## Goerli

### Ethereum (Goerli)

Chain ID: `5`

| URL                                                            |
| -------------------------------------------------------------- |
| `https://goerli.infura.io/v3/84842078b09946638c03157f83405213` |

### Polygon (Mumbai)

Chain ID: `80001`

| URL                                               |
| ------------------------------------------------- |
| `https://rpc.ankr.com/polygon_mumbai` |
| `https://matic-testnet-archive-rpc.bwarelabs.com` |

### Gnosis Chain (formerly xDai) Goerli

Gnosis Chain is not supported on Goerli

### Optimism (Goerli)

| URL                          |
| ---------------------------- |
| `https://rpc.ankr.com/optimism_testnet` |
| `https://goerli.optimism.io` |

### Base (Goerli)

| URL                       |
| ------------------------- |
| `https://goerli.base.org` |

### Linea (Goerli)

Chain ID: `59140`

| URL                               |
| --------------------------------- |
| `https://rpc.goerli.linea.build`  |
