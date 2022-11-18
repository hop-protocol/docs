---
description: API examples
---

# API

## Endpoints

## GET /v1/quote

> Get estimated bonder fee to use for transfers

Example request

```sh
curl "http://localhost:8000/v1/quote?amount=1000000&token=USDC&fromChain=polygon&toChain=gnosis&slippage=0.5"
```

Example response

```json
{"amountIn":"1000000","amountOutMin":"994836","bonderFee":"250613","estimatedRecieved":"749223"}
```

## GET /v1/transfer-status

> Get transfer status for tx

Example request

```sh
curl "http://localhost:8000/v1/transfer-status?transferId=0x5a15b2abd4d0f2e5d0ea3d5fc93758374b14940096487d70f7c95b5393fc9c89"
```

Example response

```json
{"transferId":"0x5a15b2abd4d0f2e5d0ea3d5fc93758374b14940096487d70f7c95b5393fc9c89","transactionHash":"0xbe6953dac8149e3f4d3a5719445170fb9835c461a980cbdaf9ad5cce10c9d27c", ... }
```
