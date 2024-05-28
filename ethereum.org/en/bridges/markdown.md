Skip to main content

[](/en/)

  * Learn
  * Use
  * Build
  * Participate
  * Research

Search```K`

Languages EN

  1. [Home](/en/)/
  2. [Blockchain bridges](/en/bridges/)

Page last updated: April 22, 2024

On this page

  * What are bridges?
  * Why do we need bridges?
  * Bridge use cases
    * Lower transaction fees
    * Dapps on other blockchains
    * Explore blockchain ecosystems
    * Own native crypto assets
  * Types of bridge
  * Risk using bridges
  * Further reading

# Blockchain bridges

 _Web3 has evolved into an ecosystem of L1 blockchains and L2 scaling
solutions, each designed with unique capabilities and trade-offs. As the
number of blockchain protocols increases, so does the demand to move assets
across chains.  To fulfill this demand, we need bridges._

## What are bridges?

Blockchain bridges work just like the bridges we know in the physical world.
Just as a physical bridge connects two physical locations, a blockchain bridge
connects two blockchain ecosystems. **Bridges facilitate communication between
blockchains through the transfer of information and assets**.

Let's consider an example:

You're from the USA and are planning a trip to Europe. You have USD, but you
need EUR to spend. To exchange your USD for EUR you can use a currency
exchange for a small fee.

But, what do you do if you want to make a similar exchange to use a different
_blockchain_? Let's say you want to exchange _ETH_ on Ethereum Mainnet for ETH
on [Arbitrum(opens in a new tab)](https://arbitrum.io/). Like the currency
exchange we made for EUR, we need a mechanism to move our ETH from Ethereum to
Arbitrum. Bridges make such a transaction possible. In this case, [Arbitrum
has a native bridge(opens in a new tab)](https://bridge.arbitrum.io/) that can
transfer ETH from Mainnet onto Arbitrum.

## Why do we need bridges?

All blockchains have their limitations. For Ethereum to scale and keep up with
demand, it has required _rollups_. Alternatively, L1s like Solana and
Avalanche are designed differently to enable higher throughput but at the cost
of decentralization.

However, all blockchains develop in isolated environments and have different
rules and _consensus_ mechanisms. This means they cannot natively communicate,
and tokens cannot move freely between blockchains.

Bridges exist to connect blockchains, allowing the transfer of information and
tokens between them.

**Bridges enable** :

  * the cross-chain transfer of assets and information.
  * _dapps_ to access the strengths of various blockchains – thus enhancing their capabilities (as protocols now have more design space for innovation).
  * users to access new platforms and leverage the benefits of different chains.
  * developers from different blockchain ecosystems to collaborate and build new platforms for the users.

[How to bridge tokens to layer 2](/en/guides/how-to-use-a-bridge/)

## Bridge use cases

The following are some scenarios where you can use a bridge:

### Lower transaction fees

Let’s say you have ETH on Ethereum Mainnet but want cheaper transaction fees
to explore different dapps. By bridging your ETH from the Mainnet to an
Ethereum L2 rollup, you can enjoy lower transaction fees.

### Dapps on other blockchains

If you’ve been using Aave on Ethereum Mainnet to lend USDT but the interest
rate for lending USDT using Aave on Polygon is higher.

### Explore blockchain ecosystems

If you have ETH on Ethereum Mainnet and you want to explore an alt L1 to try
out their native dapps. You can use a bridge to transfer your ETH from
Ethereum Mainnet to the alt L1.

### Own native crypto assets

Let’s say you want to own native Bitcoin (BTC), but you only have funds on
Ethereum Mainnet. To gain exposure to BTC on Ethereum, you can buy Wrapped
Bitcoin (WBTC). However, WBTC is an _ERC-20_ token native to the Ethereum
network, which means it’s an Ethereum version of Bitcoin and not the original
asset on the Bitcoin blockchain. To own native BTC, you would have to bridge
your assets from Ethereum to Bitcoin using a bridge. This will bridge your
WBTC and convert it into native BTC. Alternatively, you might own BTC and want
to use it in Ethereum _DeFi_ protocols. This would require bridging the other
way, from BTC to WBTC which can then be used as an asset on Ethereum.

![💡](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4a1.svg)

You can also do all of the above using a [centralized exchange](/en/get-eth/).
However, unless your funds are already on an exchange, it would involve
multiple steps, and you’d likely be better off using a bridge.

## Types of bridge

Bridges have many types of designs and intricacies. Generally, bridges fall
into two categories: trusted and trustless bridges.

Trusted Bridges| Trustless Bridges  
---|---  
Trusted bridges depend upon a central entity or system for their operations.|
Trustless bridges operate using smart contracts and algorithms.  
They have trust assumptions with respect to the custody of funds and the
security of the bridge. Users mostly rely on the bridge operator's
reputation.| They are trustless, i.e., the security of the bridge is the same
as that of the underlying blockchain.  
Users need to give up control of their crypto assets.| Through _smart
contracts_ , trustless bridges enable users to remain in control of their
funds.  
  
In a nutshell, we can say that trusted bridges have trust assumptions, whereas
trustless bridges are trust-minimized and don’t make new trust assumptions
beyond those of the underlying domains. Here’s how these terms can be
described:

  * **Trustless** : having equivalent security to the underlying domains. As described by [Arjun Bhuptani in this article.(opens in a new tab)](https://medium.com/connext/the-interoperability-trilemma-657c2cf69f17)
  * **Trust assumptions:**  moving away from the security of the underlying domains by adding external verifiers in the system, thus making it less crypto-economically secure.

To develop a better understanding of the key differences between the two
approaches, let’s take an example:

Imagine you’re at the airport security checkpoint. There are two types of
checkpoints:

  1. Manual Checkpoints — operated by officials who manually check all the details of your ticket and identity before handing over the boarding pass.
  2. Self Check-In — operated by a machine where you put in your flight details and receive the boarding pass if everything checks out.

A manual checkpoint is similar to a trusted model as it depends upon a third
party, i.e., the officials, for its operations. As a user, you trust the
officials to make the right decisions and use your private information
correctly.

Self check-in is similar to a trustless model as it removes the operator's
role and uses technology for its operations. Users always remain in control of
their data and don’t have to trust a third party with their private
information.

Many bridging solutions adopt models between these two extremes with varying
degrees of trustlessness.

## Risk using bridges

Bridges are in the early stages of development. It is likely that the optimal
bridge design has not yet been discovered. Interacting with any type of bridge
carries risk:

  * **Smart Contract Risk —** the risk of a bug in the code that can cause user funds to be lost
  * **Technology Risk —** software failure, buggy code, human error, spam, and malicious attacks can possibly disrupt user operations

Moreover, since trusted bridges add trust assumptions, they carry additional
risks such as:

  * **Censorship Risk —** bridge operators can theoretically stop users from transferring their assets using the bridge
  * **Custodial Risk —** bridge operators can collude to steal the users’ funds

User's funds are at risk if:

  * there is a bug in the smart contract
  * the user makes an error
  * the underlying blockchain is hacked
  * the bridge operators have malicious intent in a trusted bridge
  * the bridge gets hacked

One recent hack was Solana’s Wormhole bridge, [where 120k wETH ($325 million
USD) was stolen during the hack(opens in a new
tab)](https://rekt.news/wormhole-rekt/). Many of the [top hacks in blockchains
involved bridges(opens in a new tab)](https://rekt.news/leaderboard/).

Bridges are crucial to onboarding users onto Ethereum L2s, and even for users
who want to explore different ecosystems. However, given the risks involved in
interacting with bridges, users must understand the trade-offs the bridges are
making. These are some [strategies for cross-chain security(opens in a new
tab)](https://blog.debridge.finance/10-strategies-for-cross-chain-
security-8ed5f5879946).

## Further reading

  * [EIP-5164: Cross-Chain Execution(opens in a new tab)](https://ethereum-magicians.org/t/eip-5164-cross-chain-execution/9658) _June 18, 2022 - Brendan Asselstine_
  * [L2Bridge Risk Framework(opens in a new tab)](https://gov.l2beat.com/t/l2bridge-risk-framework/31) _July 5, 2022 - Bartek Kiepuszewski_
  * ["Why the future will be multi-chain, but it will not be cross-chain."(opens in a new tab)](https://old.reddit.com/r/ethereum/comments/rwojtk/ama_we_are_the_efs_research_team_pt_7_07_january/hrngyk8/) _January 8, 2022 - Vitalik Buterin_

### Was this article helpful?

YesNo

  * [Edit page(opens in a new tab)](https://github.com/ethereum/ethereum-org-website/tree/dev/public/content/bridges/index.md)
  * On this page

    * What are bridges?
    * Why do we need bridges?
    * Bridge use cases
      * Lower transaction fees
      * Dapps on other blockchains
      * Explore blockchain ecosystems
      * Own native crypto assets
    * Types of bridge
    * Risk using bridges
    * Further reading

Website last updated: May 22, 2024

[(opens in a new tab)](https://github.com/ethereum/ethereum-org-
website)[(opens in a new tab)](https://twitter.com/ethdotorg)[(opens in a new
tab)](https://discord.gg/ethereum-org)

### Learn

  * [Learn Hub](/en/learn/)
  * [What is Ethereum?](/en/what-is-ethereum/)
  * [What is ether (ETH)?](/en/eth/)
  * [Ethereum wallets](/en/wallets/)
  * [What is Web3?](/en/web3/)
  * [Smart contracts](/en/smart-contracts/)
  * [Gas fees](/en/gas/)
  * [Run a node](/en/run-a-node/)
  * [Ethereum security and scam prevention](/en/security/)
  * [Quiz Hub](/en/quizzes/)
  * [Ethereum glossary](/en/glossary/)

### Use

  * [Guides](/en/guides/)
  * [Choose your wallet](/en/wallets/find-wallet/)
  * [Get ETH](/en/get-eth/)
  * [Dapps - Decentralized applications](/en/dapps/)
  * [Stablecoins](/en/stablecoins/)
  * [NFTs - Non-fungible tokens](/en/nft/)
  * [DeFi - Decentralized finance](/en/defi/)
  * [DAOs - Decentralized autonomous organizations](/en/dao/)
  * [Decentralized identity](/en/decentralized-identity/)
  * [Stake ETH](/en/staking/)
  * [Layer 2](/en/layer-2/)

### Build

  * [Builder's home](/en/developers/)
  * [Tutorials](/en/developers/tutorials/)
  * [Documentation](/en/developers/docs/)
  * [Learn by coding](/en/developers/learning-tools/)
  * [Set up local environment](/en/developers/local-environment/)
  * [Grants](/en/community/grants/)
  * [Foundational topics](/en/developers/docs/intro-to-ethereum/)
  * [UX/UI design fundamentals](/en/developers/docs/design-and-ux/)
  * [Enterprise - Mainnet Ethereum](/en/enterprise/)
  * [Enterprise - Private Ethereum](/en/enterprise/private-ethereum/)

### Participate

  * [Community hub](/en/community/)
  * [Online communities](/en/community/online/)
  * [Ethereum events](/en/community/events/)
  * [Contributing to ethereum.org](/en/contributing/)
  * [Translation Program](/en/contributing/translation-program/)
  * [Ethereum bug bounty program](/en/bug-bounty/)
  * [Ethereum Foundation](/en/foundation/)
  * [Ethereum Foundation Blog(opens in a new tab)](https://blog.ethereum.org/)
  * [Ecosystem Support Program(opens in a new tab)](https://esp.ethereum.foundation)
  * [Devcon(opens in a new tab)](https://devcon.org/)

### Research

  * [Ethereum Whitepaper](/en/whitepaper/)
  * [Ethereum roadmap](/en/roadmap/)
  * [Improved security](/en/roadmap/security/)
  * [Technical history of Ethereum](/en/history/)
  * [Open research](/en/community/research/)
  * [Ethereum Improvement Proposals](/en/eips/)
  * [Ethereum governance](/en/governance/)

  * [About us](/en/about/)
  * [Ethereum brand assets](/en/assets/)
  * [Code of conduct](/en/community/code-of-conduct/)
  * [Jobs](/en/about/#open-jobs)
  * [Privacy policy](/en/privacy-policy/)
  * [Terms of use](/en/terms-of-use/)
  * [Cookie policy](/en/cookie-policy/)
  * [Press Contact(opens in a new tab)](mailto:press@ethereum.org)

Is this page helpful?

### Blockchain

A blockchain is a database of transactions, duplicated and shared on all
computers in the network, ensuring data cannot be altered retroactively.

### Ether

The native cryptocurrency of Ethereum, commonly referred to as “ETH”. It is
used to cover transaction fees when using Ethereum ecosystem and applications.
[More on ether](/en/eth/).

### Rollups

A type of [layer 2](/en/glossary/#layer-2) scaling solution that batches
multiple transactions and submits them to [the Ethereum main
chain](/en/glossary/#mainnet) in a single transaction. This allows for
reductions in [gas](/en/glossary/#gas) costs and increases in
[transaction](/en/glossary/#transaction) throughput. There are Optimistic and
Zero-knowledge rollups which use different security methods to offer these
scalability gains. [More on rollups](/en/developers/docs/scaling/#rollups).

### Consensus

When more than 2/3 of the computers in a network agree that they have the same
set of records, making sure everyone is on the same page. This isn't about the
rules they follow, but making sure they all have the same information.

### Dapp

A dApp is a decentralized application that runs on a blockchain network,
offering services without a central controlling authority. [More on
decentralized applications](/en/dapps/).

### ERC-20

Is the standard set of rules that most tokens on Ethereum network are created
with.

### DeFi

A broad category of Ethereum apps aiming to provide financial services backed
by the blockchain, without any intermediaries. [More on decentralized finance
(DeFi)](/en/defi/)

### Smart contract

A smart contract is a program that automatically executes agreements on a
blockchain, like a self-enforcing digital contract. [Introduction to smart
contracts](/en/smart-contracts/).

