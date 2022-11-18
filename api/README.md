---
description: API examples
---

# API

## Endpoints

## GET /v1/quote

> Get estimated bonder fee to use for transfers

Input query parameters:

| Parameters  | Description                  |
| ----------- | ---------------------------- |
| `amount`    | Amount in smallest use (eg. 1000000 which is 1 USDC) |
| `token`     | Token symbol (eg. USDC) |
| `fromChain` | From chain slug (eg. optimism) |
| `toChain`   | To chain slug (eg. polygon) |
| `slippage`  | Slippage percentage (eg. 0.5 which is 0.5%) |

Example request

```sh
curl "https://api.hop.exchange/v1/quote?amount=1000000&token=USDC&fromChain=polygon&toChain=gnosis&slippage=0.5"
```

Example response

```json
{
  "amountIn": "1000000",
  "amountOutMin": "994836",
  "bonderFee": "250613",
  "estimatedRecieved": "749223"
}
```

Output response:

| Parameters  | Description                  |
| ----------- | ---------------------------- |
| `amountIn`  | Amount in |
| `amountOutMin` | The minimum amount out to receive from AMM taking account AMM fees and slippage |
| `bonderFee` | The suggested bonder fee for the amount in |
| `estimatedReceived` | The estimated amount you'll receive at the destination taking account all fees and slippage |

## GET /v1/transfer-status

> Get transfer status for tx

Input query parameters:

| Parameters  | Description                  |
| ----------- | ---------------------------- |
| `transferId`  | Transfer ID or origin transfer transaction hash |

Example request

```sh
curl "https://api.hop.exchange/v1/transfer-status?transferId=0x5a15b2abd4d0f2e5d0ea3d5fc93758374b14940096487d70f7c95b5393fc9c89"
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
  "deadline": 1662159408,
  "recipientAddress": "0xd813a52b1158fc08f69ba52ca72ca4360e255ba3",
  "bonderFee": "479123",
  "bonderFeeFormatted": 0.479123,
  "bonderFeeUsd": 0.4803243928791597,
  "bonded": true,
  "bondTransactionHash": "0x659225113a0711d73bd576d2edb916b1031d4fb3e422a08ee8e0f863c4fb5af7",
  "bonderAddress": "0xa6a688f107851131f0e1dce493ebbebfaf99203e",
  "token": "USDC",
  "timestamp": 1661554612,
  ...
}
```

Output response:

| Parameters  | Description                  |
| ----------- | ---------------------------- |
| `transferId`  | Transfer ID |
| `transactionHash`  | Origin transaction hash |
| `sourceChainId`  | Chain ID of origin chain |
| `sourceChainSlug`  | Chain slug of origin chain |
| `destinationChainId`  | Chain ID of destination chain |
| `destinationChainSlug`  | Chain slug of destination chain |
| `accountAddress`  | Address of transfer originator |
| `amount`  | Original amount transferred in smallest unit (eg. wei) |
| `amountFormatted`  | Original amount transferred in human readable format |
| `amountUsd`  | Original amount transferred in USD |
| `deadline`  | Deadline timestamp specified in transfer |
| `recipientAddress`  | Address of recipient set for transfer |
| `bonderFee`  | The bonder fee amount specified in transfer in smallest unit in terms of token transferred (eg. wei) |
| `bonderFeeFormatted`  | The bonder fee amount specified in transfer in human readable format |
| `bonded`  | True if this transfer has been bonded (received) at the destination. Will be false if the transfer is still pending or is unbondable |
| `bondTransactionHash` | Bond (received) destination transaction hash |
| `bonderAddress`  | Address of bonder for this transfer |
| `token` | Token symbol of asset bridged |
| `timestamp` | Unix timestamp of origin transfer transaction |
