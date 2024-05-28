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
  3. [Proposer-builder separation](/en/roadmap/pbs/)

Page last updated: February 13, 2024

On this page

  * PBS and censorship resistance
  * PBS and MEV
  * PBS and Danksharding
  * Current progress
  * Further Reading

# Proposer-builder separation

Present-day Ethereum validators create _and_ broadcast blocks. They bundle
together transactions that they have heard about through the gossip network
and package them into a block that is sent out to peers on the Ethereum
network. **Proposer-builder separation (PBS)** splits these tasks across
multiple validators. Block builders become responsible for creating blocks and
offering them to the block proposer in each slot. The block proposer cannot
see the contents of the block, they simply choose the most profitable one,
paying a fee to the block builder before sending the block to its peers.

This is an important upgrade for several reasons. First, it creates
opportunities to prevent transaction censorship at the protocol level. Second,
it prevents hobbyist validators from being out-competed by institutional
players that can better optimize the profitability of their block building.
Third, it helps with scaling Ethereum by enabling the Danksharding upgrades.

## PBS and censorship resistance

Separating out block builders and block proposers makes it much harder for
block builders to censor transactions. This is because relatively complex
inclusion criteria can be added that ensure no censorship has taken place
before the block is proposed. As the block proposer is a separate entity from
the block builder, it can take on the role of protector against censoring
block builders.

For example, inclusion lists can be introduced so that when validators know
about transactions but don't see them included in blocks, they can impose them
as must-haves in the next block. The inclusion list is generated from the
block proposers local mempool (the list of transactions it is aware of) and
sent to their peers just before a block is proposed. If any of the
transactions from the inclusion list are missing, the proposer could either
reject the block, add the missing transactions before proposing it, or propose
it and let it get rejected by other validators when they receive it. There is
also a potentially more efficient version of this idea that asserts that
builders must fully utilize the available block space and if they don't
transactions are added from the proposer's inclusion list. This is still an
area of active research and the optimal configuration for the inclusion lists
has not yet been determined.

[Encrypted mempools(opens in a new
tab)](https://www.youtube.com/watch?v=fHDjgFcha0M&list=PLpktWkixc1gUqkyc1-iE6TT0RWQTBJELe&index=3)
could also make it impossible for builders and proposers to know which
transactions they are including in a block until after the block was already
broadcast.

###

What kinds of censorship does PBS solve?

More

Powerful organizations can pressure validators to censor transactions to or
from certain addresses. Validators comply with this pressure by detecting
blacklisted addresses in their transaction pool and omitting them from the
blocks they propose. After PBS this will no longer be possible because block
proposers will not know which transactions they are broadcasting in their
blocks. It might be important for certain individuals or apps to comply with
censorship rules, for example when it is made law in their region. In these
cases, compliance happens at the application level, while the protocol remains
permissionless and censorship free.

## PBS and MEV

**Maximum extractable value (MEV)** refers to validators maximizing their
profitability by favorably ordering transactions. Common examples include
arbitraging swaps on decentralized exchanges (e.g. frontrunning a large sale
or purchase) or identifying opportunities to liquidate DeFi positions.
Maximizing MEV requires sophisticated technical know-how and custom software
appended to normal validators, making it much more likely that institutional
operators outperform individuals and hobbyist validators at MEV extraction.
This means staking returns are likely to be higher with centralized operators,
creating a centralizing force that disincentivizes home staking.

PBS solves this problem by reconfiguring the economics of MEV. Instead of the
block proposer doing their own MEV searching, they simply pick a block from
many offered to them by block builders. The block builders might have done
sophisticated MEV extraction, but the reward for it goes to the block
proposer. This means that even if a small pool of specialized block builders
dominate MEV extraction, the reward for it could go to any validator on the
network, including individual home stakers.

###

Why is it OK to centralize block building?

More

Individuals could be incentivized to stake with pools rather than on their own
due to the enhanced rewards offered by sophisticated MEV strategies.
Separating the block building from the block proposal means that the MEV
extracted will be distributed over more validators rather than centralizing
with the most effective MEV searcher. At the same time, allowing specialized
block builders to exist takes the burden of block building away from
individuals, and also prevents individuals from stealing MEV for themselves,
while maximizing the number of individual, independent validators that can
check the blocks are honest. The important concept is "prover-verifier
asymmetry" which refers to the idea that centralized block production is fine
as long as there is a robust and maximally decentralized network of validators
able to prove the blocks are honest. Decentralization is a means, not an end
goal - what we want are honest blocks.

## PBS and Danksharding

Danksharding is the way Ethereum will scale to >100,000 transactions per
second and minimize fees for rollup users. It relies upon PBS because it adds
to the workload for block builders, who will have to compute proofs for up to
64 MB of rollup data in less than 1 second. This will probably require
specialized builders that can dedicate fairly substantial hardware to the
task. However, in the current situation block building could become
increasingly centralized around more sophisticated and powerful operators
anyway due to MEV extraction. Proposer-builder separation is a way to embrace
this reality and prevent it from exerting centralizing force on block
validation (the important part) or the distribution of staking rewards. A
great side-benefit is that the specialized block builders are also willing and
able to compute the necessary data proofs for Danksharding.

## Current progress

PBS is in an advanced stage of research, but there are still some important
design questions that need to be resolved before it can be prototyped in
Ethereum clients. There is no finalized specification yet. This means PBS is
likely a year away or more. Check the latest [state of the research(opens in a
new tab)](https://notes.ethereum.org/@vbuterin/pbs_censorship_resistance).

## Further Reading

  * [State of research: censorship resistance under PBS(opens in a new tab)](https://notes.ethereum.org/@vbuterin/pbs_censorship_resistance)
  * [PBS-friendly fee market designs(opens in a new tab)](https://ethresear.ch/t/proposer-block-builder-separation-friendly-fee-market-designs/9725)
  * [PBS and censorship resistance(opens in a new tab)](https://notes.ethereum.org/@fradamt/H1TsYRfJc#Secondary-auctions)
  * [Inclusion lists(opens in a new tab)](https://notes.ethereum.org/@fradamt/H1ZqdtrBF)

### Was this article helpful?

YesNo

  * [Edit page(opens in a new tab)](https://github.com/ethereum/ethereum-org-website/tree/dev/public/content/roadmap/pbs/index.md)
  * On this page

    * PBS and censorship resistance
    * PBS and MEV
    * PBS and Danksharding
    * Current progress
    * Further Reading

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

