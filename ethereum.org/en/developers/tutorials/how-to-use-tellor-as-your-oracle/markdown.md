Skip to main content

[](/en/)

  * Learn
  * Use
  * Build
  * Participate
  * Research

Search```K`

Languages EN

# How to Set Up Tellor as your Oracle

soliditysmart contractsoracles

Beginner

![✍️](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/270d.svg)Tellor

![📚](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4da.svg)[Tellor
Docs(opens in a new tab)](https://docs.tellor.io/tellor/)

![📆](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4c6.svg)
June 29, 2021

![⏱️](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/23f1.svg)2
minute read minute read

On this page

  * (Soft) Prerequisites
  * Overview
  * UsingTellor
    * BTC/USD Example

Pop Quiz: Your protocol is just about finished, but it needs an oracle to get
access to off chain data...What do you do?

## (Soft) Prerequisites

This post aims to make accessing an oracle feed as simple and straightforward
as possible. That said, we're assuming the following about your coding skill-
level to focus on the oracle aspect.

Assumptions:

  * you can navigate a terminal
  * you have npm installed
  * you know how to use npm to manage dependencies

Tellor is a live and open-sourced oracle ready for implementation. This
beginner's guide is here to showcase the ease with which one can get up and
running with Tellor, providing your project with a fully decentralized and
censorship-resistant oracle.

## Overview

Tellor is an oracle system where parties can request the value of an offchain
data point (e.g. BTC/USD) and reporters compete to add this value to an
onchain data-bank, accessible by all Ethereum smart contracts. The inputs to
this data-bank are secured by a network of staked reporters. Tellor utilizes
crypto-economic incentive mechanisms, rewarding honest data submissions by
reporters and punishing bad actors through the issuance of Tellor’s token,
Tributes (TRB), and a dispute mechanism.

In this tutorial we'll go over:

  * Setting up the initial toolkit you'll need to get up and running.
  * Walk through a simple example.
  * List out testnet addresses of networks you currently can test Tellor on.

## UsingTellor

The first thing you'll want to do is install the basic tools necessary for
using Tellor as your oracle. Use [this package(opens in a new
tab)](https://github.com/tellor-io/usingtellor) to install the Tellor User
Contracts:

`npm install usingtellor`

Once installed this will allow your contracts to inherit the functions from
the contract 'UsingTellor'.

Great! Now that you've got the tools ready, let's go through a simple exercise
where we retrieve the bitcoin price:

### BTC/USD Example

Inherit the UsingTellor contract, passing the Tellor address as a constructor
argument:

Here's an example:

    
    
    1import "usingtellor/contracts/UsingTellor.sol";
    
    2
    
    3contract PriceContract is UsingTellor {
    
    4  uint256 public btcPrice;
    
    5
    
    6 //This Contract now has access to all functions in UsingTellor
    
    7
    
    8constructor(address payable _tellorAddress) UsingTellor(_tellorAddress) public {}
    
    9
    
    10function setBtcPrice() public {
    
    11    bytes memory _b = abi.encode("SpotPrice",abi.encode("btc","usd"));
    
    12    bytes32 _queryId = keccak256(_b);
    
    13
    
    14    uint256 _timestamp;
    
    15    bytes _value;
    
    16
    
    17    (_value, _timestamp) = getDataBefore(_queryId, block.timestamp - 15 minutes);
    
    18
    
    19    btcPrice = abi.decode(_value,(uint256));
    
    20  }
    
    21}
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

For a complete list of contract addresses refer [here(opens in a new
tab)](https://docs.tellor.io/tellor/the-basics/contracts-reference).

For ease of use, the UsingTellor repo comes with a version of the [Tellor
Playground(opens in a new tab)](https://github.com/tellor-io/TellorPlayground)
contract for easier integration. See [here(opens in a new
tab)](https://github.com/tellor-io/sampleUsingTellor#tellor-playground) for a
list of helpful functions.

For a more robust implementation of the Tellor oracle, check out the full list
of available functions [here(opens in a new tab)](https://github.com/tellor-
io/usingtellor/blob/master/README.md).

n

Last edit: [@nhsz(opens in a new tab)](https://github.com/nhsz), August 15,
2023

See contributors

### Was this tutorial helpful?

YesNo

  * [Edit page(opens in a new tab)](https://github.com/ethereum/ethereum-org-website/tree/dev/public/content/developers/tutorials/how-to-use-tellor-as-your-oracle/index.md)
  * On this page

    * (Soft) Prerequisites
    * Overview
    * UsingTellor
      * BTC/USD Example

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

