Skip to main content

[](/en/)

  * Learn
  * Use
  * Build
  * Participate
  * Research

Search```K`

Languages EN

# Gas fees

## Network fees

Network fees on Ethereum are called gas.  
Gas is the fuel that powers Ethereum.

  * What is gas?

![Hero header
image](/_next/image/?url=%2F_next%2Fstatic%2Fmedia%2Finfrastructure_transparent.8849e91b.png&w=1920&q=75)

Summary

  * Every transaction on Ethereum requires a small form of payment to process
  * These fees are known as ‘gas’ fee
  * Gas fees are not set, they change based on network congestion

## What are gas fees?

Think of Ethereum as a large computer network where people can do tasks like
sending messages or running programs. Just like in the real world, these tasks
require energy to get done.

In Ethereum, each computational action has a set "gas" price. **Your gas fees
are the total cost of the actions in your transaction**. When you send a
transaction or run a _smart contract_ , you pay in gas fees to process it.

![A
robot](/_next/image/?url=%2F_next%2Fstatic%2Fmedia%2Fwallet.454231ba.png&w=1920&q=75)

## How do I pay less gas?

While higher fees on Ethereum are sometimes inevitable, there are strategies
you can use to reduce the cost:

### Time your transactions

Just like travelling off-peak is less crowded and more affordable, Ethereum is
generally cheaper to use when North America is asleep.

### Wait for gas to go down

Gas prices go up and down every twelve seconds based on how congested Ethereum
is. When gas prices are high, waiting just a few minutes before making a
transaction could see a significant drop in what you pay.

### Use layer 2

Layer-2 chains are built atop Ethereum, offering lower fees and handling more
transactions. They're a good choice to save on fees for transactions that
don't need to happen on the main Ethereum network.

[Try layer 2](/en/layer-2/)

### What causes high gas fees?

Whenever the amount of computation (gas) on Ethereum exceeds a certain
threshold, gas fees begin to rise. The more the gas exceeds this threshold,
the quicker gas fees increase.

Higher fees could be caused by things like popular _decentralized apps
(dapps)_ or NFTs, periodically increased trading on _DEXs_ , or an
overwhelming number of user activity at peak times.

Developers on Ethereum should take care to optimise their smart contracts
usage before deploying. If lots of people are using a poorly written smart
contract, it will consume more gas and could inadvertently cause network
congestion.

Want to dive deeper? [Check out the developer docs.](/en/developers/docs/gas/)

### Attack of the Cryptokitties

In November 2017, the popular CryptoKitties project was launched. Its rapid
spike in popularity caused significant network congestion and extremely high
gas fees. The challenges posed by CryptoKitties accelerated the urgency of
finding solutions for scaling Ethereum.

## Why do we need gas?

Gas is a critical element in keeping Ethereum secure and processing
transactions. Gas helps in many ways:

Gas keeps Ethereum _sybil-resistant_ by preventing malicious actors from
overwhelming the network with fraudulent activities.

Because computation costs gas, spamming Ethereum with expensive transactions,
either accidentally and maliciously, is financially disincentivized.

A hard-limit on the amount of computation that can be done at any one time
prevents Ethereum from being overwhelmed, helping to ensure the network is
always accessible.

![](/_next/image/?url=%2F_next%2Fstatic%2Fmedia%2Feth.28aff33d.png&w=1200&q=75)

## How is gas calculated?

Advanced

The total gas fee you pay is made up of a few parts:

  * **Base fee:** a fee set by the network that has to be paid for a transaction
  * **Priority fee:** an optional tip to incentivise node operators to include your transaction
  * **Units of gas used _*_ :** remember we said gas represented computation? More complex actions, like interacting with a smart contract, use more gas than simple ones, such as sending a transaction.
    * _* See Figure 1 to see how much gas different types of transactions use_

The formula for calculating a gas fee is units of gas used * (base fee +
priority fee). Most wallets will calculate gas usage and display it in a more
straight-forward way.

_Figure 1: Gas used by transaction type_ Transaction type| Units of gas used  
---|---  
Sending ETH| 21,000  
Sending ERC-20 tokens| 65,000  
Transferring an NFT| 84,904  
Swapping on Uniswap| 184,523  
  
## Frequently asked questions

###

Who gets paid the gas fee in my transaction?

More

The majority of the gas fee—the base fee— is destroyed by the protocol
(burned). The priority fee, if included in your transaction, will be given to
the validator who proposed your transaction.

You can read a detailed description of the process in [the gas developer
docs.](/en/developers/docs/gas/)

###

Do I need to pay gas in ETH?

More

Yes. All gas fees on Ethereum must be paid in the native ETH currency.

[More on ETH](/eth/)

###

What is gwei?

More

In most wallets or gas trackers, you will see gas prices denominated as
‘gwei’.

Gwei is just a smaller unit of ETH, just as pennies are to dollars, with the
difference being that 1 ETH equals 1 billion gwei. Gwei is useful when talking
about very small amounts of ETH.

![](/_next/image/?url=%2F_next%2Fstatic%2Fmedia%2Fwhat-is-
ethereum.b37ce60e.png&w=640&q=75)

### Use layer 2

Layer-2 chains are built atop Ethereum, offering lower fees and handling more
transactions. They're a good choice to save on fees for transactions that
don't need to happen on the main Ethereum network.

[Use layer 2](/en/layer-2/)

![Explore dapps](/_next/image/?url=%2F_next%2Fstatic%2Fmedia%2Fdoge-
computer.482265f8.png&w=640&q=75)

### Try some dapps

Dapps are applications built on Ethereum. Dapps are disrupting current
business models and inventing new ones.

[Explore dapps](/en/dapps/)

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

### Smart contract

A smart contract is a program that automatically executes agreements on a
blockchain, like a self-enforcing digital contract. [Introduction to smart
contracts](/en/smart-contracts/).

### Dapp

A dApp is a decentralized application that runs on a blockchain network,
offering services without a central controlling authority. [More on
decentralized applications](/en/dapps/).

### Decentralized exchange (DEX)

A type of Ethereum app that lets you swap tokens with peers on the network.
DEXes are not subject to geographical restrictions like centralized exchanges
– anyone can participate.

### Anti-Sybil

Are ways to stop people from pretending to be many users at once on the
internet, ensuring each user is a real, separate person. This helps keep
online interactions fair and honest.

