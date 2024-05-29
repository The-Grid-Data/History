Skip to main content

[](/en/)

  * Learn
  * Use
  * Build
  * Participate
  * Research

Search```K`

Languages EN

# Waffle say hello world tutorial with hardhat and ethers

wafflesmart contractssoliditytestinghardhatethers.js

Beginner

![✍️](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/270d.svg)MiZiet

![📆](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4c6.svg)
October 16, 2020

![⏱️](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/23f1.svg)4
minute read minute read

On this page

  * Now let's talk about some of these files:
  * Next step consists of compiling our contract and running tests:
  * Everything looks great so far, let's add some more complexity to our project
  * Conclusion

In this [Waffle(opens in a new tab)](https://ethereum-waffle.readthedocs.io)
tutorial, we will learn how to set up a simple "Hello world" smart contract
project, using [hardhat(opens in a new tab)](https://hardhat.org/) and
[ethers.js(opens in a new tab)](https://docs.ethers.io/v5/). Then we will
learn how to add a new functionality to our smart contract and how to test it
with Waffle.

Let's start by creating a new project:

    
    
    yarn init

or

    
    
    npm init

and installing required packages:

    
    
    yarn add -D hardhat @nomiclabs/hardhat-ethers ethers @nomiclabs/hardhat-waffle ethereum-waffle chai

or

    
    
    npm install -D hardhat @nomiclabs/hardhat-ethers ethers @nomiclabs/hardhat-waffle ethereum-waffle chai

Next step is creating a sample hardhat project by running `npx hardhat`.

    
    
    888    888                      888 888               888
    
    888    888                      888 888               888
    
    888    888                      888 888               888
    
    8888888888  8888b.  888d888 .d88888 88888b.   8888b.  888888
    
    888    888     "88b 888P"  d88" 888 888 "88b     "88b 888
    
    888    888 .d888888 888    888  888 888  888 .d888888 888
    
    888    888 888  888 888    Y88b 888 888  888 888  888 Y88b.
    
    888    888 "Y888888 888     "Y88888 888  888 "Y888888  "Y888
    
    👷 Welcome to Hardhat v2.0.3 👷‍
    
    ? What do you want to do? …
    
    ❯ Create a sample project
    
    Create an empty hardhat.config.js
    
    Quit
    
    Show all

Select `Create a sample project`

Our project's structure should look like this:

    
    
    1MyWaffleProject
    
    2├── contracts
    
    3│   └── Greeter.sol
    
    4├── node_modules
    
    5├── scripts
    
    6│   └── sample-script.js
    
    7├── test
    
    8│   └── sample-test.js
    
    9├── .gitattributes
    
    10├── .gitignore
    
    11├── hardhat.config.js
    
    12└── package.json
    
    Show all

### Now let's talk about some of these files:

  * Greeter.sol - our smart contract written in solidity;

    
    
    1contract Greeter {
    
    2string greeting;
    
    3
    
    4constructor(string memory _greeting) public {
    
    5console.log("Deploying a Greeter with greeting:", _greeting);
    
    6greeting = _greeting;
    
    7}
    
    8
    
    9function greet() public view returns (string memory) {
    
    10return greeting;
    
    11}
    
    12
    
    13function setGreeting(string memory _greeting) public {
    
    14console.log("Changing greeting from '%s' to '%s'", greeting, _greeting);
    
    15greeting = _greeting;
    
    16}
    
    17}
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Our smart contract can be divided into three parts:

  1. constructor - where we declare a string type variable called `greeting`,
  2. function greet - a function that will return the `greeting` when called,
  3. function setGreeting - a function that allows us to change the `greeting` value.

  * sample-test.js - our tests file

    
    
    1describe("Greeter", function () {
    
    2  it("Should return the new greeting once it's changed", async function () {
    
    3    const Greeter = await ethers.getContractFactory("Greeter")
    
    4    const greeter = await Greeter.deploy("Hello, world!")
    
    5
    
    6    await greeter.deployed()
    
    7    expect(await greeter.greet()).to.equal("Hello, world!")
    
    8
    
    9    await greeter.setGreeting("Hola, mundo!")
    
    10    expect(await greeter.greet()).to.equal("Hola, mundo!")
    
    11  })
    
    12})
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

### Next step consists of compiling our contract and running tests:

Waffle tests use Mocha (a test framework) with Chai (an assertion library).
All you have to do is run `npx hardhat test` and wait for the following
message to appear.

    
    
    ✓ Should return the new greeting once it's changed

### Everything looks great so far, let's add some more complexity to our
project
![🙂](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f642.svg)

Imagine a situation where someone adds an empty string as a greeting. It
wouldn't be a warm greeting, right?  
Let's make sure that doesn't happen:

We want to use solidity's `revert` when someone passes an empty string. A good
thing is that we can easily test this functionality with Waffle's chai matcher
`to.be.revertedWith()`.

    
    
    1it("Should revert when passing an empty string", async () => {
    
    2  const Greeter = await ethers.getContractFactory("Greeter")
    
    3  const greeter = await Greeter.deploy("Hello, world!")
    
    4
    
    5  await greeter.deployed()
    
    6  await expect(greeter.setGreeting("")).to.be.revertedWith(
    
    7    "Greeting should not be empty"
    
    8  )
    
    9})
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Looks like our new test didn't pass:

    
    
    Deploying a Greeter with greeting: Hello, world!
    
    Changing greeting from 'Hello, world!' to 'Hola, mundo!'
    
        ✓ Should return the new greeting once it's changed (1514ms)
    
    Deploying a Greeter with greeting: Hello, world!
    
    Changing greeting from 'Hello, world!' to ''
    
        1) Should revert when passing an empty string
    
      1 passing (2s)
    
      1 failing
    
    Show all

Let's implement this functionality into our smart contract:

    
    
    1require(bytes(_greeting).length > 0, "Greeting should not be empty");
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Now, our setGreeting function looks like this:

    
    
    1function setGreeting(string memory _greeting) public {
    
    2require(bytes(_greeting).length > 0, "Greeting should not be empty");
    
    3console.log("Changing greeting from '%s' to '%s'", greeting, _greeting);
    
    4greeting = _greeting;
    
    5}
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Let's run tests again:

    
    
    ✓ Should return the new greeting once it's changed (1467ms)
    
    ✓ Should revert when passing an empty string (276ms)
    
    2 passing (2s)

Congrats! You made it :)

### Conclusion

We made a simple project with Waffle, Hardhat and ethers.js. We learned how to
set up a project, add a test and implement new functionality.

For more great chai matchers to test your smart contracts, check [official
Waffle's docs(opens in a new tab)](https://ethereum-
waffle.readthedocs.io/en/latest/matchers.html).

p

Last edit: [@pettinarip(opens in a new tab)](https://github.com/pettinarip),
December 8, 2023

See contributors

### Was this tutorial helpful?

YesNo

  * [Edit page(opens in a new tab)](https://github.com/ethereum/ethereum-org-website/tree/dev/public/content/developers/tutorials/waffle-say-hello-world-with-hardhat-and-ethers/index.md)
  * On this page

    * Now let's talk about some of these files:
    * Next step consists of compiling our contract and running tests:
    * Everything looks great so far, let's add some more complexity to our project
    * Conclusion

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

