Skip to main content

[](/en/)

  * Learn
  * Use
  * Build
  * Participate
  * Research

Search```K`

Languages EN

# Interact with other contracts from Solidity

smart contractssolidityremixdeployingcomposability

Advanced

![✍️](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/270d.svg)jdourlens

![📚](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4da.svg)[EthereumDev(opens
in a new tab)](https://ethereumdev.io/interact-with-other-contracts-from-
solidity/)

![📆](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4c6.svg)
April 5, 2020

![⏱️](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/23f1.svg)4
minute read minute read

comp-tutorial-metadata-tip-author 0x19dE91Af973F404EDF5B4c093983a7c6E3EC8ccE

On this page

In the previous tutorials we learnt a lot [how to deploy your first smart
contract](/en/developers/tutorials/deploying-your-first-smart-contract/) and
add some features to it like [control access with modifiers(opens in a new
tab)](https://ethereumdev.io/organize-your-code-and-control-access-to-your-
smart-contract-with-modifiers/) or [error handling in Solidity(opens in a new
tab)](https://ethereumdev.io/handle-errors-in-solidity-with-require-and-
revert/). In this tutorial we’ll learn how to deploy a smart contract from an
existing contract and interact with it.

We’ll make a contract that enables anyone to have his own `Counter` smart
contract by creating a factory for it, its name will be `CounterFactory`.
First here is the code of our initial `Counter` smart contract:

    
    
    1pragma solidity 0.5.17;
    
    2
    
    3contract Counter {
    
    4
    
    5    uint256 private _count;
    
    6    address private _owner;
    
    7    address private _factory;
    
    8
    
    9
    
    10     modifier onlyOwner(address caller) {
    
    11        require(caller == _owner, "You're not the owner of the contract");
    
    12        _;
    
    13    }
    
    14
    
    15    modifier onlyFactory() {
    
    16        require(msg.sender == _factory, "You need to use the factory");
    
    17        _;
    
    18    }
    
    19
    
    20     constructor(address owner) public {
    
    21        _owner = owner;
    
    22        _factory = msg.sender;
    
    23    }
    
    24
    
    25     function getCount() public view returns (uint256) {
    
    26        return _count;
    
    27    }
    
    28
    
    29    function increment(address caller) public onlyFactory onlyOwner(caller) {
    
    30        _count++;
    
    31    }
    
    32
    
    33}
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Note that we slightly modified the contract code to keep a track of the
address of the factory and the address of the contract owner. When you call a
contract code from another contract, the msg.sender will refer to the address
of our contract factory. This is **a really important point to understand** as
using a contract to interact with other contracts is a common practice. You
should therefore take care of who is the sender in complex cases.

For this we also added an `onlyFactory` modifier that make sure that the state
changing function can only be called by the factory that will pass the
original caller as a parameter.

Inside of our new `CounterFactory` that will manage all the other Counters,
we’ll add a mapping that will associate an owner to the address of his counter
contract:

    
    
    1mapping(address => Counter) _counters;
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

In Ethereum, mapping are equivalent of objects in javascript, they enable to
map a key of type A to a value of type B. In this case we map the address of
an owner with the instance of its Counter.

Instantiating a new Counter for someone will look like this:

    
    
    1  function createCounter() public {
    
    2      require (_counters[msg.sender] == Counter(0));
    
    3      _counters[msg.sender] = new Counter(msg.sender);
    
    4  }
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

We first check if the person already owns a counter. If he does not own a
counter we instantiate a new counter by passing his address to the `Counter`
constructor and assign the newly created instance to the mapping.

To get the count of a specific Counter it will look like this:

    
    
    1function getCount(address account) public view returns (uint256) {
    
    2    require (_counters[account] != Counter(0));
    
    3    return (_counters[account].getCount());
    
    4}
    
    5
    
    6function getMyCount() public view returns (uint256) {
    
    7    return (getCount(msg.sender));
    
    8}
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

The first function check if the Counter contract exists for a given address
and then calls the `getCount` method from the instance. The second function:
`getMyCount` is just a short end to pass the msg.sender directly to the
`getCount` function.

The `increment` function is quite similar but pass the original transaction
sender to the `Counter` contract:

    
    
    1function increment() public {
    
    2      require (_counters[msg.sender] != Counter(0));
    
    3      Counter(_counters[msg.sender]).increment(msg.sender);
    
    4  }
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Note that if called to many times, our counter could possibly victim of an
overflow. You should use the [SafeMath library(opens in a new
tab)](https://ethereumdev.io/using-safe-math-library-to-prevent-from-
overflows/) as much as possible to protect from this possible case.

To deploy our contract, you will need to provide both the code of the
`CounterFactory` and the `Counter`. When deploying for example in Remix you’ll
need to select CounterFactory.

Here is the full code:

    
    
    1pragma solidity 0.5.17;
    
    2
    
    3contract Counter {
    
    4
    
    5    uint256 private _count;
    
    6    address private _owner;
    
    7    address private _factory;
    
    8
    
    9
    
    10     modifier onlyOwner(address caller) {
    
    11        require(caller == _owner, "You're not the owner of the contract");
    
    12        _;
    
    13    }
    
    14
    
    15    modifier onlyFactory() {
    
    16        require(msg.sender == _factory, "You need to use the factory");
    
    17        _;
    
    18    }
    
    19
    
    20     constructor(address owner) public {
    
    21        _owner = owner;
    
    22        _factory = msg.sender;
    
    23    }
    
    24
    
    25     function getCount() public view returns (uint256) {
    
    26        return _count;
    
    27    }
    
    28
    
    29    function increment(address caller) public onlyFactory onlyOwner(caller) {
    
    30        _count++;
    
    31    }
    
    32
    
    33}
    
    34
    
    35contract CounterFactory {
    
    36
    
    37    mapping(address => Counter) _counters;
    
    38
    
    39    function createCounter() public {
    
    40        require (_counters[msg.sender] == Counter(0));
    
    41        _counters[msg.sender] = new Counter(msg.sender);
    
    42    }
    
    43
    
    44    function increment() public {
    
    45        require (_counters[msg.sender] != Counter(0));
    
    46        Counter(_counters[msg.sender]).increment(msg.sender);
    
    47    }
    
    48
    
    49    function getCount(address account) public view returns (uint256) {
    
    50        require (_counters[account] != Counter(0));
    
    51        return (_counters[account].getCount());
    
    52    }
    
    53
    
    54    function getMyCount() public view returns (uint256) {
    
    55        return (getCount(msg.sender));
    
    56    }
    
    57
    
    58}
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

After compiling, in the Remix deploy section you’ll select the factory to be
deployed:

[![Selecting the factory to be deployed in
Remix](/_next/image/?url=%2Fcontent%2Fdevelopers%2Ftutorials%2Finteract-with-
other-contracts-from-solidity%2Fcounterfactory-
deploy.png&w=1080&q=75)](/content/developers/tutorials/interact-with-other-
contracts-from-solidity/counterfactory-deploy.png)

Then you can play with your contract factory and check the value changing. If
you’d like to call the smart contract from a different address you’ll need to
change the address in the Account select of Remix.

n

Last edit: [@nhsz(opens in a new tab)](https://github.com/nhsz), August 15,
2023

See contributors

### Was this tutorial helpful?

YesNo

  * [Edit page(opens in a new tab)](https://github.com/ethereum/ethereum-org-website/tree/dev/public/content/developers/tutorials/interact-with-other-contracts-from-solidity/index.md)
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

