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
  2. [Merge](/en/roadmap/merge/)

# The Merge

  * Ethereum Mainnet uses proof-of-stake, but this wasn't always the case.
  * The upgrade from the original proof-of-work mechanism to proof-of-stake was called The Merge.
  * The Merge refers to the original Ethereum Mainnet merging with a separate proof-of-stake blockchain called the Beacon Chain, now existing as one chain.
  * The Merge reduced Ethereum's energy consumption by ~99.95%.

Page last updated: April 24, 2024

![](/_next/image/?url=%2Fupgrades%2Fmerge.png&w=1920&q=75)

Guide to Ethereum upgrades

[The Beacon Chain](/en/roadmap/beacon-chain/)[The Merge](/en/roadmap/merge/)

## On this page

  * What was The Merge?
  * Merging with Mainnet
  * The Merge and energy consumption
  * The Merge and scaling
  * Misconceptions about The Merge
  * What happened to 'Eth2'?
  * Relationship between upgrades
  * Further reading

## When's it shipping?

Shipped!

The Merge was executed on September 15, 2022. This completed Ethereum's
transition to proof-of-stake consensus, officially deprecating proof-of-work
and reducing energy consumption by ~99.95%.

## What was The Merge?

The Merge was the joining of the original execution layer of Ethereum (the
Mainnet that has existed since [genesis](/en/history/#frontier)) with its new
proof-of-stake consensus layer, the Beacon Chain. It eliminated the need for
energy-intensive mining and instead enabled the network to be secured using
staked ETH. It was a truly exciting step in realizing the Ethereum vision—more
scalability, security, and sustainability.

Ethereum State: transactions, apps, contracts, balances

⛏ Proof-of-work🌱 Proof-of-stake🚀 Beacon Chain🐼 The Merge🌳 Sharding

Initially, the [Beacon Chain](/en/roadmap/beacon-chain/) shipped separately
from _Mainnet_. Ethereum Mainnet - with all its accounts, balances, smart
contracts, and blockchain state - continued to be secured by [proof-of-
work](/en/developers/docs/consensus-mechanisms/pow/), even while the Beacon
Chain ran in parallel using [proof-of-stake](/en/developers/docs/consensus-
mechanisms/pos/). The Merge was when these two systems finally came together,
and proof-of-work was permanently replaced by proof-of-stake.

Imagine Ethereum is a spaceship that launched before it was quite ready for an
interstellar voyage. With the Beacon Chain, the community built a new engine
and a hardened hull. After significant testing, it became time to hot-swap the
new engine for the old one mid-flight. This merged the new, more efficient
engine into the existing ship enabling it to put in some serious light years
and take on the universe.

## Merging with Mainnet

Proof-of-work secured Ethereum Mainnet from genesis until The Merge. This
allowed the Ethereum blockchain we're all used to come into existence in July
2015 with all its familiar features—transactions, smart contracts, accounts,
etc.

Throughout Ethereum's history, developers prepared for an eventual transition
away from proof-of-work to proof-of-stake. On December 1, 2020, the Beacon
Chain was created as a separate blockchain to Mainnet, running in parallel.

The Beacon Chain was not originally processing Mainnet transactions. Instead,
it was reaching consensus on its own state by agreeing on active validators
and their account balances. After extensive testing, it became time for the
Beacon Chain to reach consensus on real world data. After The Merge, the
Beacon Chain became the consensus engine for all network data, including
execution layer transactions and account balances.

The Merge represented the official switch to using the Beacon Chain as the
engine of block production. Mining is no longer the means of producing valid
blocks. Instead, the proof-of-stake validators have adopted this role and are
now responsible for processing the validity of all transactions and proposing
blocks.

No history was lost in The Merge. As Mainnet merged with the Beacon Chain, it
also merged the entire transactional history of Ethereum.

This transition to proof-of-stake changed the way ether is issued. Learn more
about [ether issuance before and after The
Merge](/en/roadmap/merge/issuance/).

### Users and holders

**The Merge did not change anything for holders/users.**

_This bears repeating_ : As a user or holder of ETH or any other digital asset
on Ethereum, as well as non-node-operating stakers, **you do not need to do
anything with your funds or wallet to account for The Merge.** ETH is just
ETH. There is no such thing as "old ETH"/"new ETH" or "ETH1"/"ETH2" and
wallets work exactly the same after The Merge as they did before—people
telling you otherwise are likely scammers.

Despite swapping out proof-of-work, the entire history of Ethereum since
genesis remained intact and unaltered by the transition to proof-of-stake. Any
funds held in your wallet before The Merge are still accessible after The
Merge. **No action is required to upgrade on your part.**

[More on Ethereum security](/en/security/#eth2-token-scam)

### Node operators and dapp developers

###

Staking node operators and providers

If you are a staker running your own node setup or a node infrastructure
provider, there are a few things you need to be aware of after The Merge.

More

Key action items include:

  1. Run _both_ a consensus client and an execution client; third-party endpoints to obtain execution data no longer work since The Merge.
  2. Authenticate both execution and consensus clients with a shared JWT secret so they can securely communicate.
  3. Set a `fee recipient` address to receive your earned transaction fee tips/MEV.

Not completing the first two items above will result in your node being seen
as "offline" until both layers are synced and authenticated.

Not setting a `fee recipient` will still allow your validator to behave as
usual, but you will miss out on unburnt fee tips and any MEV you would have
otherwise earned in blocks your validator proposes.

###

Non-validating node operators and infrastructure providers

If you're operating a non-validating Ethereum node, the most significant
change that came with The Merge was the requirement to run clients for BOTH
the execution layer AND the consensus layer.

More

Up until The Merge, an execution client (such as Geth, Erigon, Besu or
Nethermind) was enough to receive, properly validate, and propagate blocks
being gossiped by the network. _After The Merge_ , the validity of
transactions contained within an execution payload now also depends on the
validity of the "consensus block" it is contained within.

As a result, a full Ethereum node now requires both an execution client and a
consensus client. These two clients work together using a new Engine API. The
Engine API requires authentication using a JWT secret, which is provided to
both clients allowing secure communication.

Key action items include:

  * Install a consensus client in addition to an execution client
  * Authenticate execution and consensus clients with a shared JWT secret so they can securely communicate with one another.

Not completing the above items will result in your node appearing to be
"offline" until both layers are synced and authenticated.

###

Dapp and smart contract developers

The Merge was designed to have minimal impact on smart contract and dapp
developers.

More

The Merge came with changes to consensus, which also includes changes related
to:<

  * block structure
  * slot/block timing
  * opcode changes
  * sources of on-chain randomness
  * concept of _safe head_ and _finalized blocks_

For more information, check out this blog post by Tim Beiko on [How The Merge
Impacts Ethereum’s Application Layer(opens in a new
tab)](https://blog.ethereum.org/2021/11/29/how-the-merge-impacts-app-layer/).

## The Merge and energy consumption

The Merge marked the end of proof-of-work for Ethereum and start the era of a
more sustainable, eco-friendly Ethereum. Ethereum's energy consumption dropped
by an estimated 99.95%, making Ethereum a green blockchain. Learn more about
[Ethereum energy consumption](/en/energy-consumption/).

## The Merge and scaling

The Merge also set the stage for further scalability upgrades not possible
under proof-of-work, bringing Ethereum one step closer to achieving the full
scale, security and sustainability outlined in its [Ethereum
vision](/en/roadmap/vision/).

## Misconceptions about The Merge

###

Misconception: "Running a node requires staking 32 ETH."

False. Anyone is free to sync their own self-verified copy of Ethereum (i.e.
run a node). No ETH is required—not before The Merge, not after The Merge, not
ever.

More

There are two types of Ethereum nodes: nodes that can propose blocks and nodes
that don't.

Nodes that propose blocks are only a small number of the total nodes on
Ethereum. This category includes mining nodes under proof-of-work (PoW) and
validator nodes under proof-of-stake (PoS). This category requires committing
economic resources (such as GPU hash power in proof-of-work or staked ETH in
proof-of-stake) in exchange for the ability to occasionally propose the next
block and earn protocol rewards.

The other nodes on the network (i.e. the majority) are not required to commit
any economic resources beyond a consumer-grade computer with 1-2 TB of
available storage and an internet connection. These nodes do not propose
blocks, but they still serve a critical role in securing the network by
holding all block proposers accountable by listening for new blocks and
verifying their validity on arrival according to the network consensus rules.
If the block is valid, the node continues propagating it through the network.
If the block is invalid for whatever reason, the node software will disregard
it as invalid and stop its propagation.

Running a non-block-producing node is possible for anyone under either
consensus mechanism (proof-of-work or proof-of-stake); it is _strongly
encouraged_ for all users if they have the means. Running a node is immensely
valuable for Ethereum and gives added benefits to any individual running one,
such as improved security, privacy and censorship resistance.

The ability for anyone to run their own node is _absolutely essential_ to
maintaining the decentralization of the Ethereum network.

[More on running your own node](/en/run-a-node/)

###

Misconception: "The Merge failed to reduced gas fees."

False. The Merge was a change of consensus mechanism, not an expansion of
network capacity, and was never intended to lower gas fees.

More

Gas fees are a product of network demand relative to the capacity of the
network. The Merge deprecated the use of proof-of-work, transitioning to
proof-of-stake for consensus, but did not significantly change any parameters
that directly influence network capacity or throughput.

With a [rollup-centric roadmap(opens in a new tab)](https://ethereum-
magicians.org/t/a-rollup-centric-ethereum-roadmap/4698), efforts are being
focused on scaling user activity at [layer 2](/en/layer-2/), while enabling
layer 1 Mainnet as a secure decentralized settlement layer optimized for
rollup data storage to help make rollup transactions exponentially cheaper.
The transition to proof-of-stake is a critical precursor to realizing this.
[More on gas and fees.](/en/developers/docs/gas/)

###

Misconception: "Transactions were accelerated substantially by The Merge."

False. Though some slight changes exist, transaction speed is mostly the same
on layer 1 now as it was before The Merge.

More

A transaction's "speed" can be measured in a few ways, including time to be
included in a block and time to finalization. Both of these changes slightly,
but not in a way that users will notice.

Historically, on proof-of-work, the target was to have a new block every ~13.3
seconds. Under proof-of-stake, slots occur precisely every 12 seconds, each of
which is an opportunity for a validator to publish a block. Most slots have
blocks, but not necessarily all (i.e. a validator is offline). In proof-of-
stake, blocks are produced ~10% more frequently than on proof-of-work. This
was a fairly insignificant change and is unlikely to be noticed by users.

Proof-of-stake introduced the transaction finality concept that did not
previously exist. In proof-of-work, the ability to reverse a block gets
exponentially more difficult with every passing block mined on top of a
transaction, but it never quite reaches zero. Under proof-of-stake, blocks are
bundled into epochs (6.4 minute spans of time containing 32 chances for
blocks) which validators vote on. When an epoch ends, validators vote on
whether to consider the epoch 'justified'. If validators agree to justify the
epoch, it gets finalized in the next epoch. Undoing finalized transactions is
economically inviable as it would require obtaining and burning over one-third
of the total staked ETH.

###

Misconception: "The Merge enabled staking withdrawals."

False, but staking withdrawals have since been enabled via the
Shanghai/Capella upgrade.

More

Initially after The Merge, stakers could only access fee tips and MEV that
were earned as a result of block proposals. These rewards are credited to a
non-staking account controlled by the validator (known as the _fee
recipient_), and are available immediately. These rewards are separate from
protocol rewards for performing validator duties.

Since the Shanghai/Capella network upgrade, stakers can now designate a
_withdrawal address_ to start receiving automatic payouts of any excess
staking balance (ETH over 32 from protocol rewards). This upgrade also enabled
the ability for a validator to unlock and reclaim its entire balance upon
exiting from the network.

[More on staking withdrawals](/en/staking/withdrawals/)

###

Misconception: "Now that The Merge is complete, and withdrawals are enabled,
stakers could all exit at once."

False. Validator exits are rate limited for security reasons.

More

Since the Shanghai/Capella upgrade enabled withdrawals, validators are
incentivized to withdraw their staking balance above 32 ETH, as these funds do
not add to yield and are otherwise locked. Depending on the APR (determined by
total ETH staked), they may be incentivized to exit their validator(s) to
reclaim their entire balance or potentially stake even more using their
rewards to earn more yield.

An important caveat here, full validator exits are rate limited by the
protocol, and only so many validators may exit per epoch (every 6.4 minutes).
This limit fluctuates depending on the number of active validators, but comes
out to approximately 0.33% of total ETH staked can be exited from the network
in a single day.

This prevents a mass exodus of staked funds. Furthermore, it prevents a
potential attacker with access to a large portion of the total ETH staked from
committing a slashable offense and exiting/withdrawing all of the offending
validator balances in the same epoch before the protocol can enforce the
slashing penalty.

The APR is also intentionally dynamic, allowing a market of stakers to balance
how much they're willing to be paid to help secure the network. If the rate is
too low, then validators will exit at a rate limited by the protocol.
Gradually this will raise the APR for everyone who remains, attracting new or
returning stakers yet again.

## What happened to 'Eth2'?

The term 'Eth2' has been deprecated. After merging 'Eth1' and 'Eth2' into a
single chain, there is no longer any need to distinguish between two Ethereum
networks; there is just Ethereum.

To limit confusion, the community has updated these terms:

  * 'Eth1' is now the 'execution layer', which handles transactions and execution.
  * 'Eth2' is now the 'consensus layer', which handles proof-of-stake consensus.

These terminology updates only change naming conventions; this does not alter
Ethereum's goals or roadmap.

[Learn more about the 'Eth2' renaming(opens in a new
tab)](https://blog.ethereum.org/2022/01/24/the-great-eth2-renaming/)

## Relationship between upgrades

The Ethereum upgrades are all somewhat interrelated. So let’s recap how The
Merge relates to the other upgrades.

### The Merge and the Beacon Chain

The Merge represents the formal adoption of the Beacon Chain as the new
consensus layer to the original Mainnet execution layer. Since The Merge,
validators are assigned to secure Ethereum Mainnet, and mining on [proof-of-
work](/en/developers/docs/consensus-mechanisms/pow/) is no longer a valid
means of block production.

Blocks are instead proposed by validating nodes that have staked ETH in return
for the right to participate in consensus. These upgrades set the stage for
future scalability upgrades, including sharding.

[The Beacon Chain](/en/roadmap/beacon-chain/)

### The Merge and the Shanghai upgrade

In order to simplify and maximize focus on a successful transition to proof-
of-stake, The Merge upgrade did not include certain anticipated features such
as the ability to withdraw staked ETH. This functionality was enabled
separately with the Shanghai/Capella upgrade.

For those curious, learn more about [What Happens After The Merge(opens in a
new tab)](https://youtu.be/7ggwLccuN5s?t=101), presented by Vitalik at the
April 2021 ETHGlobal event.

### The Merge and sharding

Originally, the plan was to work on sharding before The Merge to address
scalability. However, with the boom of [layer 2 scaling
solutions](/en/layer-2/), the priority shifted to swapping proof-of-work to
proof-of-stake first.

Plans for sharding are rapidly evolving, but given the rise and success of
layer 2 technologies to scale transaction execution, sharding plans have
shifted to finding the most optimal way to distribute the burden of storing
compressed calldata from rollup contracts, allowing for exponential growth in
network capacity. This would not be possible without first transitioning to
proof-of-stake.

[Sharding](/en/roadmap/danksharding/)

## Further reading

[Ethmerge(opens in a new tab)](https://ethmerge.com/)

Ethmerge

↗

[The Merge is Coming(opens in a new tab)](https://www.alchemy.com/the-merge)

Alchemy

↗

[The State of The Merge: An Update on Ethereum’s Merge to Proof of Stake in
2022(opens in a new tab)](https://consensys.net/blog/news/the-state-of-the-
merge-an-update-on-ethereums-merge-to-proof-of-stake-in-2022/)

Consensys

↗

[Announcing the Ropsten Merge Testnet(opens in a new
tab)](https://blog.ethereum.org/2022/05/30/ropsten-merge-announcement/)

Ethereum Foundation

↗

[Execution layer specs(opens in a new
tab)](https://github.com/ethereum/execution-specs/)

Ethereum Foundation

↗

[Consensus layer specs(opens in a new
tab)](https://github.com/ethereum/consensus-specs/tree/dev/specs/bellatrix)

Ethereum Foundation

↗

[Engine API specs(opens in a new tab)](https://github.com/ethereum/execution-
apis/tree/main/src/engine)

Ethereum Foundation

↗

[The Hitchhikers Guide To Ethereum(opens in a new
tab)](https://members.delphidigital.io/reports/the-hitchhikers-guide-to-
ethereum)

Delphi Digital

↗

## Test your Ethereum knowledge

The Merge

Question number 1:Ethereum’s consensus layer was formerly known as:

A

Proof-of-work

B

Eth2

C

Eth1

D

Staking

Check answer

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

### Mainnet

Short for "main network," this is the main public Ethereum
[blockchain](/en/glossary/#blockchain).

