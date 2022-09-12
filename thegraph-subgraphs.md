---
description: Subgraph links and examples
---

# TheGraph Subgraphs

## Subgraph Links

Subgraph links

* [hop-protocol/hop-mainnet](https://thegraph.com/hosted-service/subgraph/hop-protocol/hop-mainnet)
* [hop-protocol/hop-polygon](https://thegraph.com/hosted-service/subgraph/hop-protocol/hop-polygon)
* [hop-protocol/hop-xdai](https://thegraph.com/hosted-service/subgraph/hop-protocol/hop-xdai)
* [hop-protocol/hop-arbitrum](https://thegraph.com/hosted-service/subgraph/hop-protocol/hop-arbitrum)
* [hop-protocol/hop-optimism](https://thegraph.com/hosted-service/subgraph/hop-protocol/hop-optimism)

## Examples

### Transfers

Use these subgraphs for querying L2->L2 or L2->L1 transfers (query for `transferSent` entities)

* `hop-protocol/hop-polygon`
* `hop-protocol/hop-xdai`
* `hop-protocol/hop-arbitrum`
* `hop-protocol/hop-optimism`

Use this subgraph for L1->L2 transfers (query for `transferSentToL2` entities)

* `hop-protocol/hop-mainnet`

#### Get transfer root info

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

#### Get list of transfer roots

```graphql
{
  transfersCommitteds(
    orderBy: timestamp,
    orderDirection: desc
  ) {
    totalAmount
    transactionHash
    token
    timestamp
  }
}
```

#### Get source transfer info&#x20;

L2->L1 or L2->L2

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

Getting `transferId` by transaction hash

```graphql
{
  transferSents(
    where: {
      transactionHash: "0xb61a2468312ed2d5af1ed288cdfafe64d97a4df56d929f44c039649bc8dec892"
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

Get list of transfers

L2->L2 or L2->L1

```graphql
{
  transferSents(
    orderBy: timestamp,
    orderDirection: desc
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

L1->L2

```graphql
{
  transferFromL1Completeds(
    where: {
      recipient: "0x7d5fda35a5f885a286da02ccc2fa4614eb3842da"
    },
    orderBy: timestamp,
    orderDirection: desc
  ) {
    amount
    transactionHash
    token
    timestamp
    from
  }
}
```

#### Get destination transfer info

L2->L1 or L2->L2

```graphql
{
  withdrawalBondeds(
    where: {
      transferId: "0x696c75a27f70ae5210192164a0006a105e71a5b09c117340756bb09d85ddd9a5"
    }
  ) {
    amount
    transactionHash
    token
    timestamp
    from
  }
}
```

L1->L2

There is no bonding sending L1-> so you need to check the event `transferFromL1Completeds` and **not** `withdrawalBondeds`.&#x20;

There is **no** `transferId` when sending L1->L2 so you need to use something like `recipient` and `amount` in the where clause to match the origin transfer from the `transferSentToL2s` event.

```graphql
{
  transferFromL1Completeds(
    where: {
      recipient: "0x7d5fda35a5f885a286da02ccc2fa4614eb3842da"
    },
    orderBy: timestamp,
    orderDirection: desc
  ) {
    amount
    transactionHash
    token
    timestamp
    from
  }
}
```

#### Get list of transfers to a destination chain

**L2->L2** or **L2->L1**&#x20;

Use L2 subgraphs for these queries (the subgraph used is the origin chain)

```graphql
{
  transferSents(
    where: {
      timestamp_gt: 1650331530,
      timestamp_lt: 1652898343,
      destinationChainId: 42161
    },
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

**L1->L2**

Use L1 mainnet subgraph for these queries (the L1 subgraph is the origin chain)&#x20;

```graphql
{
  transferSentToL2S(
    where: {
      timestamp_gt: 1650331530,
      timestamp_lt: 1652898343,
      destinationChainId: 42161
    },
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

Note: there is **no** `transferId` for L1->L2 transfers. The `id` is **not** the same as a `transferId`.

#### Get list of transfers that were bonded at destination chain

Use the destination chain subgraph for these queries

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

Note: The `WithdrawalBonded` event does not contain the recipient or the original sender, so a lookup using the `transferId` will need to be used on `TransferSent` (origin from L2) or `TransferSentToL2` (origin from L1) to retrieve those values.

### Volume

#### Cumulative volume

```graphql
{
  volumes {
    amount
    token
  }
}
```

Manual calculation

The amount on `transferSents` (xdai, polygon, arbitrum, optimism) and `transferSentToL2S` (mainnet) entities can be added up to get overall tx volume on each chain.

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

#### Daily volume

```graphql
{
  dailyVolumes(
    where: {
      token: "ETH",
      date_gt: 1636416000,
      date_lte: 1636583276
    },
    orderBy: date,
    orderDirection: desc,
    first: 1
  ) {
    id
    amount
    token
    date
  }
}
```

The date range is calculated as such:

```javascript
const now = Math.floor(Date.now() / 1000)
const dayId = Math.floor(now / 86400)
const startDate = (dayId - 1) * 86400
const endDate = now
```

### TVL

⚠️ currently the TVL entities don't report fully accurate data because it's only using add/remove liquidity events instead of tracking transfer events. Use [defillama](https://defillama.com/protocol/hop-protocol) to view accurate TVL.

#### Cumulative TVL

```graphql
{
  tvls {
    amount
    token
  }
}
```

#### Cumulative AMM TVL

```graphql
{
  ammTvls {
    amount
    token
  }
}
```

### Fees

#### Cumulative AMM Fees

```graphql
{
  ammFees {
    amount
    token
  }
}
```

#### Cumulative Bonder fees

```graphql
{
  bonderFees {
    amount
    token
  }
}
```

Manual calculation

The bonder fee can be calculated by adding the `bonderFee` value from `transferSents` entities

```graphql
{
  transferSents {
    bonderFee
    destinationChainId
    token
  }
}
```

#### LP fees

The LP fees can be calculated by adding up `tokensSold*0.0004` from `tokenSwaps` entities

```graphql
{
  tokenSwaps {
    tokensSold
    token
  }
}
```

### Pagination

See [TheGraph API Pagination docs](https://thegraph.com/docs/en/developer/graphql-api/#pagination) for example on how to paginate queries

### JavaScript fetch example

```javascript
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

### FAQ

#### Why are there multiple subgraphs?

At the moment a subgraph with TheGraph can only be tied to one chain meaning it doesn't have the context or events from the other chains, hence the chain specific subgraph urls. Maybe in the future TheGraph will support multi-chain subgraphs.
