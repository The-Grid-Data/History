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
  2. [Ethereum roadmap](/en/roadmap/)/
  3. [Future-proofing](/en/roadmap/future-proofing/)

# Future-proofing Ethereum

These upgrades cement Ethereum as the resilient, decentralized base layer for
the future, whatever it may hold.

On this page

  * Quantum resistance
  * Simpler and more efficient Ethereum
  * Current progress

![Ethereum roadmap](/_next/image/?url=%2Froadmap%2Froadmap-
future.png&w=1920&q=75)

Roadmap Options

[Roadmap home](/en/roadmap/)[Better
security](/en/roadmap/security/)[Scaling](/en/roadmap/scaling/)[Better user
experience](/en/roadmap/user-experience/)[Future-proofing](/en/roadmap/future-
proofing/)

## On this page

  * Quantum resistance
  * Simpler and more efficient Ethereum
  * Current progress

Some parts of the roadmap are not necessarily required for scaling or securing
Ethereum in the near-term, but set Ethereum up for stability and reliability
far into the future.

## Quantum resistance

Some of the _cryptography_ securing present-day Ethereum will be compromised
when quantum computing becomes a reality. Although quantum computers are
probably decades away from being a genuine threat to modern cryptography,
Ethereum is being built to be secure for centuries to come. This means making
[Ethereum quantum resistant(opens in a new
tab)](https://consensys.net/blog/developers/how-will-quantum-supremacy-affect-
blockchain/) as soon as possible.

The challenge facing Ethereum developers is that the current _proof-of-stake_
protocol relies upon a very efficient signature scheme known as BLS to
aggregate votes on valid _blocks_. This signature scheme is broken by quantum
computers, but the quantum resistant alternatives are not as efficient.

The [“KZG” commitment schemes](/en/roadmap/danksharding/#what-is-kzg) used in
several places across Ethereum to generate cryptographic secrets are known to
be quantum-vulnerable. Currently, this is circumvented using “trusted setups”
where many users generate randomness that cannot be reverse-engineered by a
quantum computer. However, the ideal solution would simply be to incorporate
quantum safe cryptography instead. There are two leading approaches that could
become efficient replacements for the BLS scheme: [STARK-based(opens in a new
tab)](https://hackmd.io/@vbuterin/stark_aggregation) and [lattice-based(opens
in a new tab)](https://medium.com/asecuritysite-when-bob-met-alice/so-what-is-
lattice-encryption-326ac66e3175) signing. **These are still being researched
and prototyped**.

[ Read about KZG and trusted setups](/en/roadmap/danksharding/#what-is-kzg)

## Simpler and more efficient Ethereum

Complexity creates opportunities for bugs or vulnerabilities that can be
exploited by attackers. Therefore, part of the roadmap is simplifying Ethereum
and removing code that has hung around through various upgrades but is no
longer needed or can now be improved upon. A leaner, simpler codebase is
easier for developers to maintain and reason about.

There are several updates that will be made to the [Ethereum Virtual Machine
(EVM)](/en/developers/docs/evm/) to make it simpler and more efficient. These
include [removing the SELFDESTRUCT opcode(opens in a new
tab)](https://hackmd.io/@vbuterin/selfdestruct) \- a rarely used command that
is no longer needed and in some circumstances can be dangerous to use,
especially when combined with other future upgrades to Ethereum’s storage
model. _Ethereum clients_ also still support some old transaction types that
can now be completely removed. The way _gas_ is calculated can also be
improved and more efficient methods for the arithmetic underpinning some
cryptographic operations can be brought in.

Similarly, there are updates that can be made to other parts of present-day
Ethereum clients. One example is that current execution and consensus clients
use a different type of data compression. It will be much easier and more
intuitive to share data between clients when the compression scheme is unified
across the whole network.

## Current progress

Most of the upgrades required for future-proofing Ethereum are **still in the
research phase and may be several years away** from being implemented.
Upgrades such as removing SELF-DESTRUCT and harmonizing the compression scheme
used in the execution and consensus clients are likely to come sooner than
quantum resistant cryptography.

**Further reading**

  * [Gas](/en/developers/docs/gas/)
  * [EVM](/en/developers/docs/evm/)
  * [Data structures](/en/developers/docs/data-structures-and-encoding/)

### Was this page helpful?

YesNo

Roadmap Options

[Roadmap home](/en/roadmap/)[Better
security](/en/roadmap/security/)[Scaling](/en/roadmap/scaling/)[Better user
experience](/en/roadmap/user-experience/)[Future-proofing](/en/roadmap/future-
proofing/)

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

### Cryptography

It is the practice of making communication private and secure so that only
those for whom the information is intended can read it.

### Proof-of-stake (PoS)

A method by which a cryptocurrency blockchain protocol aims to achieve
distributed [consensus](/en/glossary/#consensus). PoS asks users to prove
ownership of a certain amount of cryptocurrency (their "stake" in the network)
in order to be able to participate in the validation of transactions. [More on
proof-of-stake](/en/developers/docs/consensus-mechanisms/pos/).

### Block

A block is where transactions or digital actions are stored. Once a block is
full, it gets linked to the previous one, creating a chain of blocks or a
"blockchain". [More on blocks](/en/developers/docs/blocks/).

### Consensus client

Consensus clients (such as Prysm, Teku, Nimbus, Lighthouse, Lodestar) run
Ethereum's [proof-of-stake](/en/glossary/#pos) consensus algorithm allowing
the network to reach agreement about the head of the Beacon Chain. Consensus
clients do not participate in validating/broadcasting transactions or
executing state transitions. This is done by [execution
clients](/en/glossary/#execution-client). Consensus clients do not attest to,
or propose new blocks. This is done by the [validator
client](/en/glossary/#validator) which is an optional add-on to the consensus
client.

### Gas

Gas is the fee paid for transactions and smart contracts on a blockchain, like
Ethereum. [More on gas and fees](/en/gas/).

