Skip to main content

[](/en/)

  * Learn
  * Use
  * Build
  * Participate
  * Research

Search```K`

Languages EN

# Testing simple smart contract with Waffle library

smart contractssolidityWaffletesting

Beginner

![✍️](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/270d.svg)Ewa
Kowalska

![📆](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4c6.svg)
February 26, 2021

![⏱️](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/23f1.svg)6
minute read minute read

On this page

  * In this tutorial you'll learn how to
  * Assumptions

## In this tutorial you'll learn how to

  * Test the changes of wallet balance
  * Test emission of events with specified arguments
  * Assert that a transaction was reverted

## Assumptions

  * You can create a new JavaScript or TypeScript project
  * You have some basic experience with tests in JavaScript
  * You have used some package managers like yarn or npm
  * You possess very basic knowledge of smart contracts and Solidity

# Getting started

The tutorial demonstrates test setup and run using yarn, but there is no
problem if you prefer npm - I will provide proper references to the official
Waffle [documentation(opens in a new tab)](https://ethereum-
waffle.readthedocs.io/en/latest/index.html).

## Install Dependencies

[Add(opens in a new tab)](https://ethereum-
waffle.readthedocs.io/en/latest/getting-started.html#installation) ethereum-
waffle and typescript dependencies to the dev dependencies of your project.

    
    
    yarn add --dev ethereum-waffle ts-node typescript @types/jest

## Example smart contract

During the tutorial we'll work on a simple smart contract example -
EtherSplitter. It does not much apart from allowing anyone to send some wei
and split it evenly between two predefined receivers. The split function
requires the number of wei to be even, otherwise it will revert. For both
receivers it performs a wei transfer followed by emission of the Transfer
event.

Place the snippet of EtherSplitter code in `src/EtherSplitter.sol`.

    
    
    1pragma solidity ^0.6.0;
    
    2
    
    3contract EtherSplitter {
    
    4    address payable receiver1;
    
    5    address payable receiver2;
    
    6
    
    7    event Transfer(address from, address to, uint256 amount);
    
    8
    
    9    constructor(address payable _address1, address payable _address2) public {
    
    10        receiver1 = _address1;
    
    11        receiver2 = _address2;
    
    12    }
    
    13
    
    14    function split() public payable {
    
    15        require(msg.value % 2 == 0, 'Uneven wei amount not allowed');
    
    16        receiver1.transfer(msg.value / 2);
    
    17        emit Transfer(msg.sender, receiver1, msg.value / 2);
    
    18        receiver2.transfer(msg.value / 2);
    
    19        emit Transfer(msg.sender, receiver2, msg.value / 2);
    
    20    }
    
    21}
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

## Compile the contract

To [compile(opens in a new tab)](https://ethereum-
waffle.readthedocs.io/en/latest/getting-started.html#compiling-the-contract)
the contract add the following entry to the package.json file:

    
    
    1"scripts": {
    
    2    "build": "waffle"
    
    3  }
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Next, create the Waffle configuration file in the project root directory -
`waffle.json` \- and then paste the following configuration there:

    
    
    1{
    
    2  "compilerType": "solcjs",
    
    3  "compilerVersion": "0.6.2",
    
    4  "sourceDirectory": "./src",
    
    5  "outputDirectory": "./build"
    
    6}
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Run `yarn build`. As the result, the `build` directory will appear with the
EtherSplitter compiled contract in JSON format.

## Test setup

Testing with Waffle requires using Chai matchers and Mocha, so you need to
[add(opens in a new tab)](https://ethereum-
waffle.readthedocs.io/en/latest/getting-started.html#writing-tests) them to
your project. Update your package.json file and add the `test` entry in the
scripts part:

    
    
    1"scripts": {
    
    2    "build": "waffle",
    
    3    "test": "export NODE_ENV=test && mocha -r ts-node/register 'test/**/*.test.ts'"
    
    4  }
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

If you want to [execute(opens in a new tab)](https://ethereum-
waffle.readthedocs.io/en/latest/getting-started.html#running-tests) your
tests, just run `yarn test` .

# Testing

Now create the `test` directory and create the new file
`test\EtherSplitter.test.ts`. Copy the snippet below and paste it to our test
file.

    
    
    1import { expect, use } from "chai"
    
    2import { Contract } from "ethers"
    
    3import { deployContract, MockProvider, solidity } from "ethereum-waffle"
    
    4import EtherSplitter from "../build/EtherSplitter.json"
    
    5
    
    6use(solidity)
    
    7
    
    8describe("Ether Splitter", () => {
    
    9  const [sender, receiver1, receiver2] = new MockProvider().getWallets()
    
    10  let splitter: Contract
    
    11
    
    12  beforeEach(async () => {
    
    13    splitter = await deployContract(sender, EtherSplitter, [
    
    14      receiver1.address,
    
    15      receiver2.address,
    
    16    ])
    
    17  })
    
    18
    
    19  // add the tests here
    
    20})
    
    Show all

A few words before we start. The `MockProvider` comes up with a mock version
of the blockchain. It also delivers mock wallets that will serve us for
testing EtherSplitter contract. We can get up to ten wallets by calling
`getWallets()` method on the provider. In the example, we get three wallets -
for the sender and for two receivers.

Next, we declare a variable called 'splitter' - this is our mock EtherSplitter
contract. It is created before each execution of a single test by the
`deployContract` method. This method simulates deployment of a contract from
the wallet passed as the first parameter (sender's wallet in our case). The
second parameter is the ABI and the bytecode of the tested contract - we pass
there the json file of the compiled EtherSplitter contract from the `build`
directory. The third parameter is an array with the contract's constructor
arguments, which in our case, are the two addresses of the receivers.

## changeBalances

First, we will check if the split method actually changes the balances of
receivers' wallets. If we split 50 wei from senders account, we would expect
the balances of both receivers to increase by 25 wei. We will use Waffle's
`changeBalances` matcher:

    
    
    1it("Changes accounts balances", async () => {
    
    2  await expect(() => splitter.split({ value: 50 })).to.changeBalances(
    
    3    [receiver1, receiver2],
    
    4    [25, 25]
    
    5  )
    
    6})

As the first parameter of the matcher, we pass an array of receivers' wallets,
and as the second - an array of expected increases on corresponding accounts.
If we wanted to check the balance of one specific wallet, we could also use
`changeBalance` matcher, which does not require passing arrays, as in the
example below:

    
    
    1it("Changes account balance", async () => {
    
    2  await expect(() => splitter.split({ value: 50 })).to.changeBalance(
    
    3    receiver1,
    
    4    25
    
    5  )
    
    6})

Note that in both cases of `changeBalance` and `changeBalances` we pass the
split function as a callback because the matcher needs to access the state of
balances before and after the call.

Next, we'll test if the Transfer event was emitted after each transfer of wei.
We'll turn to another matcher from Waffle:

## Emit

    
    
    1it("Emits event on the transfer to the first receiver", async () => {
    
    2  await expect(splitter.split({ value: 50 }))
    
    3    .to.emit(splitter, "Transfer")
    
    4    .withArgs(sender.address, receiver1.address, 25)
    
    5})
    
    6
    
    7it("Emits event on the transfer to the second receiver", async () => {
    
    8  await expect(splitter.split({ value: 50 }))
    
    9    .to.emit(splitter, "Transfer")
    
    10    .withArgs(sender.address, receiver2.address, 25)
    
    11})
    
    Show all

The `emit` matcher allows us to check if a contract emitted an event on
calling a method. As the parameters to the `emit` matcher, we provide the mock
contract that we predict to emit the event, along with the name of that event.
In our case, the mock contract is `splitter` and the name of the event -
`Transfer`. We can also verify the precise values of arguments that the event
was emitted with - we pass as many arguments to `withArgs` matcher, as our
event declaration expects. In case of EtherSplitter contract, we pass the
addresses of the sender and the receiver along with the transferred wei
amount.

## revertedWith

As the last example, we'll check if the transaction was reverted in case of
uneven number of wei. We'll use `revertedWith` matcher:

    
    
    1it("Reverts when Vei amount uneven", async () => {
    
    2  await expect(splitter.split({ value: 51 })).to.be.revertedWith(
    
    3    "Uneven wei amount not allowed"
    
    4  )
    
    5})

The test, if passed, will assure us that the transaction was reverted indeed.
However, there must be also an exact match between the messages that we passed
in `require` statement and the message we expect in `revertedWith`. If we go
back to the code of EtherSplitter contract, in the `require` statement for the
wei amount, we provide the message: 'Uneven wei amount not allowed'. This
matches the message we expect in our test. If they were not equal, the test
would fail.

# Congratulations!

You've made your first big step towards testing smart contracts with Waffle!
You might be interested in other Waffle tutorials:

  * [Testing ERC20 with Waffle](/en/developers/tutorials/testing-erc-20-tokens-with-waffle/)
  * [Waffle: Dynamic mocking and testing contract calls](/en/developers/tutorials/waffle-dynamic-mocking-and-testing-calls/#gatsby-focus-wrapper)
  * [Waffle say hello world tutorial with hardhat and ethers](/en/developers/tutorials/waffle-say-hello-world-with-hardhat-and-ethers/)

n

Last edit: [@nhsz(opens in a new tab)](https://github.com/nhsz), February 27,
2024

See contributors

### Was this tutorial helpful?

YesNo

  * [Edit page(opens in a new tab)](https://github.com/ethereum/ethereum-org-website/tree/dev/public/content/developers/tutorials/waffle-test-simple-smart-contract/index.md)
  * On this page

    * In this tutorial you'll learn how to
    * Assumptions

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

