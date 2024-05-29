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
  3. [Scaling](/en/roadmap/scaling/)

# Scaling Ethereum

Rollups batch transactions together off-chain, reducing costs for the user.
However, the way rollups currently use data is too expensive, limiting how
cheap transactions can be. Proto-Danksharding fixes this.

On this page

  * Making data cheaper
    * Proto-Danksharding
    * Danksharding
  * Decentralizing rollups
  * Current progress

![Ethereum roadmap](/_next/image/?url=%2Froadmap%2Froadmap-
transactions.png&w=1920&q=75)

Roadmap Options

[Roadmap home](/en/roadmap/)[Better
security](/en/roadmap/security/)[Scaling](/en/roadmap/scaling/)[Better user
experience](/en/roadmap/user-experience/)[Future-proofing](/en/roadmap/future-
proofing/)

## On this page

  * Making data cheaper
  * Decentralizing rollups
  * Current progress

Ethereum is scaled using [layer 2s](/en/layer-2/#rollups) (also known as
rollups), which batch transactions together and send the output to Ethereum.
Even though rollups are up to eight times less expensive than Ethereum
Mainnet, it's possible to optimize rollups further to reduce costs for end
users. Rollups also rely on some centralized components that developers can
remove as the rollups mature.

Transaction costs

  * Today’s rollups are **~5-20x** cheaper than Ethereum layer 1
  * ZK-rollups will soon lower fees by **~40-100x**
  * Upcoming changes to Ethereum will provide another **~100-1000x** of scaling
  * Users should benefit from transactions **costing less than $0.001**

## Making data cheaper

Rollups collect large numbers of transactions, execute them and submit the
results to Ethereum. This generates a lot of data that needs to be openly
available so that anyone can execute the transactions for themselves and
verify that the rollup operator was honest. If someone finds a discrepancy,
they can raise a challenge.

### Proto-Danksharding

Rollup data has historically been stored on Ethereum permanently, which is
expensive. Over 90% of the transaction cost users pay on rollups is due to
this data storage. To reduce transaction costs, we can move the data into a
new temporary 'blob' storage. Blobs are cheaper because they are not
permanent; they get deleted from Ethereum once they are no longer needed.
Storing rollup data long-term becomes the responsibility of the people that
need it, such as rollup operators, exchanges, indexing services etc. Adding
blob transactions to Ethereum is part of an upgrade known as "Proto-
Danksharding".

With Proto-Danksharding, it is possible to add many blobs to Ethereum blocks.
This enables another substantial (>100x) scale-up to Ethereum’s throughput and
scale-down to transaction costs.

### Danksharding

The second stage of expanding blob data is complicated because it requires new
methods for checking rollup data is available on the network and relies on
_validators_ separating their _block_ building and block proposal
responsibilities. It also requires a way to cryptographically prove that
validators have verified small subsets of the blob data.

This second step is known as [“Danksharding”](/en/roadmap/danksharding/). **It
is likely several years away** from being fully implemented. Danksharding
relies on other developments such as [separating block building and block
proposal](/en/roadmap/pbs/) and new network designs that enable the network to
efficiently confirm that data is available by randomly sampling a few
kilobytes at a time, known as [data availability sampling
(DAS)](/en/developers/docs/data-availability/).

[More on Danksharding](/en/roadmap/danksharding/)

## Decentralizing rollups

[Rollups](/en/layer-2/) are already scaling Ethereum. A [rich ecosystem of
rollup projects(opens in a new tab)](https://l2beat.com/scaling/tvl) is
enabling users to transact quickly and cheaply, with a range of security
guarantees. However, rollups have been bootstrapped using centralized
sequencers (computers that do all the transaction processing and aggregation
before submitting them to Ethereum). This is vulnerable to censorship, because
the sequencer operators can be sanctioned, bribed or otherwise compromised. At
the same time, [rollups vary(opens in a new tab)](https://l2beat.com) in the
way they validate incoming data. The best way is for "provers" to submit
_fraud proofs_ or validity proofs, but not all rollups are there yet. Even
those rollups that do use validity/fraud proofs use a small pool of known
provers. Therefore, the next critical step in scaling Ethereum is to
distribute responsibility for running sequencers and provers across more
people.

[More on rollups](/en/developers/docs/scaling/)

## Current progress

Proto-Danksharding is the first of these roadmap items to be implemented as
part of the Cancun-Deneb ("Dencun") network upgrade in March of 2024. **Full
Danksharding is likely several years away** , as it relies upon several other
roadmap items being completed first. Decentralizing rollup infrastructure is
likely to be a gradual process - there are many different rollups that are
building slightly different systems and will fully decentralize at different
rates.

[More on the Dencun network upgrade](/en/roadmap/dencun/)

## Test your Ethereum knowledge

Scaling

Question number 1:Which of the following is Ethereum using to scale?

A

Layer 2 rollups

B

Proto-Danksharding

C

Danksharding

D

All of the above

Check answer

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

### Validator

A [node](/en/glossary/#node) in a [proof-of-stake](/en/glossary/#pos) system
responsible for storing data, processing transactions, and adding new blocks
to the blockchain. To activate validator software, you need to be able to
[stake](/en/glossary/#staking) 32 ETH. [More on staking in
Ethereum](/en/staking/).

### Block

A block is where transactions or digital actions are stored. Once a block is
full, it gets linked to the previous one, creating a chain of blocks or a
"blockchain". [More on blocks](/en/developers/docs/blocks/).

### Fraud proof

A security model for certain [layer 2](/en/glossary/#layer-2) solutions where,
to increase speed, transactions are [rolled up](/en/glossary/#rollups) into
batches and submitted to Ethereum in a single transaction. Other network
participants can re-execute the transactions to check that they were executed
honestly. If they uncover a discrepancy between the posted data and their own
version they can post a cryptographic proof that demonstrates where some fraud
took place. Some [rollups](/en/glossary/#rollups) use [validity
proofs](/en/glossary/#validity-proof).

