Skip to main content

[](/en/)

  * Learn
  * Use
  * Build
  * Participate
  * Research

Search```K`

Languages EN

# Hello World Smart Contract for Beginners

solidityhardhatalchemysmart contractsdeploying

Beginner

![✍️](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/270d.svg)elanh

![📆](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4c6.svg)
March 31, 2021

![⏱️](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/23f1.svg)12
minute read minute read

On this page

  * Step 1: Connect to the Ethereum network
  * Step 2: Create your app (and API key)
  * Step 3: Create an Ethereum account (address)
  * Step 4: Add ether from a Faucet
  * Step 5: Check your Balance
  * Step 6: Initialize our project
  * Step 7: Download Hardhat
  * Step 8: Create Hardhat project
  * Step 9: Add project folders
  * Step 10: Write our contract
  * Step 11: Connect MetaMask & Alchemy to your project
  * Step 12: Install Ethers.js
  * Step 13: Update hardhat.config.js
  * Step 14: Compile our contract
  * Step 15: Write our deploy script
  * Step 16: Deploy our contract

If you are new to blockchain development and don’t know where to start, or if
you just want to understand how to deploy and interact with smart contracts,
this guide is for you. We will walk through creating and deploying a simple
smart contract on the Goerli test network using a virtual wallet
[MetaMask(opens in a new tab)](https://metamask.io/), [Solidity(opens in a new
tab)](https://docs.soliditylang.org/en/v0.8.0/), [Hardhat(opens in a new
tab)](https://hardhat.org/), and [Alchemy(opens in a new
tab)](https://alchemyapi.io/eth) (don’t worry if you don’t understand what any
of this means yet, we will explain it).

> **Warning**
>
> 🚧 Deprecation Notice
>
> For the entirety of this guide, the Goerli test network is being used for
> creating and deploying a smart contract. However, please note that the
> Ethereum Foundation has announced that [Goerli will soon be deprecated(opens
> in a new tab)](https://www.alchemy.com/blog/goerli-faucet-deprecation).
>
> We recommend you to use the [Sepolia(opens in a new
> tab)](https://www.alchemy.com/overviews/sepolia-testnet) and [Sepolia
> faucet(opens in a new tab)](https://sepoliafaucet.com/) for this tutorial.

In [part 2(opens in a new tab)](https://docs.alchemy.com/docs/interacting-
with-a-smart-contract) of this tutorial we’ll go through how we can interact
with our smart contract once it’s deployed here, and in [part 3(opens in a new
tab)](https://docs.alchemy.com/docs/submitting-your-smart-contract-to-
etherscan) we’ll cover how to publish it on Etherscan.

If you have questions at any point feel free to reach out in the [Alchemy
Discord(opens in a new tab)](https://discord.gg/gWuC7zB)!

## Step 1: Connect to the Ethereum network

There are many ways to make requests to the Ethereum chain. For simplicity,
we’ll use a free account on Alchemy, a blockchain developer platform and API
that allows us to communicate with the Ethereum chain without having to run
our own nodes. The platform also has developer tools for monitoring and
analytics that we’ll take advantage of in this tutorial to understand what’s
going on under the hood in our smart contract deployment. If you don’t already
have an Alchemy account, [you can sign up for free here(opens in a new
tab)](https://dashboard.alchemyapi.io/signup).

## Step 2: Create your app (and API key)

Once you’ve created an Alchemy account, you can generate an API key by
creating an app. This will allow us to make requests to the Goerli test
network. If you’re not familiar with testnets, check out [this
page](/en/developers/docs/networks/).

  1. Navigate to the “Create App” page in your Alchemy Dashboard by hovering over “Apps” in the nav bar and clicking “Create App”

[![Hello world create
app](/_next/image/?url=%2Fcontent%2Fdevelopers%2Ftutorials%2Fhello-world-
smart-contract%2Fhello-world-create-
app.png&w=1920&q=75)](/content/developers/tutorials/hello-world-smart-
contract/hello-world-create-app.png)

  2. Name your app “Hello World”, offer a short description, select “Staging” for the Environment (used for your app bookkeeping), and choose “Goerli” for your network.

[![create app view hello
world](/_next/image/?url=%2Fcontent%2Fdevelopers%2Ftutorials%2Fhello-world-
smart-contract%2Fcreate-app-view-hello-
world.png&w=1920&q=75)](/content/developers/tutorials/hello-world-smart-
contract/create-app-view-hello-world.png)

  3. Click “Create app” and that’s it! Your app should appear in the table below.

## Step 3: Create an Ethereum account (address)

We need an Ethereum account to send and receive transactions. For this
tutorial, we’ll use MetaMask, a virtual wallet in the browser used to manage
your Ethereum account address. More on
[transactions](/en/developers/docs/transactions/).

You can download and create a MetaMask account for free [here(opens in a new
tab)](https://metamask.io/download.html). When you are creating an account, or
if you already have an account, make sure to switch over to the “Goerli Test
Network” in the upper right (so that we’re not dealing with real money).

[![metamask ropsten
example](/_next/image/?url=%2Fcontent%2Fdevelopers%2Ftutorials%2Fhello-world-
smart-contract%2Fmetamask-ropsten-
example.png&w=1080&q=75)](/content/developers/tutorials/hello-world-smart-
contract/metamask-ropsten-example.png)

## Step 4: Add ether from a Faucet

In order to deploy our smart contract to the test network, we’ll need some
fake Eth. To get Eth you can go to the [Goerli faucet(opens in a new
tab)](https://goerlifaucet.com/) and log into your Alchemy account and enter
your wallet address, then click “Send Me Eth.” It may take some time to
receive your fake Eth due to network traffic. (At the time of writing this, it
took around 30 minutes.) You should see Eth in your Metamask account soon
after!

## Step 5: Check your Balance

To double check our balance is there, let’s make an [eth_getBalance(opens in a
new tab)](https://docs.alchemyapi.io/alchemy/documentation/alchemy-api-
reference/json-rpc#eth_getbalance) request using [Alchemy’s composer
tool(opens in a new
tab)](https://composer.alchemyapi.io?composer_state=%7B%22network%22%3A0%2C%22methodName%22%3A%22eth_getBalance%22%2C%22paramValues%22%3A%5B%22%22%2C%22latest%22%5D%7D).
This will return the amount of ETH in our wallet. After you input your
MetaMask account address and click “Send Request”, you should see a response
like this:

    
    
    1{ "jsonrpc": "2.0", "id": 0, "result": "0x2B5E3AF16B1880000" }
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

> **NOTE:** This result is in wei not ETH. Wei is used as the smallest
> denomination of ether. The conversion from wei to ETH is: 1 eth = 1018 wei.
> So if we convert 0x2B5E3AF16B1880000 to decimal we get 5*10¹⁸ which equals 5
> ETH.
>
> Phew! Our fake money is all there
> ![🤑](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f911.svg).

## Step 6: Initialize our project

First, we’ll need to create a folder for our project. Navigate to your command
line and type:

    
    
    1mkdir hello-world
    
    2cd hello-world

Now that we’re inside our project folder, we’ll use `npm init` to initialize
the project. If you don’t already have npm installed, follow [these
instructions(opens in a new
tab)](https://docs.alchemyapi.io/alchemy/guides/alchemy-for-macs#1-install-
nodejs-and-npm) (we’ll also need Node.js so download that too!).

    
    
    1npm init

It doesn’t really matter how you answer the installation questions, here is
how we did it for reference:

    
    
    1package name: (hello-world)
    
    2version: (1.0.0)
    
    3description: hello world smart contract
    
    4entry point: (index.js)
    
    5test command:
    
    6git repository:
    
    7keywords:
    
    8author:
    
    9license: (ISC)
    
    10About to write to /Users/.../.../.../hello-world/package.json:
    
    11
    
    12{
    
    13  "name": "hello-world",
    
    14  "version": "1.0.0",
    
    15  "description": "hello world smart contract",
    
    16  "main": "index.js",
    
    17  "scripts": {
    
    18     "test": "echo \\"Error: no test specified\\" && exit 1"
    
    19  },
    
    20  "author": "",
    
    21  "license": "ISC"
    
    22}
    
    Show all

Approve the package.json and we’re good to go!

## Step 7: Download [Hardhat(opens in a new tab)](https://hardhat.org/getting-
started/#overview)

Hardhat is a development environment to compile, deploy, test, and debug your
Ethereum software. It helps developers when building smart contracts and dapps
locally before deploying to the live chain.

Inside our `hello-world` project run:

    
    
    1npm install --save-dev hardhat

Check out this page for more details on [installation instructions(opens in a
new tab)](https://hardhat.org/getting-started/#overview).

## Step 8: Create Hardhat project

Inside our project folder run:

    
    
    1npx hardhat

You should then see a welcome message and option to select what you want to
do. Select “create an empty hardhat.config.js”:

    
    
    1888    888                      888 888               888
    
    2888    888                      888 888               888
    
    3888    888                      888 888               888
    
    48888888888  8888b.  888d888 .d88888 88888b.   8888b.  888888
    
    5888    888     "88b 888P"  d88" 888 888 "88b     "88b 888
    
    6888    888 .d888888 888    888  888 888  888 .d888888 888
    
    7888    888 888  888 888    Y88b 888 888  888 888  888 Y88b.
    
    8888    888 "Y888888 888     "Y88888 888  888 "Y888888  "Y888
    
    9
    
    10👷 Welcome to Hardhat v2.0.11 👷‍?
    
    11
    
    12What do you want to do? …
    
    13Create a sample project
    
    14❯ Create an empty hardhat.config.js
    
    15Quit
    
    Show all

This will generate a `hardhat.config.js` file for us which is where we’ll
specify all of the set up for our project (on step 13).

## Step 9: Add project folders

To keep our project organized we’ll create two new folders. Navigate to the
root directory of your project in your command line and type:

    
    
    1mkdir contracts
    
    2mkdir scripts

  * `contracts/` is where we’ll keep our hello world smart contract code file
  * `scripts/` is where we’ll keep scripts to deploy and interact with our contract

## Step 10: Write our contract

You might be asking yourself, when the heck are we going to write code?? Well,
here we are, on step 10.

Open up the hello-world project in your favorite editor (we like [VSCode(opens
in a new tab)](https://code.visualstudio.com/)). Smart contracts are written
in a language called Solidity which is what we will use to write our
HelloWorld.sol smart contract.‌

  1. Navigate to the “contracts” folder and create a new file called HelloWorld.sol
  2. Below is a sample Hello World smart contract from the Ethereum Foundation that we will be using for this tutorial. Copy and paste in the contents below into your HelloWorld.sol file, and be sure to read the comments to understand what this contract does:

    
    
    1// Specifies the version of Solidity, using semantic versioning.
    
    2// Learn more: https://solidity.readthedocs.io/en/v0.5.10/layout-of-source-files.html#pragma
    
    3pragma solidity ^0.7.0;
    
    4
    
    5// Defines a contract named `HelloWorld`.
    
    6// A contract is a collection of functions and data (its state). Once deployed, a contract resides at a specific address on the Ethereum blockchain. Learn more: https://solidity.readthedocs.io/en/v0.5.10/structure-of-a-contract.html
    
    7contract HelloWorld {
    
    8
    
    9   // Declares a state variable `message` of type `string`.
    
    10   // State variables are variables whose values are permanently stored in contract storage. The keyword `public` makes variables accessible from outside a contract and creates a function that other contracts or clients can call to access the value.
    
    11   string public message;
    
    12
    
    13   // Similar to many class-based object-oriented languages, a constructor is a special function that is only executed upon contract creation.
    
    14   // Constructors are used to initialize the contract's data. Learn more:https://solidity.readthedocs.io/en/v0.5.10/contracts.html#constructors
    
    15   constructor(string memory initMessage) {
    
    16
    
    17      // Accepts a string argument `initMessage` and sets the value into the contract's `message` storage variable).
    
    18      message = initMessage;
    
    19   }
    
    20
    
    21   // A public function that accepts a string argument and updates the `message` storage variable.
    
    22   function update(string memory newMessage) public {
    
    23      message = newMessage;
    
    24   }
    
    25}
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

This is a super simple smart contract that stores a message upon creation and
can be updated by calling the `update` function.

## Step 11: Connect MetaMask & Alchemy to your project

We’ve created a MetaMask wallet, Alchemy account, and written our smart
contract, now it’s time to connect the three.

Every transaction sent from your virtual wallet requires a signature using
your unique private key. To provide our program with this permission, we can
safely store our private key (and Alchemy API key) in an environment file.

> To learn more about sending transactions, check out [this
> tutorial](/en/developers/tutorials/sending-transactions-using-web3-and-
> alchemy/) on sending transactions using web3.

First, install the dotenv package in your project directory:

    
    
    1npm install dotenv --save

Then, create a `.env` file in the root directory of our project, and add your
MetaMask private key and HTTP Alchemy API URL to it.

  * Follow [these instructions(opens in a new tab)](https://metamask.zendesk.com/hc/en-us/articles/360015289632-How-to-Export-an-Account-Private-Key) to export your private key
  * See below to get HTTP Alchemy API URL

[![get alchemy api key](/content/developers/tutorials/hello-world-smart-
contract/get-alchemy-api-key.gif)](/content/developers/tutorials/hello-world-
smart-contract/get-alchemy-api-key.gif)

Copy Alchemy API URL

Your `.env` should look like this:

    
    
    1API_URL = "https://eth-goerli.alchemyapi.io/v2/your-api-key"
    
    2PRIVATE_KEY = "your-metamask-private-key"

To actually connect these to our code, we’ll reference these variables in our
`hardhat.config.js` file on step 13.

Don't commit `.env`! Please make sure never to share or expose your `.env`
file with anyone, as you are compromising your secrets in doing so. If you are
using version control, add your `.env` to a [gitignore(opens in a new
tab)](https://git-scm.com/docs/gitignore) file.

## Step 12: Install Ethers.js

Ethers.js is a library that makes it easier to interact and make requests to
Ethereum by wrapping [standard JSON-RPC
methods](/en/developers/docs/apis/json-rpc/) with more user friendly methods.

Hardhat makes it super easy to integrate [Plugins(opens in a new
tab)](https://hardhat.org/plugins/) for additional tooling and extended
functionality. We’ll be taking advantage of the [Ethers plugin(opens in a new
tab)](https://hardhat.org/plugins/nomiclabs-hardhat-ethers.html) for contract
deployment ([Ethers.js(opens in a new tab)](https://github.com/ethers-
io/ethers.js/) has some super clean contract deployment methods).

In your project directory type:

    
    
    1npm install --save-dev @nomiclabs/hardhat-ethers "ethers@^5.0.0"

We’ll also require ethers in our `hardhat.config.js` in the next step.

## Step 13: Update hardhat.config.js

We’ve added several dependencies and plugins so far, now we need to update
`hardhat.config.js` so that our project knows about all of them.

Update your `hardhat.config.js` to look like this:

    
    
    1require('dotenv').config();
    
    2
    
    3require("@nomiclabs/hardhat-ethers");
    
    4const { API_URL, PRIVATE_KEY } = process.env;
    
    5
    
    6/**
    
    7* @type import('hardhat/config').HardhatUserConfig
    
    8*/
    
    9module.exports = {
    
    10   solidity: "0.7.3",
    
    11   defaultNetwork: "goerli",
    
    12   networks: {
    
    13      hardhat: {},
    
    14      goerli: {
    
    15         url: API_URL,
    
    16         accounts: [`0x${PRIVATE_KEY}`]
    
    17      }
    
    18   },
    
    19}
    
    Show all

## Step 14: Compile our contract

To make sure everything is working so far, let’s compile our contract. The
`compile` task is one of the built-in hardhat tasks.

From the command line run:

    
    
    1npx hardhat compile

You might get a warning about `SPDX license identifier not provided in source
file` , but no need to worry about that — hopefully everything else looks
good! If not, you can always message in the [Alchemy discord(opens in a new
tab)](https://discord.gg/u72VCg3).

## Step 15: Write our deploy script

Now that our contract is written and our configuration file is good to go,
it’s time to write our contract deploy script.

Navigate to the `scripts/` folder and create a new file called `deploy.js` ,
adding the following contents to it:

    
    
    1async function main() {
    
    2   const HelloWorld = await ethers.getContractFactory("HelloWorld");
    
    3
    
    4   // Start deployment, returning a promise that resolves to a contract object
    
    5   const hello_world = await HelloWorld.deploy("Hello World!");
    
    6   console.log("Contract deployed to address:", hello_world.address);}
    
    7
    
    8main()
    
    9  .then(() => process.exit(0))
    
    10  .catch(error => {
    
    11    console.error(error);
    
    12    process.exit(1);
    
    13  });
    
    Show all

Hardhat does an amazing job of explaining what each of these lines of code
does in their [Contracts tutorial(opens in a new
tab)](https://hardhat.org/tutorial/testing-contracts.html#writing-tests),
we’ve adopted their explanations here.

    
    
    1const HelloWorld = await ethers.getContractFactory("HelloWorld");

A `ContractFactory` in ethers.js is an abstraction used to deploy new smart
contracts, so `HelloWorld` here is a factory for instances of our hello world
contract. When using the `hardhat-ethers` plugin `ContractFactory` and
`Contract` instances are connected to the first signer by default.

    
    
    1const hello_world = await HelloWorld.deploy();

Calling `deploy()` on a `ContractFactory` will start the deployment, and
return a `Promise` that resolves to a `Contract`. This is the object that has
a method for each of our smart contract functions.

## Step 16: Deploy our contract

We’re finally ready to deploy our smart contract! Navigate to the command line
and run:

    
    
    1npx hardhat run scripts/deploy.js --network goerli

You should then see something like:

    
    
    1Contract deployed to address: 0x6cd7d44516a20882cEa2DE9f205bF401c0d23570

If we go to the [Goerli etherscan(opens in a new
tab)](https://goerli.etherscan.io/) and search for our contract address we
should able to see that it has been deployed successfully. The transaction
will look something like this:

[![etherscan
contract](/_next/image/?url=%2Fcontent%2Fdevelopers%2Ftutorials%2Fhello-world-
smart-contract%2Fetherscan-
contract.png&w=1920&q=75)](/content/developers/tutorials/hello-world-smart-
contract/etherscan-contract.png)

The `From` address should match your MetaMask account address and the To
address will say “Contract Creation” but if we click into the transaction
we’ll see our contract address in the `To` field:

[![etherscan
transaction](/_next/image/?url=%2Fcontent%2Fdevelopers%2Ftutorials%2Fhello-
world-smart-contract%2Fetherscan-
transaction.png&w=1920&q=75)](/content/developers/tutorials/hello-world-smart-
contract/etherscan-transaction.png)

Congrats! You just deployed a smart contract to the Ethereum chain 🎉

To understand what’s going on under the hood, let’s navigate to the Explorer
tab in our [Alchemy dashboard(opens in a new
tab)](https://dashboard.alchemyapi.io/explorer). If you have multiple Alchemy
apps make sure to filter by app and select “Hello World”. [![hello world
explorer](/_next/image/?url=%2Fcontent%2Fdevelopers%2Ftutorials%2Fhello-world-
smart-contract%2Fhello-world-
explorer.png&w=1920&q=75)](/content/developers/tutorials/hello-world-smart-
contract/hello-world-explorer.png)

Here you’ll see a handful of JSON-RPC calls that Hardhat/Ethers made under the
hood for us when we called the `.deploy()` function. Two important ones to
call out here are [`eth_sendRawTransaction`(opens in a new
tab)](https://docs.alchemyapi.io/alchemy/documentation/alchemy-api-
reference/json-rpc#eth_sendrawtransaction), which is the request to actually
write our contract onto the Goerli chain, and
[`eth_getTransactionByHash`(opens in a new
tab)](https://docs.alchemyapi.io/alchemy/documentation/alchemy-api-
reference/json-rpc#eth_gettransactionbyhash) which is a request to read
information about our transaction given the hash (a typical pattern when
transactions). To learn more about sending transactions, check out this
tutorial on [sending transactions using
Web3](/en/developers/tutorials/sending-transactions-using-web3-and-alchemy/)

That’s all for part 1 of this tutorial, in part 2 we’ll actually [interact
with our smart contract(opens in a new
tab)](https://docs.alchemyapi.io/alchemy/tutorials/hello-world-smart-
contract#part-2-interact-with-your-smart-contract) by updated our initial
message, and in part 3 we’ll [publish our smart contract to Etherscan(opens in
a new tab)](https://docs.alchemyapi.io/alchemy/tutorials/hello-world-smart-
contract#optional-part-3-publish-your-smart-contract-to-etherscan) so everyone
will know how to interact with it.

**Want to learn more about Alchemy? Check out our[website(opens in a new
tab)](https://alchemyapi.io/eth). Never want to miss an update? Subscribe to
our newsletter [here(opens in a new
tab)](https://www.alchemyapi.io/newsletter)! Be sure to also follow our
[Twitter(opens in a new tab)](https://twitter.com/alchemyplatform) and join
our [Discord(opens in a new tab)](https://discord.com/invite/u72VCg3)**.

p

Last edit: [@pettinarip(opens in a new tab)](https://github.com/pettinarip),
November 23, 2023

See contributors

### Was this tutorial helpful?

YesNo

  * [Edit page(opens in a new tab)](https://github.com/ethereum/ethereum-org-website/tree/dev/public/content/developers/tutorials/hello-world-smart-contract/index.md)
  * On this page

    * Step 1: Connect to the Ethereum network
    * Step 2: Create your app (and API key)
    * Step 3: Create an Ethereum account (address)
    * Step 4: Add ether from a Faucet
    * Step 5: Check your Balance
    * Step 6: Initialize our project
    * Step 7: Download Hardhat
    * Step 8: Create Hardhat project
    * Step 9: Add project folders
    * Step 10: Write our contract
    * Step 11: Connect MetaMask & Alchemy to your project
    * Step 12: Install Ethers.js
    * Step 13: Update hardhat.config.js
    * Step 14: Compile our contract
    * Step 15: Write our deploy script
    * Step 16: Deploy our contract

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

