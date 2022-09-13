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
| id               | ID!          | Entity ID |
| newBonder        | String!      | New bonder address |
| block            | Block!       | Block entity |
| transaction      | Transaction! | Transaction entity |
| tokenEntity      | Token!       | Bridge token asset entity |
| transactionHash  | String!      | Transaction hash |
| transactionIndex | BigInt!      | Transaction index |
| timestamp        | BigInt!      | Transaction timestamp |
| blockNumber      | BigInt!      | Transaction block number |
| contractAddress  | String!      | Contract address |
| from             | String!      | From address |
| token            | String!      | Bridge token asset symbol |

# BonderRemoved

Description:

| Field            | Type         | Description |
| ---------------- | ------------ | ----------- |
| id               | ID!          | Entity ID |
| previousBonder   | String!      | Removed bonder address |
| block            | Block!       | Block entity |
| transaction      | Transaction! | Transaction entity |
| tokenEntity      | Token!       | Bridge token asset entity |
| transactionHash  | String!      | Transaction hash |
| transactionIndex | BigInt!      | Transaction index |
| timestamp        | BigInt!      | Transaction timestamp |
| blockNumber      | BigInt!      | Transaction block number |
| contractAddress  | String!      | Contract address |
| from             | String!      | From address |
| token            | String!      | Bridge token asset symbol |

# ChallengeResolved

Description:

| Field            | Type         | Description |
| ---------------- | ------------ | ----------- |
| id               | ID!          | Entity ID |
| transferRootId   | Bytes!       | Transfer root ID |
| rootHash         | Bytes!       | Transfer root hash |
| originalAmount   | BigInt!      | Transfer root original amount |
| block            | Block!       | Block entity |
| transaction      | Transaction! | Transaction entity |
| tokenEntity      | Token!       | Bridge token asset entity |
| transactionHash  | String!      | Transaction hash |
| transactionIndex | BigInt!      | Transaction index |
| timestamp        | BigInt!      | Transaction timestamp |
| blockNumber      | BigInt!      | Transaction block number |
| contractAddress  | String!      | Contract address |
| from             | String!      | From address |
| token            | String!      | Bridge token asset symbol |

# MultipleWithdrawalSettled

Description:

| Field             | Type         | Description |
| ----------------- | ------------ | ----------- |
| id                | ID!          | Entity ID |
| bonder            | String!      | Bonder address |
| rootHash          | Bytes!       | Transfer root hash |
| totalBondsSettled | BigInt!      | Total bonds settled amount |
| block             | Block!       | Block entity |
| transaction       | Transaction! | Transaction entity |
| tokenEntity       | Token!       | Bridge token asset entity |
| transactionHash   | String!      | Transaction hash |
| transactionIndex  | BigInt!      | Transaction index |
| timestamp         | BigInt!      | Transaction timestamp |
| blockNumber       | BigInt!      | Transaction block number |
| contractAddress   | String!      | Contract address |
| from              | String!      | From address |
| token             | String!      | Bridge token asset symbol |

# Stake

Description:

| Field            | Type         | Description |
| ---------------- | ------------ | ----------- |
| id               | ID!          | Entity ID |
| account          | String!      | Bonder account address |
| amount           | BigInt!      | Staked amount |
| block            | Block!       | Block entity |
| transaction      | Transaction! | Transaction entity |
| tokenEntity      | Token!       | Bridge token asset entity |
| transactionHash  | String!      | Transaction hash |
| transactionIndex | BigInt!      | Transaction index |
| timestamp        | BigInt!      | Transaction timestamp |
| blockNumber      | BigInt!      | Transaction block number |
| contractAddress  | String!      | Contract address |
| from             | String!      | From address |
| token            | String!      | Bridge token asset symbol |

# TransferBondChallenged

Description:

| Field            | Type         | Description |
| ---------------- | ------------ | ----------- |
| id               | ID!          | Entity ID |
| transferRootId   | Bytes!       | Transfer root ID |
| rootHash         | Bytes!       | Transfer root hash |
| originalAmount   | BigInt!      | Transfer root original amount |
| block            | Block!       | Block entity |
| transaction      | Transaction! | Transaction entity |
| tokenEntity      | Token!       | Bridge token asset entity |
| transactionHash  | String!      | Transaction hash |
| transactionIndex | BigInt!      | Transaction index |
| timestamp        | BigInt!      | Transaction timestamp |
| blockNumber      | BigInt!      | Transaction block number |
| contractAddress  | String!      | Contract address |
| from             | String!      | From address |
| token            | String!      | Bridge token asset symbol |

# TransferRootBonded

Description:

| Field            | Type         | Description |
| ---------------- | ------------ | ----------- |
| id               | ID!          | Entity ID |
| root             | Bytes!       | Transfer root hash |
| amount           | BigInt!      | Transfer root amount |
| block            | Block!       | Block entity |
| transaction      | Transaction! | Transaction entity |
| tokenEntity      | Token!       | Bridge token asset entity |
| transactionHash  | String!      | Transaction hash |
| transactionIndex | BigInt!      | Transaction index |
| timestamp        | BigInt!      | Transaction timestamp |
| blockNumber      | BigInt!      | Transaction block number |
| contractAddress  | String!      | Contract address |
| from             | String!      | From address |
| token            | String!      | Bridge token asset symbol |

# TransferRootConfirmed

Description:

| Field              | Type         | Description |
| ------------------ | ------------ | ----------- |
| id                 | ID!          | Entity ID |
| originChainId      | BigInt!      | Origin chain ID |
| destinationChainId | BigInt!      | Destination chain ID |
| rootHash           | Bytes!       | Transfer root hash |
| totalAmount        | BigInt!      | Transfer root total amount |
| block              | Block!       | Block entity |
| transaction        | Transaction! | Transaction entity |
| tokenEntity        | Token!       | Bridge token asset entity |
| transactionHash    | String!      | Transaction hash |
| transactionIndex   | BigInt!      | Transaction index |
| timestamp          | BigInt!      | Transaction timestamp |
| blockNumber        | BigInt!      | Transaction block number |
| contractAddress    | String!      | Contract address |
| from               | String!      | From address |
| token              | String!      | Bridge token asset symbol |

# TransferRootSet

Description:

| Field            | Type         | Description |
| ---------------- | ------------ | ----------- |
| id               | ID!          | Entity ID |
| rootHash         | Bytes!       | Transfer root hash |
| totalAmount      | BigInt!      | Transfer root total amount |
| block            | Block!       | Block entity |
| transaction      | Transaction! | Transaction entity |
| tokenEntity      | Token!       | Bridge token asset entity |
| transactionHash  | String!      | Transaction hash |
| transactionIndex | BigInt!      | Transaction index |
| timestamp        | BigInt!      | Transaction timestamp |
| blockNumber      | BigInt!      | Transaction block number |
| contractAddress  | String!      | Contract address |
| from             | String!      | From address |
| token            | String!      | Bridge token asset symbol |

# TransferSentToL2

Description:

| Field              | Type         | Description |
| ------------------ | ------------ | ----------- |
| id                 | ID!          | Entity ID |
| destinationChainId | BigInt!      | Destination chain ID |
| recipient          | String!      | Recipient address |
| amount             | BigInt!      | Amount |
| amountOutMin       | BigInt!      | Minimum amount out |
| deadline           | BigInt!      | Deadline timestamp |
| relayer            | String!      | Relayer address |
| relayerFee         | BigInt!      | Relayer fee amount |
| block              | Block!       | Block entity |
| transaction        | Transaction! | Transaction entity |
| tokenEntity        | Token!       | Bridge token asset entity |
| logIndex           | BigInt!      | Transaction log index |
| transactionHash    | String!      | Transaction hash |
| transactionIndex   | BigInt!      | Transaction index |
| timestamp          | BigInt!      | Transaction timestamp |
| blockNumber        | BigInt!      | Transaction block number |
| contractAddress    | String!      | Contract address |
| from               | String!      | From address |
| token              | String!      | Bridge token asset symbol |

# Unstake

Description:

| Field            | Type         | Description |
| ---------------- | ------------ | ----------- |
| id               | ID!          | Entity ID |
| account          | String!      | Bonder account address |
| amount           | BigInt!      | Unstaked amount |
| block            | Block!       | Block entity |
| transaction      | Transaction! | Transaction entity |
| tokenEntity      | Token!       | Bridge token asset entity |
| transactionHash  | String!      | Transaction hash |
| transactionIndex | BigInt!      | Transaction index |
| timestamp        | BigInt!      | Transaction timestamp |
| blockNumber      | BigInt!      | Transaction block number |
| contractAddress  | String!      | Contract address |
| from             | String!      | From address |
| token            | String!      | Bridge token asset symbol |

# WithdrawalBondSettled

Description:

| Field            | Type         | Description |
| ---------------- | ------------ | ----------- |
| id               | ID!          | Entity ID |
| bonder           | String!      | Bonder address |
| transferId       | Bytes!       | Transfer ID |
| rootHash         | Bytes!       | Transfer root hash |
| block            | Block!       | Block entity |
| transaction      | Transaction! | Transaction entity |
| tokenEntity      | Token!       | Bridge token asset entity |
| transactionHash  | String!      | Transaction hash |
| transactionIndex | BigInt!      | Transaction index |
| timestamp        | BigInt!      | Transaction timestamp |
| blockNumber      | BigInt!      | Transaction block number |
| contractAddress  | String!      | Contract address |
| from             | String!      | From address |
| token            | String!      | Bridge token asset symbol |

# WithdrawalBonded

Description:

| Field            | Type         | Description |
| ---------------- | ------------ | ----------- |
| id               | ID!          | Entity ID |
| transferId       | Bytes!       | Transfer ID |
| amount           | BigInt!      | Amount |
| block            | Block!       | Block entity |
| transaction      | Transaction! | Transaction entity |
| tokenEntity      | Token!       | Bridge token asset entity |
| transactionHash  | String!      | Transaction hash |
| transactionIndex | BigInt!      | Transaction index |
| timestamp        | BigInt!      | Transaction timestamp |
| blockNumber      | BigInt!      | Transaction block number |
| contractAddress  | String!      | Contract address |
| from             | String!      | From address |
| token            | String!      | Bridge token asset symbol |

# Withdrew

Description:

| Field            | Type         | Description |
| ---------------- | ------------ | ----------- |
| id               | ID!          | Entity ID |
| transferId       | Bytes!       | Transfer ID |
| recipient        | String!      | Recipient address |
| amount           | BigInt!      | Amount |
| transferNonce    | Bytes!       | Transfer nonce |
| block            | Block!       | Block entity |
| transaction      | Transaction! | Transaction entity |
| tokenEntity      | Token!       | Bridge token asset entity |
| transactionHash  | String!      | Transaction hash |
| transactionIndex | BigInt!      | Transaction index |
| timestamp        | BigInt!      | Transaction timestamp |
| blockNumber      | BigInt!      | Transaction block number |
| contractAddress  | String!      | Contract address |
| from             | String!      | From address |
| token            | String!      | Bridge token asset symbol |

# Transfer

Description:

| Field            | Type         | Description |
| ---------------- | ------------ | ----------- |
| id               | ID!          | Entity ID |
| from             | String!      | From address |
| to               | String!      | To address |
| value            | BigInt!      | Transfer amount |
| block            | Block!       | Block entity |
| transaction      | Transaction! | Transaction entity |
| tokenEntity      | Token!       | Bridge token asset entity |
| transactionHash  | String!      | Transaction hash |
| transactionIndex | BigInt!      | Transaction index |
| timestamp        | BigInt!      | Transaction timestamp |
| blockNumber      | BigInt!      | Transaction block number |
| contractAddress  | String!      | Contract address |
| token            | String!      | Bridge token asset symbol            |

# Tvl

Description:

| Field  | Type    | Description |
| ------ | ------- | ----------- |
| id     | ID!     | Entity ID |
| amount | BigInt! | TVL total amount |
| token  | String! | Bridge token asset symbol |

# Volume

Description:

| Field       | Type    | Description |
| ----------- | ------- | ----------- |
| id          | ID!     | Entity ID |
| amount      | BigInt! | Cumulative volume total amount |
| tokenEntity | Token!  | Bridge token asset entity |
| token       | String! | Bridge token asset symbol |

# DailyVolume

Description:

| Field       | Type    | Description |
| ----------- | ------- | ----------- |
| id          | ID!     | Entity ID |
| amount      | BigInt! | Daily volume amount |
| date        | Int!    | Date unix timestamp |
| tokenEntity | Token!  | Bridge token asset entity |
| token       | String! | Bridge token asset symbol |

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
