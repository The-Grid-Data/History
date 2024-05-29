Skip to main content

[](/en/)

  * Learn
  * Use
  * Build
  * Participate
  * Research

Search```K`

Languages EN

# Hello World Smart Contract for Beginners - Fullstack

solidityhardhatalchemysmart
contractsdeployingblockexplorerfrontendtransactions

Beginner

![✍️](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/270d.svg)nstrike2

![📆](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4c6.svg)
October 25, 2021

![⏱️](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/23f1.svg)45
minute read minute read

On this page

  * Part 1 - Create and Deploy your Smart Contract using Hardhat
    * Connect to the Ethereum network
    * Create your app and API key
    * Create an Ethereum account
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
  * Part 2: Interact with your Smart Contract
    * Create a interact.js file
    * Update your .env file
    * Grab your contract ABI
    * Create an instance of your contract
    * Read the init message
    * Update the message
    * Read the new message
  * Part 3: Publish your Smart Contract to Etherscan
    * Step 1: Generate an API Key on your Etherscan account
    * Hardhat-deployed smart contracts
    * Check out your smart contract on Etherscan!
  * Part 4 - Integrating your smart contract with the frontend
    * Clone the starter files
    * Check out the starter files
    * Step 3: Read from your smart contract
    * Step 4: Set up your Ethereum wallet
    * Step 5: Connect MetaMask to your UI
    * Step 6: Implement the updateMessage function
    * Make your own custom dapp

This guide is for you if you are new to blockchain development and don't know
where to start or how to deploy and interact with smart contracts. We will
walk through creating and deploying a simple, smart contract on the Goerli
test network using [MetaMask(opens in a new tab)](https://metamask.io),
[Solidity(opens in a new tab)](https://docs.soliditylang.org/en/v0.8.0/),
[Hardhat(opens in a new tab)](https://hardhat.org), and [Alchemy(opens in a
new tab)](https://alchemyapi.io/eth).

You'll need an Alchemy account to complete this tutorial. [Sign up for a free
account(opens in a new tab)](https://www.alchemy.com/).

If you have questions at any point, feel free to reach out in the [Alchemy
Discord(opens in a new tab)](https://discord.gg/gWuC7zB)!

## Part 1 - Create and Deploy your Smart Contract using Hardhat

### Connect to the Ethereum network

There are many ways to make requests to the Ethereum chain. For simplicity,
we'll use a free account on Alchemy, a blockchain developer platform and API
that allows us to communicate with the Ethereum chain without running a node
ourselves. Alchemy also has developer tools for monitoring and analytics;
we'll take advantage of these in this tutorial to understand what's going on
under the hood in our smart contract deployment.

### Create your app and API key

Once you've created an Alchemy account, you can generate an API key by
creating an app. This will allow you to make requests to the Goerli testnet.
If you're not familiar with testnets you can [read Alchemy's guide to choosing
a network(opens in a new tab)](https://docs.alchemyapi.io/guides/choosing-a-
network).

On the Alchemy dashboard, find the **Apps** dropdown in the navigation bar and
click **Create App**.

[![Hello world create
app](/_next/image/?url=%2Fcontent%2Fdevelopers%2Ftutorials%2Fhello-world-
smart-contract-fullstack%2Fhello-world-create-
app.png&w=1920&q=75)](/content/developers/tutorials/hello-world-smart-
contract-fullstack/hello-world-create-app.png)

Give your app the name '_Hello World_ ' and write a short description. Select
**Staging** as your environment and **Goerli** as your network.

[![create app view hello
world](/_next/image/?url=%2Fcontent%2Fdevelopers%2Ftutorials%2Fhello-world-
smart-contract-fullstack%2Fcreate-app-view-hello-
world.png&w=1920&q=75)](/content/developers/tutorials/hello-world-smart-
contract-fullstack/create-app-view-hello-world.png)

_Note: be sure to select**Goerli** , or this tutorial won't work._

Click **Create app**. Your app will appear in the table below.

### Create an Ethereum account

You need an Ethereum account to send and receive transactions. We'll use
MetaMask, a virtual wallet in the browser that lets users manage their
Ethereum account address.

You can download and create a MetaMask account for free [here(opens in a new
tab)](https://metamask.io/download.html). When you are creating an account, or
if you already have an account, make sure to switch over to the “Goerli Test
Network” in the upper right (so that we’re not dealing with real money).

### Step 4: Add ether from a Faucet

To deploy your smart contract to the test network, you'll need some fake ETH.
To get ETH on the Goerli network, go to a Goerli faucet and enter your Goerli
account address. Note that Goerli faucets can be a bit unreliable recently -
see the [test networks page](/en/developers/docs/networks/#goerli) for a list
of options to try:

_Note: due to network congestion, this might take a while._ ``

### Step 5: Check your Balance

To double-check the ETH is in your wallet, let’s make an [eth_getBalance(opens
in a new tab)](https://docs.alchemyapi.io/alchemy/documentation/alchemy-api-
reference/json-rpc#eth_getbalance) request using [Alchemy’s composer
tool(opens in a new
tab)](https://composer.alchemyapi.io/?composer_state=%7B%22network%22%3A0%2C%22methodName%22%3A%22eth_getBalance%22%2C%22paramValues%22%3A%5B%22%22%2C%22latest%22%5D%7D).
This will return the amount of ETH in our wallet. To learn more check out
[Alchemy's short tutorial on how to use the composer tool(opens in a new
tab)](https://youtu.be/r6sjRxBZJuU).

Enter you input your MetaMask account address and click **Send Request**. You
will see a response that looks like the code snippet below.

    
    
    1{ "jsonrpc": "2.0", "id": 0, "result": "0x2B5E3AF16B1880000" }
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

>  _Note: This result is in wei, not ETH. Wei is used as the smallest
> denomination of ether._

Phew! Our fake money is all there.

### Step 6: Initialize our project

First, we'll need to create a folder for our project. Navigate to your command
line and input the following.

    
    
    1mkdir hello-world
    
    2cd hello-world

Now that we’re inside our project folder, we’ll use `npm init` to initialize
the project.

> If you don’t have npm installed yet, follow [these instructions to install
> Node.js and npm(opens in a new
> tab)](https://docs.alchemyapi.io/alchemy/guides/alchemy-for-macs#1-install-
> nodejs-and-npm).

For the purpose of this tutorial, it doesn't matter how you answer the
initialization questions. Here is how we did it for reference:

    
    
    1package name: (hello-world)
    
    2version: (1.0.0)
    
    3description: hello world smart contract
    
    4entry point: (index.js)
    
    5test command:
    
    6git repository:
    
    7keywords:
    
    8author:
    
    9license: (ISC)
    
    10
    
    11About to write to /Users/.../.../.../hello-world/package.json:
    
    12
    
    13{
    
    14   "name": "hello-world",
    
    15   "version": "1.0.0",
    
    16   "description": "hello world smart contract",
    
    17   "main": "index.js",
    
    18   "scripts": {
    
    19      "test": "echo \"Error: no test specified\" && exit 1"
    
    20   },
    
    21   "author": "",
    
    22   "license": "ISC"
    
    23}
    
    Show all

Approve the package.json and we’re good to go!

### Step 7: Download Hardhat

Hardhat is a development environment to compile, deploy, test, and debug your
Ethereum software. It helps developers when building smart contracts and dapps
locally before deploying to the live chain.

Inside our `hello-world` project run:

    
    
    1npm install --save-dev hardhat

Check out this page for more details on [installation instructions(opens in a
new tab)](https://hardhat.org/getting-started/#overview).

### Step 8: Create Hardhat project

Inside our `hello-world` project folder, run:

    
    
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
    
    10👷 Welcome to Hardhat v2.0.11 👷‍
    
    11
    
    12What do you want to do? …
    
    13Create a sample project
    
    14❯ Create an empty hardhat.config.js
    
    15Quit
    
    Show all

This will generate a `hardhat.config.js` file in the project. We'll use this
later in the tutorial to specify the setup for our project.

### Step 9: Add project folders

To keep the project organized, let's create two new folders. In the command
line, navigate to the root directory of your `hello-world` project and type:

    
    
    1mkdir contracts
    
    2mkdir scripts

  * `contracts/` is where we’ll keep our hello world smart contract code file
  * `scripts/` is where we’ll keep scripts to deploy and interact with our contract

### Step 10: Write our contract

You might be asking yourself, when are we going to write code? It's time!

Open up the hello-world project in your favorite editor. Smart contracts most
commonly are written in Solidity, which we will use to write our smart
contract.‌

  1. Navigate to the `contracts` folder and create a new file called `HelloWorld.sol`
  2. Below is a sample Hello World smart contract that we will be using for this tutorial. Copy the contents below into the `HelloWorld.sol` file.

_Note: Be sure to read the comments to understand what this contract does._

    
    
     1// Specifies the version of Solidity, using semantic versioning.
    
    2// Learn more: https://solidity.readthedocs.io/en/v0.5.10/layout-of-source-files.html#pragma
    
    3pragma solidity >=0.7.3;
    
    4
    
    5// Defines a contract named `HelloWorld`.
    
    6// A contract is a collection of functions and data (its state). Once deployed, a contract resides at a specific address on the Ethereum blockchain. Learn more: https://solidity.readthedocs.io/en/v0.5.10/structure-of-a-contract.html
    
    7contract HelloWorld {
    
    8
    
    9   //Emitted when update function is called
    
    10   //Smart contract events are a way for your contract to communicate that something happened on the blockchain to your app front-end, which can be 'listening' for certain events and take action when they happen.
    
    11   event UpdatedMessages(string oldStr, string newStr);
    
    12
    
    13   // Declares a state variable `message` of type `string`.
    
    14   // State variables are variables whose values are permanently stored in contract storage. The keyword `public` makes variables accessible from outside a contract and creates a function that other contracts or clients can call to access the value.
    
    15   string public message;
    
    16
    
    17   // Similar to many class-based object-oriented languages, a constructor is a special function that is only executed upon contract creation.
    
    18   // Constructors are used to initialize the contract's data. Learn more:https://solidity.readthedocs.io/en/v0.5.10/contracts.html#constructors
    
    19   constructor(string memory initMessage) {
    
    20
    
    21      // Accepts a string argument `initMessage` and sets the value into the contract's `message` storage variable).
    
    22      message = initMessage;
    
    23   }
    
    24
    
    25   // A public function that accepts a string argument and updates the `message` storage variable.
    
    26   function update(string memory newMessage) public {
    
    27      string memory oldMsg = message;
    
    28      message = newMessage;
    
    29      emit UpdatedMessages(oldMsg, newMessage);
    
    30   }
    
    31}
    
    Show all

This is a basic smart contract that stores a message upon creation. It can be
updated by calling the `update` function.

### Step 11: Connect MetaMask & Alchemy to your project

We’ve created a MetaMask wallet, Alchemy account, and written our smart
contract, now it’s time to connect the three.

Every transaction sent from your wallet requires a signature using your unique
private key. To provide our program with this permission, we can safely store
our private key in an environment file. We will also store an API key for
Alchemy here.

> To learn more about sending transactions, check out [this tutorial(opens in
> a new tab)](https://docs.alchemyapi.io/alchemy/tutorials/sending-
> transactions-using-web3-and-alchemy) on sending transactions using web3.

First, install the dotenv package in your project directory:

    
    
    1npm install dotenv --save

Then, create a `.env` file in the root directory of the project. Add your
MetaMask private key and HTTP Alchemy API URL to it.

Your environment file must be named `.env` or it won't be recognized as an
environment file.

Do not name it `process.env` or `.env-custom` or anything else.

  * Follow [these instructions(opens in a new tab)](https://metamask.zendesk.com/hc/en-us/articles/360015289632-How-to-Export-an-Account-Private-Key) to export your private key
  * See below to get HTTP Alchemy API URL

[![](/content/developers/tutorials/hello-world-smart-contract-fullstack/get-
alchemy-api-key.gif)](/content/developers/tutorials/hello-world-smart-
contract-fullstack/get-alchemy-api-key.gif)

Your `.env` should look like this:

    
    
    1API_URL = "https://eth-goerli.alchemyapi.io/v2/your-api-key"
    
    2PRIVATE_KEY = "your-metamask-private-key"

To actually connect these to our code, we’ll reference these variables in our
`hardhat.config.js` file on step 13.

### Step 12: Install Ethers.js

Ethers.js is a library that makes it easier to interact and make requests to
Ethereum by wrapping [standard JSON-RPC methods(opens in a new
tab)](https://docs.alchemyapi.io/alchemy/documentation/alchemy-api-
reference/json-rpc) with more user friendly methods.

Hardhat allows us to integrate [plugins(opens in a new
tab)](https://hardhat.org/plugins/) for additional tooling and extended
functionality. We’ll be taking advantage of the [Ethers plugin(opens in a new
tab)](https://hardhat.org/plugins/nomiclabs-hardhat-ethers.html) for contract
deployment.

In your project directory type:

    
    
    npm install --save-dev @nomiclabs/hardhat-ethers "ethers@^5.0.0"

### Step 13: Update hardhat.config.js

We’ve added several dependencies and plugins so far, now we need to update
`hardhat.config.js` so that our project knows about all of them.

Update your `hardhat.config.js` to look like this:

    
    
    1/**
    
    2 * @type import('hardhat/config').HardhatUserConfig
    
    3 */
    
    4
    
    5require("dotenv").config()
    
    6require("@nomiclabs/hardhat-ethers")
    
    7
    
    8const { API_URL, PRIVATE_KEY } = process.env
    
    9
    
    10module.exports = {
    
    11  solidity: "0.7.3",
    
    12  defaultNetwork: "goerli",
    
    13  networks: {
    
    14    hardhat: {},
    
    15    goerli: {
    
    16      url: API_URL,
    
    17      accounts: [`0x${PRIVATE_KEY}`],
    
    18    },
    
    19  },
    
    20}
    
    Show all

### Step 14: Compile our contract

To make sure everything is working so far, let’s compile our contract. The
`compile` task is one of the built-in hardhat tasks.

From the command line run:

    
    
    npx hardhat compile

You might get a warning about `SPDX license identifier not provided in source
file`, but no need to worry about that — hopefully everything else looks good!
If not, you can always message in the [Alchemy discord(opens in a new
tab)](https://discord.gg/u72VCg3).

### Step 15: Write our deploy script

Now that our contract is written and our configuration file is good to go,
it’s time to write our contract deploy script.

Navigate to the `scripts/` folder and create a new file called `deploy.js` ,
adding the following contents to it:

    
    
    1async function main() {
    
    2  const HelloWorld = await ethers.getContractFactory("HelloWorld")
    
    3
    
    4  // Start deployment, returning a promise that resolves to a contract object
    
    5  const hello_world = await HelloWorld.deploy("Hello World!")
    
    6  console.log("Contract deployed to address:", hello_world.address)
    
    7}
    
    8
    
    9main()
    
    10  .then(() => process.exit(0))
    
    11  .catch((error) => {
    
    12    console.error(error)
    
    13    process.exit(1)
    
    14  })
    
    Show all

Hardhat does an amazing job of explaining what each of these lines of code
does in their [Contracts tutorial(opens in a new
tab)](https://hardhat.org/tutorial/testing-contracts.html#writing-tests),
we’ve adopted their explanations here.

    
    
    1const HelloWorld = await ethers.getContractFactory("HelloWorld")

A `ContractFactory` in ethers.js is an abstraction used to deploy new smart
contracts, so `HelloWorld` here is a [factory(opens in a new
tab)](https://en.wikipedia.org/wiki/Factory_\(object-oriented_programming\))
for instances of our hello world contract. When using the `hardhat-ethers`
plugin `ContractFactory` and `Contract`, instances are connected to the first
signer (owner) by default.

    
    
    1const hello_world = await HelloWorld.deploy()

Calling `deploy()` on a `ContractFactory` will start the deployment, and
return a `Promise` that resolves to a `Contract` object. This is the object
that has a method for each of our smart contract functions.

### Step 16: Deploy our contract

We’re finally ready to deploy our smart contract! Navigate to the command line
and run:

    
    
    npx hardhat run scripts/deploy.js --network goerli

You should then see something like:

    
    
    Contract deployed to address: 0x6cd7d44516a20882cEa2DE9f205bF401c0d23570

**Please save this address**. We will be using it later in the tutorial.

If we go to the [Goerli etherscan(opens in a new
tab)](https://goerli.etherscan.io) and search for our contract address we
should able to see that it has been deployed successfully. The transaction
will look something like this:

[![](/_next/image/?url=%2Fcontent%2Fdevelopers%2Ftutorials%2Fhello-world-
smart-contract-fullstack%2Fetherscan-
contract.png&w=1920&q=75)](/content/developers/tutorials/hello-world-smart-
contract-fullstack/etherscan-contract.png)

The `From` address should match your MetaMask account address and the `To`
address will say **Contract Creation**. If we click into the transaction we’ll
see our contract address in the `To` field.

[![](/_next/image/?url=%2Fcontent%2Fdevelopers%2Ftutorials%2Fhello-world-
smart-contract-fullstack%2Fetherscan-
transaction.png&w=1920&q=75)](/content/developers/tutorials/hello-world-smart-
contract-fullstack/etherscan-transaction.png)

Congrats! You just deployed a smart contract to an Ethereum testnet.

To understand what’s going on under the hood, let’s navigate to the Explorer
tab in our [Alchemy dashboard(opens in a new
tab)](https://dashboard.alchemyapi.io/explorer). If you have multiple Alchemy
apps make sure to filter by app and select **Hello World**.

[![](/_next/image/?url=%2Fcontent%2Fdevelopers%2Ftutorials%2Fhello-world-
smart-contract-fullstack%2Fhello-world-
explorer.png&w=1920&q=75)](/content/developers/tutorials/hello-world-smart-
contract-fullstack/hello-world-explorer.png)

Here you’ll see a handful of JSON-RPC methods that Hardhat/Ethers made under
the hood for us when we called the `.deploy()` function. Two important methods
here are [`eth_sendRawTransaction`(opens in a new
tab)](https://docs.alchemyapi.io/alchemy/documentation/alchemy-api-
reference/json-rpc#eth_sendrawtransaction), which is the request to write our
contract onto the Goerli chain, and [`eth_getTransactionByHash`(opens in a new
tab)](https://docs.alchemyapi.io/alchemy/documentation/alchemy-api-
reference/json-rpc#eth_gettransactionbyhash), which is a request to read
information about our transaction given the hash. To learn more about sending
transactions, check out [our tutorial on sending transactions using
Web3](/en/developers/tutorials/sending-transactions-using-web3-and-alchemy/).

## Part 2: Interact with your Smart Contract

Now that we've successfully deployed a smart contract to the Goerli network
let's learn how to interact with it.

### Create a interact.js file

This is the file where we'll write our interaction script. We'll be using the
Ethers.js library that you previously installed in Part 1.

Inside the `scripts/`folder, create a new file named `interact.js` add the
following code:

    
    
    1// interact.js
    
    2
    
    3const API_KEY = process.env.API_KEY
    
    4const PRIVATE_KEY = process.env.PRIVATE_KEY
    
    5const CONTRACT_ADDRESS = process.env.CONTRACT_ADDRESS

### Update your .env file

We will be using new environment variables, so we need to define them in the
`.env`file that we created earlier.

We'll need to add a definition for our Alchemy `API_KEY` and the
`CONTRACT_ADDRESS` where your smart contract was deployed.

Your `.env` file should look something like this:

    
    
    # .env
    
    API_URL = "https://eth-goerli.alchemyapi.io/v2/<your-api-key>"
    
    API_KEY = "<your-api-key>"
    
    PRIVATE_KEY = "<your-metamask-private-key>"
    
    CONTRACT_ADDRESS = "0x<your contract address>"

### Grab your contract ABI

Our contract _ABI (Application Binary Interface)_ is the interface to interact
with our smart contract. Hardhat automatically generates an ABI and saves it
in `HelloWorld.json`. To use the ABI, we'll need to parse out the contents by
adding the following lines of code to our `interact.js` file:

    
    
    1// interact.js
    
    2const contract = require("../artifacts/contracts/HelloWorld.sol/HelloWorld.json")

If you want to see the ABI you can print it to your console:

    
    
    1console.log(JSON.stringify(contract.abi))

To see your ABI printed to the console, navigate to your terminal and run:

    
    
    npx hardhat run scripts/interact.js

### Create an instance of your contract

To interact with our contract, we need to create a contract instance in our
code. To do so with Ethers.js, we'll need to work with three concepts:

  1. Provider - a node provider that gives you read and write access to the blockchain
  2. Signer - represents an Ethereum account that can sign transactions
  3. Contract - an Ethers.js object representing a specific contract deployed on-chain

We'll use the contract ABI from the previous step to create our instance of
the contract:

    
    
    1// interact.js
    
    2
    
    3// Provider
    
    4const alchemyProvider = new ethers.providers.AlchemyProvider(
    
    5  (network = "goerli"),
    
    6  API_KEY
    
    7)
    
    8
    
    9// Signer
    
    10const signer = new ethers.Wallet(PRIVATE_KEY, alchemyProvider)
    
    11
    
    12// Contract
    
    13const helloWorldContract = new ethers.Contract(
    
    14  CONTRACT_ADDRESS,
    
    15  contract.abi,
    
    16  signer
    
    17)
    
    Show all

Learn more about Providers, Signers, and Contracts in the [ethers.js
documentation(opens in a new tab)](https://docs.ethers.io/v5/).

### Read the init message

Remember when we deployed our contract with the `initMessage = "Hello
world!"`? We are now going to read that message stored in our smart contract
and print it to the console.

In JavaScript, asynchronous functions get used when interacting with networks.
To learn more about asynchronous functions, [read this medium article(opens in
a new tab)](https://blog.bitsrc.io/understanding-asynchronous-javascript-the-
event-loop-74cd408419ff).

Use the code below to call the `message` function in our smart contract and
read the init message:

    
    
    1// interact.js
    
    2
    
    3// ...
    
    4
    
    5async function main() {
    
    6  const message = await helloWorldContract.message()
    
    7  console.log("The message is: " + message)
    
    8}
    
    9main()
    
    Show all

After running the file using `npx hardhat run scripts/interact.js` in the
terminal we should see this response:

    
    
    1The message is: Hello world!

Congrats! You've just successfully read smart contract data from the Ethereum
blockchain, way to go!

### Update the message

Instead of just reading the message, we can also update the message saved in
our smart contract using the `update` function! Pretty cool, right?

To update the message, we can directly call the `update` function on our
instantiated Contract object:

    
    
    1// interact.js
    
    2
    
    3// ...
    
    4
    
    5async function main() {
    
    6  const message = await helloWorldContract.message()
    
    7  console.log("The message is: " + message)
    
    8
    
    9  console.log("Updating the message...")
    
    10  const tx = await helloWorldContract.update("This is the new message.")
    
    11  await tx.wait()
    
    12}
    
    13main()
    
    Show all

Note that on line 11, we make a call to `.wait()` on the returned transaction
object. This ensures that our script waits for the transaction to get mined on
the blockchain before exiting the function. If the `.wait()` call isn't
included, the script may not see the updated `message` value in the contract.

### Read the new message

You should be able to repeat the previous step to read the updated `message`
value. Take a moment and see if you can make the changes necessary to print
out that new value!

If you need a hint, here's what your `interact.js` file should look like at
this point:

    
    
    1// interact.js
    
    2
    
    3const API_KEY = process.env.API_KEY
    
    4const PRIVATE_KEY = process.env.PRIVATE_KEY
    
    5const CONTRACT_ADDRESS = process.env.CONTRACT_ADDRESS
    
    6
    
    7const contract = require("../artifacts/contracts/HelloWorld.sol/HelloWorld.json")
    
    8
    
    9// provider - Alchemy
    
    10const alchemyProvider = new ethers.providers.AlchemyProvider(
    
    11  (network = "goerli"),
    
    12  API_KEY
    
    13)
    
    14
    
    15// signer - you
    
    16const signer = new ethers.Wallet(PRIVATE_KEY, alchemyProvider)
    
    17
    
    18// contract instance
    
    19const helloWorldContract = new ethers.Contract(
    
    20  CONTRACT_ADDRESS,
    
    21  contract.abi,
    
    22  signer
    
    23)
    
    24
    
    25async function main() {
    
    26  const message = await helloWorldContract.message()
    
    27  console.log("The message is: " + message)
    
    28
    
    29  console.log("Updating the message...")
    
    30  const tx = await helloWorldContract.update("this is the new message")
    
    31  await tx.wait()
    
    32
    
    33  const newMessage = await helloWorldContract.message()
    
    34  console.log("The new message is: " + newMessage)
    
    35}
    
    36
    
    37main()
    
    Show all

Now just run the script and you should be able to see the old message, the
updating status, and the new message printed out to your terminal!

`npx hardhat run scripts/interact.js --network goerli`

    
    
    1The message is: Hello World!
    
    2Updating the message...
    
    3The new message is: This is the new message.

While running that script, you may notice that the `Updating the message...`
step takes a while to load before the new message loads. That is due to the
mining process; if you are curious about tracking transactions while they are
being mined, visit the [Alchemy mempool(opens in a new
tab)](https://dashboard.alchemyapi.io/mempool) to see the status of a
transaction. If the transaction is dropped, it's also helpful to check [Goerli
Etherscan(opens in a new tab)](https://goerli.etherscan.io) and search for
your transaction hash.

## Part 3: Publish your Smart Contract to Etherscan

You did all the hard work of bringing your smart contract to life; now it's
time to share it with the world!

By verifying your smart contract on Etherscan, anyone can view your source
code and interact with your smart contract. Let's get started!

### Step 1: Generate an API Key on your Etherscan account

An Etherscan API Key is necessary to verify that you own the smart contract
you are trying to publish.

If you don't have an Etherscan account already, [sign up for an account(opens
in a new tab)](https://etherscan.io/register).

Once logged in, find your username in the navigation bar, hover over it and
select the **My profile** button.

On your profile page, you should see a side navigation bar. From the side
navigation bar, select **API Keys**. Next, press the "Add" button to create a
new API key, name your app **hello-world** and press the **Create New API
Key** button.

Your new API key should appear in the API key table. Copy the API key to your
clipboard.

Next, we need to add the Etherscan API key to our `.env` file.

After adding it, your `.env`file should look like this:

    
    
    1API_URL = "https://eth-goerli.alchemyapi.io/v2/your-api-key"
    
    2PUBLIC_KEY = "your-public-account-address"
    
    3PRIVATE_KEY = "your-private-account-address"
    
    4CONTRACT_ADDRESS = "your-contract-address"
    
    5ETHERSCAN_API_KEY = "your-etherscan-key"

### Hardhat-deployed smart contracts

#### Install hardhat-etherscan

Publishing your contract to Etherscan using Hardhat is straightforward. You
will first need to install the `hardhat-etherscan` plugin to get started.
`hardhat-etherscan` will automatically verify the smart contract's source code
and ABI on Etherscan. To add this, in the `hello-world` directory run:

    
    
    1npm install --save-dev @nomiclabs/hardhat-etherscan

Once installed, include the following statement at the top of your
`hardhat.config.js`, and add the Etherscan config options:

    
    
    1// hardhat.config.js
    
    2
    
    3require("dotenv").config()
    
    4require("@nomiclabs/hardhat-ethers")
    
    5require("@nomiclabs/hardhat-etherscan")
    
    6
    
    7const { API_URL, PRIVATE_KEY, ETHERSCAN_API_KEY } = process.env
    
    8
    
    9module.exports = {
    
    10  solidity: "0.7.3",
    
    11  defaultNetwork: "goerli",
    
    12  networks: {
    
    13    hardhat: {},
    
    14    goerli: {
    
    15      url: API_URL,
    
    16      accounts: [`0x${PRIVATE_KEY}`],
    
    17    },
    
    18  },
    
    19  etherscan: {
    
    20    // Your API key for Etherscan
    
    21    // Obtain one at https://etherscan.io/
    
    22    apiKey: ETHERSCAN_API_KEY,
    
    23  },
    
    24}
    
    Show all

#### Verify your smart contract on Etherscan

Ensure all files are saved and all `.env` variables are correctly configured.

Run the `verify` task, passing the contract address, and the network to where
it's deployed:

    
    
    1npx hardhat verify --network goerli DEPLOYED_CONTRACT_ADDRESS 'Hello World!'

Make sure that `DEPLOYED_CONTRACT_ADDRESS` is the address of your deployed
smart contract on the Goerli test network. Also, the final argument (`'Hello
World!'`) must be the same string value used during the deploy step in part 1.

If all goes well, you will see the following message in your terminal:

    
    
    1Successfully submitted source code for contract
    
    2contracts/HelloWorld.sol:HelloWorld at 0xdeployed-contract-address
    
    3for verification on Etherscan. Waiting for verification result...
    
    4
    
    5
    
    6Successfully verified contract HelloWorld on Etherscan.
    
    7https://goerli.etherscan.io/address/<contract-address>#contracts

Congrats! Your smart contract code is on Etherescan!

### Check out your smart contract on Etherscan!

When you navigate to the link provided in your terminal, you should be able to
see your smart contract code and ABI published on Etherscan!

**Wahooo - you did it champ! Now anyone can call or write to your smart
contract! We can't wait to see what you build next!**

## Part 4 - Integrating your smart contract with the frontend

By the end of this tutorial, you'll know how to:

  * Connect a MetaMask wallet to your dapp
  * Read data from your smart contract using the [Alchemy Web3(opens in a new tab)](https://docs.alchemy.com/alchemy/documentation/alchemy-web3) API
  * Sign Ethereum transactions using MetaMask

For this dapp, we'll be using [React(opens in a new
tab)](https://reactjs.org/) as our frontend framework; however, it's important
to note that we won't be spending much time breaking down its fundamentals, as
we'll mostly be focusing on bringing Web3 functionality to our project.

As a prerequisite, you should have a beginner-level understanding of React. If
not, we recommend completing the official [Intro to React tutorial(opens in a
new tab)](https://reactjs.org/tutorial/tutorial.html).

### Clone the starter files

First, go to the [hello-world-part-four GitHub repository(opens in a new
tab)](https://github.com/alchemyplatform/hello-world-part-four-tutorial) to
get the starter files for this project and clone this repository to your local
machine.

Open the cloned repository locally. Notice that it contains two folders:
`starter-files` and `completed`.

  * `starter-files`\- **we will be working in this directory** , we will connect the UI to your Ethereum wallet and the smart contract we published to Etherscan in Part 3.
  * `completed` contains the entire completed tutorial and should only be used as a reference if you get stuck.

Next, open your copy of `starter-files` to your favorite code editor, and then
navigate into the `src` folder.

All of the code we'll write will live under the `src` folder. We'll be editing
the `HelloWorld.js` component and the `util/interact.js` JavaScript files to
give our project Web3 functionality.

### Check out the starter files

Before we start coding, let's explore what is provided to us in the starter
files.

#### Get your react project running

Let's start by running the React project in our browser. The beauty of React
is that once we have our project running in our browser, any changes we save
will be updated live in our browser.

To get the project running, navigate to the root directory of the `starter-
files` folder, and the run `npm install` in your terminal to install the
dependencies of the project:

    
    
    cd starter-files
    
    npm install

Once those have finished installing, run `npm start` in your terminal:

    
    
    npm start

Doing so should open <http://localhost:3000/>[(opens in a new
tab)](http://localhost:3000/) in your browser, where you'll see the frontend
for our project. It should consist of one field (a place to update the message
stored in your smart contract), a "Connect Wallet" button, and an "Update"
button.

If you try clicking either button, you'll notice that they don't work—that's
because we still need to program their functionality.

#### The `HelloWorld.js`component

Let's go back into the `src` folder in our editor and open the `HelloWorld.js`
file. It's super important that we understand everything in this file, as it
is the primary React component we will be working on.

At the top of this file, you'll notice we have several import statements that
are necessary to get our project running, including the React library,
useEffect and useState hooks, some items from the `./util/interact.js` (we'll
describe them in more details soon!), and the Alchemy logo.

    
    
    1// HelloWorld.js
    
    2
    
    3import React from "react"
    
    4import { useEffect, useState } from "react"
    
    5import {
    
    6  helloWorldContract,
    
    7  connectWallet,
    
    8  updateMessage,
    
    9  loadCurrentMessage,
    
    10  getCurrentWalletConnected,
    
    11} from "./util/interact.js"
    
    12
    
    13import alchemylogo from "./alchemylogo.svg"
    
    Show all

Next, we have our state variables that we will update after specific events.

    
    
    1// HelloWorld.js
    
    2
    
    3//State variables
    
    4const [walletAddress, setWallet] = useState("")
    
    5const [status, setStatus] = useState("")
    
    6const [message, setMessage] = useState("No connection to the network.")
    
    7const [newMessage, setNewMessage] = useState("")

Here's what each of the variables represents:

  * `walletAddress` \- a string that stores the user's wallet address
  * `status`\- a string that stores a helpful message that guides the user on how to interact with the dapp
  * `message` \- a string that stores the current message in the smart contract
  * `newMessage` \- a string that stores the new message that will be written to the smart contract

After the state variables, you'll see five un-implemented functions:
`useEffect` ,`addSmartContractListener`, `addWalletListener` ,
`connectWalletPressed`, and `onUpdatePressed`. We'll explain what they do
below:

    
    
    1// HelloWorld.js
    
    2
    
    3//called only once
    
    4useEffect(async () => {
    
    5  //TODO: implement
    
    6}, [])
    
    7
    
    8function addSmartContractListener() {
    
    9  //TODO: implement
    
    10}
    
    11
    
    12function addWalletListener() {
    
    13  //TODO: implement
    
    14}
    
    15
    
    16const connectWalletPressed = async () => {
    
    17  //TODO: implement
    
    18}
    
    19
    
    20const onUpdatePressed = async () => {
    
    21  //TODO: implement
    
    22}
    
    Show all

  * [`useEffect`(opens in a new tab)](https://reactjs.org/docs/hooks-effect.html)\- this is a React hook that is called after your component is rendered. Because it has an empty array `[]` prop passed into it (see line 4), it will only be called on the component's _first_ render. Here we'll load the current message stored in our smart contract, call our smart contract and wallet listeners, and update our UI to reflect whether a wallet is already connected.
  * `addSmartContractListener`\- this function sets up a listener that will watch for our HelloWorld contract's `UpdatedMessages` event and update our UI when the message is changed in our smart contract.
  * `addWalletListener`\- this function sets up a listener that detects changes in the user's MetaMask wallet state, such as when the user disconnects their wallet or switches addresses.
  * `connectWalletPressed`\- this function will be called to connect the user's MetaMask wallet to our dapp.
  * `onUpdatePressed` \- this function will be called when the user wants to update the message stored in the smart contract.

Near the end of this file, we have the UI of our component.

    
    
    1// HelloWorld.js
    
    2
    
    3//the UI of our component
    
    4return (
    
    5  <div id="container">
    
    6    <img id="logo" src={alchemylogo}></img>
    
    7    <button id="walletButton" onClick={connectWalletPressed}>
    
    8      {walletAddress.length > 0 ? (
    
    9        "Connected: " +
    
    10        String(walletAddress).substring(0, 6) +
    
    11        "..." +
    
    12        String(walletAddress).substring(38)
    
    13      ) : (
    
    14        <span>Connect Wallet</span>
    
    15      )}
    
    16    </button>
    
    17
    
    18    <h2 style={{ paddingTop: "50px" }}>Current Message:</h2>
    
    19    <p>{message}</p>
    
    20
    
    21    <h2 style={{ paddingTop: "18px" }}>New Message:</h2>
    
    22
    
    23    <div>
    
    24      <input
    
    25        type="text"
    
    26        placeholder="Update the message in your smart contract."
    
    27        onChange={(e) => setNewMessage(e.target.value)}
    
    28        value={newMessage}
    
    29      />
    
    30      <p id="status">{status}</p>
    
    31
    
    32      <button id="publishButton" onClick={onUpdatePressed}>
    
    33        Update
    
    34      </button>
    
    35    </div>
    
    36  </div>
    
    37)
    
    Show all

If you scan this code carefully, you'll notice where we use our various state
variables in our UI:

  * On lines 6-12, if the user's wallet is connected (i.e. `walletAddress.length > 0`), we display a truncated version of the user `walletAddress` in the button with ID "walletButton;" otherwise it simply says "Connect Wallet."
  * On line 17, we display the current message stored in the smart contract, which is captured in the `message` string.
  * On lines 23-26, we use a [controlled component(opens in a new tab)](https://reactjs.org/docs/forms.html#controlled-components) to update our `newMessage` state variable when the input in the text field changes.

In addition to our state variables, you'll also see that
`connectWalletPressed` and `onUpdatePressed` functions are called when the
buttons with IDs `publishButton` and `walletButton` are clicked respectively.

Finally, let's address where is this `HelloWorld.js` component added.

If you go to the `App.js` file, which is the main component in React that acts
as a container for all other components, you'll see that our `HelloWorld.js`
component is injected on line 7.

Last but not least, let's check out one more file provided for you, the
`interact.js` file.

#### The `interact.js`file

Because we want to prescribe to the [M-V-C(opens in a new
tab)](https://en.wikipedia.org/wiki/Model%E2%80%93view%E2%80%93controller)
paradigm, we'll want a separate file that contains all our functions to manage
the logic, data, and rules of our dapp, and then be able to export those
functions to our frontend (our `HelloWorld.js` component).

👆🏽This is the exact purpose of our `interact.js` file!

Navigate to the `util` folder in your `src` directory, and you'll notice we've
included a file called `interact.js` that will contain all of our smart
contract interaction and wallet functions and variables.

    
    
    1// interact.js
    
    2
    
    3//export const helloWorldContract;
    
    4
    
    5export const loadCurrentMessage = async () => {}
    
    6
    
    7export const connectWallet = async () => {}
    
    8
    
    9const getCurrentWalletConnected = async () => {}
    
    10
    
    11export const updateMessage = async (message) => {}
    
    Show all

You'll notice at the top of the file that we've commented out the
`helloWorldContract` object. Later in this tutorial, we will uncomment this
object and instantiate our smart contract in this variable, which we will then
export into our `HelloWorld.js` component.

The four unimplemented functions after our `helloWorldContract` object do the
following:

  * `loadCurrentMessage` \- this function handles the logic of loading the current message stored in the smart contract. It will make a _read_ call to the Hello World smart contract using the [Alchemy Web3 API(opens in a new tab)](https://github.com/alchemyplatform/alchemy-web3).
  * `connectWallet` \- this function will connect the user's MetaMask to our dapp.
  * `getCurrentWalletConnected` \- this function will check if an Ethereum account is already connected to our dapp on page load and update our UI accordingly.
  * `updateMessage` \- this function will update the message stored in the smart contract. It will make a _write_ call to the Hello World smart contract, so the user's MetaMask wallet will have to sign an Ethereum transaction to update the message.

Now that we understand what we're working with, let's figure out how to read
from our smart contract!

### Step 3: Read from your smart contract

To read from your smart contract, you'll need to successfully set up:

  * An API connection to the Ethereum chain
  * A loaded instance of your smart contract
  * A function to call to your smart contract function
  * A listener to watch for updates when the data you're reading from the smart contract changes

This may sounds like a lot of steps, but don't worry! We'll walk you through
how to do each of them step-by-step! :)

#### Establish an API connection to the Ethereum chain

So remember how in Part 2 of this tutorial, we used our [Alchemy Web3 key to
read from our smart contract(opens in a new
tab)](https://docs.alchemy.com/alchemy/tutorials/hello-world-smart-
contract/interacting-with-a-smart-contract#step-1-install-web3-library)?
You'll also need an Alchemy Web3 key in your dapp to read from the chain.

If you don't have it already, first install [Alchemy Web3(opens in a new
tab)](https://github.com/alchemyplatform/alchemy-web3) by navigating to the
root directory of your `starter-files` and running the following in your
terminal:

    
    
    1npm install @alch/alchemy-web3

[Alchemy Web3(opens in a new tab)](https://github.com/alchemyplatform/alchemy-
web3) is a wrapper around [Web3.js(opens in a new
tab)](https://docs.web3js.org/), providing enhanced API methods and other
crucial benefits to make your life as a web3 developer easier. It is designed
to require minimal configuration so you can start using it in your app right
away!

Then, install the [dotenv(opens in a new
tab)](https://www.npmjs.com/package/dotenv) package in your project directory,
so we have a secure place to store our API key after we fetch it.

    
    
    1npm install dotenv --save

For our dapp, **we'll be using our Websockets API key** instead of our HTTP
API key, as it will allow us to set up a listener that detects when the
message stored in the smart contract changes.

Once you have your API key, create a `.env` file in your root directory and
add your Alchemy Websockets url to it. Afterwards, your `.env` file should
look like so:

    
    
    1REACT_APP_ALCHEMY_KEY = wss://eth-goerli.ws.alchemyapi.io/v2/<key>

Now, we're ready to set up our Alchemy Web3 endpoint in our dapp! Let's go
back to our `interact.js`, which is nested inside our `util` folder and add
the following code at the top of the file:

    
    
    1// interact.js
    
    2
    
    3require("dotenv").config()
    
    4const alchemyKey = process.env.REACT_APP_ALCHEMY_KEY
    
    5const { createAlchemyWeb3 } = require("@alch/alchemy-web3")
    
    6const web3 = createAlchemyWeb3(alchemyKey)
    
    7
    
    8//export const helloWorldContract;

Above, we first imported the Alchemy key from our `.env` file and then passed
our `alchemyKey` to `createAlchemyWeb3` to establish our Alchemy Web3
endpoint.

With this endpoint ready, it's time to load our smart contract!

#### Loading your Hello World smart contract

To load your Hello World smart contract, you'll need its contract address and
ABI, both of which can be found on Etherscan if you completed [Part 3 of this
tutorial.](/en/developers/tutorials/hello-world-smart-contract-
fullstack/#part-3-publish-your-smart-contract-to-etherscan-part-3-publish-
your-smart-contract-to-etherscan)

#### How to get your contract ABI from Etherscan

If you skipped Part 3 of this tutorial, you can use the HelloWorld contract
with address [0x6f3f635A9762B47954229Ea479b4541eAF402A6A(opens in a new
tab)](https://goerli.etherscan.io/address/0x6f3f635a9762b47954229ea479b4541eaf402a6a#code).
Its ABI can be found [here(opens in a new
tab)](https://goerli.etherscan.io/address/0x6f3f635a9762b47954229ea479b4541eaf402a6a#code).

A contract ABI is necessary for specifying which function a contract will
invoke as well ensuring that the function will return data in the format
you're expecting. Once we've copied our contract ABI, let's save it as a JSON
file called `contract-abi.json` in your `src` directory.

Your contract-abi.json should be stored in your src folder.

Armed with our contract address, ABI, and Alchemy Web3 endpoint, we can use
the [contract method(opens in a new
tab)](https://docs.web3js.org/api/web3-eth-contract/class/Contract) to load an
instance of our smart contract. Import your contract ABI into the
`interact.js` file and add your contract address.

    
    
    1// interact.js
    
    2
    
    3const contractABI = require("../contract-abi.json")
    
    4const contractAddress = "0x6f3f635A9762B47954229Ea479b4541eAF402A6A"

We can now finally uncomment our `helloWorldContract` variable, and load the
smart contract using our AlchemyWeb3 endpoint:

    
    
    1// interact.js
    
    2export const helloWorldContract = new web3.eth.Contract(
    
    3  contractABI,
    
    4  contractAddress
    
    5)

To recap, the first 12 lines of your `interact.js` should now look like this:

    
    
    1// interact.js
    
    2
    
    3require("dotenv").config()
    
    4const alchemyKey = process.env.REACT_APP_ALCHEMY_KEY
    
    5const { createAlchemyWeb3 } = require("@alch/alchemy-web3")
    
    6const web3 = createAlchemyWeb3(alchemyKey)
    
    7
    
    8const contractABI = require("../contract-abi.json")
    
    9const contractAddress = "0x6f3f635A9762B47954229Ea479b4541eAF402A6A"
    
    10
    
    11export const helloWorldContract = new web3.eth.Contract(
    
    12  contractABI,
    
    13  contractAddress
    
    14)
    
    Show all

Now that we have our contract loaded, we can implement our
`loadCurrentMessage` function!

#### Implementing `loadCurrentMessage` in your `interact.js`file

This function is super simple. We're going make a simple async web3 call to
read from our contract. Our function will return the message stored in the
smart contract:

Update the `loadCurrentMessage` in your `interact.js` file to the following:

    
    
    1// interact.js
    
    2
    
    3export const loadCurrentMessage = async () => {
    
    4  const message = await helloWorldContract.methods.message().call()
    
    5  return message
    
    6}

Since we want to display this smart contract in our UI, let's update the
`useEffect` function in our `HelloWorld.js` component to the following:

    
    
    1// HelloWorld.js
    
    2
    
    3//called only once
    
    4useEffect(async () => {
    
    5  const message = await loadCurrentMessage()
    
    6  setMessage(message)
    
    7}, [])

Note, we only want our `loadCurrentMessage` to be called once during the
component's first render. We'll soon implement `addSmartContractListener` to
automatically update the UI after the message in the smart contract changes.

Before we dive into our listener, let's check out what we have so far! Save
your `HelloWorld.js` and `interact.js` files, and then go to
<http://localhost:3000/>[(opens in a new tab)](http://localhost:3000/)

You'll notice that the current message no longer says "No connection to the
network." Instead it reflects the message stored in the smart contract. Sick!

#### Your UI should now reflect the message stored in the smart contract

Now speaking of that listener...

#### Implement `addSmartContractListener`

If you think back to the `HelloWorld.sol` file we wrote in [Part 1 of this
tutorial series(opens in a new
tab)](https://docs.alchemy.com/alchemy/tutorials/hello-world-smart-
contract#step-10-write-our-contract), you'll recall that there is a smart
contract event called `UpdatedMessages` that is emitted after our smart
contract's `update` function is invoked (see lines 9 and 27):

    
    
    1// HelloWorld.sol
    
    2
    
    3// Specifies the version of Solidity, using semantic versioning.
    
    4// Learn more: https://solidity.readthedocs.io/en/v0.5.10/layout-of-source-files.html#pragma
    
    5pragma solidity ^0.7.3;
    
    6
    
    7// Defines a contract named `HelloWorld`.
    
    8// A contract is a collection of functions and data (its state). Once deployed, a contract resides at a specific address on the Ethereum blockchain. Learn more: https://solidity.readthedocs.io/en/v0.5.10/structure-of-a-contract.html
    
    9contract HelloWorld {
    
    10
    
    11   //Emitted when update function is called
    
    12   //Smart contract events are a way for your contract to communicate that something happened on the blockchain to your app front-end, which can be 'listening' for certain events and take action when they happen.
    
    13   event UpdatedMessages(string oldStr, string newStr);
    
    14
    
    15   // Declares a state variable `message` of type `string`.
    
    16   // State variables are variables whose values are permanently stored in contract storage. The keyword `public` makes variables accessible from outside a contract and creates a function that other contracts or clients can call to access the value.
    
    17   string public message;
    
    18
    
    19   // Similar to many class-based object-oriented languages, a constructor is a special function that is only executed upon contract creation.
    
    20   // Constructors are used to initialize the contract's data. Learn more:https://solidity.readthedocs.io/en/v0.5.10/contracts.html#constructors
    
    21   constructor(string memory initMessage) {
    
    22
    
    23      // Accepts a string argument `initMessage` and sets the value into the contract's `message` storage variable).
    
    24      message = initMessage;
    
    25   }
    
    26
    
    27   // A public function that accepts a string argument and updates the `message` storage variable.
    
    28   function update(string memory newMessage) public {
    
    29      string memory oldMsg = message;
    
    30      message = newMessage;
    
    31      emit UpdatedMessages(oldMsg, newMessage);
    
    32   }
    
    33}
    
    Show all

Smart contract events are a way for your contract to communicate that
something happened (i.e. there was an _event_) on the blockchain to your
front-end application, which can be 'listening' for specific events and take
action when they happen.

The `addSmartContractListener` function is going to specifically listen for
our Hello World smart contract's `UpdatedMessages` event, and update our UI to
display the new message.

Modify `addSmartContractListener` to the following:

    
    
    1// HelloWorld.js
    
    2
    
    3function addSmartContractListener() {
    
    4  helloWorldContract.events.UpdatedMessages({}, (error, data) => {
    
    5    if (error) {
    
    6      setStatus("😥 " + error.message)
    
    7    } else {
    
    8      setMessage(data.returnValues[1])
    
    9      setNewMessage("")
    
    10      setStatus("🎉 Your message has been updated!")
    
    11    }
    
    12  })
    
    13}
    
    Show all

Let's break down what happens when the listener detects an event:

  * If an error occurs when the event is emitted, it will be reflected in the UI via our `status` state variable.
  * Otherwise, we will use the `data` object returned. The `data.returnValues` is an array indexed at zero where the first element in the array stores the previous message and second element stores the updated one. Altogether, on a successful event we'll set our `message` string to the updated message, clear the `newMessage` string, and update our `status` state variable to reflect that a new message has been published on our smart contract.

Finally, let's call our listener in our `useEffect` function so it is
initialized on the `HelloWorld.js` component's first render. Altogether, your
`useEffect` function should look like this:

    
    
    1// HelloWorld.js
    
    2
    
    3useEffect(async () => {
    
    4  const message = await loadCurrentMessage()
    
    5  setMessage(message)
    
    6  addSmartContractListener()
    
    7}, [])

Now that we're able to read from our smart contract, it would be great to
figure out how to write to it too! However, to write to our dapp, we must
first have an Ethereum wallet connected to it.

So, next we'll tackle setting up our Ethereum wallet (MetaMask) and then
connecting it to our dapp!

### Step 4: Set up your Ethereum wallet

To write anything to the Ethereum chain, users must sign transactions using
their virtual wallet's private keys. For this tutorial, we’ll use
[MetaMask(opens in a new tab)](https://metamask.io/), a virtual wallet in the
browser used to manage your Ethereum account address, as it makes this
transaction signing super easy for the end-user.

If you want to understand more about how transactions on Ethereum work, check
out [this page](/en/developers/docs/transactions/) from the Ethereum
foundation.

#### Download MetaMask

You can download and create a MetaMask account for free [here(opens in a new
tab)](https://metamask.io/download.html). When you are creating an account, or
if you already have an account, make sure to switch over to the “Goerli Test
Network” in the upper right (so that we’re not dealing with real money).

#### Add ether from a Faucet

To sign a transaction on the Ethereum blockchain, we’ll need some fake Eth. To
get Eth you can go to the [FaucETH(opens in a new
tab)](https://fauceth.komputing.org) and enter your Goerli account address,
click “Request funds”, then select “Ethereum Testnet Goerli” in the dropdown
and finally click “Request funds” button again. You should see Eth in your
MetaMask account soon after!

#### Check your Balance

To double check our balance is there, let’s make an [eth_getBalance(opens in a
new tab)](https://docs.alchemyapi.io/alchemy/documentation/alchemy-api-
reference/json-rpc#eth_getbalance) request using [Alchemy’s composer
tool(opens in a new
tab)](https://composer.alchemyapi.io/?composer_state=%7B%22network%22%3A0%2C%22methodName%22%3A%22eth_getBalance%22%2C%22paramValues%22%3A%5B%22%22%2C%22latest%22%5D%7D).
This will return the amount of Eth in our wallet. After you input your
MetaMask account address and click “Send Request”, you should see a response
like this:

    
    
    1{"jsonrpc": "2.0", "id": 0, "result": "0xde0b6b3a7640000"}

**NOTE:** This result is in wei not eth. Wei is used as the smallest
denomination of ether. The conversion from wei to eth is: 1 eth = 10¹⁸ wei. So
if we convert 0xde0b6b3a7640000 to decimal we get 1*10¹⁸ which equals 1 eth.

Phew! Our fake money is all there! 🤑

### Step 5: Connect MetaMask to your UI

Now that our MetaMask wallet is set up, let's connect our dapp to it!

#### The `connectWallet`function

In our `interact.js`file, let's implement the `connectWallet` function, which
we can then call in our `HelloWorld.js` component.

Let's modify `connectWallet` to the following:

    
    
    1// interact.js
    
    2
    
    3export const connectWallet = async () => {
    
    4  if (window.ethereum) {
    
    5    try {
    
    6      const addressArray = await window.ethereum.request({
    
    7        method: "eth_requestAccounts",
    
    8      })
    
    9      const obj = {
    
    10        status: "👆🏽 Write a message in the text-field above.",
    
    11        address: addressArray[0],
    
    12      }
    
    13      return obj
    
    14    } catch (err) {
    
    15      return {
    
    16        address: "",
    
    17        status: "😥 " + err.message,
    
    18      }
    
    19    }
    
    20  } else {
    
    21    return {
    
    22      address: "",
    
    23      status: (
    
    24        <span>
    
    25          <p>
    
    26            {" "}
    
    27            🦊 <a target="_blank" href={`https://metamask.io/download.html`}>
    
    28              You must install MetaMask, a virtual Ethereum wallet, in your
    
    29              browser.
    
    30            </a>
    
    31          </p>
    
    32        </span>
    
    33      ),
    
    34    }
    
    35  }
    
    36}
    
    Show all

So what does this giant block of code do exactly?

Well, first, it checks if it `window.ethereum` is enabled in your browser.

`window.ethereum` is a global API injected by MetaMask and other wallet
providers that allows websites to request users' Ethereum accounts. If
approved, it can read data from the blockchains the user is connected to, and
suggest that the user sign messages and transactions . Check out the [MetaMask
docs(opens in a new tab)](https://docs.metamask.io/guide/ethereum-
provider.html#table-of-contents) for more info!

If `window.ethereum` _is not_ present, then that means MetaMask is not
installed. This results in a JSON object being returned, where `address`
returned is an empty string, and the `status` JSX object relays that the user
must install MetaMask.

Now if `window.ethereum` _is_ present, then that's when things get
interesting.

Using a try/catch loop, we'll try to connect to MetaMask by calling
[`window.ethereum.request({ method: "eth_requestAccounts" });`(opens in a new
tab)](https://docs.metamask.io/guide/rpc-api.html#eth-requestaccounts).
Calling this function will open up MetaMask in the browser, whereby the user
will be prompted to connect their wallet to your dapp.

  * If the user chooses to connect, `method: "eth_requestAccounts"` will return an array that contains all of the user's account addresses that connected to the dapp. Altogether, our `connectWallet` function will return a JSON object that contains the _first_ `address` in this array (see line 9) and a `status` message that prompts the user to write a message to the smart contract.
  * If the user rejects the connection, then the JSON object will contain an empty string for the `address` returned and a `status` message that reflects that the user rejected the connection.

Now that we've written this `connectWallet` function, the next step is to call
it to our `HelloWorld.js`component.

#### Add the `connectWallet` function to your `HelloWorld.js`UI Component

Navigate to the `connectWalletPressed` function in `HelloWorld.js`, and update
it to the following:

    
    
    1// HelloWorld.js
    
    2
    
    3const connectWalletPressed = async () => {
    
    4  const walletResponse = await connectWallet()
    
    5  setStatus(walletResponse.status)
    
    6  setWallet(walletResponse.address)
    
    7}

Notice how most of our functionality is abstracted away from our
`HelloWorld.js` component from the `interact.js` file? This is so we comply
with the M-V-C paradigm!

In `connectWalletPressed`, we simply make an await call to our imported
`connectWallet` function, and using its response, we update our `status` and
`walletAddress` variables via their state hooks.

Now, let's save both files (`HelloWorld.js` and `interact.js`) and test out
our UI so far.

Open your browser on the <http://localhost:3000/>[(opens in a new
tab)](http://localhost:3000/) page, and press the "Connect Wallet" button on
the top right of the page.

If you have MetaMask installed, you should be prompted to connect your wallet
to your dapp. Accept the invitation to connect.

You should see that the wallet button now reflects that your address is
connected! Yasssss 🔥

Next, try refreshing the page... this is strange. Our wallet button is
prompting us to connect MetaMask, even though it is already connected...

However, have no fear! We easily can address that (get it?) by implementing
`getCurrentWalletConnected`, which will check if an address is already
connected to our dapp and update our UI accordingly!

#### The `getCurrentWalletConnected`function

Update your `getCurrentWalletConnected` function in the `interact.js` file to
the following:

    
    
    1// interact.js
    
    2
    
    3export const getCurrentWalletConnected = async () => {
    
    4  if (window.ethereum) {
    
    5    try {
    
    6      const addressArray = await window.ethereum.request({
    
    7        method: "eth_accounts",
    
    8      })
    
    9      if (addressArray.length > 0) {
    
    10        return {
    
    11          address: addressArray[0],
    
    12          status: "👆🏽 Write a message in the text-field above.",
    
    13        }
    
    14      } else {
    
    15        return {
    
    16          address: "",
    
    17          status: "🦊 Connect to MetaMask using the top right button.",
    
    18        }
    
    19      }
    
    20    } catch (err) {
    
    21      return {
    
    22        address: "",
    
    23        status: "😥 " + err.message,
    
    24      }
    
    25    }
    
    26  } else {
    
    27    return {
    
    28      address: "",
    
    29      status: (
    
    30        <span>
    
    31          <p>
    
    32            {" "}
    
    33            🦊 <a target="_blank" href={`https://metamask.io/download.html`}>
    
    34              You must install MetaMask, a virtual Ethereum wallet, in your
    
    35              browser.
    
    36            </a>
    
    37          </p>
    
    38        </span>
    
    39      ),
    
    40    }
    
    41  }
    
    42}
    
    Show all

This code is _very_ similar to the `connectWallet` function we just wrote in
the previous step.

The main difference is that instead of calling the method
`eth_requestAccounts`, which opens MetaMask for the user to connect their
wallet, here we call the method `eth_accounts`, which simply returns an array
containing the MetaMask addresses currently connected to our dapp.

To see this function in action, let's call it in our `useEffect` function of
our `HelloWorld.js` component:

    
    
    1// HelloWorld.js
    
    2
    
    3useEffect(async () => {
    
    4  const message = await loadCurrentMessage()
    
    5  setMessage(message)
    
    6  addSmartContractListener()
    
    7
    
    8  const { address, status } = await getCurrentWalletConnected()
    
    9  setWallet(address)
    
    10  setStatus(status)
    
    11}, [])
    
    Show all

Notice, we use the response of our call to `getCurrentWalletConnected` to
update our `walletAddress` and `status` state variables.

Now that you've added this code, let's try refreshing our browser window.

Niceeeee! The button should say that you're connected, and show a preview of
your connected wallet's address - even after you refresh!

#### Implement `addWalletListener`

The final step in our dapp wallet setup is implementing the wallet listener so
our UI updates when our wallet's state changes, such as when the user
disconnects or switches accounts.

In your `HelloWorld.js` file, modify your `addWalletListener` function as the
following:

    
    
    1// HelloWorld.js
    
    2
    
    3function addWalletListener() {
    
    4  if (window.ethereum) {
    
    5    window.ethereum.on("accountsChanged", (accounts) => {
    
    6      if (accounts.length > 0) {
    
    7        setWallet(accounts[0])
    
    8        setStatus("👆🏽 Write a message in the text-field above.")
    
    9      } else {
    
    10        setWallet("")
    
    11        setStatus("🦊 Connect to MetaMask using the top right button.")
    
    12      }
    
    13    })
    
    14  } else {
    
    15    setStatus(
    
    16      <p>
    
    17        {" "}
    
    18        🦊 <a target="_blank" href={`https://metamask.io/download.html`}>
    
    19          You must install MetaMask, a virtual Ethereum wallet, in your browser.
    
    20        </a>
    
    21      </p>
    
    22    )
    
    23  }
    
    24}
    
    Show all

I bet you don't even need our help to understand what's going on here at this
point, but for thoroughness purposes, let's quickly break it down:

  * First, our function checks if `window.ethereum` is enabled (i.e. MetaMask is installed).
    * If it's not, we simply set our `status` state variable to a JSX string that prompts the user to install MetaMask.
    * If it is enabled, we set up the listener `window.ethereum.on("accountsChanged")` on line 3 that listens for state changes in the MetaMask wallet, which include when the user connects an additional account to the dapp, switches accounts, or disconnects an account. If there is at least one account connected, the `walletAddress` state variable is updated as the first account in the `accounts` array returned by the listener. Otherwise, `walletAddress` is set as an empty string.

Last but not least, we must call it in our `useEffect` function:

    
    
    1// HelloWorld.js
    
    2
    
    3useEffect(async () => {
    
    4  const message = await loadCurrentMessage()
    
    5  setMessage(message)
    
    6  addSmartContractListener()
    
    7
    
    8  const { address, status } = await getCurrentWalletConnected()
    
    9  setWallet(address)
    
    10  setStatus(status)
    
    11
    
    12  addWalletListener()
    
    13}, [])
    
    Show all

And that's it! We've successfully completed programming all of our wallet
functionality! Now onto our last task: updating the message stored in our
smart contract!

### Step 6: Implement the `updateMessage`function

Alrighty fam, we've arrived at the home stretch! In the `updateMessage` of
your `interact.js` file, we're going to do the following:

  1. Make sure the message we wish to publish in our smart contact is valid
  2. Sign our transaction using MetaMask
  3. Call this function from our `HelloWorld.js` frontend component

This won't take very long; let's finish this dapp!

#### Input error handling

Naturally, it makes sense to have some sort of input error handling at the
start of the function.

We'll want our function to return early if there is no MetaMask extension
installed, there is no wallet connected (i.e. the `address` passed in is an
empty string), or the `message` is an empty string. Let's add the following
error handling to `updateMessage`:

    
    
    1// interact.js
    
    2
    
    3export const updateMessage = async (address, message) => {
    
    4  if (!window.ethereum || address === null) {
    
    5    return {
    
    6      status:
    
    7        "💡 Connect your MetaMask wallet to update the message on the blockchain.",
    
    8    }
    
    9  }
    
    10
    
    11  if (message.trim() === "") {
    
    12    return {
    
    13      status: "❌ Your message cannot be an empty string.",
    
    14    }
    
    15  }
    
    16}
    
    Show all

Now that it have proper input error handling, it's time to sign the
transaction via MetaMask!

#### Signing our transaction

If you're already comfortable with traditional web3 Ethereum transactions, the
code we write next will be very familiar. Below your input error handling
code, add the following to `updateMessage`:

    
    
    1// interact.js
    
    2
    
    3//set up transaction parameters
    
    4const transactionParameters = {
    
    5  to: contractAddress, // Required except during contract publications.
    
    6  from: address, // must match user's active address.
    
    7  data: helloWorldContract.methods.update(message).encodeABI(),
    
    8}
    
    9
    
    10//sign the transaction
    
    11try {
    
    12  const txHash = await window.ethereum.request({
    
    13    method: "eth_sendTransaction",
    
    14    params: [transactionParameters],
    
    15  })
    
    16  return {
    
    17    status: (
    
    18      <span>
    
    19        ✅{" "}
    
    20        <a target="_blank" href={`https://goerli.etherscan.io/tx/${txHash}`}>
    
    21          View the status of your transaction on Etherscan!
    
    22        </a>
    
    23        <br />
    
    24        ℹ️ Once the transaction is verified by the network, the message will be
    
    25        updated automatically.
    
    26      </span>
    
    27    ),
    
    28  }
    
    29} catch (error) {
    
    30  return {
    
    31    status: "😥 " + error.message,
    
    32  }
    
    33}
    
    Show all

Let's breakdown what's happening. First, we set up our transactions
parameters, where:

  * `to` specifies the recipient address (our smart contract)
  * `from` specifies the signer of the transaction, the `address` variable we passed into our function
  * `data` contains the call to our Hello World smart contract's `update` method, receiving our `message` string variable as input

Then, we make an await call, `window.ethereum.request`, where we ask MetaMask
to sign the transaction. Notice, on lines 11 and 12, we're specifying our eth
method, `eth_sendTransaction`and passing in our `transactionParameters`.

At this point, MetaMask will open up in the browser, and prompt the user to
sign or reject the transaction.

  * If the transaction is successful, the function will return a JSON object where the `status` JSX string prompts the user to check out Etherscan for more information about their transaction.
  * If the transaction fails, the function will return a JSON object where the `status` string relays the error message.

Altogether, our `updateMessage` function should look like this:

    
    
    1// interact.js
    
    2
    
    3export const updateMessage = async (address, message) => {
    
    4  //input error handling
    
    5  if (!window.ethereum || address === null) {
    
    6    return {
    
    7      status:
    
    8        "💡 Connect your MetaMask wallet to update the message on the blockchain.",
    
    9    }
    
    10  }
    
    11
    
    12  if (message.trim() === "") {
    
    13    return {
    
    14      status: "❌ Your message cannot be an empty string.",
    
    15    }
    
    16  }
    
    17
    
    18  //set up transaction parameters
    
    19  const transactionParameters = {
    
    20    to: contractAddress, // Required except during contract publications.
    
    21    from: address, // must match user's active address.
    
    22    data: helloWorldContract.methods.update(message).encodeABI(),
    
    23  }
    
    24
    
    25  //sign the transaction
    
    26  try {
    
    27    const txHash = await window.ethereum.request({
    
    28      method: "eth_sendTransaction",
    
    29      params: [transactionParameters],
    
    30    })
    
    31    return {
    
    32      status: (
    
    33        <span>
    
    34          ✅{" "}
    
    35          <a target="_blank" href={`https://goerli.etherscan.io/tx/${txHash}`}>
    
    36            View the status of your transaction on Etherscan!
    
    37          </a>
    
    38          <br />
    
    39          ℹ️ Once the transaction is verified by the network, the message will
    
    40          be updated automatically.
    
    41        </span>
    
    42      ),
    
    43    }
    
    44  } catch (error) {
    
    45    return {
    
    46      status: "😥 " + error.message,
    
    47    }
    
    48  }
    
    49}
    
    Show all

Last but not least, we need to connect our `updateMessage` function to our
`HelloWorld.js` component.

#### Connect `updateMessage` to the `HelloWorld.js`frontend

Our `onUpdatePressed` function should make an await call to the imported
`updateMessage` function and modify the `status` state variable to reflect
whether our transaction succeeded or failed:

    
    
    1// HelloWorld.js
    
    2
    
    3const onUpdatePressed = async () => {
    
    4  const { status } = await updateMessage(walletAddress, newMessage)
    
    5  setStatus(status)
    
    6}

It's super clean and simple. And guess what... YOUR DAPP IS COMPLETE!!!

Go ahead and test out the **Update** button!

### Make your own custom dapp

Wooooo, you made it to the end of the tutorial! To recap, you learned how to:

  * Connect a MetaMask wallet to your dapp project
  * Read data from your smart contract using the [Alchemy Web3(opens in a new tab)](https://docs.alchemy.com/alchemy/documentation/alchemy-web3) API
  * Sign Ethereum transactions using MetaMask

Now you're fully equipped to apply the skills from this tutorial to build out
your own custom dapp project! As always, if you have any questions, don't
hesitate to reach out to us for help in the [Alchemy Discord(opens in a new
tab)](https://discord.gg/gWuC7zB). 🧙‍♂️

Once you complete this tutorial, let us know how your experience was or if you
have any feedback by tagging us on Twitter [@alchemyplatform(opens in a new
tab)](https://twitter.com/AlchemyPlatform)!

w

Last edit: [@wackerow(opens in a new tab)](https://github.com/wackerow), May
7, 2024

See contributors

### Was this tutorial helpful?

YesNo

  * [Edit page(opens in a new tab)](https://github.com/ethereum/ethereum-org-website/tree/dev/public/content/developers/tutorials/hello-world-smart-contract-fullstack/index.md)
  * On this page

    * Part 1 - Create and Deploy your Smart Contract using Hardhat
      * Connect to the Ethereum network
      * Create your app and API key
      * Create an Ethereum account
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
    * Part 2: Interact with your Smart Contract
      * Create a interact.js file
      * Update your .env file
      * Grab your contract ABI
      * Create an instance of your contract
      * Read the init message
      * Update the message
      * Read the new message
    * Part 3: Publish your Smart Contract to Etherscan
      * Step 1: Generate an API Key on your Etherscan account
      * Hardhat-deployed smart contracts
      * Check out your smart contract on Etherscan!
    * Part 4 - Integrating your smart contract with the frontend
      * Clone the starter files
      * Check out the starter files
      * Step 3: Read from your smart contract
      * Step 4: Set up your Ethereum wallet
      * Step 5: Connect MetaMask to your UI
      * Step 6: Implement the updateMessage function
      * Make your own custom dapp

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

### Application Binary Interface (ABI)

A JSON file that defines the functions and variables included in a smart
contract. The ABI allows bytecode to be mapped into human-readable formats.

