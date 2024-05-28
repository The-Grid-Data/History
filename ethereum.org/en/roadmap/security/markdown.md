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
  3. [Security](/en/roadmap/security/)

# A more secure Ethereum

Ethereum is the most secure and decentralized smart-contract platform in
existence. However, there are still improvements that can be made so that
Ethereum stays resilient to any level of attack far into the future.

On this page

  * Staking withdrawals
  * Defending against attacks
  * Defending against censorship
  * Protecting validators
  * Current progress

![Ethereum roadmap](/_next/image/?url=%2Froadmap%2Froadmap-
security.png&w=1920&q=75)

Roadmap Options

[Roadmap home](/en/roadmap/)[Better
security](/en/roadmap/security/)[Scaling](/en/roadmap/scaling/)[Better user
experience](/en/roadmap/user-experience/)[Future-proofing](/en/roadmap/future-
proofing/)

## On this page

  * Staking withdrawals
  * Defending against attacks
  * Defending against censorship
  * Protecting validators
  * Current progress

**Ethereum is already a very secure** , decentralized _smart-contract_
platform. However, there are still improvements that can be made so that
Ethereum stays resilient to all kinds of attack far into the future. These
include subtle changes to the way _Ethereum clients_ deal with competing
_blocks_ , as well as increasing the speed the network considers blocks to be
["finalized"](/en/developers/docs/consensus-mechanisms/pos/#finality) (meaning
they can't be changed without extreme economic losses to an attacker).

There are also improvements that make censoring transactions much more
difficult by making block proposers blind to the actual contents of their
blocks, and new ways to identify when a client is censoring. Together these
improvements will upgrade the _proof-of-stake_ protocol so that users - from
individuals to corporations - have instant confidence in their apps, data and
assets on Ethereum.

## Staking withdrawals

The upgrade from _proof-of-work_ to proof-of-stake began with Ethereum
pioneers “staking” their ETH in a deposit contract. That ETH is used to
protect the network. There has been a second update on April 12, 2023 to allow
withdraw the staked ETH. Since then validators can freely stake or withdraw
ETH.

[Read about withdrawals](/en/staking/withdrawals/)

## Defending against attacks

There are improvements that can be made to Ethereum's proof-of-stake protocol.
One is known as [view-merge(opens in a new tab)](https://ethresear.ch/t/view-
merge-as-a-replacement-for-proposer-boost/13739) \- a more secure _fork_
-choice algorithm that makes certain sophisticated types of attack more
difficult.

Reducing the time Ethereum takes to _finalize_ blocks would provide a better
user experience and prevent sophisticated "reorg" attacks where attackers try
to reshuffle very recent blocks to extract profit or censor certain
transactions. [**Single slot finality (SSF)**](/en/roadmap/single-slot-
finality/) is a **way to minimize the finalization delay**. Right now there
are 15 mins worth of blocks that an attacker could theoretically convince
other validators to reconfigure. With SSF, there are 0. Users, from
individuals to apps and exchanges, benefit from fast assurance that their
transactions will not be reverted, and the network benefits by shutting down a
whole class of attacks.

[Read about single slot finality](/en/roadmap/single-slot-finality/)

## Defending against censorship

Decentralization prevents individuals or small groups of _validators_ from
becoming too influential. New staking technologies can help to ensure
Ethereum's validators stay as decentralized as possible while also defending
them against hardware, software and network failures. This includes software
that shares validator responsibilities across multiple _nodes_. This is known
as **distributed validator technology (DVT)**. _Staking pools_ are
incentivized to use DVT because it allows multiple computers to collectively
participate in validation, adding redundancy and fault-tolerance. It also
splits validator keys across several systems, rather than having single
operators running multiple validators. This makes it harder for dishonest
operators to coordinate attacks on Ethereum. Overall, the idea is to derive
security benefits by running validators as _communities_ rather than as
individuals.

[Read about distributed validator technology](/en/staking/dvt/)

Implementing **proposer-builder separation (PBS)** will drastically improve
Ethereum's built-in defenses against censorship. PBS allows one validator to
create a block and another to broadcast it across the Ethereum network. This
ensures that the gains from professional profit-maximizing block building
algorithms are shared more fairly across the network, **preventing stake from
concentrating** with the best-performing institutional stakers over time. The
block proposer gets to select the most profitable block offered to them by a
market of block builders. To censor, a block proposer would often have to
choose a less profitable block, which would be **economically irrational and
also obvious to the rest of the validators** on the network.

There are potential add-ons to PBS, such as encrypted transactions and
inclusion lists, that could further improve Ethereum's censorship resistance.
These make the block builder and proposer blind to the actual transactions
included in their blocks.

[Read about proposer-builder separation](/en/roadmap/pbs/)

## Protecting validators

It is possible that a sophisticated attacker could identify upcoming
validators and spam them to prevent them from proposing blocks; this is known
as a **denial of service (DoS)** attack. Implementing [**secret leader
election (SLE)**](/en/roadmap/secret-leader-election/) will protect against
this type of attack by preventing block proposers from being knowable in
advance. This works by continually shuffling a set of cryptographic
commitments representing candidate block proposers and using their order to
determine which validator is selected in such a way that only the validators
themselves know their ordering in advance.

[Read about secret leader election](/en/roadmap/secret-leader-election/)

## Current progress

**Security upgrades on the roadmap are in advanced stages of research** , but
they are not expected to be implemented for some time. The next steps for
view-merge, PBS, SSF and SLE is to finalize a specification and start building
prototypes.

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

### Smart contract

A smart contract is a program that automatically executes agreements on a
blockchain, like a self-enforcing digital contract. [Introduction to smart
contracts](/en/smart-contracts/).

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

### Block

A block is where transactions or digital actions are stored. Once a block is
full, it gets linked to the previous one, creating a chain of blocks or a
"blockchain". [More on blocks](/en/developers/docs/blocks/).

### Proof-of-stake (PoS)

A method by which a cryptocurrency blockchain protocol aims to achieve
distributed [consensus](/en/glossary/#consensus). PoS asks users to prove
ownership of a certain amount of cryptocurrency (their "stake" in the network)
in order to be able to participate in the validation of transactions. [More on
proof-of-stake](/en/developers/docs/consensus-mechanisms/pos/).

### Proof-of-work (PoW)

A security mechanism for blockchains that requires nodes to expend energy in
the form of computation to find a certain value.

### Fork

A change in protocol causing the creation of an alternative chain.

### Finality

Finality is the guarantee that a set of transactions cannot be changed without
a huge amount of ETH being lost.

### Validator

A [node](/en/glossary/#node) in a [proof-of-stake](/en/glossary/#pos) system
responsible for storing data, processing transactions, and adding new blocks
to the blockchain. To activate validator software, you need to be able to
[stake](/en/glossary/#staking) 32 ETH. [More on staking in
Ethereum](/en/staking/).

### Node

A software client that participates in the network. [More on nodes and
clients](/en/developers/docs/nodes-and-clients/).

### Staking pool

The combined ETH of more than one Ethereum staker, used to reach the 32 ETH
required to activate a set of validator keys. A node operator uses these keys
to participate in consensus and the [block rewards](/en/glossary/#block-
reward) are split amongst contributing stakers. Staking pools or delegating
staking are not native to the Ethereum protocol, but many solutions have been
built by the community. [More on pooled staking](/en/staking/pools/).

