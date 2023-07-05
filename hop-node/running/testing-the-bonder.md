---
description: Testing the Bonder
---

You are now ready to test the bonder! Follow the instructions to test that the bonder client is correctly set up! This test will send a transaction to yourself on the Ethereum mainnet to validate that your bonder can transact. It will then stake and unstake the token on the Ethereum mainnet.

## Send Funds to the Bonder Address

You must start by sending funds to the bonder address. Since this is a test, you only need to send a small amount:

* 0.2 ETH
* 1 token

## Run the Self-Test Command
```bash
hop self-test --token <YOUR_TOKEN> --amount 1
```

If the test is successful, you will see logs that describe the transactions made.