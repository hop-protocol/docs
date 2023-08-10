---
description: API examples
---

# API Endpoints

> This API is a simple wrapper around the SDK offered for convenience on getting estimated bonder fee and transfer status.

Although this API is offered as a free service, it's recommended to host your own API server ([see docs here](https://github.com/hop-protocol/hop/tree/develop/packages/api)) to not have any rate limit restrictions.

## Endpoints

## GET /v1/quote

> Get estimated bonder fee to use for transfers

Input query parameters:

| Parameters  | Description                                                                                                      |
| ----------- | ---------------------------------------------------------------------------------------------------------------- |
| `amount`    | (required) Amount in smallest use (eg. `amount=1000000` which is 1 USDC)                                         |
| `token`     | (required) Token symbol (eg. `token=USDC`)                                                                       |
| `fromChain` | (required) From chain slug (eg. `fromChain=optimism`)                                                            |
| `toChain`   | (required) To chain slug (eg. `toChain=polygon`)                                                                 |
| `slippage`  | (required) Slippage percentage (eg. `slippage=0.5` which is 0.5%)                                                |
| `network`   | (optional) Ethereum network to use. Options are `mainnet` (default), `goerli` for testnet (eg. `network=goerli`) |

Chain options are: `ethereum`, `optimism`, `arbitrum`, `polygon`, `gnosis`

Example request

```bash
curl "https://api.hop.exchange/v1/quote?amount=1000000&token=USDC&fromChain=polygon&toChain=gnosis&slippage=0.5"
```

Example response

```json
{
  "amountIn": "1000000",
  "slippage": 0.5,
  "amountOutMin": "743633",
  "destinationAmountOutMin": "742915",
  "bonderFee": "250515",
  "estimatedRecieved": "747908",
  "deadline": 1679862208,
  "destinationDeadline": 1679862208
}
```

Output response:

| Parameters                | Description                                                                                                                                                                                     |
| ------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `amountIn`                | Specified amount in.                                                                                                                                                                            |
| `slippage`                | Specified slippage.                                                                                                                                                                             |
| `amountOutMin`            | The minimum amount out to receive from AMM at origin chain (or destination chain if sending from L1), taking account AMM fees, slippage, and total bonder fee.                                  |
| `destinationAmountOutMin` | The minimum amount out to receive from AMM at destination chain, taking account, AMM fees, slippage, and total bonder fee. Note: There is no AMM on L1, so this should be 0 when sending to L1. |
| `bonderFee`               | The suggested bonder fee for the amount in. The bonder fee also includes the cost of the destination transaction fee.                                                                           |
| `estimatedReceived`       | The estimated amount you'll receive at the destination taking account all fees and slippage.                                                                                                    |
| `deadline`                | A default deadline of 7 days to perform swap at origin AMM (or destination AMM if sending from L1).                                                                                             |
| `destinationDeadline`     | A default deadline of 7 days to perform swap at destination AMM. Note: There is no AMM on L1, so this should be 0 when sending to L1.                                                           |

## GET /v1/transfer-status

> Get transfer status for tx

Input query parameters:

| Parameters     | Description                                                                               |
| -------------- | ----------------------------------------------------------------------------------------- |
| `transferHash` | (optional\*) Origin transfer transaction hash                                             |
| `transferId`   | (optional\*) Transfer ID                                                                  |
| `network`      | (optional) Ethereum network to use. Options are `mainnet` (default), `goerli` for testnet |

\* Must use at lease one option, either `transactionHash` or `transferId`.

Example request

```
curl "https://api.hop.exchange/v1/transfer-status?transactionHash=0xbe6953dac8149e3f4d3a5719445170fb9835c461a980cbdaf9ad5cce10c9d27c"
```

Example response

```json
{
  "transferId": "0x5a15b2abd4d0f2e5d0ea3d5fc93758374b14940096487d70f7c95b5393fc9c89",
  "transactionHash": "0xbe6953dac8149e3f4d3a5719445170fb9835c461a980cbdaf9ad5cce10c9d27c",
  "sourceChainId": 10,
  "sourceChainSlug": "optimism",
  "destinationChainId": 42161,
  "destinationChainSlug": "arbitrum",
  "accountAddress": "0xd813a52b1158fc08f69ba52ca72ca4360e255ba3",
  "amount": "2996498",
  "amountFormatted": 2.996498,
  "amountUsd": 3.004011668430896,
  "amountOutMin": "2503144",
  "deadline": 1662159408,
  "recipientAddress": "0xd813a52b1158fc08f69ba52ca72ca4360e255ba3",
  "bonderFee": "479123",
  "bonderFeeFormatted": 0.479123,
  "bonderFeeUsd": 0.4803243928791597,
  "bonded": true,
  "bondTransactionHash": "0x659225113a0711d73bd576d2edb916b1031d4fb3e422a08ee8e0f863c4fb5af7",
  "bonderAddress": "0xa6a688f107851131f0e1dce493ebbebfaf99203e",
  "token": "USDC",
  "timestamp": 1661554612
}
```

Output response:

| Parameters             | Description                                                                                                                          |
| ---------------------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| `transferId`           | Transfer ID                                                                                                                          |
| `transactionHash`      | Origin transaction hash                                                                                                              |
| `sourceChainId`        | Chain ID of origin chain                                                                                                             |
| `sourceChainSlug`      | Chain slug of origin chain                                                                                                           |
| `destinationChainId`   | Chain ID of destination chain                                                                                                        |
| `destinationChainSlug` | Chain slug of destination chain                                                                                                      |
| `accountAddress`       | Address of transfer originator                                                                                                       |
| `amount`               | Original amount transferred in smallest unit (eg. wei)                                                                               |
| `amountFormatted`      | Original amount transferred in human readable format                                                                                 |
| `amountUsd`            | Original amount transferred in USD                                                                                                   |
| `amountOutMin`         | The minimum amount out specified for AMM swap                                                                                        |
| `deadline`             | Deadline timestamp specified in transfer                                                                                             |
| `recipientAddress`     | Address of recipient set for transfer                                                                                                |
| `bonderFee`            | The bonder fee amount specified in transfer in smallest unit in terms of token transferred (eg. wei)                                 |
| `bonderFeeFormatted`   | The bonder fee amount specified in transfer in human readable format                                                                 |
| `bonded`               | True if this transfer has been bonded (received) at the destination. Will be false if the transfer is still pending or is unbondable |
| `bondTransactionHash`  | Bond (received) destination transaction hash                                                                                         |
| `bonderAddress`        | Address of bonder for this transfer                                                                                                  |
| `token`                | Token symbol of asset bridged                                                                                                        |
| `timestamp`            | Unix timestamp of origin transfer transaction                                                                                        |

## GET /v1/available-routes

> Get available routes

Input query parameters:

| Parameters     | Description                                                                               |
| -------------- | ----------------------------------------------------------------------------------------- |
| `network`      | (optional) Ethereum network to use. Options are `mainnet` (default), `goerli` for testnet |

Example request

```
curl "https://api.hop.exchange/v1/available-routes"
```

Example response

```json
[
  {
    "token": "USDC",
    "sourceChain": "ethereum",
    "sourceChainId": 1,
    "destinationChain": "gnosis",
    "destinationChainId": 100
  },
  {
    "token": "ETH",
    "sourceChain": "base",
    "sourceChainId": 8453,
    "destinationChain": "arbitrum",
    "destinationChainId": 42161
  },
  ...
]
```

Output response:

| Parameters             | Description                                                                                                                          |
| ---------------------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| `token`                | Token Symbol
| `sourceChainSlug`      | Source chain slug
| `sourceChainId`        | Source chain ID
| `destinationChainSlug` | Destination chain slug
| `destinationChainId`   | Destination chain ID

## Using custom RPC providers

You can set query parameter to specify what RPC url to use for a chain.

By default, public RPC urls are used, which are subject to rate limits. You can get better performance by specifying your own custom provider instead.

Input query parameters:

| Parameters         | Description                                                                                                       |
| ------------------ | ----------------------------------------------------------------------------------------------------------------- |
| `rpcUrl[ethereum]` | (optional) Ethereum RPC url (eg. rpcUrl\[ethereum]=https://mainnet.infura.io/v3/84842078b09946638c03157f83405213) |
| `rpcUrl[optimism]` | (optional) Optimism RPC url (eg. rpcUrl\[optimism]=https://mainnet.optimism.io)                                   |
| `rpcUrl[arbitrum]` | (optional) Arbitrum RPC url (eg. rpcUrl\[arbitrum]=https://arb1.arbitrum.io/rpc)                                  |
| `rpcUrl[polygon]`  | (optional) Polygon RPC url (eg. rpcUrl\[polygon]=https://polygon-rpc.com)                                         |
| `rpcUrl[gnosis]`   | (optional) Gnosis Chain RPC url (eg. rpcUrl\[gnosis]=https://rpc.gnosischain.com)                                 |
| `rpcUrl[nova]`     | (optional) Nova RPC url (eg. rpcUrl\[nova]=https://nova.arbitrum.io/rpc)                                          |
| `rpcUrl[base]`     | (optional) Base RPC url (eg. rpcUrl\[base]=https://goerli.base.org)                                               |

Example request

```bash
curl -g "https://api.hop.exchange/v1/quote?amount=1000000&token=USDC&fromChain=polygon&toChain=gnosis&slippage=0.5&rpcUrl[polygon]=https://polygon-rpc.com&rpcUrl[gnosis]=https://rpc.gnosischain.com"
```

## Source code

The API server source code is [available on github](https://github.com/hop-protocol/hop/tree/develop/packages/api).

## Additional endpoints

If you're looking for a complete API to compose bridge transfer transactions, checking approvals, and more; check out this self hosted server [example on github](https://github.com/hop-protocol/hop/tree/develop/packages/sdk-api-example).
