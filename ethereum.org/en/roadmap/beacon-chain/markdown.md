Skip to main content

[](/en/)

  * Learn
  * Use
  * Build
  * Participate
  * Research

Search```K`

Languages EN

  1. [Ethereum roadmap](/en/roadmap/)/
  2. [Beacon Chain](/en/roadmap/beacon-chain/)

# The Beacon Chain

  * The Beacon Chain introduced proof-of-stake to the Ethereum ecosystem.
  * It was merged with the original Ethereum proof-of-work chain in September 2022.
  * The Beacon Chain introduced the consensus logic and block gossip protocol which now secures Ethereum.

Page last updated: February 23, 2024

![](/_next/image/?url=%2Fupgrades%2Fcore.png&w=1920&q=75)

Guide to Ethereum upgrades

[The Beacon Chain](/en/roadmap/beacon-chain/)[The Merge](/en/roadmap/merge/)

## On this page

  * What is the Beacon Chain?
  * What does the Beacon Chain do?
  * Beacon Chain impact
  * Relationship between upgrades
  * Further Reading

## When's it shipping?

Shipped!

The Beacon Chain shipped on December 1, 2020, and formalized proof-of-stake as
Ethereum's consensus mechanism with The Merge upgrade on September 15, 2022.

## What is the Beacon Chain?

The Beacon Chain is the name of the original proof-of-stake blockchain that
was launched in 2020. It was created to ensure the proof-of-stake consensus
logic was sound and sustainable before enabling it on Ethereum Mainnet.
Therefore, it ran alongside the original proof-of-work Ethereum. The Beacon
Chain was a chain of 'empty' blocks, but switching off proof-of-work and
switching on proof-of-stake on Ethereum required instructing the Beacon Chain
to accept transaction data from execution clients, bundle them into blocks and
then organize them into a blockchain using a proof-of-stake-based consensus
mechanism. At the same moment, the original Ethereum clients turned off their
mining, block propagation and consensus logic, handing that all over to the
Beacon Chain. This event was known as [The Merge](/en/roadmap/merge/). Once
The Merge happened, there were no longer two blockchains. Instead, there was
just one proof-of-stake Ethereum, which now requires two different clients per
node. The Beacon Chain is now the consensus layer, a peer-to-peer network of
consensus clients that handles block gossip and consensus logic, while the
original clients form the execution layer, which is responsible for gossiping
and executing transactions, and managing Ethereum's state. The two layers can
communicate with one another using the Engine API.

## What does the Beacon Chain do?

The Beacon Chain is the name given to a ledger of accounts that conducted and
coordinated the network of Ethereum [stakers](/en/staking/) before those
stakers started validating real Ethereum blocks. It does not process
transactions or handle smart contract interactions though because that is
being done in the execution layer. The Beacon Chain is responsible for things
like block and attestation handling, running the fork choice algorithm, and
managing rewards and penalties. Read more on our [node architecture
page](/en/developers/docs/nodes-and-clients/node-architecture/#node-
comparison).

## Beacon Chain impact

### Introducing staking

The Beacon Chain introduced [proof-of-stake](/en/developers/docs/consensus-
mechanisms/pos/) to Ethereum. This keeps Ethereum secure and earns validators
more ETH in the process. In practice, staking involves staking ETH in order to
activate validator software. As a staker, you run the software that creates
and validates new blocks in the chain.

Staking serves a similar purpose that [mining](/en/developers/docs/consensus-
mechanisms/pow/mining/) used to, but is different in many ways. Mining
required large up-front expenditures in the form of powerful hardware and
energy consumption, resulting in economies of scale, and promoting
centralization. Mining also did not come with any requirement to lock up
assets as collateral, limiting the protocol's ability to punish bad actors
after an attack.

The transition to proof-of-stake made Ethereum significantly more secure and
decentralized by comparison to proof-of-work. The more people that participate
in the network, the more decentralized and safe from attacks it becomes.

And using proof-of-stake as consensus mechanism is a foundational component
for [the secure, environmentally friendly and scalable Ethereum we have
now](/en/roadmap/vision/).

![💰](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4b0.svg)

If you're interested in becoming a validator and helping secure Ethereum,
[learn more about staking](/en/staking/).

### Setting up for sharding

Since the Beacon Chain merged with the original Ethereum Mainnet, the Ethereum
community started looking to scaling the network.

Proof-of-stake has the advantage of having a registry of all approved block
producers at any given time, each with ETH at stake. This registry sets the
stage for the ability to divide and conquer but reliably split up specific
network responsibilities.

This responsibility is in contrast to proof-of-work, where miners have no
obligation to the network and could stop mining and turn their node software
off permanently in an instant without repercussion. There is also no registry
of known block proposers and no reliable way to split network responsibilities
safely.

[More on sharding](/en/roadmap/danksharding/)

## Relationship between upgrades

The Ethereum upgrades are all somewhat interrelated. So let’s recap how the
Beacon Chain affects the other upgrades.

### Beacon Chain and The Merge

At first, The Beacon Chain existed separately from Ethereum Mainnet, but they
were merged in 2022.

[The Merge](/en/roadmap/merge/)

### Shards and the Beacon Chain

Sharding can only safely enter the Ethereum ecosystem with a proof-of-stake
consensus mechanism in place. The Beacon Chain introduced staking, which
'merged' with Mainnet, paving the way for sharding to help further scale
Ethereum.

[Shard chains](/en/roadmap/danksharding/)

## Further Reading

  * [More on Ethereum's future upgrades](/en/roadmap/vision/)
  * [More on node architecture](/en/developers/docs/nodes-and-clients/node-architecture/)
  * [More of proof-of-stake](/en/developers/docs/consensus-mechanisms/pos/)

### Was this page helpful?

YesNo

Guide to Ethereum upgrades

[The Beacon Chain](/en/roadmap/beacon-chain/)[The Merge](/en/roadmap/merge/)

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

