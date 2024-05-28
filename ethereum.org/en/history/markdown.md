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
  2. [history](/en/history/)

Page last updated: March 14, 2024

On this page

  * 2024
    * Cancun-Deneb ("Dencun")
  * 2023
    * Shanghai-Capella ("Shapella")
  * 2022
    * Paris (The Merge)
    * Bellatrix
    * Gray Glacier
  * 2021
    * Arrow Glacier
    * Altair
    * London
    * Berlin
  * 2020
    * Beacon Chain genesis
    * Staking deposit contract deployed
    * Muir Glacier
  * 2019
    * Istanbul
    * Constantinople
  * 2017
    * Byzantium
  * 2016
    * Spurious Dragon
    * Tangerine whistle
    * DAO fork
    * Homestead
  * 2015
    * Frontier thawing
    * Frontier
  * 2014
    * Ether sale
    * Yellowpaper released
  * 2013
    * Whitepaper released

# The history of Ethereum

A timeline of all the major milestones, forks, and updates to the Ethereum
blockchain.

###

What are forks?

Changes to the rules of the Ethereum protocol which often include planned
technical upgrades.

More

Forks are when major technical upgrades or changes need to be made to the
network – they typically stem from [Ethereum Improvement Proposals
(EIPs)](/en/eips/) and change the "rules" of the protocol.

When upgrades are needed in traditional, centrally-controlled software, the
company will just publish a new version for the end-user. Blockchains work
differently because there is no central ownership. [Ethereum
clients](/en/developers/docs/nodes-and-clients/) must update their software to
implement the new fork rules. Plus block creators (miners in a proof-of-work
world, validators in a proof-of-stake world) and nodes must create blocks and
validate against the new rules. [More on consensus
mechanisms](/en/developers/docs/consensus-mechanisms/)

These rule changes may create a temporary split in the network. New blocks
could be produced according to the new rules or the old ones. Forks are
usually agreed upon ahead of time so that clients adopt the changes in unison
and the fork with the upgrades becomes the main chain. However, in rare cases,
disagreements over forks can cause the network to permanently split – most
notably the creation of Ethereum Classic with the DAO fork.

###

Why do some upgrades have multiple names?

Upgrades names follow a pattern

More

The software that underlies Ethereum is composed of two halves, known as the
_execution layer_ and the _consensus layer_.

**Execution upgrade naming**

Since 2021, upgrades to the **execution layer** are named according to the
city names of [previous Devcon locations(opens in a new
tab)](https://devcon.org/en/past-events/) in chronological order:

Upgrade Name| Devcon Year| Devcon Number| Upgrade Date  
---|---|---|---  
Berlin| 2015| 0| Apr 15, 2021  
London| 2016| I| Aug 5, 2021  
Shanghai| 2017| II| Apr 12, 2023  
**Cancun**|  2018| III| Mar 13, 2024  
 _Prague_|  2019| IV| TBD  
 _Osaka_|  2020| V| TBD  
 _Bogota_|  2022| VI| TBD  
 _Bangkok_|  2024| VII| TBD  
  
**Consensus upgrade naming**

Since the launch of the _Beacon Chain_ , upgrades to the **consensus layer**
are named after celestial stars beginning with letters that proceed in
alphabetical order:

Upgrade Name| Upgrade Date  
---|---  
Beacon Chain genesis| Dec 1, 2020  
[Altair(opens in a new tab)](https://en.wikipedia.org/wiki/Altair)| Oct 27,
2021  
[Bellatrix(opens in a new tab)](https://en.wikipedia.org/wiki/Bellatrix)| Sep
6, 2022  
[Capella(opens in a new tab)](https://en.wikipedia.org/wiki/Capella)| Apr 12,
2023  
[**Deneb**(opens in a new tab)](https://en.wikipedia.org/wiki/Deneb)| Mar 13,
2024  
[ _Electra_(opens in a new
tab)](https://en.wikipedia.org/wiki/Electra_\(star\))| TBD  
  
**Combined naming**

The execution and consensus upgrades were initially rolled out at different
times, but after [The Merge](/en/roadmap/merge/) in 2022 these have been
deployed simultaneously. As-such, colloquial terms have emerged to simplify
references to these upgrades using a single conjoined term. This began with
the _Shanghai-Capella_ upgrade, commonly referred to as "**Shapella** ", and
is continued with the _Cancun-Deneb_ upgrade, which may be referred to as
"**Dencun**."

Execution Upgrade| Consensus Upgrade| Short Name  
---|---|---  
Shanghai| Capella| "Shapella"  
Cancun| Deneb| "Dencun"  
  
Skip straight to information about some of the particularly important past
upgrades: [The Beacon Chain](/en/roadmap/beacon-chain/); [The
Merge](/en/roadmap/merge/); and EIP-1559

Looking for future protocol upgrades? [Learn about upcoming upgrades on the
Ethereum roadmap](/en/roadmap/).

## 2024

### Cancun-Deneb ("Dencun")

![📆](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4c6.svg)

Mar 13, 2024, 1:55:35 PM +UTC

![🧱](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f9f1.svg)Block
number: [19,426,587(opens in a new tab)](https://etherscan.io/block/19426587)

![🧱](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f9f1.svg)Epoch
number: [269,568(opens in a new tab)](https://beaconscan.com/epoch/269568)

![🧱](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f9f1.svg)Slot
number: [8,626,176(opens in a new tab)](https://beaconscan.com/slot/8626176)

![💰](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4b0.svg)ETH
price: $3,984.00

![🖥️](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f5a5.svg)[ethereum.org
on waybackmachine(opens in a new
tab)](https://web.archive.org/web/20240312070259/https://ethereum.org/en/)

#### Cancun summary

The Cancun upgrade contains a set of improvements to Ethereum's _execution_
aimed towards improving scalability, in tandem with the Deneb consensus
upgrades.

Notably this includes EIP-4844, known as **Proto-Danksharding** , which
significantly decreases the cost of data storage for layer 2 rollups. This is
achieved through the introduction of data "blobs" which enables rollups to
post data to Mainnet for a short period of time. This results in significantly
lower transaction fees for users of layer 2 rollups.

###

Cancun EIPs

Official improvements included in this upgrade.

More

  * [EIP-1153(opens in a new tab)](https://eips.ethereum.org/EIPS/eip-1153) \- _Transient storage opcodes_
  * [EIP-4788(opens in a new tab)](https://eips.ethereum.org/EIPS/eip-4788) \- _Beacon block root in the EVM_
  * [EIP-4844(opens in a new tab)](https://eips.ethereum.org/EIPS/eip-4844) \- _Shard blob transactions (Proto-Danksharding)_
  * [EIP-5656(opens in a new tab)](https://eips.ethereum.org/EIPS/eip-5656) \- _`MCOPY` \- Memory copying instruction_
  * [EIP-6780(opens in a new tab)](https://eips.ethereum.org/EIPS/eip-6780) \- _`SELFDESTRUCT` only in same transaction_
  * [EIP-7516(opens in a new tab)](https://eips.ethereum.org/EIPS/eip-7516) \- _`BLOBBASEFEE` opcode_

  * [Layer 2 rollups](/en/layer-2/)
  * [Proto-Danksharding](/en/roadmap/scaling/#proto-danksharding)
  * [Danksharding](/en/roadmap/danksharding/)
  * [Read the Cancun upgrade specification(opens in a new tab)](https://github.com/ethereum/execution-specs/blob/master/network-upgrades/mainnet-upgrades/cancun.md)

#### Deneb summary

The Deneb upgrade contains a set of improvements to Ethereum's _consensus_
aimed towards improving scalability. This upgrade comes in tandem with the
Cancun execution upgrades to enable Proto-Danksharding (EIP-4844), along with
other improvements to the Beacon Chain.

Pre-generated signed "voluntary exit messages" no longer expire, thus giving
more control to users staking their funds with a third-party node operator.
With this signed exit message, stakers can delegate node operation while
maintaining the ability to safely exit and withdrawal their funds at any time,
without needing to ask permission from anyone.

EIP-7514 brings a tightening to the issuance of ETH by capping the "churn"
rate that validators can join the network to eight (8) per epoch. Since ETH
issuance is proportional to total ETH staked, limiting the number of
validators joining caps the _growth rate_ of newly issued ETH, while also
reducing hardware requirements for node operators, helping decentralization.

###

Deneb EIPs

Official improvements included in this upgrade

More

  * [EIP-4788(opens in a new tab)](https://eips.ethereum.org/EIPS/eip-4788) \- _Beacon block root in the EVM_
  * [EIP-4844(opens in a new tab)](https://eips.ethereum.org/EIPS/eip-4844) \- _Shard blob transactions_
  * [EIP-7044(opens in a new tab)](https://eips.ethereum.org/EIPS/eip-7044) \- _Perpetually valid signed voluntary exits_
  * [EIP-7045(opens in a new tab)](https://eips.ethereum.org/EIPS/eip-7045) \- _Increase max attestation inclusion slot_
  * [EIP-7514(opens in a new tab)](https://eips.ethereum.org/EIPS/eip-7514) \- _Add max epoch churn limit_

  * [Read the Deneb upgrade specifications(opens in a new tab)](https://github.com/ethereum/consensus-specs/blob/dev/specs/deneb/)
  * [Cancun-Deneb ("Dencun") FAQ](/en/roadmap/dencun/)

## 2023

### Shanghai-Capella ("Shapella")

![📆](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4c6.svg)

Apr 12, 2023, 10:27:35 PM +UTC

![🧱](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f9f1.svg)Block
number: [17,034,870(opens in a new tab)](https://etherscan.io/block/17034870)

![🧱](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f9f1.svg)Epoch
number: [194,048(opens in a new tab)](https://beaconscan.com/epoch/194048)

![🧱](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f9f1.svg)Slot
number: [6,209,536(opens in a new tab)](https://beaconscan.com/slot/6209536)

![💰](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4b0.svg)ETH
price: $1,917.00

![🖥️](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f5a5.svg)[ethereum.org
on waybackmachine(opens in a new
tab)](https://web.archive.org/web/20230411044526/https://ethereum.org/en/)

#### Shanghai summary

The Shanghai upgrade brought staking withdrawals to the execution layer. In
tandem with the Capella upgrade, this enabled blocks to accept withdrawal
operations, which allows stakers to withdraw their ETH from the Beacon Chain
to the execution layer.

###

Shanghai EIPs

Official improvements included in this upgrade.

More

  * [EIP-3651(opens in a new tab)](https://eips.ethereum.org/EIPS/eip-3651) – _Starts the`COINBASE` address warm_
  * [EIP-3855(opens in a new tab)](https://eips.ethereum.org/EIPS/eip-3855) – _New`PUSH0` instruction_
  * [EIP-3860(opens in a new tab)](https://eips.ethereum.org/EIPS/eip-3860) – _Limit and meter initcode_
  * [EIP-4895(opens in a new tab)](https://eips.ethereum.org/EIPS/eip-4895) – _Beacon chain push withdrawals as operations_
  * [EIP-6049(opens in a new tab)](https://eips.ethereum.org/EIPS/eip-6049) \- _Deprecate`SELFDESTRUCT`_

  * [Read the Shanghai upgrade specification(opens in a new tab)](https://github.com/ethereum/execution-specs/blob/master/network-upgrades/mainnet-upgrades/shanghai.md)

#### Capella summary

The Capella upgrade was the third major upgrade to the consensus layer (Beacon
Chain) and enabled staking withdrawals. Capella occurred synchronously with
the execution layer upgrade, Shanghai, and enabled staking withdrawal
functionality.

This consensus layer upgrade brought the ability for stakers who did not
provide withdrawal credentials with their initial deposit to do so, thereby
enabling withdrawals.

The upgrade also provided automatic account sweeping functionality, which
continuously processes validator accounts for any available rewards payments
or full withdrawals.

  * [More on staking withdrawals](/en/staking/withdrawals/).
  * [Read the Capella upgrade specifications(opens in a new tab)](https://github.com/ethereum/consensus-specs/blob/dev/specs/capella/)

## 2022

### Paris (The Merge)

![📆](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4c6.svg)

Sep 15, 2022, 6:42:42 AM +UTC

![🧱](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f9f1.svg)Block
number: [15,537,394(opens in a new tab)](https://etherscan.io/block/15537394)

![💰](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4b0.svg)ETH
price: $1,472.00

![🖥️](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f5a5.svg)[ethereum.org
on waybackmachine(opens in a new
tab)](https://web.archive.org/web/20220915075314/https://ethereum.org/)

#### Summary

The Paris upgrade was triggered by the proof-of-work blockchain passing a
_terminal total difficulty_ of 58750000000000000000000. This happened at block
15537393 on 15th September 2022, triggering the Paris upgrade the next block.
Paris was [The Merge](/en/roadmap/merge/) transition - its major feature was
switching off the [proof-of-work](/en/developers/docs/consensus-
mechanisms/pow/) mining algorithm and associated consensus logic and switching
on [proof-of-stake](/en/developers/docs/consensus-mechanisms/pos/) instead.
Paris itself was an upgrade to the [execution
clients](/en/developers/docs/nodes-and-clients/#execution-clients) (equivalent
to Bellatrix on the consensus layer) that enabled them to take instruction
from their connected [consensus clients](/en/developers/docs/nodes-and-
clients/#consensus-clients). This required a new set of internal API methods,
collectively known as the [Engine API(opens in a new
tab)](https://github.com/ethereum/execution-
apis/blob/main/src/engine/common.md), to be activated. This was arguably the
most significant upgrade in Ethereum history since Homestead!

  * [Read the Paris upgrade specification(opens in a new tab)](https://github.com/ethereum/execution-specs/blob/master/network-upgrades/mainnet-upgrades/paris.md)

###

Paris EIPs

Official improvements included in this upgrade.

More

  * [EIP-3675(opens in a new tab)](https://eips.ethereum.org/EIPS/eip-3675) – _Upgrade consensus to Proof-of-Stake_
  * [EIP-4399(opens in a new tab)](https://eips.ethereum.org/EIPS/eip-4399) – _Supplant DIFFICULTY opcode with PREVRANDAO_

* * *

### Bellatrix

![📆](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4c6.svg)

Sep 6, 2022, 11:34:47 AM +UTC

![🧱](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f9f1.svg)Epoch
number: [144,896(opens in a new tab)](https://beaconscan.com/epoch/144896)

![💰](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4b0.svg)ETH
price: $1,558.00

![🖥️](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f5a5.svg)[ethereum.org
on waybackmachine(opens in a new
tab)](https://web.archive.org/web/20220906112525/https://ethereum.org/en/)

#### Summary

The Bellatrix upgrade was the second scheduled upgrade for the [Beacon
Chain](/en/roadmap/beacon-chain/), preparing the chain for [The
Merge](/en/roadmap/merge/). It brings validator penalties to their full values
for inactivity and slashable offenses. Bellatrix also includes an update to
the fork choice rules to prepare the chain for The Merge and the transition
from the last proof-of-work block to the first proof-of-stake block. This
includes making consensus clients aware of the _terminal total difficulty_ of
58750000000000000000000.

  * [Read the Bellatrix upgrade specification(opens in a new tab)](https://github.com/ethereum/consensus-specs/tree/dev/specs/bellatrix)

* * *

### Gray Glacier

![📆](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4c6.svg)

Jun 30, 2022, 10:54:04 AM +UTC

![🧱](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f9f1.svg)Block
number: [15,050,000(opens in a new tab)](https://etherscan.io/block/15050000)

![💰](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4b0.svg)ETH
price: $1,069.00

![🖥️](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f5a5.svg)[ethereum.org
on waybackmachine(opens in a new
tab)](https://web.archive.org/web/20220630094629/https://ethereum.org/en/)

#### Summary

The Gray Glacier network upgrade pushed back the _difficulty bomb_ by three
months. This is the only change introduced in this upgrade, and is similar in
nature to the Arrow Glacier and Muir Glacier upgrades. Similar changes have
been performed on the Byzantium, Constantinople and London network upgrades.

  * [EF Blog - Gray Glacier Upgrade Announcement(opens in a new tab)](https://blog.ethereum.org/2022/06/16/gray-glacier-announcement/)

###

Gray Glacier EIPs

Official improvements included in this upgrade.

More

  * [EIP-5133(opens in a new tab)](https://eips.ethereum.org/EIPS/eip-5133) – _delays the difficulty bomb until September 2022_

## 2021

### Arrow Glacier

![📆](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4c6.svg)

Dec 9, 2021, 7:55:23 AM +UTC

![🧱](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f9f1.svg)Block
number: [13,773,000(opens in a new tab)](https://etherscan.io/block/13773000)

![💰](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4b0.svg)ETH
price: $4,111.00

![🖥️](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f5a5.svg)[ethereum.org
on waybackmachine(opens in a new
tab)](https://web.archive.org/web/20211207064430/https://ethereum.org/en/)

#### Summary

The Arrow Glacier network upgrade pushed back the _difficulty bomb_ by several
months. This is the only change introduced in this upgrade, and is similar in
nature to the Muir Glacier upgrade. Similar changes have been performed on the
Byzantium, Constantinople and London network upgrades.

  * [EF Blog - Arrow Glacier Upgrade Announcement(opens in a new tab)](https://blog.ethereum.org/2021/11/10/arrow-glacier-announcement/)
  * [Ethereum Cat Herders - Ethereum Arrow Glacier Upgrade(opens in a new tab)](https://medium.com/ethereum-cat-herders/ethereum-arrow-glacier-upgrade-e8d20fa4c002)

###

Arrow Glacier EIPs

Official improvements included in this upgrade.

More

  * [EIP-4345(opens in a new tab)](https://eips.ethereum.org/EIPS/eip-4345) – _delays the difficulty bomb until June 2022_

* * *

### Altair

![📆](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4c6.svg)

Oct 27, 2021, 10:56:23 AM +UTC

![🧱](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f9f1.svg)Epoch
number: [74,240(opens in a new tab)](https://beaconscan.com/epoch/74240)

![💰](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4b0.svg)ETH
price: $4,024.00

![🖥️](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f5a5.svg)[ethereum.org
on waybackmachine(opens in a new
tab)](https://web.archive.org/web/20211026174951/https://ethereum.org/en/)

#### Summary

The Altair upgrade was the first scheduled upgrade for the [Beacon
Chain](/en/roadmap/beacon-chain/). It added support for "sync
committees"—enabling light clients, and increased validator inactivity and
slashing penalties as development progressed towards The Merge.

  * [Read the Altair upgrade specification(opens in a new tab)](https://github.com/ethereum/consensus-specs/tree/dev/specs/altair)

####
![🎉](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f389.svg)Fun
fact!

Altair was the first major network upgrade that had an exact rollout time.
Every upgrade prior had been based on a declared block number on the proof-of-
work chain, where block times vary. The Beacon Chain does not require solving
for proof-of-work, and instead works on a time-based epoch system consisting
of 32 twelve-second "slots" of time where validators can propose blocks. This
is why we knew exactly when we would hit epoch 74,240 and Altair became live!

  * [Block time](/en/developers/docs/blocks/#block-time)

* * *

### London

![📆](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4c6.svg)

Aug 5, 2021, 12:33:42 PM +UTC

![🧱](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f9f1.svg)Block
number: [12,965,000(opens in a new tab)](https://etherscan.io/block/12965000)

![💰](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4b0.svg)ETH
price: $2,621.00

![🖥️](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f5a5.svg)[ethereum.org
on waybackmachine(opens in a new
tab)](https://web.archive.org/web/20210805124609/https://ethereum.org/en/)

#### Summary

The London upgrade introduced [EIP-1559(opens in a new
tab)](https://eips.ethereum.org/EIPS/eip-1559), which reformed the transaction
fee market, along with changes to how gas refunds are handled and the _Ice
Age_ schedule.

#### What was the London Upgrade / EIP-1559?

Before the London Upgrade, Ethereum had fixed-sized blocks. In times of high
network demand, these blocks operated at full capacity. As a result, users
often had to wait for demand to reduce to get included in a block, which led
to a poor user experience. The London Upgrade introduced variable-sized blocks
to Ethereum.

The way transaction fees on the Ethereum network were calculated changed with
[the London Upgrade](/en/history/#london) of August 2021. Before the London
upgrade, fees were calculated without separating `base` and `priority` fees,
as follows:

Let's say Alice had to pay Bob 1 ETH. In the transaction, the gas limit is
21,000 units, and the gas price is 200 gwei.

The total fee would have been: `Gas units (limit) * Gas price per unit` i.e
`21,000 * 200 = 4,200,000 gwei` or 0.0042 ETH

The implementation of [EIP-1559(opens in a new
tab)](https://eips.ethereum.org/EIPS/eip-1559) in the London Upgrade made the
transaction fee mechanism more complex, but made gas fees more predictable,
resulting in a more efficient transaction fee market. Users can submit
transactions with a `maxFeePerGas` corresponding to how much they are willing
to pay for the transaction to be executed, knowing that they will not pay more
than the market price for gas (`baseFeePerGas`), and get any extra, minus
their tip, refunded.

This video explains EIP-1559 and the benefits it brings: [EIP-1559
Explained(opens in a new tab)](https://www.youtube.com/watch?v=MGemhK9t44Q)

  * [Are you a dapp developer? Be sure to upgrade your libraries and tooling.(opens in a new tab)](https://github.com/ethereum/execution-specs/blob/master/network-upgrades/london-ecosystem-readiness.md)
  * [Read the Ethereum Foundation announcement(opens in a new tab)](https://blog.ethereum.org/2021/07/15/london-mainnet-announcement/)
  * [Read the Ethereum Cat Herder's explainer(opens in a new tab)](https://medium.com/ethereum-cat-herders/london-upgrade-overview-8eccb0041b41)

###

London EIPs

Official improvements included in this upgrade.

More

  * [EIP-1559(opens in a new tab)](https://eips.ethereum.org/EIPS/eip-1559) – _improves the transaction fee market_
  * [EIP-3198(opens in a new tab)](https://eips.ethereum.org/EIPS/eip-3198) – _returns the`BASEFEE` from a block_
  * [EIP-3529(opens in a new tab)](https://eips.ethereum.org/EIPS/eip-3529) \- _reduces gas refunds for EVM operations_
  * [EIP-3541(opens in a new tab)](https://eips.ethereum.org/EIPS/eip-3541) \- _prevents deploying contracts starting with`0xEF`_
  * [EIP-3554(opens in a new tab)](https://eips.ethereum.org/EIPS/eip-3554) – _delays the Ice Age until December 2021_

* * *

### Berlin

![📆](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4c6.svg)

Apr 15, 2021, 10:07:03 AM +UTC

![🧱](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f9f1.svg)Block
number: [12,244,000(opens in a new tab)](https://etherscan.io/block/12244000)

![💰](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4b0.svg)ETH
price: $2,454.00

![🖥️](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f5a5.svg)[ethereum.org
on waybackmachine(opens in a new
tab)](https://web.archive.org/web/20210415093618/https://ethereum.org/)

#### Summary

The Berlin upgrade optimized gas cost for certain EVM actions, and increases
support for multiple transaction types.

  * [Read the Ethereum Foundation announcement(opens in a new tab)](https://blog.ethereum.org/2021/03/08/ethereum-berlin-upgrade-announcement/)
  * [Read the Ethereum Cat Herder's explainer(opens in a new tab)](https://medium.com/ethereum-cat-herders/the-berlin-upgrade-overview-2f7ad710eb80)

###

Berlin EIPs

Official improvements included in this upgrade.

More

  * [EIP-2565(opens in a new tab)](https://eips.ethereum.org/EIPS/eip-2565) – _lowers ModExp gas cost_
  * [EIP-2718(opens in a new tab)](https://eips.ethereum.org/EIPS/eip-2718) – _enables easier support for multiple transaction types_
  * [EIP-2929(opens in a new tab)](https://eips.ethereum.org/EIPS/eip-2929) – _gas cost increases for state access opcodes_
  * [EIP-2930(opens in a new tab)](https://eips.ethereum.org/EIPS/eip-2930) – _adds optional access lists_

## 2020

### Beacon Chain genesis

![📆](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4c6.svg)

Dec 1, 2020, 12:00:35 PM +UTC

![🧱](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f9f1.svg)Slot
number: [1(opens in a new tab)](https://beaconscan.com/slot/1)

![💰](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4b0.svg)ETH
price: $586.23

![🖥️](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f5a5.svg)[ethereum.org
on waybackmachine(opens in a new
tab)](https://web.archive.org/web/20201207184633/https://www.ethereum.org/en/)

#### Summary

The [Beacon Chain](/en/roadmap/beacon-chain/) needed 16384 deposits of 32
staked ETH to ship securely. This happened on November 27, meaning the Beacon
Chain started producing blocks on December 1, 2020. This is an important first
step in achieving the [Ethereum vision](/en/roadmap/vision/).

[Read the Ethereum Foundation announcement(opens in a new
tab)](https://blog.ethereum.org/2020/11/27/eth2-quick-update-no-21/)

![📃](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4c3.svg)

[The Beacon Chain](/en/roadmap/beacon-chain/)

* * *

### Staking deposit contract deployed

![📆](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4c6.svg)

Oct 14, 2020, 9:22:52 AM +UTC

![🧱](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f9f1.svg)Block
number: [11,052,984(opens in a new tab)](https://etherscan.io/block/11052984)

![💰](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4b0.svg)ETH
price: $379.04

![🖥️](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f5a5.svg)[ethereum.org
on waybackmachine(opens in a new
tab)](https://web.archive.org/web/20201104235727/https://ethereum.org/en/)

#### Summary

The staking deposit contract introduced _staking_ to the Ethereum ecosystem.
Although a _Mainnet_ contract, it had a direct impact on the timeline for
launching the [Beacon Chain](/en/roadmap/beacon-chain/), an important
[Ethereum upgrade](/en/roadmap/).

[Read the Ethereum Foundation announcement(opens in a new
tab)](https://blog.ethereum.org/2020/11/04/eth2-quick-update-no-19/)

![📃](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4c3.svg)

[Staking](/en/staking/)

* * *

### Muir Glacier

![📆](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4c6.svg)

Jan 2, 2020, 8:30:49 AM +UTC

![🧱](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f9f1.svg)Block
number: [9,200,000(opens in a new tab)](https://etherscan.io/block/9200000)

![💰](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4b0.svg)ETH
price: $127.18

![🖥️](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f5a5.svg)[ethereum.org
on waybackmachine(opens in a new
tab)](https://web.archive.org/web/20200103093618/https://ethereum.org/)

#### Summary

The Muir Glacier fork introduced a delay to the _difficulty bomb_. Increases
in block difficulty of the [proof-of-work](/en/developers/docs/consensus-
mechanisms/pow/) consensus mechanism threatened to degrade the usability of
Ethereum by increasing wait times for sending transactions and using dapps.

  * [Read the Ethereum Foundation announcement(opens in a new tab)](https://blog.ethereum.org/2019/12/23/ethereum-muir-glacier-upgrade-announcement/)
  * [Read the Ethereum Cat Herder's explainer(opens in a new tab)](https://medium.com/ethereum-cat-herders/ethereum-muir-glacier-upgrade-89b8cea5a210)

###

Muir Glacier EIPs

Official improvements included in this fork.

More

  * [EIP-2384(opens in a new tab)](https://eips.ethereum.org/EIPS/eip-2384) – _delays the difficulty bomb for another 4,000,000 blocks, or ~611 days._

## 2019

### Istanbul

![📆](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4c6.svg)

Dec 8, 2019, 12:25:09 PM +UTC

![🧱](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f9f1.svg)Block
number: [9,069,000(opens in a new tab)](https://etherscan.io/block/9069000)

![💰](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4b0.svg)ETH
price: $151.06

![🖥️](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f5a5.svg)[ethereum.org
on waybackmachine(opens in a new
tab)](https://web.archive.org/web/20191216101254if*/https://ethereum.org/)

#### Summary

The Istanbul fork:

  * Optimised the _gas_ cost of certain actions in the [EVM](/en/developers/docs/ethereum-stack/#ethereum-virtual-machine).
  * Improved denial-of-service attack resilience.
  * Made [Layer 2 scaling](/en/developers/docs/scaling/#layer-2-scaling) solutions based on SNARKs and STARKs more performant.
  * Enabled Ethereum and Zcash to interoperate.
  * Allowed contracts to introduce more creative functions.

[Read the Ethereum Foundation announcement(opens in a new
tab)](https://blog.ethereum.org/2019/11/20/ethereum-istanbul-upgrade-
announcement/)

###

Istanbul EIPs

Official improvements included in this fork.

More

  * [EIP-152(opens in a new tab)](https://eips.ethereum.org/EIPS/eip-152) – _allow Ethereum to work with privacy-preserving currency like Zcash._
  * [EIP-1108(opens in a new tab)](https://eips.ethereum.org/EIPS/eip-1108) – _cheaper cryptography to improve _gas_ costs._
  * [EIP-1344(opens in a new tab)](https://eips.ethereum.org/EIPS/eip-1344) – _protects Ethereum against replay attacks by adding`CHAINID` [opcode](/en/developers/docs/ethereum-stack/#ethereum-virtual-machine)._
  * [EIP-1884(opens in a new tab)](https://eips.ethereum.org/EIPS/eip-1884) – _optimising opcode gas prices based on consumption._
  * [EIP-2028(opens in a new tab)](https://eips.ethereum.org/EIPS/eip-2028) – _reduces the cost of CallData to allow more data in blocks – good for[Layer 2 scaling](/en/developers/docs/scaling/#layer-2-scaling)._
  * [EIP-2200(opens in a new tab)](https://eips.ethereum.org/EIPS/eip-2200) – _other opcode gas price alterations._

* * *

### Constantinople

![📆](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4c6.svg)

Feb 28, 2019, 7:52:04 AM +UTC

![🧱](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f9f1.svg)Block
number: [7,280,000(opens in a new tab)](https://etherscan.io/block/7280000)

![💰](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4b0.svg)ETH
price: $136.29

![🖥️](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f5a5.svg)[ethereum.org
on waybackmachine(opens in a new
tab)](https://web.archive.org/web/20190415163751/https://www.ethereum.org/)

#### Summary

The Constantinople fork:

  * Reduced block [mining](/en/developers/docs/consensus-mechanisms/pow/mining/) rewards from 3 to 2 ETH.
  * Ensured the blockchain didn't freeze before proof-of-stake was implemented.
  * Optimised the _gas_ cost of certain actions in the [EVM](/en/developers/docs/ethereum-stack/#ethereum-virtual-machine).
  * Added the ability to interact with addresses that haven't been created yet.

[Read the Ethereum Foundation announcement(opens in a new
tab)](https://blog.ethereum.org/2019/02/22/ethereum-constantinople-st-
petersburg-upgrade-announcement/)

###

Constantinople EIPs

Official improvements included in this fork.

More

  * [EIP-145(opens in a new tab)](https://eips.ethereum.org/EIPS/eip-145) – _optimises cost of certain on-chain actions._
  * [EIP-1014(opens in a new tab)](https://eips.ethereum.org/EIPS/eip-1014) – _allows you to interact with addresses that have yet to be created._
  * [EIP-1052(opens in a new tab)](https://eips.ethereum.org/EIPS/eip-1052) – _optimises cost of certain on-chain actions._
  * [EIP-1234(opens in a new tab)](https://eips.ethereum.org/EIPS/eip-1234) – _makes sure the blockchain doesn't freeze before proof-of-stake and reduces block reward from 3 to 2 ETH._

## 2017

### Byzantium

![📆](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4c6.svg)

Oct 16, 2017, 5:22:11 AM +UTC

![🧱](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f9f1.svg)Block
number: [4,370,000(opens in a new tab)](https://etherscan.io/block/4370000)

![💰](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4b0.svg)ETH
price: $334.23

![🖥️](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f5a5.svg)[ethereum.org
on waybackmachine(opens in a new
tab)](https://web.archive.org/web/20171017201143/https://www.ethereum.org/)

#### Summary

The Byzantium fork:

  * Reduced block [mining](/en/developers/docs/consensus-mechanisms/pow/mining/) rewards from 5 to 3 ETH.
  * Delayed the _difficulty bomb_ by a year.
  * Added ability to make non-state-changing calls to other contracts.
  * Added certain cryptography methods to allow for [layer 2 scaling](/en/developers/docs/scaling/#layer-2-scaling).

[Read the Ethereum Foundation announcement(opens in a new
tab)](https://blog.ethereum.org/2017/10/12/byzantium-hf-announcement/)

###

Byzantium EIPs

Official improvements included in this fork.

More

  * [EIP-140(opens in a new tab)](https://eips.ethereum.org/EIPS/eip-140) – _adds`REVERT` opcode._
  * [EIP-658(opens in a new tab)](https://eips.ethereum.org/EIPS/eip-658) – _status field added to transaction receipts to indicate success or failure._
  * [EIP-196(opens in a new tab)](https://eips.ethereum.org/EIPS/eip-196) – _adds elliptic curve and scalar multiplication to allow for[ZK-Snarks](/en/developers/docs/scaling/zk-rollups/)._
  * [EIP-197(opens in a new tab)](https://eips.ethereum.org/EIPS/eip-197) – _adds elliptic curve and scalar multiplication to allow for[ZK-Snarks](/en/developers/docs/scaling/zk-rollups/)._
  * [EIP-198(opens in a new tab)](https://eips.ethereum.org/EIPS/eip-198) – _enables RSA signature verification._
  * [EIP-211(opens in a new tab)](https://eips.ethereum.org/EIPS/eip-211) – _adds support for variable length return values._
  * [EIP-214(opens in a new tab)](https://eips.ethereum.org/EIPS/eip-214) – _adds`STATICCALL` opcode, allowing non-state-changing calls to other contracts._
  * [EIP-100(opens in a new tab)](https://eips.ethereum.org/EIPS/eip-100) – _changes difficulty adjustment formula._
  * [EIP-649(opens in a new tab)](https://eips.ethereum.org/EIPS/eip-649) – _delays _difficulty bomb_ by 1 year and reduces block reward from 5 to 3 ETH._

## 2016

### Spurious Dragon

![📆](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4c6.svg)

Nov 22, 2016, 4:15:44 AM +UTC

![🧱](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f9f1.svg)Block
number: [2,675,000(opens in a new tab)](https://etherscan.io/block/2675000)

![💰](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4b0.svg)ETH
price: $9.84

![🖥️](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f5a5.svg)[ethereum.org
on waybackmachine(opens in a new
tab)](https://web.archive.org/web/20161127154654/https://www.ethereum.org/)

#### Summary

The Spurious Dragon fork was the second response to the denial of service
(DoS) attacks on the network (September/October 2016) including:

  * tuning opcode pricing to prevent future attacks on the network.
  * enabling “debloat” of the blockchain state.
  * adding replay attack protection.

[Read the Ethereum Foundation announcement(opens in a new
tab)](https://blog.ethereum.org/2016/11/18/hard-fork-no-4-spurious-dragon/)

###

Spurious Dragon EIPs

Official improvements included in this fork.

More

  * [EIP-155(opens in a new tab)](https://eips.ethereum.org/EIPS/eip-155) – _prevents transactions from one Ethereum chain from being rebroadcasted on an alternative chain, for example a testnet transaction being replayed on the main Ethereum chain._
  * [EIP-160(opens in a new tab)](https://eips.ethereum.org/EIPS/eip-160) – _adjusts prices of`EXP` opcode – makes it more difficult to slow down the network via computationally expensive contract operations._
  * [EIP-161(opens in a new tab)](https://eips.ethereum.org/EIPS/eip-161) – _allows for removal of empty accounts added via the DOS attacks._
  * [EIP-170(opens in a new tab)](https://eips.ethereum.org/EIPS/eip-170) – _changes the maximum code size that a contract on the blockchain can have – to 24576 bytes._

* * *

### Tangerine whistle

![📆](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4c6.svg)

Oct 18, 2016, 1:19:31 AM +UTC

![🧱](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f9f1.svg)Block
number: [2,463,000(opens in a new tab)](https://etherscan.io/block/2463000)

![💰](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4b0.svg)ETH
price: $12.50

![🖥️](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f5a5.svg)[ethereum.org
on waybackmachine(opens in a new
tab)](https://web.archive.org/web/20161030043727/https://www.ethereum.org/)

#### Summary

The Tangerine Whistle fork was the first response to the denial of service
(DoS) attacks on the network (September/October 2016) including:

  * addressing urgent network health issues concerning underpriced operation codes.

[Read the Ethereum Foundation announcement(opens in a new
tab)](https://blog.ethereum.org/2016/10/18/faq-upcoming-ethereum-hard-fork/)

###

Tangerine Whistle EIPs

Official improvements included in this fork.

More

  * [EIP-150(opens in a new tab)](https://eips.ethereum.org/EIPS/eip-150) – _increases gas costs of opcodes that can be used in spam attacks._
  * [EIP-158(opens in a new tab)](https://eips.ethereum.org/EIPS/eip-158) – _reduces state size by removing a large number of empty accounts that were put in the state at very low cost due to flaws in earlier versions of the Ethereum protocol._

* * *

### DAO fork

![📆](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4c6.svg)

Jul 20, 2016, 1:20:40 AM +UTC

![🧱](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f9f1.svg)Block
number: [1,920,000(opens in a new tab)](https://etherscan.io/block/1920000)

![💰](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4b0.svg)ETH
price: $12.54

![🖥️](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f5a5.svg)[ethereum.org
on waybackmachine(opens in a new
tab)](https://web.archive.org/web/20160803215306/https://ethereum.org/)

#### Summary

The DAO fork was in response to the [2016 DAO attack(opens in a new
tab)](https://www.coindesk.com/learn/understanding-the-dao-attack/) where an
insecure _DAO_ contract was drained of over 3.6 million ETH in a hack. The
fork moved the funds from the faulty contract to a [new contract(opens in a
new
tab)](https://etherscan.io/address/0xbf4ed7b27f1d666546e30d74d50d173d20bca754)
with a single function: withdraw. Anyone who lost funds could withdraw 1 ETH
for every 100 DAO tokens in their wallets.

This course of action was voted on by the Ethereum community. Any ETH holder
was able to vote via a transaction on [a voting platform(opens in a new
tab)](https://web.archive.org/web/20170620030820/http://v1.carbonvote.com/).
The decision to fork reached over 85% of the votes.

Some miners refused to fork because the DAO incident wasn't a defect in the
protocol. They went on to form [Ethereum Classic(opens in a new
tab)](https://ethereumclassic.org/).

[Read the Ethereum Foundation announcement(opens in a new
tab)](https://blog.ethereum.org/2016/07/20/hard-fork-completed/)

* * *

### Homestead

![📆](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4c6.svg)

Mar 14, 2016, 6:49:53 AM +UTC

![🧱](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f9f1.svg)Block
number: [1,150,000(opens in a new tab)](https://etherscan.io/block/1150000)

![💰](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4b0.svg)ETH
price: $12.50

![🖥️](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f5a5.svg)[ethereum.org
on waybackmachine(opens in a new
tab)](https://web.archive.org/web/20160313203843/https://www.ethereum.org/)

#### Summary

The Homestead fork that looked to the future. It included several protocol
changes and a networking change that gave Ethereum the ability to do further
network upgrades.

[Read the Ethereum Foundation announcement(opens in a new
tab)](https://blog.ethereum.org/2016/02/29/homestead-release/)

###

Homestead EIPs

Official improvements included in this fork.

More

  * [EIP-2(opens in a new tab)](https://eips.ethereum.org/EIPS/eip-2) – _makes edits to contract creation process._
  * [EIP-7(opens in a new tab)](https://eips.ethereum.org/EIPS/eip-7) – _adds new opcode:`DELEGATECALL`_
  * [EIP-8(opens in a new tab)](https://eips.ethereum.org/EIPS/eip-8) – _introduces devp2p forward compatibility requirements_

## 2015

### Frontier thawing

![📆](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4c6.svg)

Sep 7, 2015, 9:33:09 AM +UTC

![🧱](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f9f1.svg)Block
number: [200,000(opens in a new tab)](https://etherscan.io/block/200000)

![💰](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4b0.svg)ETH
price: $1.24

![🖥️](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f5a5.svg)[ethereum.org
on waybackmachine(opens in a new
tab)](https://web.archive.org/web/20150912193811/https://www.ethereum.org/)

#### Summary

The frontier thawing fork lifted the 5,000 _gas_ limit per _block_ and set the
default gas price to 51 _gwei_. This allowed for transactions – transactions
require 21,000 gas. The _difficulty bomb_ was introduced to ensure a future
hard-fork to _proof-of-stake_.

  * [Read the Ethereum Foundation announcement(opens in a new tab)](https://blog.ethereum.org/2015/08/04/the-thawing-frontier/)
  * [Read the Ethereum Protocol Update 1(opens in a new tab)](https://blog.ethereum.org/2015/08/04/ethereum-protocol-update-1/)

* * *

### Frontier

![📆](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4c6.svg)

Jul 30, 2015, 3:26:13 AM +UTC

![🖥️](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f5a5.svg)[ethereum.org
on waybackmachine(opens in a new
tab)](https://web.archive.org/web/20150802035735/https://www.ethereum.org/)

#### Summary

Frontier was a live, but barebone implementation of the Ethereum project. It
followed the successful Olympic testing phase. It was intended for technical
users, specifically developers. _Blocks_ had a _gas_ limit of 5,000. This
‘thawing’ period enabled miners to start their operations and for early
adopters to install their clients without having to ‘rush’.

[Read the Ethereum Foundation announcement(opens in a new
tab)](https://blog.ethereum.org/2015/07/22/frontier-is-coming-what-to-expect-
and-how-to-prepare/)

## 2014

### Ether sale

![📆](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4c6.svg)

Jul 22, 2014, 12:00:00 AM +UTC

![🖥️](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f5a5.svg)[ethereum.org
on waybackmachine(opens in a new
tab)](https://web.archive.org/web/20140804235628/https://www.ethereum.org/)

Ether officially went on sale for 42 days. You could buy it with BTC.

[Read the Ethereum Foundation announcement(opens in a new
tab)](https://blog.ethereum.org/2014/07/22/launching-the-ether-sale/)

* * *

### Yellowpaper released

![📆](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4c6.svg)

Apr 1, 2014, 12:00:00 AM +UTC

![🖥️](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f5a5.svg)[ethereum.org
on waybackmachine(opens in a new
tab)](https://web.archive.org/web/20140509173418/https://www.ethereum.org/)

The Yellow Paper, authored by Dr. Gavin Wood, is a technical definition of the
Ethereum protocol.

[View the Yellow Paper(opens in a new
tab)](https://github.com/ethereum/yellowpaper)

## 2013

### Whitepaper released

![📆](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4c6.svg)

Nov 27, 2013, 12:00:00 AM +UTC

![🖥️](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f5a5.svg)[ethereum.org
on waybackmachine(opens in a new
tab)](https://web.archive.org/web/20140208030136/http://www.ethereum.org/)

The introductory paper, published in 2013 by Vitalik Buterin, the founder of
Ethereum, before the project's launch in 2015.

![📃](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4c3.svg)

[Whitepaper](/en/whitepaper/)

### Was this article helpful?

YesNo

  * [Edit page(opens in a new tab)](https://github.com/ethereum/ethereum-org-website/tree/dev/public/content/history/index.md)
  * On this page

    * 2024
      * Cancun-Deneb ("Dencun")
    * 2023
      * Shanghai-Capella ("Shapella")
    * 2022
      * Paris (The Merge)
      * Bellatrix
      * Gray Glacier
    * 2021
      * Arrow Glacier
      * Altair
      * London
      * Berlin
    * 2020
      * Beacon Chain genesis
      * Staking deposit contract deployed
      * Muir Glacier
    * 2019
      * Istanbul
      * Constantinople
    * 2017
      * Byzantium
    * 2016
      * Spurious Dragon
      * Tangerine whistle
      * DAO fork
      * Homestead
    * 2015
      * Frontier thawing
      * Frontier
    * 2014
      * Ether sale
      * Yellowpaper released
    * 2013
      * Whitepaper released

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

### Execution layer

Ethereum's execution layer is the network of [execution
clients](/en/glossary/#execution-client).

### Consensus layer

Ethereum's consensus layer is the network of [consensus
clients](/en/glossary/#consensus-client).

### beacon-chain-term

beacon-chain-definition

### Terminal total difficulty (TTD)

The total difficulty is the sum of the Ethash mining difficulty for all blocks
up to some specific point in the blockchain. The terminal total difficulty is
a specific value for the total difficulty that was used as the trigger for
execution clients to switch off their mining and block gossip functions
enabling the network to transition to proof-of-stake. It is no longer relevant
because Ethereum moved to [proof-of-stake](/en/glossary/#pos).

### Terminal total difficulty (TTD)

The total difficulty is the sum of the Ethash mining difficulty for all blocks
up to some specific point in the blockchain. The terminal total difficulty is
a specific value for the total difficulty that was used as the trigger for
execution clients to switch off their mining and block gossip functions
enabling the network to transition to proof-of-stake. It is no longer relevant
because Ethereum moved to [proof-of-stake](/en/glossary/#pos).

### Difficulty bomb

Planned exponential increase in [proof-of-work](/en/glossary/#pow)
[difficulty](/en/glossary/#difficulty) setting that was designed to motivate
the transition to [proof-of-stake](/en/glossary/#pos), reducing the chances of
a [fork](/en/glossary/#hard-fork). The difficulty bomb was deprecated with
[the Merge](/en/roadmap/merge/).

### Difficulty bomb

Planned exponential increase in [proof-of-work](/en/glossary/#pow)
[difficulty](/en/glossary/#difficulty) setting that was designed to motivate
the transition to [proof-of-stake](/en/glossary/#pos), reducing the chances of
a [fork](/en/glossary/#hard-fork). The difficulty bomb was deprecated with
[the Merge](/en/roadmap/merge/).

### ice-age-term

ice-age-definition

### Staking

Depositing a quantity of [ether](/en/glossary/#ether) (your stake) to become a
validator and secure the [network](/en/glossary/#network). A validator checks
[transactions](/en/glossary/#transaction) and proposes
[blocks](/en/glossary/#block) under a [proof-of-stake](/en/glossary/#pos)
consensus model. Staking gives you an economic incentive to act in the best
interests of the network. You'll get rewards for carrying out your
[validator](/en/glossary/#validator) duties, but lose varying amounts of ETH
if you don't. [More on Ethereum staking](/en/staking/).

### Mainnet

Short for "main network," this is the main public Ethereum
[blockchain](/en/glossary/#blockchain).

### Difficulty bomb

Planned exponential increase in [proof-of-work](/en/glossary/#pow)
[difficulty](/en/glossary/#difficulty) setting that was designed to motivate
the transition to [proof-of-stake](/en/glossary/#pos), reducing the chances of
a [fork](/en/glossary/#hard-fork). The difficulty bomb was deprecated with
[the Merge](/en/roadmap/merge/).

### Gas

Gas is the fee paid for transactions and smart contracts on a blockchain, like
Ethereum. [More on gas and fees](/en/gas/).

### Gas

Gas is the fee paid for transactions and smart contracts on a blockchain, like
Ethereum. [More on gas and fees](/en/gas/).

### Gas

Gas is the fee paid for transactions and smart contracts on a blockchain, like
Ethereum. [More on gas and fees](/en/gas/).

### Difficulty bomb

Planned exponential increase in [proof-of-work](/en/glossary/#pow)
[difficulty](/en/glossary/#difficulty) setting that was designed to motivate
the transition to [proof-of-stake](/en/glossary/#pos), reducing the chances of
a [fork](/en/glossary/#hard-fork). The difficulty bomb was deprecated with
[the Merge](/en/roadmap/merge/).

### Difficulty bomb

Planned exponential increase in [proof-of-work](/en/glossary/#pow)
[difficulty](/en/glossary/#difficulty) setting that was designed to motivate
the transition to [proof-of-stake](/en/glossary/#pos), reducing the chances of
a [fork](/en/glossary/#hard-fork). The difficulty bomb was deprecated with
[the Merge](/en/roadmap/merge/).

### Decentralized autonomous organization (DAO)

A DAO is a digital organization run by rules coded on a blockchain, where
decisions are made by member votes, not a central authority. [More on
decentralized autonomous organizations (DAOs)](/en/dao/).

### Gas

Gas is the fee paid for transactions and smart contracts on a blockchain, like
Ethereum. [More on gas and fees](/en/gas/).

### Block

A block is where transactions or digital actions are stored. Once a block is
full, it gets linked to the previous one, creating a chain of blocks or a
"blockchain". [More on blocks](/en/developers/docs/blocks/).

### Gwei

Short for gigawei, a denomination of [ether](/en/glossary/#ether), commonly
utilized to price [gas](/en/glossary/#gas). 1 gwei = 109
[wei](/en/glossary/#wei). 109 gwei = 1 ether.

### Difficulty bomb

Planned exponential increase in [proof-of-work](/en/glossary/#pow)
[difficulty](/en/glossary/#difficulty) setting that was designed to motivate
the transition to [proof-of-stake](/en/glossary/#pos), reducing the chances of
a [fork](/en/glossary/#hard-fork). The difficulty bomb was deprecated with
[the Merge](/en/roadmap/merge/).

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

### Gas

Gas is the fee paid for transactions and smart contracts on a blockchain, like
Ethereum. [More on gas and fees](/en/gas/).

