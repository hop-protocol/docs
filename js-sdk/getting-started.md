---
description: ⚠️ JavaScript SDK is in beta
---

# Getting started

## Install module

Using NPM:

```bash
npm install @hop-protocol/sdk
```

Using Yarn:

```bash
yarn add @hop-protocol/sdk
```

## CDN

[jsDeliver](https://www.jsdelivr.com/) CDN:

```html
<script src="https://cdn.jsdelivr.net/npm/@hop-protocol/sdk@latest/hop.js"></script>
```

[unpkg](https://unpkg.com/) CDN:

```html
<script src="https://unpkg.com/@hop-protocol/sdk@latest/hop.js"></script>
```

## Import module

Import as ES6 module (e.g. Using TypeScript, babel, webpack):

```javascript
import { Hop } from '@hop-protocol/sdk'
```

Import as commonJS module (e.g. Using Node.js directly or no ES6 modules):

```javascript
const { Hop } = require('@hop-protocol/sdk')
```

## Instantiate SDK

```javascript
import { Hop } from '@hop-protocol/sdk'

const hop = new Hop('mainnet')
```

Supported network is only `mainnet`at the moment.

#### Instantiate with ethers Signer for sending transactions:

```javascript
import { Hop } from '@hop-protocol/sdk'
import { Wallet, providers } from 'ethers'

const provider = new providers.getDefaultProvider('mainnet')
const signer = new Wallet(privateKey, provider)
const hop = new Hop('mainnet', signer)
```

Example: Using window web3 provider as signer:

```javascript
import { Hop } from '@hop-protocol/sdk'
import { Wallet } from 'ethers'

const provider = new ethers.providers.Web3Provider(window.ethereum, 'any')
const signer = provider.getSigner()

const hop = new Hop('mainnet', signer)
```

## SDK with Node.js

Basic example that instantiates sdk with signer

```javascript
require('dotenv').config()
const { Hop } = require('@hop-protocol/sdk')
const { Wallet, providers } = require('ethers')

const privateKey = process.env.PRIVATE_KEY
const provider = new providers.getDefaultProvider('mainnet')
const signer = new Wallet(privateKey, provider)

const hop = new Hop('mainnet', signer)
console.log(hop.version)
```

Create `.env` file

```bash
PRIVATE_KEY=<your private key>
```

Running example

```bash
$ node example.js
0.0.1-beta.198
```

## Demo

A simple Hop SDK Demo:

[https://sdk-demo.hop.exchange/](https://sdk-demo.hop.exchange/)

## Examples

### Unit conversion using ethers

The SDK accepts amounts as inputs as big number and most SDK methods return outputs as big numbers, so it's important to know how to convert to and from big numbers.

```javascript
import { parseUnits, formatUnits } from 'ethers/lib/utils'

const decimals = 6

const amountBN = parseUnits('1', decimals)
console.log(amountBN.toString()) // 1000000

const amount = formatUnits('1000000', decimals)
console.log(amount.toString()) // 1.0
```

#### Token decimals

| Symbol | Decimals |
| ------ | -------- |
| USDC   | 6        |
| USDT   | 6        |
| DAI    | 18       |
| MATIC  | 18       |
| ETH    | 18       |
| WBTC   | 8        |
| FRAX   | 18       |
| HOP    | 18       |

### Send tokens across chains

Note: when sending (or generally dealing with amounts in sdk), use values in big number format, e.g. 1 ETH = "1000000000000000000"

#### Send L1->L2

```javascript
import { Hop, Chain } from '@hop-protocol/sdk'

const hop = new Hop('mainnet')
const bridge = hop.connect(signer).bridge('USDC')

// send 100 USDC tokens from Ethereum -> Polygon
const tx = await bridge.send('100000000', Chain.Ethereum, Chain.Polygon)
console.log(tx.hash)
```

Note: there is no bonder fee when sending L1->L2 because transfers go through the native messaging bridge and don't require bonding.

#### Send L2->L1

```javascript
import { Hop, Chain } from '@hop-protocol/sdk'

const hop = new Hop('mainnet')
const bridge = hop.connect(signer).bridge('USDC')

// send 100 USDC tokens from Polygon -> Ethereum
const tx = await bridge.send('100000000', Chain.Polygon, Chain.Ethereum)
console.log(tx.hash)
```

Note: a bonder fee is required when sending L2->L1. It'll calculate it the bonder fee if don't is not explicitly specified. See [specifying a custom fee](https://docs.hop.exchange/js-sdk/getting-started#specifying-custom-bonder-fee) for more info.

#### Send L2->L2

```javascript
import { Hop, Chain } from '@hop-protocol/sdk'

const hop = new Hop('mainnet')
const bridge = hop.connect(signer).bridge('USDC')

// send 100 USDC tokens from Polygon -> Gnosis
const tx = await bridge.send('100000000', Chain.Polygon, Chain.Gnosis)
console.log(tx.hash)
```

Note: a bonder fee is required when sending L2->L2. It'll calculate it the bonder fee if don't is not explicitly specified. See [specifying a custom fee](https://docs.hop.exchange/js-sdk/getting-started#specifying-custom-bonder-fee) for more info.

#### Send ETH

Sending ETH is the same as sending any other ERC-20. The sdk handles inputting the tx `value` based on input amount.

Example

```typescript
const bridge = hop.connect(signer).bridge('ETH')

// send 1 ETH from Polygon -> Gnosis
const tx = await bridge.send('1000000000000000000', Chain.Polygon, Chain.Gnosis)
```

#### Get send calldata only

```typescript
import { Hop, Chain } from '@hop-protocol/sdk'

const hop = new Hop('mainnet')
const bridge = hop.connect(signer).bridge('USDC')

// get tx calldata for sending 100 USDC tokens from Polygon -> Gnosis
const tx = await bridge.populateSendTx('100000000', Chain.Polygon, Chain.Gnosis)
console.log(tx) // { data: '0xdeace8f5000000000000000000000000000000000000000000000000000000000000000a0000000000000000000000002a6303e6b99d451df3566068ebb110708335658f00000000000000000000000000000000000000000000000000000000000f42400000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000006227bdad00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000', to: '0x3666f603Cc164936C1b87e207F36BEBa4AC5f18a' }
```

#### Using BigNumber as amount input

```javascript
import { Hop, Chain } from '@hop-protocol/sdk'
import { parseUnits } from 'ethers/lib/utils'

const hop = new Hop('mainnet')
const bridge = hop.connect(signer).bridge('USDC')

// send 100 USDC tokens from Ethereum -> Polygon
const decimals = 6
const amount = parseUnits('100', decimals)
const tx = await bridge.send(amount, Chain.Ethereum, Chain.Polygon)
console.log(tx.hash)
```

#### Specifying custom bonder fee

By default, the sdk will use the recommended bonder fee if one is not specified. You can set a custom bonder fee in the `bonderFee` field. See [getSendData(...)](https://docs.hop.exchange/js-sdk/getting-started#get-all-send-data-info) for more info on the fee breakdown.

```javascript
import { Hop, Chain } from '@hop-protocol/sdk'

const hop = new Hop('mainnet')
const bridge = hop.connect(signer).bridge('USDC')

const amountBN = '10000000'
const source = Chain.Polygon
const destination =  Chain.Gnosis

// send 100 USDC tokens from Polygon -> Gnosis
const { totalFee } = await bridge.getSendData(amountBN, source, destination)
const tx = await bridge.send(amountBN, source, destination, {
  bonderFee: totalFee
})
console.log(tx.hash)
```

#### Sending to a custom recipient

```javascript
import { Hop, Chain } from '@hop-protocol/sdk'

const hop = new Hop('mainnet')
const bridge = hop.connect(signer).bridge('USDC')

// send 100 USDC tokens from Polygon -> Gnosis
const tx = await bridge.send('100000000', Chain.Polygon, Chain.Gnosis, {
  recipient: '0x123...'
})
console.log(tx.hash)
```

#### Specifying custom min amount out

```javascript
import { Hop, Chain } from '@hop-protocol/sdk'

const hop = new Hop('mainnet')
const bridge = hop.connect(signer).bridge('USDC')

// send 100 USDC tokens from Polygon -> Gnosis
const tx = await bridge.send('100000000', Chain.Polygon, Chain.Gnosis, {
  amountOutMin: '99863953' // must take account fee and slippage
})

console.log(tx.hash)
```

Note: The `amountOutMin` will be `0` if one is not specified. You can use the result from `getSendData(...)` to calculate the estimated `amountOutMin` value.

#### Specify custom deadline

```javascript
import { Hop, Chain } from '@hop-protocol/sdk'

const hop = new Hop('mainnet')
const bridge = hop.connect(signer).bridge('USDC')

// send 100 USDC tokens from Polygon -> Gnosis
const deadline = Math.floor((Date.now() / 1000) + (24 * 60 * 60)) // expire after one day
const tx = await bridge.send('100000000', Chain.Polygon, Chain.Gnosis, {
  deadline
})

console.log(tx.hash)
```

Note: a deadline will be 7 days if one is not specified. The `deadline` is required for L2->L1 transfers and L2->L2 transfers. Additionally, `destinationDeadline` is also required for L2->L1 transfers and L2->L2 transfers to swap the hTokens for the canonical tokens at the destination.

### Get approval address for sending over bridge

```javascript
import { Hop, Chain } from '@hop-protocol/sdk'
import { constants } from 'ethers'

const hop = new Hop('mainnet')
const bridge = hop.connect(signer).bridge('USDC')

// get address to approve for sending over Ethereum -> Polygon Hop bridge
const approvalAddress = await bridge.getSendApprovalAddress(Chain.Ethereum)
console.log(approvalAddress)

const token = bridge.getCanonicalToken(Chain.Ethereum)
const amountToApprove = constants.MaxUint256
const tx = await token.approve(approvalAddress, amountToApprove)
console.log(tx.hash)
```

### Get approval address for sending hTokens over bridge

```javascript
import { Hop, Chain } from '@hop-protocol/sdk'
import { constants } from 'ethers'

const hop = new Hop('mainnet')
const bridge = hop.connect(signer).bridge('USDC')

// get address to approve for sending over Ethereum -> Polygon Hop bridge
const isHToken = true
const approvalAddress = await bridge.getSendApprovalAddress(Chain.Ethereum, isHToken)
console.log(approvalAddress)
```

### Get allowance for bridge approval address

```javascript
import { Hop, Chain } from '@hop-protocol/sdk'
import { constants } from 'ethers'

const hop = new Hop('mainnet')
const bridge = hop.connect(signer).bridge('USDC')

const approvalAddress = await bridge.getSendApprovalAddress(Chain.Ethereum)
const token = bridge.getCanonicalToken(Chain.Ethereum)
const allowance = await token.allowance(approvalAddress)
console.log(allowance)
```

### Check allowance and send approval

```typescript
import { Hop, Chain } from '@hop-protocol/sdk'
import { constants } from 'ethers'
import { parseUnits, formatUnits } from 'ethers/lib/utils'

const hop = new Hop('mainnet')
const bridge = hop.connect(signer).bridge('USDC')

const approvalAddress = await bridge.getSendApprovalAddress(Chain.Ethereum)
const token = bridge.getCanonicalToken(Chain.Ethereum)
const allowance = await token.allowance(approvalAddress)
const transferAmount = parseUnits('1', 6) // 1 USDC
if (allowance.lt(transferAmount)) {
    const tx = await token.approve(approvalAddress, transferAmount)
    console.log(tx.hash)
    await tx.wait()
}
// ...
```

### Send tokens over canonical bridge (deprecated)

#### Deposit tokens (L1 -> L2):

```javascript
import { Hop, Chain } from '@hop-protocol/sdk'

const hop = new Hop('mainnet')
const bridge = hop.connect(signer).canonicalBridge('USDC', Chain.Gnosis)

// send 1 USDC tokens from Ethereum -> Gnosis
const tx = await bridge.deposit('100000000')
console.log(tx.hash)
```

#### Withdraw tokens (L2 -> L1):

```javascript
import { Hop, Chain } from '@hop-protocol/sdk'

const hop = new Hop('mainnet')
const bridge = hop.connect(signer).canonicalBridge('USDC', Chain.Gnosis)

// send 100 USDC tokens from Gnosis -> Ethereum
const tx = await bridge.withdraw('100000000')
console.log(tx.hash)
```

### Estimate tokens amount out from swap

Call this to estimate how many tokens the swap will provide (does not take account slippage or bonder fee):

```javascript
import { Hop, Chain } from '@hop-protocol/sdk'

const hop = new Hop('mainnet')
const bridge = hop.connect(signer).bridge('USDC')

// estimate tokens amount out for 100 USDC
const amountOut = await bridge.getAmountOut('1000000', Chain.Polygon, Chain.Gnosis)
console.log(amountOut) // 998608
```

### Estimate tokens that will be received at destination

Call this to estimate how you'll receive at the destination. This is what the UI uses to show user the estimated tokens amount out.

```javascript
import { Hop, Chain } from '@hop-protocol/sdk'

const hop = new Hop('mainnet')
const bridge = hop.connect(signer).bridge('USDC')

// get estimated tokens out when sending 100 USDC Polygon -> Gnosis
const { estimatedReceived } = await bridge.getSendData('10000000', Chain.Polygon, Chain.Gnosis)
console.log(estimatedReceived.toString()) // 98866001
```

The `estimatedReceived` value takes account the bonder fee and destination transaction fee.

### Estimate total bonder fee

The total bonder fee is `bonderFee`+ `destinationTxFee`

Make sure to use the total bonder fee when sending a transfer over the Hop bridge.

```javascript
import { Hop, Chain } from '@hop-protocol/sdk'

const hop = new Hop('mainnet')
const bridge = hop.connect(signer).bridge('USDC')

// estimate total bonder fee for sending 100 UDSC Polygon -> Gnosis
const totalBonderFee = await bridge.getTotalFee('10000000', Chain.Polygon, Chain.Gnosis)
console.log(toalBonderFee.toString()) // 998239
```

The method `bridge.getTotalFee(...)` is a simple wrapper for `const { totalFee } = await bridge.getSendData(...).`

The following examples below are for retrieving the individual fees if you're interested in the breakdown of the total bonder fee.

#### Estimate base bonder fee:

The base bonder fee is the fee the bonder takes for fronting liquidity at the destination. The bonder receives this fee when bonding the transfer at the destination.

```javascript
import { Hop, Chain } from '@hop-protocol/sdk'

const hop = new Hop('mainnet')
const bridge = hop.connect(signer).bridge('USDC')

// estimate base bonder fee for sending 100 UDSC Polygon -> Gnosis
const totalBonderFee = await bridge.getBonderFee('10000000', Chain.Polygon, Chain.Gnosis)
console.log(toalBonderFee.toString()) // 1000000
```

#### Estimate bonder destination transaction fee:

The bonder destination transaction fee is the regular chain transaction fee that the bonder pays to get transaction included in block. The sender of the transfer must compensate the bonder for this fee which is why this fee exists. The destination transaction fee returned here is in terms of the asset being transferred.

```javascript
import { Hop, Chain } from '@hop-protocol/sdk'

const hop = new Hop('mainnet')
const bridge = hop.connect(signer).bridge('USDC')

// estimate bonder destination tx fee for sending USDC Polygon -> Gnosis
const destinationTxFee = await bridge.getBonderFee(Chain.Polygon, Chain.Gnosis)
console.log(destinationTxFee.toString()) // 772
```

#### Get all send data info:

```javascript
import { Hop, Chain } from '@hop-protocol/sdk'

const hop = new Hop('mainnet')
const bridge = hop.connect(signer).bridge('USDC')

// get all send data info for sending 100 USDC Polygon -> Gnosis
const sendData = await bridge.getSendData('10000000', Chain.Polygon, Chain.Gnosis)
console.log(sendData)
/*
{ amountOut: BigNumber { _hex: '0x05f3cd91', _isBigNumber: true },
  rate: 0.998639,
  priceImpact: -0.06402805611223007,
  requiredLiquidity: BigNumber { _hex: '0x05f7a763', _isBigNumber: true },
  lpFees: BigNumber { _hex: '0x013880', _isBigNumber: true },
  adjustedBonderFee: BigNumber { _hex: '0x0f386a', _isBigNumber: true },
  adjustedDestinationTxFee: BigNumber { _hex: '0x01d6', _isBigNumber: true },
  totalFee: BigNumber { _hex: '0x0f3a40', _isBigNumber: true },
  estimatedReceived: BigNumber { _hex: '0x05e49351', _isBigNumber: true } }
}
*/
```

Return values of `getSendData`

| Property                   | Type      | Description                                                                                                                                                                                 |
| -------------------------- | --------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `amountOut`                | BigNumber | The estimated amount out but without taking account slippage or fees. Use the value `estimatedReceived` if you're looking for the final estimated out amount which takes account fees.      |
| `rate`                     | Number    | The ratio between `amountIn` and `amountOut`                                                                                                                                                |
| `priceImpact`              | Number    | Price impact percentage. Depositing underpooled assets will give you bonus LP tokens. Depositing overpooled assets will give you less LP tokens (shown as negative price impact).           |
| `requiredLiquidity`        | BigNumber | The amount of required liquidity the bonder must have in order for this transfer to go through. Use `getFrontendAvailableLiquidity(...)` to check total available liquidity before sending. |
| `lpFees`                   | BigNumber | The AMM swap fees for `amountIn`                                                                                                                                                            |
| `adjustedBonderFee`        | BigNumber | Small fee bonder takes for fronting liquidity at the destination when bonding transfer. There is a bonderFee going L2->L2 or L2->L1. There is no bonder fee going L1->L2.                   |
| `adjustedDestinationTxFee` | BigNumber | The destination transaction fee that the bonder has to pay when bonding transfer. The sender pays this fee in terms of the token being sent.                                                |
| `totalFee`                 | BigNumber | The total fee consists of bonderFee + destinationTxFee. Use this `totalFee` value for the `bonderFee` parameter when sending transfer going L2->L2 or L2->L1.                               |
| `estimatedReceived`        | BigNumber | The estimated amount that will be received at destination when slippage and all fees (bonderFee + destinationTxfee) are accounted for. This is what the UI displays.                        |

The `getSendData` logic can [viewed in github here](https://github.com/hop-protocol/hop/blob/develop/packages/sdk/src/HopBridge.ts) if you would like to know how it works or implement in another language.

### Get available liquidity for transfer

A transfer can only be bonded if the availale liquidity amount is greater than or equal to the transfer amount. The transfer bond at the destination may be delayed if it is sent when there is low or no available liquidity.

```javascript
import { Hop, Chain } from '@hop-protocol/sdk'

const hop = new Hop('mainnet')
const bridge = hop.connect(signer).bridge('USDC')

// get total available liquidity for Polygon -> Gnosis
const availableLiquidity = await bridge.getFrontendAvailableLiquidity(Chain.Polygon, Chain.Gnosis)
console.log(availableLiquidity.toString()) // 38142941773
```

### Get pool deposit price impact percent

```typescript
import { Hop, Chain } from '@hop-protocol/sdk'
import { parseUnits, formatUnits } from 'ethers/lib/utils'

const hop = new Hop('mainnet')
const bridge = await hop.bridge('USDC').connect(signer)
const amm = bridge.getAmm(Chain.Polygon)
const canonicalTokenAmount = parseUnits('100', 6) // 100 USDC
const hTokenAmount = parseUnits('1', 6) // 1 hUSDC
const impactBn = await amm.getPriceImpact(canonicalTokenAmount, hTokenAmount)
const impactPercent = ((formatUnits(impactBn.toString(), 18)) * 100).toFixed(4)
console.log(`${impactPercent}%`) // 0.0489%
```

Depositing underpooled assets will give you bonus LP tokens. Depositing overpooled assets will give you less LP tokens (shown as negative price impact).

### Watch for receipt events

```javascript
import { Hop, Chain } from '@hop-protocol/sdk'

const hop = new Hop('mainnet')
const bridge = hop.connect(signer).bridge('USDC')
const tx = await bridge.send('1000000', Chain.Ethereum, Chain.Gnosis)

hop
  .watch(tx.hash, Token.USDC, Chain.Ethereum, Chain.Gnosis)
  .on('receipt', data => {
    const { receipt, chain } = data
    console.log(receipt, chain)
  })
})
```

Note: You can also utilize TheGraph for quering for transaction receipts at the destination. See [Hop TheGraph docs](https://docs.hop.exchange/thegraph-subgraphs).

### Set custom provider RPC URLs

```javascript
import { providers } from 'ethers'
import { Hop } from '@hop-protocol/sdk'

const hop = new Hop('mainnet')

hop.setChainProviders({
  ethereum: new providers.StaticJsonRpcProvider('https://mainnet.infura.io/v3/84842078b09946638c03157f83405213'),
  polygon: new providers.StaticJsonRpcProvider('https://polygon-rpc.com'),
  gnosis: new providers.StaticJsonRpcProvider('https://rpc.gnosischain.com'),
  optimism: new providers.StaticJsonRpcProvider('https://mainnet.optimism.io'),
  arbitrum: new providers.StaticJsonRpcProvider('https://arb1.arbitrum.io/rpc'),
})
```

### More examples

If you'd like to see more examples or have any feedback, message us on [Discord](https://discord.gg/PwCF88emV4)!

### SDK API Reference

{% content-ref url="api-reference.md" %}
[api-reference.md](api-reference.md)
{% endcontent-ref %}

### Contract addresses

{% content-ref url="../contract-addresses.md" %}
[contract-addresses.md](../contract-addresses.md)
{% endcontent-ref %}
