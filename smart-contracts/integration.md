---
description: Smart contract integration
---

# Integration

## L1->L2

To send funds L1->L2, call the `sendToL2` [method](https://github.com/hop-protocol/contracts/blob/8cefc3975115b6e3e706dd110670badad954a3bd/contracts/bridges/L1\_Bridge.sol#L109) on the L1 Bridge contract:

```solidity
sendToL2(
    uint256 chainId,
    address recipient,
    uint256 amount,
    uint256 amountOutMin,
    uint256 deadline,
    address relayer,
    uint256 relayerFee
)
```

The `relayer` and `relayerFee` is only used if a 3rd party is relaying the transfer on the user's behalf (ie the relayer is paying for transaction fee). You can set the `relayer` to the zero address and `relayerFee` to `0` if you are not using a relayer (majority of integrations do not use a relayer).

### L2->L1 and L2->L2

To send funds L2->L1 or L2->L2, call the `swapAndSend` [method](https://github.com/hop-protocol/contracts/blob/8cefc3975115b6e3e706dd110670badad954a3bd/contracts/bridges/L2\_AmmWrapper.sol#L58) on the L2 AMM Wrapper contract:

```solidity
swapAndSend(
    uint256 chainId,
    address recipient,
    uint256 amount,
    uint256 bonderFee,
    uint256 amountOutMin,
    uint256 deadline,
    uint256 destinationAmountOutMin,
    uint256 destinationDeadline
)
```

Note: **Do not set `destinationAmountOutMin` and `destinationDeadline` when sending to L1 because there is no AMM on L1, otherwise the calculated transferId will be invalid and the transfer will be unbondable.** These parameters should be set to `0` when sending to L1.

### L2 hTokens->L2 or L2 hTokens -> L1

To send hTokens L2->L2 or hTokens L2->L1, call the `send` [method](https://github.com/hop-protocol/contracts/blob/8cefc3975115b6e3e706dd110670badad954a3bd/contracts/bridges/L2\_Bridge.sol#L117) on the L2 Bridge contract:

```solidity
send(
    uint256 chainId,
    address recipient,
    uint256 amount,
    uint256 bonderFee,
    uint256 amountOutMin,
    uint256 deadline
)
```

Note: There are no hTokens on L1 so sending L2 hUSDC to L1 means you'll receive USDC on L1.

Note: **Do not set `amountOutMin` and `deadline` when sending to L1 because there is no AMM on L1, otherwise the calculated transferId will be invalid and the transfer will be unbondable.** These parameters should be set to `0` when sending to L1.

### Sending ETH vs Token

When sending native asset from source chain (ie ETH on Ethereum, Optimism, Arbitrum, or XDAI on Gnosis Chain, or MATIC on Polygon), set the transaction `value` to match the `amount` parameter.

### swapAndSend vs send

`swapAndSend` (on L2 AMM Wrapper) on the source chain swaps your canonical token (eg USDC) to hTokens (eg hUSDC) and burns the hTokens and then you receive the canonical tokens (eg USDC) on the destination chain.

`send` on (on L2 Bridge) is for only dealing with hTokens. The `send` method on the source chain takes your hTokens (ie hUSDC), burns the hTokens and then you receive hTokens (eg hUSDC) on the destination chain.

swapAndSend is what you'd want to use most of the time since the canonical tokens are what users are interested in.

### Calling Hop from smart contract

Some good examples you can check out as a reference are:

* [InstaDapp](https://instadapp.io/) DSA connector contracts ([helpers.sol](https://github.com/Instadapp/dsa-connectors/blob/b0a9c6f8333eb2252a49f3c6ac4900ab03db8d21/contracts/mainnet/connectors/hop/helpers.sol#L38))
* [movr](https://www.movr.network/) bridge aggregator contracts ([Hop.sol](https://polygonscan.com/address/0x2b42AFFD4b7C14d9B7C2579229495c052672Ccd3#code))
* [LI.FI](https://li.fi/) bridge aggregator contracts ([HopFacet.sol](https://polygonscan.com/address/0xc46304a0b2accc4462d9bdcaa0f6bf632510d617#code))

### Contract addresses

The L1 Bridge addresses, L2 Bridge addresses, L2 AMM wrapper addresses, and other Hop contract addresses can be found on this link:

{% content-ref url="../contract-addresses.md" %}
[contract-addresses.md](../contract-addresses.md)
{% endcontent-ref %}
