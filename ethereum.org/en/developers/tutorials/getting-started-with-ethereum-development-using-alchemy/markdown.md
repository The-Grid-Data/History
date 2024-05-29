Skip to main content

[](/en/)

  * Learn
  * Use
  * Build
  * Participate
  * Research

Search```K`

Languages EN

# Getting Started with Ethereum Development

javascriptethers.jsnodesqueryingalchemy

Beginner

![✍️](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/270d.svg)Elan
Halpern

![📚](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4da.svg)[Medium(opens
in a new tab)](https://medium.com/alchemy-api/getting-started-with-ethereum-
development-using-alchemy-c3d6a45c567f)

![📆](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4c6.svg)
October 30, 2020

![⏱️](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/23f1.svg)4
minute read minute read

On this page

  * 1\. Sign Up for a Free Alchemy Account
  * 2\. Create an Alchemy App
  * 3\. Make a Request from the Command Line
  * 4\. Set up your Web3 Client
  * 5\. Write your first Web3 Script!

[![Ethereum and Alchemy
logos](/_next/image/?url=%2Fcontent%2Fdevelopers%2Ftutorials%2Fgetting-
started-with-ethereum-development-using-alchemy%2Fethereum-
alchemy.png&w=1920&q=75)](/content/developers/tutorials/getting-started-with-
ethereum-development-using-alchemy/ethereum-alchemy.png)

This is a beginners guide to getting started with Ethereum development. For
this tutorial we'll be using [Alchemy(opens in a new
tab)](https://alchemyapi.io/), the leading blockchain developer platform
powering millions of users from 70% of the top blockchain apps, including
Maker, 0x, MyEtherWallet, Dharma, and Kyber. Alchemy will give us access to an
API endpoint on the Ethereum chain so we can read and write transactions.

We’ll take you from signing up with Alchemy to writing your first web3 script!
No blockchain development experience necessary!

## 1\. Sign Up for a Free Alchemy Account

Creating an account with Alchemy is easy, [sign up for free here(opens in a
new tab)](https://auth.alchemyapi.io/signup).

## 2\. Create an Alchemy App

To communicate with the Ethereum chain and to use Alchemy’s products, you need
an API key to authenticate your requests.

You can [create API keys from the dashboard(opens in a new
tab)](http://dashboard.alchemyapi.io/). To make a new key, navigate to “Create
App” as shown below:

Special thanks to [_ShapeShift_(opens in a new tab)](https://shapeshift.com/)
_for letting us show their dashboard!_

[![Alchemy
dashboard](/_next/image/?url=%2Fcontent%2Fdevelopers%2Ftutorials%2Fgetting-
started-with-ethereum-development-using-alchemy%2Falchemy-
dashboard.png&w=1920&q=75)](/content/developers/tutorials/getting-started-
with-ethereum-development-using-alchemy/alchemy-dashboard.png)

Fill in the details under “Create App” to get your new key. You can also see
apps you previously made and those made by your team here. Pull existing keys
by clicking on “View Key” for any app.

[![Create app with Alchemy
screenshot](/_next/image/?url=%2Fcontent%2Fdevelopers%2Ftutorials%2Fgetting-
started-with-ethereum-development-using-alchemy%2Fcreate-
app.png&w=1920&q=75)](/content/developers/tutorials/getting-started-with-
ethereum-development-using-alchemy/create-app.png)

You can also pull existing API keys by hovering over “Apps” and selecting one.
You can “View Key” here, as well as “Edit App” to whitelist specific domains,
see several developer tools, and view analytics.

[![Gif showing a user how to pull API
keys](/content/developers/tutorials/getting-started-with-ethereum-development-
using-alchemy/pull-api-keys.gif)](/content/developers/tutorials/getting-
started-with-ethereum-development-using-alchemy/pull-api-keys.gif)

## 3\. Make a Request from the Command Line

Interact with the Ethereum blockchain through Alchemy using JSON-RPC and curl.

For manual requests, we recommend interacting with the `JSON-RPC` via `POST`
requests. Simply pass in the `Content-Type: application/json` header and your
query as the `POST` body with the following fields:

  * `jsonrpc`: The JSON-RPC version—currently, only `2.0` is supported.
  * `method`: The ETH API method. [See API reference.(opens in a new tab)](https://docs.alchemyapi.io/documentation/alchemy-api-reference/json-rpc)
  * `params`: A list of parameters to pass to the method.
  * `id`: The ID of your request. Will be returned by the response so you can keep track of which request a response belongs to.

Here is an example you can run from the command line to retrieve the current
gas price:

    
    
    curl https://eth-mainnet.alchemyapi.io/v2/demo \
    
    -X POST \
    
    -H "Content-Type: application/json" \
    
    -d '{"jsonrpc":"2.0","method":"eth_gasPrice","params":[],"id":73}'

_**NOTE:** Replace [https://eth-mainnet.alchemyapi.io/v2/demo(opens in a new
tab)](https://eth-mainnet.alchemyapi.io/jsonrpc/demo) with your own API key
`https://eth-mainnet.alchemyapi.io/v2/**your-api-key`._

**Results:**

    
    
     1{ "id": 73,"jsonrpc": "2.0","result": "0x09184e72a000" // 10000000000000 }
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

## 4\. Set up your Web3 Client

**If you have an existing client,** change your current node provider URL to
an Alchemy URL with your API key: `“https://eth-mainnet.alchemyapi.io/v2/your-
api-key"`

**_NOTE:_** The scripts below need to be run in a **node context** or **saved
in a file** , not run from the command line. If you don’t already have Node or
npm installed, check out this quick [set-up guide for macs(opens in a new
tab)](https://app.gitbook.com/@alchemyapi/s/alchemy/guides/alchemy-for-macs).

There are tons of [Web3 libraries(opens in a new
tab)](https://docs.alchemyapi.io/guides/getting-started#other-web3-libraries)
you can integrate with Alchemy, however, we recommend using [Alchemy
Web3(opens in a new tab)](https://docs.alchemy.com/reference/api-overview), a
drop-in replacement for web3.js, built and configured to work seamlessly with
Alchemy. This provides multiple advantages such as automatic retries and
robust WebSocket support.

To install AlchemyWeb3.js, **navigate to your project directory** and run:

**With Yarn:**

    
    
     1yarn add @alch/alchemy-web3

**With NPM:**

    
    
     1npm install @alch/alchemy-web3

To interact with Alchemy’s node infrastructure, run in NodeJS or add this to a
JavaScript file:

    
    
    1const { createAlchemyWeb3 } = require("@alch/alchemy-web3")
    
    2const web3 = createAlchemyWeb3(
    
    3  "https://eth-mainnet.alchemyapi.io/v2/your-api-key"
    
    4)
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

## 5\. Write your first Web3 Script!

Now to get our hands dirty with a little web3 programming we’ll write a simple
script that prints out the latest block number from the Ethereum Mainnet.

**1\. If you haven’t already, in your terminal create a new project directory
and cd into it:**

    
    
     1mkdir web3-example
    
    2cd web3-example

**2\. Install the Alchemy web3 (or any web3) dependency into your project if
you have not already:**

    
    
     1npm install @alch/alchemy-web3

**3\. Create a file named`index.js` and add the following contents:**

> You should ultimately replace `demo` with your Alchemy HTTP API key.
    
    
    1async function main() {
    
    2  const { createAlchemyWeb3 } = require("@alch/alchemy-web3")
    
    3  const web3 = createAlchemyWeb3("https://eth-mainnet.alchemyapi.io/v2/demo")
    
    4  const blockNumber = await web3.eth.getBlockNumber()
    
    5  console.log("The latest block number is " + blockNumber)
    
    6}
    
    7main()
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Unfamiliar with the async stuff? Check out this [Medium post(opens in a new
tab)](https://medium.com/better-programming/understanding-async-await-in-
javascript-1d81bb079b2c).

**4\. Run it in your terminal using node**

    
    
     1node index.js

**5\. You should now see the latest block number output in your console!**

    
    
     1The latest block number is 11043912

**Woo! Congrats! You just wrote your first web3 script using Alchemy 🎉**

Not sure what to do next? Try deploying your first smart contract and get your
hands dirty with some solidity programming in our [Hello World Smart Contract
Guide(opens in a new tab)](https://docs.alchemyapi.io/tutorials/hello-world-
smart-contract), or test your dashboard knowledge with the [Dashboard Demo
App(opens in a new tab)](https://docs.alchemyapi.io/tutorials/demo-app)!

_[Sign up with Alchemy for free(opens in a new
tab)](https://auth.alchemyapi.io/signup), check out our [documentation(opens
in a new tab)](https://docs.alchemyapi.io/), and for the latest news, follow
us on [Twitter(opens in a new tab)](https://twitter.com/AlchemyPlatform)_.

n

Last edit: [@nhsz(opens in a new tab)](https://github.com/nhsz), August 15,
2023

See contributors

### Was this tutorial helpful?

YesNo

  * [Edit page(opens in a new tab)](https://github.com/ethereum/ethereum-org-website/tree/dev/public/content/developers/tutorials/getting-started-with-ethereum-development-using-alchemy/index.md)
  * On this page

    * 1\. Sign Up for a Free Alchemy Account
    * 2\. Create an Alchemy App
    * 3\. Make a Request from the Command Line
    * 4\. Set up your Web3 Client
    * 5\. Write your first Web3 Script!

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

