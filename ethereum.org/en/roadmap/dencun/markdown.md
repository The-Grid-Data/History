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
  3. [dencun](/en/roadmap/dencun/)

Page last updated: March 14, 2024

On this page

  * When do we expect rollups to reflect lower fees due to Proto-Danksharding?
  * How can ETH be converted after the hard fork?
  * What problem is the Dencun network upgrade solving?
  * How is old blob data accessed?
  * How does this upgrade contribute to the broader Ethereum roadmap?
  * Does this upgrade affect all Ethereum consensus and validator clients?
  * How does Cancun-Deneb (Dencun) affect Goerli or other Ethereum testnets?
  * Will all transactions on L2s now use temporary blob space, or will you be able to choose?
  * Will 4844 reduce L1 gas?
  * Will this reduce fees on other EVM layer 1 blockchains?
  * More of a visual learner?
  * Further reading

# Cancun-Deneb (Dencun)

Cancun-Deneb (Dencun) is an upgrade to the Ethereum network, which activates
**Proto-Danksharding (EIP-4844)** , introducing temporary data **blobs** for
cheaper _layer 2 (L2)_ rollup storage.

A new transaction type enables rollup providers to store data more cost-
effectively in what are known as "blobs." Blobs are guaranteed to be available
to the network for around 18 days (more precisely, 4096 _epochs_). After this
period, blobs are pruned from the network, but applications can still verify
the validity of their data using proofs.

This significantly reduces the cost of rollups, limits chain growth, and helps
to support more users while maintaining security and a decentralized set of
node operators.

## When do we expect rollups to reflect lower fees due to Proto-Danksharding?

  * This upgrade activated at epoch 269568, on **13-Mar-2024 at 13:55PM (UTC)**
  * All major rollup providers, such as Arbitrum or Optimism, have signalled that blobs will be supported immediately following the upgrade
  * The timeline for individual rollup support may vary, as each provider must update their systems to take advantage of the new blob space

## How can ETH be converted after the hard fork?

  * **No Action Required for Your ETH** : Following the Ethereum Dencun upgrade, there is no need to convert or upgrade your ETH. Your account balances will remain the same, and the ETH you currently hold will remain accessible in its existing form after the hard fork.
  * **Beware of Scams!** ![⚠️](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/26a0.svg) **anyone instructing you to "upgrade" your ETH is trying to scam you.** There is nothing you need to do in relation to this upgrade. Your assets will stay completely unaffected. Remember, staying informed is the best defense against scams.

[More on recognizing and avoiding scams](/en/security/)

## What problem is the Dencun network upgrade solving?

Dencun primarily addresses **scalability** (handling more users and more
transactions) with **affordable fees** , while **maintaining
decentralization** of the network.

The Ethereum community has been taking a "rollup-centric" approach to its
growth, which places layer 2 rollups as the primary means to safely support
more users.

Rollup networks handle the _processing_ (or "execution") of transactions
separate from Mainnet and then publish a cryptographic proof and/or compressed
transaction data of the results back to Mainnet for record keeping. Storing
these proofs carries an expense (in the form of _gas_), which, before Proto-
Danksharding, had to be stored permanently by all network node operators,
making it an expensive task.

The introduction of Proto-Danksharding in the Dencun upgrade adds cheaper data
storage for these proofs by only requiring node operators to store this data
for about 18 days, after which data can be safely removed to prevent expansion
of hardware requirements. Because rollups typically have a withdrawal period
of 7 days, their security model is unchanged as long as blobs are available on
L1 for this duration. The 18-day pruning window provides a significant buffer
for this period.

[More on scaling Ethereum](/en/roadmap/scaling/)

## How is old blob data accessed?

While regular Ethereum nodes will always hold the _current state_ of the
network, historical blob data can be discarded approximately 18 days after its
introduction. Before discarding this data, Ethereum ensures that it has been
made available to all network participants, allowing time for:

  * Interested parties to download and store the data.
  * Completion of all rollup challenge periods.
  * Finalization of the rollup transactions.

_Historical_ blob data may be desired for a variety of reasons and can be
stored and accessed using several decentralized protocols:

  * **Third-party indexing protocols** , such as The Graph, store this data through a decentralized network of node operators incentivized by crypto-economic mechanisms.
  * **BitTorrent** is a decentralized protocol where volunteers can hold and distribute this data to others.
  * **[Ethereum portal network](/en/developers/docs/networking-layer/portal-network/)** aims to provide access to all Ethereum data through a decentralized network of node operators by distributing data among participants akin to BitTorrent.
  * **Individual users** are always free to store their own copies of any data they wish for historical reference.
  * **Rollup providers** are incentivized to store this data to enhance the user experience of their rollup.
  * **Block explorers** typically run archival nodes that index and store all this information for easy historical reference, accessible to users via a web interface.

It is important to note that recovering historical state operates on a
**1-of-N trust model**. This means that you only need data from _a single
trustworthy source_ to verify its correctness using the current state of the
network.

## How does this upgrade contribute to the broader Ethereum roadmap?

Proto-Danksharding sets the stage for the full implementation of
[Danksharding](/en/roadmap/danksharding/). Danksharding is designed to
distribute the storage of rollup data across node operators, so each operator
only needs to handle a small part of the total data. This distribution will
increase the number of data blobs per block, which is essential for scaling
Ethereum to handle more users and transactions.

This scalability is crucial to [supporting billions of users on
Ethereum](/en/roadmap/scaling/) with affordable fees and more advanced
applications, while maintaining a decentralized network. Without these
changes, the hardware demands for node operators would escalate, leading to
the need for increasingly expensive equipment. This could price out smaller
operators, resulting in a concentration of network control among a few large
operators, which would go against the principle of decentralization.

## Does this upgrade affect all Ethereum consensus and validator clients?

Yes, Proto-Danksharding (EIP-4844) requires updates to both execution clients
and consensus clients. All main Ethereum clients have released versions
supporting the upgrade. To maintain synchronization with the Ethereum network
post-upgrade, node operators must ensure they are running a supported client
version. Note that the information about client releases is time-sensitive,
and users should refer to the latest updates for the most current details.
[See details on supported client releases(opens in a new
tab)](https://blog.ethereum.org/2024/02/27/dencun-mainnet-announcement#client-
releases).

The consensus clients handle the _Validator_ software, which has all been
updated to accommodate the upgrade.

## How does Cancun-Deneb (Dencun) affect Goerli or other Ethereum testnets?

  * Devnets, Goerli, Sepolia and Holesky have all undergone the Dencun upgrade and have Proto-Danksharding fully functioning
  * Rollup developers can use these networks for EIP-4844 testing
  * Most users will be completely unaffected by this change to each testnet

## Will all transactions on L2s now use temporary blob space, or will you be
able to choose?

Rollup transactions on Layer 2 (L2) of Ethereum have the option of using two
types of data storage: temporary blob space or permanent smart contract
calldata. Blob space is an economical choice, providing temporary storage at a
lower cost. It guarantees data availability for all necessary challenge
periods. On the other hand, smart contract calldata offers permanent storage
but is more expensive.

The decision between using blob space or calldata is primarily made by rollup
providers. They base this decision on the current demand for blob space. If
blob space is in high demand, rollups may opt for calldata to ensure the data
is posted in a timely manner.

While it's theoretically possible for users to choose their preferred storage
type, rollup providers typically manage this choice. Offering this option to
users would add complexity, particularly in cost-effective bundling
transactions. For specific details on this choice, users should refer to the
documentation provided by individual rollup providers.

## Will 4844 reduce L1 gas?

Not significantly. A new gas market is introduced exclusively for blob space,
for use by rollup providers. _Although fees on L1 may be reduced by off-
loading rollup data to blobs, this upgrade primarily focuses on the reduction
of L2 fees. Reduction of fees on L1 (Mainnet) may occur as a second-order
effect to a lesser extent._

  * L1 gas reduction will be proportional to adoption/usage of blob data by rollup providers
  * L1 gas is likely to remain competitive from non-rollup related activity
  * Rollups that adopt the use of blob space will demand less L1 gas, helping push L1 gas fees downward in the near-term
  * Blob space is still limited, so if blobs within a block are saturated/full, then rollups may be required to post their data as permanent data in the meantime, which would drive L1 and L2 gas prices up

## Will this reduce fees on other EVM layer 1 blockchains?

No. The benefits of Proto-Danksharding are specific to Ethereum layer 2
rollups that store their proofs on layer 1 (Mainnet).

Simply being compatible with the Ethereum Virtual Machine (EVM) does not mean
that a network will see any benefit from this upgrade. Networks that operate
independently of Ethereum (whether EVM compatible or not) do not store their
data on Ethereum and will not see any benefit from this upgrade.

[More about layer 2 rollups](/en/layer-2/)

## More of a visual learner?

_Unlocking Ethereum's Scaling, EIP-4844 — Finematics_

 _Blobspace 101 with Domothy — Bankless_

## Further reading

  * [EIP4844.com(opens in a new tab)](https://www.eip4844.com/)
  * [EIP-4844: Shard blob transactions (Proto-Danksharding)(opens in a new tab)](https://eips.ethereum.org/EIPS/eip-4844)
  * [Dencun Mainnet Announcement(opens in a new tab)](https://blog.ethereum.org/2024/02/27/dencun-mainnet-announcement) \- _Ethereum Foundation blog_
  * [The Hitchhiker's Guide to Ethereum: Proto-Danksharding(opens in a new tab)](https://members.delphidigital.io/reports/the-hitchhikers-guide-to-ethereum/#proto-danksharding-eip-4844) \- _Jon Charbonneau_
  * [Proto-Danksharding FAQ(opens in a new tab)](https://notes.ethereum.org/@vbuterin/proto_danksharding_faq) \- _Vitalik Buterin_
  * [An In-depth Explanation of EIP-4844: The Core of the Cancun Upgrade(opens in a new tab)](https://medium.com/@ebunker.io/an-in-depth-explanation-of-eip-4844-the-core-of-the-cancun-upgrade-de7b13761d2c) \- _Ebunker_
  * [AllCoreDevs Update 016(opens in a new tab)](https://tim.mirror.xyz/HzH5MpK1dnw7qhBSmzCfdCIxpwpD6DpwlfxtaAwEFro) \- _Tim Beiko_

### Was this article helpful?

YesNo

  * [Edit page(opens in a new tab)](https://github.com/ethereum/ethereum-org-website/tree/dev/public/content/roadmap/dencun/index.md)
  * On this page

    * When do we expect rollups to reflect lower fees due to Proto-Danksharding?
    * How can ETH be converted after the hard fork?
    * What problem is the Dencun network upgrade solving?
    * How is old blob data accessed?
    * How does this upgrade contribute to the broader Ethereum roadmap?
    * Does this upgrade affect all Ethereum consensus and validator clients?
    * How does Cancun-Deneb (Dencun) affect Goerli or other Ethereum testnets?
    * Will all transactions on L2s now use temporary blob space, or will you be able to choose?
    * Will 4844 reduce L1 gas?
    * Will this reduce fees on other EVM layer 1 blockchains?
    * More of a visual learner?
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

### Layer 2

Layer 2s are another networks built on top of Ethereum main network to make
transactions faster and cheaper. [More on layer 2](/en/layer-2/).

### Epoch

A period of 32 [slots](/en/glossary/#slot), each slot being 12 seconds,
totalling 6.4 minutes. Validator [committees](/en/glossary/#committee) are
shuffled every epoch for security reasons. Each epoch has an opportunity for
the chain to be [finalized](/en/glossary/#finality). Each validator is
assigned new responsibilities at the start of each epoch. [More on proof-of-
stake](/en/developers/docs/consensus-mechanisms/pos/#how-does-validation-work)

### Gas

Gas is the fee paid for transactions and smart contracts on a blockchain, like
Ethereum. [More on gas and fees](/en/gas/).

