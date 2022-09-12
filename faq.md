---
description: Frequenty asked questions
---

# FAQ

## What is Hop Protocol?

Hop is a scalable rollup-to-rollup general token bridge. It allows users to send tokens from one rollup to another almost immediately without having to wait for the rollup’s challenge period.

## Where can I find the whitepaper?

The whitepaper is available at: [https://hop.exchange/whitepaper.pdf](https://hop.exchange/whitepaper.pdf)

## Does Hop have a token?

Yes, Hop has [announced](https://twitter.com/HopProtocol/status/1522284534598967300) a governance token (HOP).

## Does Hop have a Telegram group?

No, Hop does **not** have an official telegram group. If you see any telegram groups with the Hop name and/or logo then they are probably **scams**. Be careful!

## What are hTokens (ie hETH, hUSDC, hDAI, etc)?

The “h” tokens are a cross-network bridge token that is transferred from rollup-to-rollup and are claimed on the layer-1 for the underlying asset. It is an intermediary bridge token that allows trustless swaps.

The end user doesn't need to deal with “h” tokens directly, they only deal with the respective rollup’s canonical token.

## What is a “canonical token”?

The canonical token (also called "native token") is the Layer-1 token that is being bridged on Layer-2. For example, DAI token on Layer-2 is the canonical token of DAI token on Layer-1. Users can send back and forth between Layer-1 token and Layer-2 representation of that token using the Layer-2’s official token bridge.

## Why is an AMM needed?

The AMM dynamically prices liquidity and incentivizes rebalancing liquidity on each rollup.

## What is a “bonder”?

A bonder providers up-front liquidity on the destination rollup to allow instant transfers, and are incentivized by transfer fees.

## What does a transfer consist of?

Destination chain id, destination recipient address, and transfer amount.

## What is a “transfer root”?

A transfer root object represents a bundle of transfers. A transfer root is composed of a merkle root of the transfer IDs and list of total amounts for each destination rollup chain.

## What is a “transfer bond”?

A transfer bond is the bonding of a transfer root which distributes the transfer root from Layer-1 to Layer-2 destination rollup chains. Only the bonder role can do this and requires positive credit balance. Someone may challenge this transfer root if it is believed to consist of invalid transfers.

## What is bonder “staking”?

A bonder must stake (lock up) collateral to be used as credit for transfers in order to guarantee liquidity on the destination rollup. The stake is treated like credit. The credit is subtracted when individual transfers are bonded and re-credited when transfers are settled. Transfers are settled when the bonded transfer root is propagated from Layer-2 to Layer-1 after the rollup challenge period).

## Can a bonder steal funds?

No, a bonder cannot steal any funds. The bonder can only speed up cross-domain transfers by providing liquidity. Worst case scenario is the bonder going offline then your transfer will take as long as the rollup's exit time.

## What are “liquidity providers”?

AMM’s require liquidity providers to contribute passive liquidity to the liquidity pool. LPs are rewarded with a small fee from each swap (“h” token <> canonical token).

## Can you send ETH with Hop?

ETH transfers are converted to WETH and are treated as any other ERC20 token.

## Can arbitrary contract calls be made over Hop?

At the moment Hop doesn't support arbitrary contract calls but may in the future after security risks are more understood.

## What’s an “arbitrageur”?

Arbitrageurs perform arbitrage which is buying a token on one exchange and selling on a different exchange for a profit when there’s a slippage in price. In the context of Hop, arbitrageurs swap between “h” tokens and canonical tokens on one Hop rollup AMM and trade the token on a different rollup for a profit. Eventually the price stabilizes because the liquidity is rebalanced across AMMs.

## What happens if the bonder is offline?

When bonder is offline then a fallback bonder will bond the transfers. If there are no fallback bonders, then the transfer will be settled after the rollup’s challenge period.

## What rollups does Hop Protocol support?

Supported rollups on mainnet are xDai, Polygon (formerly Matic), and soon will support Optimism, and Arbitirum.

## What happens when I "send" tokens from rollup A to rollup B?

The "hTokens" will be burned on rollup A and the Bonder will use collateral to mint hTokens on rollup B. The hTokens are immediately available to the sender.

## How does the Bonder get their collateral back?

The Bonder gets their collateral back on rollup B after they provide proof that hTokens were burned on rollup A (see above question for more context).

## How are transfers aggregated and passed to other rollups?

Transfers out of rollup A are merklelized into a "Transfer Root". The Transfer Root acts as proof that "hTokens" were burned on rollup A. The Transfer Root is sent to layer-1 (this takes \~1 week). After it's been commited on layer-1 then the Transfer Root is distributed to rollup B. At this point the Bonder can reclaim their collateral using the Transfer Root on rollup B as proof.

## How do I become a Bonder?

Currently Bonders must be allowed by the Hop Bridge smart contract governed by the Hop team. We are working on decentralizing the Bonder role completely. Reach out to the Hop team on discord if you are interested on becoming a Bonder.

## Do I need to expose any ports for the Hop Node?

No, only outgoing connections need to be allowed but all incoming connections can be disallowed.

## What are the risks of becoming a Bonder?

The risks of becoming a bonder are software bug risks on the Hop node software or smart contracts. The Hop node software has been running in production for months and the code is completely [open source](https://github.com/hop-protocol/hop/tree/develop/packages/hop-node/). The smart contracts have been audited by multiple firms.

## Do I need to run my own RPC server when becoming a Bonder?

It is not a requirement to run your own RPC server on chain supported chain. You can use an existing RPC provider like Infura when running the Hop node.

## How can I rescue my transfer that appears stuck?

You can withdraw any unbonded transfers on [Withdraw](https://app.hop.exchange/withdraw) page

[https://app.hop.exchange/withdraw](https://app.hop.exchange/#/withdraw?token=ETH)

## How does Hop Protocol make money?

Bonders and liquidity providers earn fees from transfers in exchange for providing liquidity. Other than that, there is no concrete business model detailed yet.

## Are Hop contracts audited?

Yes they are audited by [Solidified](https://solidified.io/) and [Clean Unicorn](https://twitter.com/cleanunicorn). More audits are underway.

See reports:

* [Solidified Report (PDF)](https://s3.us-west-1.amazonaws.com/assets.hop.exchange/reports/Audit\_Report\_-\_Hop\_05.05.2021.pdf)
* [MonocerosAlpha (PDF)](https://s3.us-west-1.amazonaws.com/assets.hop.exchange/reports/MonocerosAlpha\_-\_Hop\_Audit.pdf)

## Where can I find the smart contracts?

The smart contracts are available on our github: [https://github.com/hop-exchange/contracts](https://github.com/hop-exchange/contracts)

## Are smart contracts verified on Etherscan?

Yes, the Hop smart contracts are verified on Etherscan.

## When did Hop launch on mainnet?

Hop went [live](https://twitter.com/HopProtocol/status/1414624873775878148?s=20) on mainnet on July 2021.

## Where can I try Hop?

* Mainnet: [https://app.hop.exchange](https://app.hop.exchange/)
* Kovan: [https://kovan.hop.exchange](https://kovan.hop.exchange) (unmaintained now)
* Goerli: [https://goerli.hop.exchange](https://goerli.hop.exchange) (unmaintained now)

## Where can I get xDai for transaction fees (faucet)?

Available faucets:

* [https://xdai-app.herokuapp.com/faucet](https://xdai-app.herokuapp.com/faucet)
* [https://stakely.io/faucet/xdai-chain](https://stakely.io/faucet/xdai-chain)
* [https://faucet.prussia.dev/xdai](https://faucet.prussia.dev/xdai)

## What are the blockchain explorers I can use?

* ETH: [https://etherscan.io/](https://etherscan.io/)
* xDai: [https://blockscout.com/xdai/mainnet/](https://blockscout.com/xdai/mainnet/)
* Polygon: [https://polygonscan.com/](https://polygonscan.com/)
* Optimism: [https://optimistic.etherscan.io/](https://optimistic.etherscan.io/)
* Arbitrum: [https://arbiscan.io/](https://arbiscan.io/)

## What is the IPFS link for Hop?

Check out the github release page for latest IPFS links:

[https://github.com/hop-protocol/hop/releases](https://github.com/hop-protocol/hop/releases)

You can also try the following Hop IPFS links:

* [https://hop.eth.limo](https://hop.eth.limo)
* [https://hop.eth.link](https://hop.eth.link)
* [ https://hop-exchange.ipns.dweb.link/](https://hop-exchange.ipns.dweb.link/)
* [ https://hop-exchange.ipns.cf-ipfs.com/](https://hop-exchange.ipns.cf-ipfs.com/)

## How can I contribute to Hop?

If you'd like to contribute, talk to us on [Discord](https://discord.gg/PwCF88emV4)!

## Where can I find stats?

* [https://dune.xyz/rchen8/Hop-Exchange](https://dune.xyz/rchen8/Hop-Exchange)
* [https://defillama.com/protocol/hop-protocol](https://defillama.com/protocol/hop-protocol)
* [https://cryptofees.info/](https://cryptofees.info/)
* [https://vfat.tools/polygon/hop/](https://vfat.tools/polygon/hop/)
* [https://explorer.hop.exchange/](https://explorer.hop.exchange/mainnet/)
* [https://app.hop.exchange/stats](https://app.hop.exchange/stats?token=USDC)
* [https://volume.hop.exchange/](https://volume.hop.exchange/)
* [https://tvl.hop.exchange/](https://tvl.hop.exchange/)

## How can I can track my positions?

* [https://zapper.fi/dashboard](https://zapper.fi/dashboard)
* [https://debank.com/](https://debank.com/)

## Does Hop have an explorer?

It's very primitive but you can try it: [https://explorer.hop.exchange/](https://explorer.hop.exchange/mainnet/)

## Where can I see volume stats?

* [https://volume.hop.exchange/](https://volume.hop.exchange/)

## Where can I find Hop subgraphs (TheGraph)?

Subgraph links can be found on the Hop subgraph repo:[ https://github.com/hop-protocol/subgraph](https://github.com/hop-protocol/subgraph)

## Why don't I see my funds after transferring to a centralized exchange?

Make sure that the centralized exchange supports reading internal transactions. For example, transferring ETH to a Binance address on Arbitrum could result in loss of funds because Binance doesn't support internal transactions and won't recognize the transaction.



## Does Hop have a web bug bounty program?

Yes, Hop has a web bug bounty program.

### Scope for Web Applications

**In-Scope Vulnerabilities**

Accepted, in-scope vulnerabilities include, but are not limited to:

* Disclosure of sensitive or personally identifiable information
* Cross-Site Scripting (XSS)
* Server-side or remote code execution (RCE)
* Authentication or authorization flaws, including insecure direct object references and authentication bypass
* Vulnerability that leads to loss of user funds
* Injection vulnerabilities, including SQL and XML injection
* Significant security misconfiguration with a verifiable vulnerability
* Exposed credentials, disclosed by Hop or its employees, that pose a valid risk to an in scope asset

In-scope domains:

* hop.exchange
* app.hop.exchange

subdomains used for demo purposes are out-of-scope.

**Out-of-Scope Vulnerabilities**

Certain vulnerabilities are considered out-of-scope for the Bug Bounty Program. Those out-of-scope vulnerabilities include, but are not limited to:

\
\- Scanner output or scanner-generated reports, including any automated or active exploit tool\
\- Attacks involving payment fraud, theft, or malicious merchant accounts\
\- Man-in-the-Middle attacks\
\- Vulnerabilities involving stolen credentials or physical access to a device\
\- Social engineering attacks, including those targeting or impersonating internal employees by any means\
\- Open redirection, except in the following circumstances:\
&#x20;   \- Clicking an Hop-owned URL immediately results in a redirection\
&#x20;   \- A redirection results in the loss of sensitive data (e.g. session tokens, PII, etc)\
\- Host header injections without a specific, demonstrable impact\
\- Denial of service (DOS) attacks using automated tools\
\- Self-XSS, which includes any payload entered by the victim\
\- Any vulnerabilities requiring significant and unlikely interaction by the victim, such as disabling browser controls\
\- Login/logout CSRF\
\- Content spoofing without embedding an external link or JavaScript\
\- Infrastructure vulnerabilities, including:\
&#x20;   \- Issues related to SSL certificates\
&#x20;   \- DNS configuration issues\
\- Server configuration issues (e.g. open ports, TLS versions, etc.)\
\- Most vulnerabilities within our sandbox, lab, or staging environments, except Braintree.\
\- Vulnerabilities only affecting users of outdated or unpatched browsers and platforms\
\- Vulnerabilities that only affect one browser will be considered on a case-by-case basis, and may be closed as informative due to the reduced attack surface\
\- Information disclosure of public or non-protected information (e.g. code in a public repository, server banners, etc.), or information disclosed outside of Hop's control (e.g. a personal, non-employee repository; a list from a previous infodump; etc.)\
\- Exposed credentials that are either no longer valid, or do not pose a risk to an in scope asset\
\- Any XSS that requires Flash. Flash is disabled by default in most modern browsers, thus greatly reducing the attack surface and associated risk.\
\- Any other submission determined to be low risk, based on unlikely or theoretical attack vectors, requiring significant user interaction, or resulting in minimal impact\
\- Vulnerabilities on third party libraries without showing specific impact to the target application (e.g. a CVE with no exploit)\
\- Password policy\
\- Rate limiting on non-sensitive endpoints. Rate limit bugs will be considered low severity.

\- Subdomains that are managed by 3rd parties such as feedback.hop.exchange (hop.frill.co) and docs.hop.exchange (hop.gitbook.io) are out-of-scope.

### Bug Submission Requirements

**Required information**

For all submissions, please include:

\- Full description of the vulnerability being reported, including the exploitability and impact\
Evidence and explanation of all steps required to reproduce the submission, which may include:\
&#x20;   \- Videos\
&#x20;   \- Screenshots\
&#x20;   \- Exploit code\
&#x20;   \- Traffic logs\
&#x20;   \- Web/API requests and responses\
&#x20;   \- Email address or user ID of any test accounts\
&#x20;   \- IP address used during testing

Reward Amounts

\- Informational: TBD

\- Low severity: maximum of $500 for automated attacks, such as DDOS, rate-limit exploits, etc,

\- Medium: TBD

\- High: TDB

\- Critical: TBD



Bounty rewards are determined on a case-by-case basis.

## Is Hop hiring?

Yes! Reach out to us on our [Discord](https://discord.gg/PwCF88emV4)

## How can I contact the Hop team?

Reach out to us on our [Discord](https://discord.gg/PwCF88emV4) or email us at [contact@hop.exchange](mailto:contact@hop.exchange)

For any transfer issues or LP issues, please reach out on Discord.

## Where can I read more FAQs?

More FAQs are at [https://help.hop.exchange/](https://help.hop.exchange/hc/en-us)
