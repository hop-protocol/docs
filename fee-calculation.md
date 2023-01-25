---
description: Fee calculation
---

# Fee Calculation

## Bonder Fee

A bonder fee is required when sending L2->L2 or L2->L1. There is no bonder fee when sending L1->L2.

The bonder fee calculation is a little complex since it involves getting AMM estimated amount outs on both source and destination chains and getting the estimated destination bond transaction fee.

The simplest way to get the estimated total bonder fee to use when sending transfers is to use the `getTotalFee()` [JS SDK method](https://docs.hop.exchange/js-sdk/getting-started#estimate-total-bonder-fee).

See bonder fee section in SDK [docs](https://docs.hop.exchange/js-sdk/getting-started#get-all-send-data-info)

{% embed url="https://docs.hop.exchange/js-sdk/getting-started#get-all-send-data-info" %}

### Implementation pseudo code

Here's an pseudo code example for calculating bonder fee.

_Note: The the live fee calculation may change and this may not be up-to-date._

```javascript
bonderFee = getBonderFee(amountIn, source, destination)

getBonderFee(amountIn, source, destination, isHTokenSend) {
  hTokenAmount = getToHTokenAmount(amountIn, source)
  bonderFeeRelative = getBonderFeeRelative(amountIn, source, destination)
  destinationTxFee = getDestinationTxFee(source, destination)
  adjustedBonderFee = 0
  adjustedDestinationTxFee = 0
  totalFee = 0

  if (source != L1) {
    if (isHTokenSend) {
      adjustedBonderFee = bonderFeeRelative
      adjustedDestinationTxFee = destinationTxFee
    } else {
      adjustedBonderFee = getFromHTokenAmount(bonderFeeRelative, destination)
      adjustedDestinationTxFee = getToHTokenAmount(destinationTxFee, destination)
    }

    bonderFeeAbsolute = getBonderFeeAbsolute()
    if (adjustedBonderFee < bonderFeeAbsolute) {
      adjustedBonderFee = bonderFeeAbsolute
    }

    totalFee = adjustedBonderFee + adjustedDestinationTxFee
  }

  return totalFee
}

getToHTokenAmount(amount, chain) {
  if (chain == L1) {
    return amount
  }

  canonicalTokenIndex = 0
  hTokenIndex = 1
  amountOut = getAmmContract(chain).calculateSwap(canonicalTokenIndex, hTokenIndex, amount)

  return amountOut
}

getFromHTokenAmount(amount, chain) {
  if (chain == L1) {
    return amount
  }

  canonicalTokenIndex = 0
  hTokenIndex = 1
  amountOut = getAmmContract(chain).calculateSwap(hTokenIndex, canonicalTokenIndex, amount)

  return amountOut
}

getBonderFeeRelative(amountIn, source, destination) {
  if (source == L1) {
    return 0
  }

  hTokenAmount = getToHTokenAmount(amountIn, source)
  feeBps = getFeeBps(token, dest)
  bonderFeeRelative = (hTokenAmount * feeBps) / 10000

  return bonderFeeRelative
}

getBonderFeeAbsolute() {
  price = getPrice(token)
  minBonderFeeUsd = 0.25
  bonderFeeAbsolute = (minBonderFeeUsd / price)

  return bonderFeeAbsolute
}

getDestinationTxFee(source, destination) {
  if (source == L1) {
    return 0
  }

  nativeTokenPrice = getPrice(getNativeToken(destination))
  tokenPrice = getPrice(token)
  gasPrice = getGasPrice(destination)
  bondTransferGasLimit = getEstimatedBondWithdrawalGasLimit(destination)
  rate = nativeTokenPrice / tokenPrice
  settlementGasLimit = getSettlementGasLimit(destination)
  totalGasLimit = bondTransferGasLimit + settlementGasLimit
  txFeeEth = gasPrice * totalGasLimit
  fee = txFeeEth * rate

  return fee
}
```

The JS implementation is found in the [SDK here](https://github.com/hop-protocol/hop/blob/develop/packages/sdk/src/HopBridge.ts):

## Questions

If you have any questions on the bonder fee calculation, please reach out on [discord](https://docs.hop.exchange/faq#how-can-i-contact-the-hop-team) #dev channel!
