---
description: Subgraph Entities
---

# Entities

- [`BonderAdded`](#bonderadded)
- [`BonderRemoved`](#bonderremoved)
- [`ChallengeResolved`](#challengeresolved)
- [`MultipleWithdrawalsSettled`](#multiplewithdrawalsettled)
- [`Stake`](#stake)
- [`TransferBondChallenged`](#transferbondchallenged)
- [`TransferRootBonded`](#transferrootbonded)
- [`TransferRootConfirmed`](#transferrootconfirmed)
- [`TransferRootSet`](#transferrootset)
- [`TransferSentToL2`](#transfersenttol2)
- [`Unstake`](#unstake)
- [`WithdrawalBondSettled`](#withdrawalbondsettled)
- [`WithdrawalBonded`](#withdrawalbonded)
- [`Withdrew`](#withdrew)
- [`Transfer`](#transfer)
- [`Tvl`](#tvl)
- [`Volume`](#volume)
- [`DailyVolume`](#dailyvolume)
- [`Block`](#block)
- [`Transaction`](#transaction)
- [`Token`](#token)

# BonderAdded

Description:

| Field            | Type         | Description |
| ---------------- | ------------ | ----------- |
| id               | ID!          |             |
| newBonder        | String!      |             |
| block            | Block!       |             |
| transaction      | Transaction! |             |
| tokenEntity      | Token!       |             |
| totalSwapVolume  | BigDecimal!  |             |
| totalSwapFee     | BigDecimal!  |             |
| transactionHash  | String!      |             |
| transactionIndex | BigInt!      |             |
| timestamp        | BigInt!      |             |
| blockNumber      | BigInt!      |             |
| contractAddress  | String!      |             |
| from             | String!      |             |
| token            | String!      |             |

# BonderRemoved

Description:

| Field            | Type         | Description |
| ---------------- | ------------ | ----------- |
| id               | ID!          |             |
| previousBonder   | String!      |             |
| block            | Block!       |             |
| transaction      | Transaction! |             |
| tokenEntity      | Token!       |             |
| transactionHash  | String!      |             |
| transactionIndex | BigInt!      |             |
| timestamp        | BigInt!      |             |
| blockNumber      | BigInt!      |             |
| contractAddress  | String!      |             |
| from             | String!      |             |
| token            | String!      |             |

# ChallengeResolved

Description:

| Field            | Type         | Description |
| ---------------- | ------------ | ----------- |
| id               | ID!          |             |
| transferRootId   | Bytes!       |             |
| rootHash         | Bytes!       |             |
| originalAmount   | BigInt!      |             |
| block            | Block!       |             |
| transaction      | Transaction! |             |
| tokenEntity      | Token!       |             |
| transactionHash  | String!      |             |
| transactionIndex | BigInt!      |             |
| timestamp        | BigInt!      |             |
| blockNumber      | BigInt!      |             |
| contractAddress  | String!      |             |
| from             | String!      |             |
| token            | String!      |             |

# MultipleWithdrawalSettled

Description:

| Field             | Type         | Description |
| ----------------- | ------------ | ----------- |
| id                | ID!          |             |
| bonder            | String!      |             |
| rootHash          | Bytes!       |             |
| totalBondsSettled | BigInt!      |             |
| block             | Block!       |             |
| transaction       | Transaction! |             |
| tokenEntity       | Token!       |             |
| transactionHash   | String!      |             |
| transactionIndex  | BigInt!      |             |
| timestamp         | BigInt!      |             |
| blockNumber       | BigInt!      |             |
| contractAddress   | String!      |             |
| from              | String!      |             |
| token             | String!      |             |

# Stake

Description:

| Field            | Type         | Description |
| ---------------- | ------------ | ----------- |
| id               | ID!          |             |
| account          | String!      |             |
| amount           | BigInt!      |             |
| block            | Block!       |             |
| transaction      | Transaction! |             |
| tokenEntity      | Token!       |             |
| transactionHash  | String!      |             |
| transactionIndex | BigInt!      |             |
| timestamp        | BigInt!      |             |
| blockNumber      | BigInt!      |             |
| contractAddress  | String!      |             |
| from             | String!      |             |
| token            | String!      |             |

# TransferBondChallenged

Description:

| Field            | Type         | Description |
| ---------------- | ------------ | ----------- |
| id               | ID!          |             |
| transferRootId   | Bytes!       |             |
| rootHash         | Bytes!       |             |
| originalAmount   | BigInt!      |             |
| block            | Block!       |             |
| transaction      | Transaction! |             |
| tokenEntity      | Token!       |             |
| transactionHash  | String!      |             |
| transactionIndex | BigInt!      |             |
| timestamp        | BigInt!      |             |
| blockNumber      | BigInt!      |             |
| contractAddress  | String!      |             |
| from             | String!      |             |
| token            | String!      |             |

# TransferRootBonded

Description:

| Field            | Type         | Description |
| ---------------- | ------------ | ----------- |
| id               | ID!          |             |
| root             | Bytes!       |             |
| amount           | BigInt!      |             |
| block            | Block!       |             |
| transaction      | Transaction! |             |
| tokenEntity      | Token!       |             |
| transactionHash  | String!      |             |
| transactionIndex | BigInt!      |             |
| timestamp        | BigInt!      |             |
| blockNumber      | BigInt!      |             |
| contractAddress  | String!      |             |
| from             | String!      |             |
| token            | String!      |             |

# TransferRootConfirmed

Description:

| Field              | Type         | Description |
| ------------------ | ------------ | ----------- |
| id                 | ID!          |             |
| originChainId      | BigInt!      |             |
| destinationChainId | BigInt!      |             |
| rootHash           | Bytes!       |             |
| totalAmount        | BigInt!      |             |
| block              | Block!       |             |
| transaction        | Transaction! |             |
| tokenEntity        | Token!       |             |
| transactionHash    | String!      |             |
| transactionIndex   | BigInt!      |             |
| timestamp          | BigInt!      |             |
| blockNumber        | BigInt!      |             |
| contractAddress    | String!      |             |
| from               | String!      |             |
| token              | String!      |             |

# TransferRootSet

Description:

| Field            | Type         | Description |
| ---------------- | ------------ | ----------- |
| id               | ID!          |             |
| rootHash         | Bytes!       |             |
| totalAmount      | BigInt!      |             |
| block            | Block!       |             |
| transaction      | Transaction! |             |
| tokenEntity      | Token!       |             |
| transactionHash  | String!      |             |
| transactionIndex | BigInt!      |             |
| timestamp        | BigInt!      |             |
| blockNumber      | BigInt!      |             |
| contractAddress  | String!      |             |
| from             | String!      |             |
| token            | String!      |             |

# TransferSentToL2

Description:

| Field              | Type         | Description |
| ------------------ | ------------ | ----------- |
| id                 | ID!          |             |
| destinationChainId | BigInt!      |             |
| recipient          | String!      |             |
| amount             | BigInt!      |             |
| amountOutMin       | BigInt!      |             |
| deadline           | BigInt!      |             |
| relayer            | String!      |             |
| relayerFee         | BigInt!      |             |
| block              | Block!       |             |
| transaction        | Transaction! |             |
| tokenEntity        | Token!       |             |
| logIndex           | BigInt!      |             |
| transactionHash    | String!      |             |
| transactionIndex   | BigInt!      |             |
| timestamp          | BigInt!      |             |
| blockNumber        | BigInt!      |             |
| contractAddress    | String!      |             |
| from               | String!      |             |
| token              | String!      |             |

# Unstake

Description:

| Field            | Type         | Description |
| ---------------- | ------------ | ----------- |
| id               | ID!          |             |
| account          | String!      |             |
| amount           | BigInt!      |             |
| block            | Block!       |             |
| transaction      | Transaction! |             |
| tokenEntity      | Token!       |             |
| transactionHash  | String!      |             |
| transactionIndex | BigInt!      |             |
| timestamp        | BigInt!      |             |
| blockNumber      | BigInt!      |             |
| contractAddress  | String!      |             |
| from             | String!      |             |
| token            | String!      |             |

# WithdrawalBondSettled

Description:

| Field            | Type         | Description |
| ---------------- | ------------ | ----------- |
| id               | ID!          |             |
| bonder           | String!      |             |
| transferId       | Bytes!       |             |
| rootHash         | Bytes!       |             |
| block            | Block!       |             |
| transaction      | Transaction! |             |
| tokenEntity      | Token!       |             |
| transactionHash  | String!      |             |
| transactionIndex | BigInt!      |             |
| timestamp        | BigInt!      |             |
| blockNumber      | BigInt!      |             |
| contractAddress  | String!      |             |
| from             | String!      |             |
| token            | String!      |             |

# WithdrawalBonded

Description:

| Field            | Type         | Description |
| ---------------- | ------------ | ----------- |
| id               | ID!          |             |
| transferId       | Bytes!       |             |
| amount           | BigInt!      |             |
| block            | Block!       |             |
| transaction      | Transaction! |             |
| tokenEntity      | Token!       |             |
| transactionHash  | String!      |             |
| transactionIndex | BigInt!      |             |
| timestamp        | BigInt!      |             |
| blockNumber      | BigInt!      |             |
| contractAddress  | String!      |             |
| from             | String!      |             |
| token            | String!      |             |

# Withdrew

Description:

| Field            | Type         | Description |
| ---------------- | ------------ | ----------- |
| id               | ID!          |             |
| transferId       | Bytes!       |             |
| recipient        | String!      |             |
| amount           | BigInt!      |             |
| transferNonce    | Bytes!       |             |
| block            | Block!       |             |
| transaction      | Transaction! |             |
| tokenEntity      | Token!       |             |
| transactionHash  | String!      |             |
| transactionIndex | BigInt!      |             |
| timestamp        | BigInt!      |             |
| blockNumber      | BigInt!      |             |
| contractAddress  | String!      |             |
| from             | String!      |             |
| token            | String!      |             |

# Transfer

Description:

| Field            | Type         | Description |
| ---------------- | ------------ | ----------- |
| id               | ID!          |             |
| from             | String!      |             |
| to               | String!      |             |
| value            | BigInt!      |             |
| block            | Block!       |             |
| transaction      | Transaction! |             |
| tokenEntity      | Token!       |             |
| transactionHash  | String!      |             |
| transactionIndex | BigInt!      |             |
| timestamp        | BigInt!      |             |
| blockNumber      | BigInt!      |             |
| contractAddress  | String!      |             |
| token            | String!      |             |

# Tvl

Description:

| Field  | Type    | Description |
| ------ | ------- | ----------- |
| id     | ID!     |             |
| amount | BigInt! |             |
| token  | String! |             |

# Volume

Description:

| Field       | Type    | Description |
| ----------- | ------- | ----------- |
| id          | ID!     |             |
| amount      | BigInt! |             |
| tokenEntity | Token!  |             |
| token       | String! |             |

# DailyVolume

Description:

| Field       | Type    | Description |
| ----------- | ------- | ----------- |
| id          | ID!     |             |
| amount      | BigInt! |             |
| date        | Int!    |             |
| tokenEntity | Token!  |             |
| token       | String! |             |

# Block

Description:

| Field            | Type    | Description             |
| ---------------- | ------- | ----------------------- |
| id               | ID!     | Block hash              |
| author           | Bytes!  | Block author            |
| difficulty       | BigInt! | Block difficulty        |
| gasLimit         | BigInt! | Block gas limit         |
| gasUsed          | BigInt! | Block gas used          |
| hash             | Bytes!  | Block hash              |
| number           | BigInt! | Block number            |
| parentHash       | Bytes!  | Block parent hash       |
| receiptsRoot     | Bytes!  | Block receipts root     |
| size             | BigInt  | Block size              |
| stateRoot        | Bytes!  | Block state root        |
| timestamp        | BigInt! | Block timestamp         |
| totalDifficulty  | BigInt! | Block total difficulty  |
| transactionsRoot | Bytes!  | Block transactions root |
| unclesHash       | Bytes!  | Block uncles hash       |

# Transaction

Description:

| Field    | Type    | Description              |
| -------- | ------- | ------------------------ |
| id       | ID!     | Transaction hash         |
| from     | Bytes!  | Transaction from address |
| gasLimit | BigInt! | Transaction gas limit    |
| gasPrice | BigInt! | Transaction gas price    |
| hash     | Bytes!  | Transaction hash         |
| index    | BigInt! | Transaction index        |
| input    | Bytes!  | Transaction input        |
| to       | Bytes   | Transaction to address   |
| value    | BigInt! | Transaction value        |

# Token

Description:

| Field    | Type    | Description    |
| -------- | ------- | -------------- |
| id       | ID!     | Token address  |
| address  | Bytes!  | Token address  |
| decimals | Int!    | Token decimals |
| name     | String! | Token name     |
| symbol   | String! | Token symbol   |
