Skip to main content

[](/en/)

  * Learn
  * Use
  * Build
  * Participate
  * Research

Search```K`

Languages EN

# Set up web3.js to use the Ethereum blockchain in JavaScript

web3.jsjavascript

Beginner

![✍️](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/270d.svg)jdourlens

![📚](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4da.svg)[EthereumDev(opens
in a new tab)](https://ethereumdev.io/setup-web3js-to-use-the-ethereum-
blockchain-in-javascript/)

![📆](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4c6.svg)
April 11, 2020

![⏱️](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/23f1.svg)3
minute read minute read

comp-tutorial-metadata-tip-author 0x19dE91Af973F404EDF5B4c093983a7c6E3EC8ccE

On this page

In this tutorial, we’ll see how to get started with [web3.js(opens in a new
tab)](https://web3js.readthedocs.io/) to interact with the Ethereum
blockchain. Web3.js can be used both in frontends and backends to read data
from the blockchain or make transactions and even deploy smart contracts.

The first step is to include web3.js in your project. To use it in a web page,
you can import the library directly using a CDN like JSDeliver.

    
    
    1<script src="https://cdn.jsdelivr.net/npm/web3@latest/dist/web3.min.js"></script>

If you prefer installing the library to use in your backend or a frontend
project that uses build you can install it using npm:

    
    
    npm install web3 --save

Then to import Web3.js into a Node.js script or Browserify frontend project,
you can use the following line of JavaScript:

    
    
    1const Web3 = require("web3")
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Now that we included the library in the project we need to initialize it. Your
project needs to be able to communicate with the blockchain. Most Ethereum
libraries communicate with a [node](/en/developers/docs/nodes-and-clients/)
through RPC calls. To initiate our Web3 provider, we’ll instantiate a Web3
instance passing as the constructor the URL of the provider. If you have a
node or [ganache instance running on your computer(opens in a new
tab)](https://ethereumdev.io/testing-your-smart-contract-with-existing-
protocols-ganache-fork/) it will look like this:

    
    
    1const web3 = new Web3("http://localhost:8545")
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

If you’d like to directly access a hosted node you can find options on [nodes
as a service](/en/developers/docs/nodes-and-clients/nodes-as-a-service/).

    
    
    1const web3 = new Web3("https://cloudflare-eth.com")
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

To test that we correctly configured our Web3 instance, we’ll try to retrieve
the latest block number using the `getBlockNumber` function. This function
accepts a callback as a parameter and returns the block number as an integer.

    
    
    1var Web3 = require("web3")
    
    2const web3 = new Web3("https://cloudflare-eth.com")
    
    3
    
    4web3.eth.getBlockNumber(function (error, result) {
    
    5  console.log(result)
    
    6})
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

If you execute this program, it will simply print the latest block number: the
top of the blockchain. You can also use `await/async` function calls to avoid
nesting callbacks in your code:

    
    
    1async function getBlockNumber() {
    
    2  const latestBlockNumber = await web3.eth.getBlockNumber()
    
    3  console.log(latestBlockNumber)
    
    4  return latestBlockNumber
    
    5}
    
    6
    
    7getBlockNumber()
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

You can see all the functions available on the Web3 instance in [the official
web3.js documentation(opens in a new tab)](https://docs.web3js.org/).

Most of Web3 libraries are asynchronous because in the background the library
makes JSON RPC calls to the node which send backs the result.

If you are working in the browser, some wallets directly inject a Web3
instance and you should try to use it whenever possible especially if you plan
to interact with the user’s Ethereum address to make transactions.

Here is the snippet to detect if a MetaMask wallet is available and try to
enable it if it is. It will later allow you to read the user’s balance and
enable them to validate transactions you’d like to make them do on the
Ethereum blockchain:

    
    
    1if (window.ethereum != null) {
    
    2  state.web3 = new Web3(window.ethereum)
    
    3  try {
    
    4    // Request account access if needed
    
    5    await window.ethereum.enable()
    
    6    // Accounts now exposed
    
    7  } catch (error) {
    
    8    // User denied account access...
    
    9  }
    
    10}
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Alternatives to web3.js like [Ethers.js(opens in a new
tab)](https://docs.ethers.io/) do exist and are also commonly used. In the
next tutorial we’ll see [how to easily listen to new incoming blocks on the
blockchain and see what they contain(opens in a new
tab)](https://ethereumdev.io/listening-to-new-transactions-happening-on-the-
blockchain/).

p

Last edit: [@pettinarip(opens in a new tab)](https://github.com/pettinarip),
December 8, 2023

See contributors

### Was this tutorial helpful?

YesNo

  * [Edit page(opens in a new tab)](https://github.com/ethereum/ethereum-org-website/tree/dev/public/content/developers/tutorials/set-up-web3js-to-use-ethereum-in-javascript/index.md)
  * On this page

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

