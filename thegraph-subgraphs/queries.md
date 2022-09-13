---
description: Sample Subgraph Queries
---

# Querying

Below are some sample queries you can use to gather information from the Hop contracts.

You can build your own queries using a [GraphQL Explorer](https://graphiql-online.com/graphiql) and enter your endpoint to limit the data to exactly what you need.

# Transfers

- Get transfer root info

```graphql
{
  transfersCommitteds(
    where: {
      rootHash: "0xdda1a36c3cd03b88089659e3c949de2f7bc9e855cb1bdb08b754af765914b4f6"
    }
  ) {
    totalAmount
    transactionHash
    token
    timestamp
  }
}
```

- Get list of transfer roots

```graphql
{
  transfersCommitteds(orderBy: timestamp, orderDirection: desc) {
    totalAmount
    transactionHash
    token
    timestamp
  }
}
```

- Get source transfer info
  - L2>L1 or L2>L2

```graphql
{
  transferSents(
    where: {
      transferId: "0x696c75a27f70ae5210192164a0006a105e71a5b09c117340756bb09d85ddd9a5"
    }
  ) {
    timestamp
    amount
    bonderFee
    transactionHash
    token
    from
    recipient
  }
}
```

- Getting _transferId_ by transaction hash

```graphql
{
  poolSnapshots(
    first: 1000
    orderBy: timestamp
    orderDirection: asc
    where: {
      pool: "0x5c6ee304399dbdb9c8ef030ab642b10820db8f56000200000000000000000014"
    }
  ) {
    amounts
    totalShares
    swapVolume
    swapFees
    liquidity
    pool {
      id
    }
  }
}
```

- Get list of transfers
  - L2>L2 or L2>L1
    - Use L2 subgraphs for these queries (the subgraph used is the origin chain)

```graphql
{
  transferSents(
    where: {
      timestamp_gt: 1650331530
      timestamp_lt: 1652898343
      destinationChainId: 42161
    }
  ) {
    transferId
    amount
    bonderFee
    transactionHash
    token
    timestamp
    from
    recipient
  }
}
```

- L1->L2
  - Use L1 mainnet subgraph for these queries (the L1 subgraph is the origin chain)
    - Note: there is no transferId for L1->L2 transfers. The id is not the same as a transferId.

```graphql
{
  transferSentToL2S(
    where: {
      timestamp_gt: 1650331530
      timestamp_lt: 1652898343
      destinationChainId: 42161
    }
  ) {
    amount
    relayerFee
    transactionHash
    token
    timestamp
    from
    recipient
  }
}
```

- Get list of transfers that were bonded at destination chain
- Use the destination chain subgraph for these queries

```graphql
{
  withdrawalBondeds {
    amount
    transferId
    timestamp
    transactionHash
  }
}
```

**_Note: The WithdrawalBonded event does not contain the recipient or the original sender, so a lookup using the transferId will need to be used on TransferSent (origin from L2) or TransferSentToL2 (origin from L1) to retrieve those values._**

# Volume

- Cumulative volume

```graphql
{
  volumes {
    amount
    token
  }
}
```

- Manual calculation
  - The amount on _transferSents_ (xdai, polygon, arbitrum, optimism) and _transferSentToL2S_ (mainnet) entities can be added up to get overall tx volume on each chain.

```graphql
{
  transferSents {
    destinationChainId
    amount
    token
  }
}
```

```graphql
{
  transferSentToL2S {
    destinationChainId
    amount
    token
  }
}
```

- Daily Volume

```graphql
{
  dailyVolumes(
    where: { token: "ETH", date_gt: 1636416000, date_lte: 1636583276 }
    orderBy: date
    orderDirection: desc
    first: 1
  ) {
    id
    amount
    token
    date
  }
}
```

**The date range is calculated as such:**

```graphql
const now = Math.floor(Date.now() / 1000)
const dayId = Math.floor(now / 86400)
const startDate = (dayId - 1) * 86400
const endDate = now
```

# TVL

⚠️ currently the TVL entities don't report fully accurate data because it's only using add/remove liquidity events instead of tracking transfer events. Use defillama to view accurate TVL.

- Cumutative TVL

```graphql
{
  tvls {
    amount
    token
  }
}
```

- Cumulative AMM TVL

```graphql
{
  ammTvls {
    amount
    token
  }
}
```

# Fees

- Cumulative AMM Fees

```graphql
{
  ammFees {
    amount
    token
  }
}
```

- Cumulative Bonder Fees

```graphql
{
  bonderFees {
    amount
    token
  }
}
```

Manual calculation
The bonder fee can be calculated by adding the _bonderFee_ value from _transferSents_ entities

```graphql
{
  transferSents {
    bonderFee
    destinationChainId
    token
  }
}
```

- LP fees
  - The LP fees can be calculated by adding up *tokensSold*0.0004* from *tokenSwaps\* entities

```graphql
{
  tokenSwaps {
    tokensSold
    token
  }
}
```

# Pagination

- See [TheGraph API Pagination docs](https://docs.hop.exchange/thegraph-subgraphs#get-destination-transfer-info:~:text=See%20TheGraph%20API%20Pagination%20docs%20for%20example%20on%20how%20to%20paginate%20queries) for example on how to paginate queries

# JavaScript fetch example

```graphql
  async function queryFetch(url, query, variables) {
    const res = await fetch(url, {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
        Accept: 'application/json'
      },
      body: JSON.stringify({
        query,
        variables: variables || {}
      })
    })
    const jsonRes = await res.json()
    if (jsonRes.errors && json.errors.length) {
      throw new Error(jsonRes.errors[0].message)
    }
    return jsonRes.data
  }

  async function main() {
    const url = 'https://api.thegraph.com/subgraphs/name/hop-protocol/hop-mainnet'
    const query = `
      query TransferSentToL2($destinationChainId: Int) {
        events: transferSentToL2S(
          where: {
            destinationChainId: $destinationChainId
          },
          orderBy: timestamp,
          orderDirection: desc
        ) {
          id
          destinationChainId
          amount
          amountOutMin
          relayerFee
          recipient
          deadline
          transactionHash
          timestamp
          token
          from
        }
      }
    `
    const variables = {
      destinationChainId: 137
    }
    const result = await queryFetch(url, query, variables)
    console.log(result)
  }

  main().catch(console.error)
```

# FAQ

Why are there multiple subgraphs?
At the moment a subgraph with TheGraph can only be tied to one chain meaning it doesn't have the context or events from the other chains, hence the chain specific subgraph urls. Maybe in the future TheGraph will support multi-chain subgraphs.
