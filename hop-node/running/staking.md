# Staking

You can now stake your funds on the Hop bridge in order to start bonding transfers! Ensure the token you are staking has been sent to the bonder on Ethereum. Additionally, you should have sent funds for gas to the bonder address on each chain.

_**Note**: Currently Bonders must be allowed by the Hop Bridge smart contract. If you are not allowed, you will not be able to stake._


To start staking, you can simply run the stake commands and specify the chain, token, and amount you want to stake. 

Example: Stake on 100 USDC on Arbitrum

{% tabs %}
{% tab title="Docker" %}
```bash
hop stake --chain=arbitrum --token=USDC --amount=100
```
{% endtab %}

{% tab title="Node" %}
```bash
hop-node stake --chain=arbitrum --token=USDC --amount=100
```
{% endtab %}
{% endtabs %}


### Notes

Staking requires hTokens on Layer-2. If you don't have hTokens but have the canonical token, you can still stake. The bonder will send canonical tokens over the Hop bridge on Layer-1 to mint hTokens at the destination Layer-2 chain which will then be used for staking.
