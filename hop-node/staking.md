# Staking

### Stake command

Add liquidity for bonding transfers.

Example: Stake on 100 USDC on Arbitrum&#x20;

{% tabs %}
{% tab title="Docker" %}
```bash
docker run -it -v ~/.hop-node:/root hopprotocol/hop-node stake --config /root/config.json --chain=arbitrum --token=USDC --amount=100
```
{% endtab %}

{% tab title="Node" %}
```bash
hop-node stake --chain=arbitrum --token=USDC --amount=100
```
{% endtab %}
{% endtabs %}

### Unstake command

Remove liquidity any unused liquidity

Example: Unstake on 100 USDC on Arbitrum&#x20;

{% tabs %}
{% tab title="Docker" %}
```bash
docker run -it -v ~/.hop-node:/root hopprotocol/hop-node unstake --config /root/config.json --chain=arbitrum --token=USDC --amount=100
```
{% endtab %}

{% tab title="Node" %}
```bash
hop-node unstake --chain=arbitrum --token=USDC --amount=100
```
{% endtab %}
{% endtabs %}

### Stake status command

Show staked amounts as credit and debit balances

Example: Show USDC amount staked on Arbitrum

{% tabs %}
{% tab title="Docker" %}
```bash
docker run -it -v ~/.hop-node:/root hopprotocol/hop-node stake-status --config /root/config.json --chain=arbitrum --token=USDC
```
{% endtab %}

{% tab title="Node" %}
```bash
hop-node stake-status --chain=arbitrum --token=USDC
```
{% endtab %}
{% endtabs %}

### Stake options

| Argument | Example    | Description                                                                                                                                                                                                         |
| -------- | ---------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `chain`  | `arbitrum` | <p>Chain to stake hTokens on. On Layer-1, canonical tokens are staked.</p><p></p><p>Options are: <code>ethereum</code>, <code>arbitrum</code>, <code>optimism</code>, <code>polygon</code>, <code>gnosis</code></p> |
| `token`  | `USDC`     | <p>Asset to stake for.</p><p></p><p>Options are: <code>USDC</code>, <code>USDT</code>, <code>DAI</code>, <code>MATIC</code>, <code>ETH</code></p>                                                                   |
| `amount` | `15000`    | Amount to stake, in human readable format. Example: `--amount=100` is exactly `100` USDC                                                                                                                            |

### Notes

Staking requires hTokens on Layer-2. If you don't have hTokens but have the canonical token, you can still stake. The bonder will send canonical tokens over the Hop bridge on Layer-1 to mint hTokens at the destination Layer-2 chain which will then be used for staking.
