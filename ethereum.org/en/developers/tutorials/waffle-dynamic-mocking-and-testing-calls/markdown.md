Skip to main content

[](/en/)

  * Learn
  * Use
  * Build
  * Participate
  * Research

Search```K`

Languages EN

# Waffle: Dynamic mocking and testing contract calls

wafflesmart contractssoliditytestingmocking

Intermediate

![✍️](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/270d.svg)Daniel
Izdebski

![📆](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4c6.svg)
November 14, 2020

![⏱️](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/23f1.svg)7
minute read minute read

On this page

  * What is this tutorial about?
  * Dynamic mocking
    * 1\. Project
    * 2\. Smart contract
    * 3\. Testing
  * Testing contract calls
  * The Finish Line

## What is this tutorial about?

In this tutorial you will learn how to:

  * use dynamic mocking
  * test interactions between smart contracts

Assumptions:

  * you already know how to write a simple smart contract in `Solidity`
  * you know your way around `JavaScript` and `TypeScript`
  * you've done other `Waffle` tutorials or know a thing or two about it

## Dynamic mocking

Why is dynamic mocking useful? Well, it allows us to write unit tests instead
of integration tests. What does it mean? It means that we don't have to worry
about smart contracts' dependencies, thus we can test all of them in complete
isolation. Let me show you how exactly you can do it.

### **1\. Project**

Before we start we need to prepare a simple node.js project:

    
    
    mkdir dynamic-mocking
    
    cd dynamic-mocking
    
    mkdir contracts src
    
    yarn init
    
    # or if you're using npm
    
    npm init

Let's start with adding typescript and test dependencies - mocha & chai:

    
    
    yarn add --dev @types/chai @types/mocha chai mocha ts-node typescript
    
    # or if you're using npm
    
    npm install @types/chai @types/mocha chai mocha ts-node typescript --save-dev

Now let's add `Waffle` and `ethers`:

    
    
    yarn add --dev ethereum-waffle ethers
    
    # or if you're using npm
    
    npm install ethereum-waffle ethers --save-dev

Your project structure should look like this now:

    
    
    1.
    
    2├── contracts
    
    3├── package.json
    
    4└── test

### **2\. Smart contract**

To start dynamic mocking, we need a smart contract with dependencies. Don't
worry, I've got you covered!

Here's a simple smart contract written in `Solidity` whose sole purpose is to
check if we're rich. It uses ERC20 token to check if we have enough tokens.
Put it in `./contracts/AmIRichAlready.sol`.

    
    
    1pragma solidity ^0.6.2;
    
    2
    
    3interface IERC20 {
    
    4    function balanceOf(address account) external view returns (uint256);
    
    5}
    
    6
    
    7contract AmIRichAlready {
    
    8    IERC20 private tokenContract;
    
    9    uint public richness = 1000000 * 10 ** 18;
    
    10
    
    11    constructor (IERC20 _tokenContract) public {
    
    12        tokenContract = _tokenContract;
    
    13    }
    
    14
    
    15    function check() public view returns (bool) {
    
    16        uint balance = tokenContract.balanceOf(msg.sender);
    
    17        return balance > richness;
    
    18    }
    
    19}
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

As we want to use dynamic mocking we don't need the whole ERC20, that's why
we're using the IERC20 interface with only one function.

It's time to build this contract! For that we will use `Waffle`. First, we're
going to create a simple `waffle.json` config file which specifies compilation
options.

    
    
    1{
    
    2  "compilerType": "solcjs",
    
    3  "compilerVersion": "0.6.2",
    
    4  "sourceDirectory": "./contracts",
    
    5  "outputDirectory": "./build"
    
    6}
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Now we're ready to build the contract with Waffle:

    
    
    npx waffle

Easy, right? In `build/` folder two files corresponding to the contract and
the interface appeared. We will use them later for testing.

### **3\. Testing**

Let's create a file called `AmIRichAlready.test.ts` for the actual testing.
First of all, we have to handle the imports. We will need them for later:

    
    
    1import { expect, use } from "chai"
    
    2import { Contract, utils, Wallet } from "ethers"
    
    3import {
    
    4  deployContract,
    
    5  deployMockContract,
    
    6  MockProvider,
    
    7  solidity,
    
    8} from "ethereum-waffle"

Except for JS dependencies, we need to import our built contract and
interface:

    
    
    1import IERC20 from "../build/IERC20.json"
    
    2import AmIRichAlready from "../build/AmIRichAlready.json"

Waffle uses `chai` for testing. However, before we can use it, we have to
inject Waffle's matchers into chai itself:

    
    
    1use(solidity)

We need to implement `beforeEach()` function that will reset the state of the
contract before each test. Let's first think of what we need there. To deploy
a contract we need two things: a wallet and a deployed ERC20 contract to pass
it as an argument for the `AmIRichAlready` contract.

Firstly we create a wallet:

    
    
    1const [wallet] = new MockProvider().getWallets()

Then we need to deploy an ERC20 contract. Here's the tricky part - we have
only an interface. This is the part where Waffle comes to save us. Waffle has
a magical `deployMockContract()` function that creates a contract using solely
the _abi_ of the interface:

    
    
    1const mockERC20 = await deployMockContract(wallet, IERC20.abi)

Now with both the wallet and the deployed ERC20, we can go ahead and deploy
the `AmIRichAlready` contract:

    
    
    1const contract = await deployContract(wallet, AmIRichAlready, [
    
    2  mockERC20.address,
    
    3])

With all of that, our `beforeEach()` function is finished. So far your
`AmIRichAlready.test.ts` file should look like this:

    
    
    1import { expect, use } from "chai"
    
    2import { Contract, utils, Wallet } from "ethers"
    
    3import {
    
    4  deployContract,
    
    5  deployMockContract,
    
    6  MockProvider,
    
    7  solidity,
    
    8} from "ethereum-waffle"
    
    9
    
    10import IERC20 from "../build/IERC20.json"
    
    11import AmIRichAlready from "../build/AmIRichAlready.json"
    
    12
    
    13use(solidity)
    
    14
    
    15describe("Am I Rich Already", () => {
    
    16  let mockERC20: Contract
    
    17  let contract: Contract
    
    18  let wallet: Wallet
    
    19
    
    20  beforeEach(async () => {
    
    21    ;[wallet] = new MockProvider().getWallets()
    
    22    mockERC20 = await deployMockContract(wallet, IERC20.abi)
    
    23    contract = await deployContract(wallet, AmIRichAlready, [mockERC20.address])
    
    24  })
    
    25})
    
    Show all

Let's write the first test for the `AmIRichAlready` contract. What do you
think our test should be about? Yeah, you're right! We should check if we are
already rich :)

But wait a second. How will our mocked contract know what values to return? We
haven't implemented any logic for the `balanceOf()` function. Again, Waffle
can help here. Our mocked contract has some new fancy stuff to it now:

    
    
    1await mockERC20.mock.<nameOfMethod>.returns(<value>)
    
    2await mockERC20.mock.<nameOfMethod>.withArgs(<arguments>).returns(<value>)

With this knowledge we can finally write our first test:

    
    
    1it("returns false if the wallet has less than 1000000 tokens", async () => {
    
    2  await mockERC20.mock.balanceOf.returns(utils.parseEther("999999"))
    
    3  expect(await contract.check()).to.be.equal(false)
    
    4})

Let's break down this test into parts:

  1. We set our mock ERC20 contract to always return balance of 999999 tokens.
  2. Check if the `contract.check()` method returns `false`.

We're ready to fire up the beast:

[![One test
passing](/_next/image/?url=%2Fcontent%2Fdevelopers%2Ftutorials%2Fwaffle-
dynamic-mocking-and-testing-calls%2Ftest-
one.png&w=1920&q=75)](/content/developers/tutorials/waffle-dynamic-mocking-
and-testing-calls/test-one.png)

So the test works, but... there's still some room for improvement. The
`balanceOf()` function will always return 99999. We can improve it by
specifying a wallet for which the function should return something - just like
a real contract:

    
    
    1it("returns false if the wallet has less than 1000001 tokens", async () => {
    
    2  await mockERC20.mock.balanceOf
    
    3    .withArgs(wallet.address)
    
    4    .returns(utils.parseEther("999999"))
    
    5  expect(await contract.check()).to.be.equal(false)
    
    6})

So far, we've tested only the case where we're not rich enough. Let's test the
opposite instead:

    
    
    1it("returns true if the wallet has at least 1000001 tokens", async () => {
    
    2  await mockERC20.mock.balanceOf
    
    3    .withArgs(wallet.address)
    
    4    .returns(utils.parseEther("1000001"))
    
    5  expect(await contract.check()).to.be.equal(true)
    
    6})

You run the tests...

[![Two tests
passing](/_next/image/?url=%2Fcontent%2Fdevelopers%2Ftutorials%2Fwaffle-
dynamic-mocking-and-testing-calls%2Ftest-
two.png&w=1920&q=75)](/content/developers/tutorials/waffle-dynamic-mocking-
and-testing-calls/test-two.png)

...and here you are! Our contract seems to work as intended :)

## Testing contract calls

Let's sum up what've done so far. We've tested the functionality of our
`AmIRichAlready` contract and it seems to be working properly. That means
we're done, right? Not exactly! Waffle allows us to test our contract even
further. But how exactly? Well, in Waffle's arsenal there's a
`calledOnContract()` and `calledOnContractWith()` matchers. They will allow us
to check if our contract called the ERC20 mock contract. Here's a basic test
with one of these matchers:

    
    
    1it("checks if contract called balanceOf on the ERC20 token", async () => {
    
    2  await mockERC20.mock.balanceOf.returns(utils.parseEther("999999"))
    
    3  await contract.check()
    
    4  expect("balanceOf").to.be.calledOnContract(mockERC20)
    
    5})

We can go even further and improve this test with the other matcher I told you
about:

    
    
    1it("checks if contract called balanceOf with certain wallet on the ERC20 token", async () => {
    
    2  await mockERC20.mock.balanceOf
    
    3    .withArgs(wallet.address)
    
    4    .returns(utils.parseEther("999999"))
    
    5  await contract.check()
    
    6  expect("balanceOf").to.be.calledOnContractWith(mockERC20, [wallet.address])
    
    7})

Let's check if the tests are correct:

[![Three tests
passing](/_next/image/?url=%2Fcontent%2Fdevelopers%2Ftutorials%2Fwaffle-
dynamic-mocking-and-testing-calls%2Ftest-
three.png&w=1920&q=75)](/content/developers/tutorials/waffle-dynamic-mocking-
and-testing-calls/test-three.png)

Great, all tests are green.

Testing contract calls with Waffle is super easy. And here's the best part.
These matchers work with both normal and mocked contracts! It is because
Waffle records and filters EVM calls rather than inject code, like it is the
case of popular testing libraries for other technologies.

## The Finish Line

Congrats! Now you know how to use Waffle to test contract calls and mock
contracts dynamically. There are far more interesting features to discover. I
recommend diving into Waffle's documentation.

Waffle's documentation is available [here(opens in a new
tab)](https://ethereum-waffle.readthedocs.io/).

Source code for this tutorial can be found [here(opens in a new
tab)](https://github.com/EthWorks/Waffle/tree/master/examples/dynamic-mocking-
and-testing-calls).

Tutorials you may also be interested in:

  * [Testing smart contracts with Waffle](/en/developers/tutorials/waffle-test-simple-smart-contract/)

n

Last edit: [@nhsz(opens in a new tab)](https://github.com/nhsz), February 27,
2024

See contributors

### Was this tutorial helpful?

YesNo

  * [Edit page(opens in a new tab)](https://github.com/ethereum/ethereum-org-website/tree/dev/public/content/developers/tutorials/waffle-dynamic-mocking-and-testing-calls/index.md)
  * On this page

    * What is this tutorial about?
    * Dynamic mocking
      * 1\. Project
      * 2\. Smart contract
      * 3\. Testing
    * Testing contract calls
    * The Finish Line

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

