Skip to main content

[](/en/)

  * Learn
  * Use
  * Build
  * Participate
  * Research

Search```K`

Languages EN

![](/_next/image/?url=%2F_next%2Fstatic%2Fmedia%2Flayer-2-hub-
hero.5bb68ce2.jpg&w=1920&q=75)

# Layer 2

## Ethereum for everyone

Scaling Ethereum for mass adoption.

What is layer 2Use layer 2

## What is layer 2?

Layer 2 (L2) is a collective term to describe a specific set of Ethereum
scaling solutions. **A layer 2 is a separate _blockchain_ that extends
Ethereum and inherits the security guarantees of Ethereum**.

Now let’s dig into it a bit more. To do this we first need to explain layer 1
(L1).

![](/_next/image/?url=%2F_next%2Fstatic%2Fmedia%2Fwhat-is-
ethereum.b37ce60e.png&w=1504&q=75)

## What is layer 1?

Layer 1 is the base blockchain. Ethereum and Bitcoin are both layer 1
blockchains because they are the **underlying foundation that various layer 2
networks build on top of**. Examples of layer 2 projects include "rollups" on
Ethereum and the Lightning Network on Bitcoin. All user transaction activity
on these layer 2 projects can ultimately settle back to the layer 1
blockchain.

Ethereum also functions as a _data availability_ layer for layer 2s. Layer 2
projects will post their transaction data onto Ethereum, relying on Ethereum
for data availability. This data can be used to get the state of the layer 2,
or to dispute transactions on layer 2.

**Ethereum as the layer 1 includes:**

  1. **A network of node operators** to secure and _validate_ the network

  2. **A network of block producers**

  3. **The blockchain** itself and the history of transaction data

  4. **The _consensus mechanism_** for the network

Still confused on Ethereum? [Learn what Ethereum is.](/en/what-is-ethereum/)

![](/_next/image/?url=%2F_next%2Fstatic%2Fmedia%2Fdao-2.62aa97a7.png&w=1080&q=75)

## Why do we need layer 2?

Three desirable properties of a blockchain are that it is **decentralized,
secure, and scalable**. The [blockchain trilemma(opens in a new
tab)](https://www.ledger.com/academy/what-is-the-blockchain-trilemma) states
that a simple blockchain architecture can only achieve two out of three. Want
a secure and decentralized blockchain? You need to sacrifice scalability.

Ethereum currently processes 1+ million transactions per day. The demand to
use Ethereum can cause transaction fee prices to be high. This is where layer
2 networks come in.

### Scalability

The main goal of layer 2 is to increase transaction throughput (higher
transactions per second) without sacrificing decentralization or security.

Ethereum _Mainnet_ (layer 1) is only able to process roughly 15 transactions
per second. When demand to use Ethereum is high, the network becomes
congested, which increases transaction fees and prices out users who cannot
afford those fees. Layer 2s are solutions that reduce those fees by processing
transactions off the layer-1 blockchain.

[More on Ethereum's vision](/en/roadmap/vision/)

### Benefits of layer 2

![💸](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4b8.svg)

### Lower fees

By combining multiple off-chain transactions into a single layer 1
transaction, transaction fees are massively reduced, making Ethereum more
accessible for all.

![🔐](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f510.svg)

### Maintain security

Layer 2 blockchains settle their transactions on Ethereum Mainnet, allowing
users to benefit from the security of the Ethereum network.

![🛠️](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f6e0.svg)

### Expand use cases

With higher transactions per second, lower fees, and new technology, projects
will expand into new applications with improved user experience.

## How does layer 2 work?

As we mentioned above, layer 2 is a collective term for Ethereum scaling
solutions that handle transactions off Ethereum layer 1 while still taking
advantage of the robust decentralized security of Ethereum layer 1. **A layer
2 is a separate blockchain that extends Ethereum**. How does that work?

There are several different types of layer 2, each having their own trade-offs
and security models. Layer 2s take the transactional burden away from the
layer 1 allowing it to become less congested, and everything becomes more
scalable.

### Rollups

Rollups bundle (or ’roll up’) hundreds of transactions into a single
transaction on layer 1. This distributes the L1 transaction fees across
everyone in the rollup, making it cheaper for each user.

The transaction data in the rollup is submitted to layer 1, but the execution
is done separately by the rollup. By submitting transaction data onto layer 1,
rollups inherit the security of Ethereum. This is because once the data is
uploaded to layer 1, reverting a rollup transaction requires reverting
Ethereum. There are two different approaches to rollups: optimistic and zero-
knowledge - they differ primarily on how this transaction data is submitted to
L1.

![](/_next/image/?url=%2F_next%2Fstatic%2Fmedia%2Frollup-2.6c65c191.png&w=1920&q=75)

![](/_next/image/?url=%2F_next%2Fstatic%2Fmedia%2Foptimistic_rollup.abeb50eb.png&w=384&q=75)

### Optimistic rollups

Optimistic rollups are 'optimistic' in the sense that transactions are assumed
to be valid, but can be challenged if necessary. If an invalid transaction is
suspected, a fault proof is run to see if this has taken place.

[More on optimistic rollups](/en/developers/docs/scaling/optimistic-rollups/)

![](/_next/image/?url=%2F_next%2Fstatic%2Fmedia%2Fzk_rollup.c80c6032.png&w=384&q=75)

### Zero-knowledge rollups

Zero-knowledge rollups use validity proofs where transactions are computed
off-chain, and then compressed data is supplied to Ethereum Mainnet as a proof
of their validity.

[More on ZK-rollups](/en/developers/docs/scaling/zk-rollups/)

## Do your own research: risks of layer 2

Many layer 2 projects are relatively young and still require users to trust
some operators to be honest as they work to decentralize their networks.
Always do your own research to decide if you're comfortable with any risks
involved.

For more information on the technology, risks, and _trust assumptions_ of
layer 2s, we recommend checking out L2BEAT, which provides a comprehensive
risk assessment framework of each project.

[Go to L2BEAT(opens in a new tab)](https://l2beat.com/scaling/risk)

## Use layer 2

Now that you understand why layer 2 exists and how it works, let's get you up
and running!

If you are using _smart contract_ wallet such as Safe or Argent, you will not
have control over this address on a layer 2 until you redeploy your contract
account to that address on the layer 2. Classic accounts with _recovery
phrase_ will automatically own the same account on all layer 2 networks.

### Generalized layer 2s

Generalized layer 2s behave just like Ethereum — but cheaper. Anything that
you can do on Ethereum layer 1, you can also do on layer 2. Many _dapps_ have
already begun to migrate to these networks or have skipped Mainnet altogether
to build projects straight on a layer 2.

![](/_next/image/?url=%2F_next%2Fstatic%2Fmedia%2Farbitrum.ac293915.png&w=256&q=75)

### Arbitrum One

universal

Arbitrum One is an Optimistic Rollup that aims to feel exactly like
interacting with Ethereum, but with transactions costing a fraction of what
they do on L1.

Note: Fraud proofs only for whitelisted users, whitelist not open yet

[Arbitrum One Bridge(opens in a new
tab)](https://bridge.arbitrum.io/)[Arbitrum One Ecosystem Portal(opens in a
new tab)](https://portal.arbitrum.one/)[Arbitrum One Token Lists(opens in a
new tab)](https://www.coingecko.com/en/categories/arbitrum-ecosystem)

[Explore Arbitrum One(opens in a new tab)](https://arbitrum.io/)

![](/_next/image/?url=%2F_next%2Fstatic%2Fmedia%2Foptimism.bd371b88.png&w=256&q=75)

### Optimism

universal

Optimism is a fast, simple, and secure EVM-equivalent optimistic rollup. It
scales Ethereum's tech while also scaling its values through retroactive
public goods funding.

Note: Fault proofs in development

[Optimism Bridge(opens in a new
tab)](https://app.optimism.io/bridge/deposit)[Optimism Ecosystem Portal(opens
in a new tab)](https://www.optimism.io/apps)[Optimism Token Lists(opens in a
new tab)](https://tokenlists.org/token-
list?url=https://static.optimism.io/optimism.tokenlist.json)

[Explore Optimism(opens in a new tab)](https://optimism.io/)

![](/_next/image/?url=%2F_next%2Fstatic%2Fmedia%2Fboba.f86419b9.png&w=256&q=75)

### Boba Network

universal

Boba is an Optimistic Rollup originally forked from Optimism which is a
scaling solution that aims to reduce gas fees, improve transaction throughput,
and extend the capabilities of smart contracts.

Note: State validation in development

[Boba Network Bridge(opens in a new tab)](https://gateway.boba.network/)

[Explore Boba Network(opens in a new tab)](https://boba.network/)

![](/_next/image/?url=%2F_next%2Fstatic%2Fmedia%2Fbase.77146b50.png&w=256&q=75)

### Base

universal

Base is a secure, low-cost, developer-friendly Ethereum L2 built to bring the
next billion users to web3. It is an Ethereum L2, incubated by Coinbase and
built on the open-source OP Stack.

Note: Fraud proof system is currently under development

[Base Bridge(opens in a new tab)](https://bridge.base.org/deposit)[Base
Ecosystem Portal(opens in a new tab)](https://www.base.org/ecosystem)

[Explore Base(opens in a new tab)](https://base.org/)

![](/_next/image/?url=%2F_next%2Fstatic%2Fmedia%2Fzksync.0decd553.png&w=256&q=75)

### zkSync

universal

zkSync is a ZK Rollup that aims to scale Ethereum and its values to mainstream
adoption, without degrading security or decentralization.

[zkSync Bridge(opens in a new tab)](https://portal.zksync.io/bridge/)

[Explore zkSync(opens in a new tab)](https://zksync.io/)

![](/_next/image/?url=%2F_next%2Fstatic%2Fmedia%2Fstarknet.bfc88bb1.png&w=256&q=75)

### Starknet

universal

Starknet is a Validity Rollup Layer 2. It provides high throughput, low gas
costs, and retains Ethereum Layer 1 levels of security.

[Starknet Bridge(opens in a new tab)](https://starkgate.starknet.io)[Starknet
Ecosystem Portal(opens in a new tab)](https://www.starknet-
ecosystem.com)[Starknet Token Lists(opens in a new
tab)](https://github.com/starknet-io/starknet-
addresses/blob/master/bridged_tokens/mainnet.json)

[Explore Starknet(opens in a new tab)](https://www.starknet.io)

### Application specific layer 2s

Application specific layer 2s are projects that specialize in optimizing for a
specific application space, bringing improved performance.

![](/_next/image/?url=%2F_next%2Fstatic%2Fmedia%2Floopring.4be82065.png&w=256&q=75)

### Loopring

paymentsexchange

Loopring's zkRollup L2 solution aims to offer the same security guarantees as
Ethereum mainnet, with a big scalability boost: throughput increased by 1000x,
and cost reduced to just 0.1% of L1.

[Loopring Bridge(opens in a new tab)](https://loopring.io/#/layer2)

[Explore Loopring(opens in a new tab)](https://loopring.org/#/)

![](/_next/image/?url=%2F_next%2Fstatic%2Fmedia%2Fzkspace.7d72fca7.png&w=256&q=75)

### ZKSpace

paymentsexchange

The ZKSpace platform consists of three main parts: a layer 2 AMM DEX utilizing
ZK-Rollups technology called ZKSwap, a payment service called ZKSquare, and an
NFT marketplace called ZKSea.

[ZKSpace Bridge(opens in a new tab)](https://zks.app/wallet/token)

[Explore ZKSpace(opens in a new tab)](https://zkbase.org/)

![](/_next/image/?url=%2F_next%2Fstatic%2Fmedia%2Faztec.83b47139.png&w=256&q=75)

### Aztec

paymentsintegrations

Aztec Network is the first private zk-rollup on Ethereum, enabling
decentralized applications to access privacy and scale.

[Aztec Bridge(opens in a new tab)](https://zk.money/)

[Explore Aztec(opens in a new tab)](https://aztec.network/)

## A note on sidechains, validiums, and alternative blockchains

**Sidechains and validiums** are blockchains that allow assets from Ethereum
to be bridged over and used on another blockchain. Sidechains and validiums
run in parallel with Ethereum, and interact with Ethereum through _bridges_ ,
but they do not derive their security or data availability from Ethereum.

Both scale similarly to layer 2s - they offer lower transaction fees and
higher transaction throughput - but have different trust assumptions.

  * [More info on sidechains](/en/developers/docs/scaling/sidechains/)
  * [More info on validiums](/en/developers/docs/scaling/validium/)

Some layer 1 blockchains report higher throughput and lower transaction fees
than Ethereum, but generally with trade-offs elsewhere, for example greater
hardware requirements for running nodes.

## How to get onto a layer 2

There are two primary ways to get your assets onto a layer 2: bridge funds
from Ethereum via a smart contract or withdraw your funds on an exchange
directly onto the layer 2 network.

#### Funds in your wallet?

If you've already got your ETH in your wallet, you'll need to use a bridge to
move it from Ethereum Mainnet to a layer 2.

[More on bridges](/en/bridges/)

Select L2 you want to bridge to

#### Funds on an exchange?

Some centralized exchanges now offer direct withdrawals and deposits to layer
2s. Check which exchanges support layer 2 withdrawals and which layer 2s they
support.

You'll also need a wallet to withdraw your funds to. [Find an Ethereum
wallet.](/en/wallets/find-wallet/)

Select...

![ethereum-logo](/_next/image/?url=%2F_next%2Fstatic%2Fmedia%2Feth-home-
icon.c8819cf4.png&w=128&q=75)

## Tools to be effective on layer 2

### Information

  * ![L2BEAT](/_next/image/?url=%2F_next%2Fstatic%2Fmedia%2Fl2beat.e5308b8d.jpg&w=256&q=75)

L2BEAT

L2BEAT is a great resource for looking at technical risk assessments of layer
2 projects. We recommend checking out their resources when researching
specific layer 2 projects.

[Goto L2BEAT website(opens in a new tab)](https://l2beat.com)

  * ![Ethereum Ecosystem](/_next/image/?url=%2F_next%2Fstatic%2Fmedia%2Fethereumecosystem.046ea086.png&w=256&q=75)

Ethereum Ecosystem

Unofficial Ecosystem page of Ethereum and its Layer 2s including Base,
Optimism, and Starknet featuring hundreds of dApps and tools.

[Goto Ethereum Ecosystem website(opens in a new tab)](https://www.ethereum-
ecosystem.com/)

  * ![growthepie](/_next/image/?url=%2F_next%2Fstatic%2Fmedia%2Fgrowthepie.2b186310.png&w=256&q=75)

growthepie

Curated analytics about Ethereum layer 2s

[Goto growthepie website(opens in a new tab)](https://growthepie.xyz)

  * ![L2 Fees](/_next/image/?url=%2F_next%2Fstatic%2Fmedia%2Fdoge-computer.482265f8.png&w=256&q=75)

L2 Fees

L2 Fees lets you see the current cost (denominated in USD) for doing
transactions on different layer 2s.

[Goto L2 Fees website(opens in a new tab)](https://l2fees.info)

  * ![Chainlist](/_next/image/?url=%2F_next%2Fstatic%2Fmedia%2Fdoge-computer.482265f8.png&w=256&q=75)

Chainlist

Chainlist is a great resource for importing network RPC's into supporting
wallets. You will find RPC's for layer 2 projects here to help get you
connected.

[Goto Chainlist website(opens in a new tab)](https://chainlist.org)

### Wallet managers

  * ![Zapper](/_next/image/?url=%2F_next%2Fstatic%2Fmedia%2Fzapper.8f3666f4.png&w=256&q=75)

Zapper

Manage your entire web3 portfolio from DeFi to NFTs and whatever comes next.
Invest in the latest opportunities from one convenient place.

[Goto Zapper website(opens in a new tab)](https://zapper.fi/)

  * ![Zerion](/_next/image/?url=%2F_next%2Fstatic%2Fmedia%2Fzerion.53cd2ff6.png&w=256&q=75)

Zerion

Build and manage your entire DeFi portfolio from one place. Discover the world
of decentralized finance today.

[Goto Zerion website(opens in a new tab)](https://zerion.io)

  * ![DeBank](/_next/image/?url=%2F_next%2Fstatic%2Fmedia%2Fdebank.c442d5b7.png&w=256&q=75)

DeBank

Keep up with all the important happenings in the web3 world

[Goto DeBank website(opens in a new tab)](https://debank.com)

## FAQ

###

Why is there no 'official' Ethereum L2?

More

Just as there is no 'official' Ethereum client, there is no 'official'
Ethereum layer 2. Ethereum is permissionless - technically anyone can create a
layer 2! Multiple teams will implement their version of a layer 2, and the
ecosystem as a whole will benefit from a diversity of design approaches that
are optimized for different use cases. Much like we have multiple Ethereum
clients developed by multiple teams in order to have diversity in the network,
this too will be how layer 2s develop in the future.

###

What is the difference between optimistic and zero-knowledge rollups?

More

Both optimistic and zero-knowledge rollups bundle (or ’roll up’) hundreds of
transactions into a single transaction on layer 1. Rollup transactions get
executed outside of layer 1 but transaction data gets posted to layer 1.

The primary difference is what data is posted to the layer 1 and how the data
is verified. Validity proofs (used by zero-knowledge rollups) run the
computations off-chain and post a proof, whereas fault proofs (used by
optimistic rollups) only run the computations on-chain when fault is suspected
and must be checked.

At the moment, most ZK-rollups are application specific, in contrast with
optimistic rollups which have largely been generalizable.

[More info on optimistic rollups](/en/developers/docs/scaling/optimistic-
rollups/)

[More info on zero-knowledge rollups](/en/developers/docs/scaling/zk-rollups/)

###

What are the risks with layer 2?

More

Layer 2 projects contain additional risks compared to holding funds and
transacting directly on Ethereum Mainnet. For instance, _sequencers_ may go
down, leading you to have to wait to access funds.

We encourage you to do your own research before transferring significant funds
to a layer 2. For more information on the technology, risks, and trust
assumptions of layer 2s, we recommend checking out [L2BEAT(opens in a new
tab)](https://l2beat.com/?view=risk), which provides a comprehensive risk
assessment framework of each project.

Blockchain bridges, which facilitate asset transfers to layer 2, are in their
early stages of development and it is likely that the optimal bridge design
has not been discovered yet. There have been [recent hacks of bridges(opens in
a new tab)](https://rekt.news/wormhole-rekt/).

[More on bridges](/en/bridges/)

###

Why aren't some layer 2 projects listed here?

More

We want to make sure we list the best resources possible so users can navigate
the layer 2 space in a safe and confident manner. We maintain a framework of
criteria for how projects are evaluated for inclusion. [View our layer 2
listing policy here.](/en/contributing/adding-layer-2s/)

Anyone is free to suggest adding a layer 2 on ethereum.org. If there's a layer
2 that we have missed, [please suggest it(opens in a new
tab)](https://github.com/ethereum/ethereum-org-
website/issues/new?&template=suggest_layer2.md).

## Further reading

  * [A rollup-centric ethereum roadmap(opens in a new tab)](https://ethereum-magicians.org/t/a-rollup-centric-ethereum-roadmap/4698) _\- Vitalik Buterin_
  * [An Incomplete Guide to Rollups(opens in a new tab)](https://vitalik.eth.limo/general/2021/01/05/rollup.html) _\- Vitalik Buterin_
  * [Polygon sidechain vs Ethereum rollups: layer 2 scaling approaches| Vitalik Buterin and Lex Fridman(opens in a new tab)](https://www.youtube.com/watch?v=DyNbmgkyxJI) _\- Lex Clips_
  * [ROLLUPS - The Ultimate Ethereum Scaling Strategy? Arbitrum & Optimism Explained(opens in a new tab)](https://www.youtube.com/watch?v=7pWxCklcNsU) _\- Finematics_
  * [Understanding rollup economics from first principals(opens in a new tab)](https://barnabe.substack.com/p/understanding-rollup-economics-from?s=r) _\- Barnabé Monnot_

## Test your Ethereum knowledge

Layer 2

Question number 1:To scale, most alternative layer 1 networks have primarily
sacrificed on:

A

Security

B

Decentralization

C

Token price

D

Security and decentralization

Check answer

### Was this page helpful?

YesNo

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

### Data availability

Any node can independently verify transactions on a blockchain in order to
maintain transparency and trust in the system.

### Validator

A [node](/en/glossary/#node) in a [proof-of-stake](/en/glossary/#pos) system
responsible for storing data, processing transactions, and adding new blocks
to the blockchain. To activate validator software, you need to be able to
[stake](/en/glossary/#staking) 32 ETH. [More on staking in
Ethereum](/en/staking/).

### Consensus

When more than 2/3 of the computers in a network agree that they have the same
set of records, making sure everyone is on the same page. This isn't about the
rules they follow, but making sure they all have the same information.

### Mainnet

Short for "main network," this is the main public Ethereum
[blockchain](/en/glossary/#blockchain).

### Trust assumptions

Trust assumptions are basic beliefs about a system's safety and dependability,
guiding what we trust for the system to function.

### Smart contract

A smart contract is a program that automatically executes agreements on a
blockchain, like a self-enforcing digital contract. [Introduction to smart
contracts](/en/smart-contracts/).

### Seed phrase/recovery phrase

A list of words given to you when you create a digital wallet. It acts like a
password that can help you get back into your wallet if you lose access,
making sure you don't lose your digital money or tokens.

### Dapp

A dApp is a decentralized application that runs on a blockchain network,
offering services without a central controlling authority. [More on
decentralized applications](/en/dapps/).

### Bridge

A blockchain bridge is used to transfer assets from one blockchain network to
another.

### Sequencer

A sequencer is a program responsible for ordering transactions in a blockchain
network.

