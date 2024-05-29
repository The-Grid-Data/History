Skip to main content

[](/en/)

  * Learn
  * Use
  * Build
  * Participate
  * Research

Search```K`

Languages EN

# Downsizing contracts to fight the contract size limit

soliditysmart contractsstoragetruffle

Intermediate

![✍️](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/270d.svg)Markus
Waas

![📚](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4da.svg)[soliditydeveloper.com(opens
in a new tab)](https://soliditydeveloper.com/max-contract-size)

![📆](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4c6.svg)
June 26, 2020

![⏱️](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/23f1.svg)6
minute read minute read

On this page

  * Why is there a limit?
  * Taking on the fight
  * Big impact
    * Separate your contracts
    * Libraries
    * Proxies
  * Medium impact
    * Remove functions
    * Avoid additional variables
    * Shorten error message
    * Use custom errors instead of error messages
    * Consider a low run value in the optimizer
  * Small impact
    * Avoid passing structs to functions
    * Declare correct visibility for functions and variables
    * Remove modifiers

## Why is there a limit?

On [November 22, 2016(opens in a new
tab)](https://blog.ethereum.org/2016/11/18/hard-fork-no-4-spurious-dragon/)
the Spurious Dragon hard-fork introduced [EIP-170(opens in a new
tab)](https://eips.ethereum.org/EIPS/eip-170) which added a smart contract
size limit of 24.576 kb. For you as a Solidity developer this means when you
add more and more functionality to your contract, at some point you will reach
the limit and when deploying will see the error:

`Warning: Contract code size exceeds 24576 bytes (a limit introduced in
Spurious Dragon). This contract may not be deployable on Mainnet. Consider
enabling the optimizer (with a low "runs" value!), turning off revert strings,
or using libraries.`

This limit was introduced to prevent denial-of-service (DOS) attacks. Any call
to a contract is relatively cheap gas-wise. However, the impact of a contract
call for Ethereum nodes increases disproportionately depending on the called
contract code's size (reading the code from disk, pre-processing the code,
adding data to the Merkle proof). Whenever you have such a situation where the
attacker requires few resources to cause a lot of work for others, you get the
potential for DOS attacks.

Originally this was less of a problem because one natural contract size limit
is the block gas limit. Obviously, a contract must be deployed within a
transaction that holds all of the contract's bytecode. If you include only
that one transaction into a block, you can use up all that gas, but it's not
infinite. Since the [London Upgrade](/en/history/#london), the block gas limit
has been able to vary between 15M and 30M units depending on network demand.

## Taking on the fight

Unfortunately, there is no easy way of getting the bytecode size of your
contracts. A great tool to help you that is the [truffle-contract-size(opens
in a new tab)](https://github.com/IoBuilders/truffle-contract-size) plugin if
you're using Truffle.

  1. `npm install truffle-contract-size`
  2. Add the plugin to the _truffle-config.js_ : `plugins: ["truffle-contract-size"]`
  3. Run `truffle run contract-size`

This will help you figure out how your changes are affecting the total
contract sizes.

In the following we will look at some methods ordered by their potential
impact. Think about it in the terms of weight-loss. The best strategy for
someone to hit their target weight (in our case 24kb) is to focus on the big
impact methods first. In most cases just fixing your diet will get you there,
but sometimes you need a little bit more. Then you might add some exercise
(medium impact) or even supplements (small impact).

## Big impact

### Separate your contracts

This should always be your first approach. How can you separate the contract
into multiple smaller ones? It generally forces you to come up with a good
architecture for your contracts. Smaller contracts are always preferred from a
code readability perspective. For splitting contracts, ask yourself:

  * Which functions belong together? Each set of functions might be best in its own contract.
  * Which functions don't require reading contract state or just a specific subset of the state?
  * Can you split storage and functionality?

### Libraries

One simple way to move functionality code away from the storage is using a
[library(opens in a new
tab)](https://solidity.readthedocs.io/en/v0.6.10/contracts.html#libraries).
Don't declare the library functions as internal as those will be [added to the
contract(opens in a new
tab)](https://ethereum.stackexchange.com/questions/12975/are-internal-
functions-in-libraries-not-covered-by-linking) directly during compilation.
But if you use public functions, then those will be in fact in a separate
library contract. Consider [using for(opens in a new
tab)](https://solidity.readthedocs.io/en/v0.6.10/contracts.html#using-for) to
make the use of libraries more convenient.

### Proxies

A more advanced strategy would be a proxy system. Libraries use `DELEGATECALL`
in the back which simply executes another contract's function with the state
of the calling contract. Check out [this blog post(opens in a new
tab)](https://hackernoon.com/how-to-make-smart-contracts-
upgradable-2612e771d5a2) to learn more about proxy systems. They give you more
functionality, e.g., they enable upgradability, but they also add a lot of
complexity. I wouldn't add those only to reduce contract sizes unless it's
your only option for whatever reason.

## Medium impact

### Remove functions

This one should be obvious. Functions increase a contract size quite a bit.

  * **External** : Often times we add a lot of view functions for convenience reasons. That's perfectly fine until you hit the size limit. Then you might want to really think about removing all but absolutely essential ones.
  * **Internal** : You can also remove internal/private functions and simply inline the code as long the function is called only once.

### Avoid additional variables

A simple change like this:

    
    
    1function get(uint id) returns (address,address) {
    
    2    MyStruct memory myStruct = myStructs[id];
    
    3    return (myStruct.addr1, myStruct.addr2);
    
    4}
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy
    
    
    1function get(uint id) returns (address,address) {
    
    2    return (myStructs[id].addr1, myStructs[id].addr2);
    
    3}
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

makes a difference of **0.28kb**. Chances are you can find many similar
situations in your contracts and those can really add up to significant
amounts.

### Shorten error message

Long revert messages and in particular many different revert messages can
bloat up the contract. Instead use short error codes and decode them in your
contract. A long message could be become much shorter:

    
    
    1require(msg.sender == owner, "Only the owner of this contract can call this function");
    
    2
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy
    
    
    1require(msg.sender == owner, "OW1");
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

### Use custom errors instead of error messages

Custom errors have been introduced in [Solidity 0.8.4(opens in a new
tab)](https://blog.soliditylang.org/2021/04/21/custom-errors/). They are a
great way to reduce the size of your contracts, because they are ABI-encoded
as selectors (just like functions are).

    
    
    1error Unauthorized();
    
    2
    
    3if (msg.sender != owner) {
    
    4    revert Unauthorized();
    
    5}
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

### Consider a low run value in the optimizer

You can also change the optimizer settings. The default value of 200 means
that it's trying to optimize the bytecode as if a function is called 200
times. If you change it to 1, you basically tell the optimizer to optimize for
the case of running each function only once. An optimized function for running
only one time means it is optimized for the deployment itself. Be aware that
**this increases the[gas costs](/en/developers/docs/gas/) for running the
functions**, so you may not want to do it.

## Small impact

### Avoid passing structs to functions

If you are using the [ABIEncoderV2(opens in a new
tab)](https://solidity.readthedocs.io/en/v0.6.10/layout-of-source-
files.html#abiencoderv2), it can help to not pass structs to a function.
Instead of passing the parameter as a struct...

    
    
    1function get(uint id) returns (address,address) {
    
    2    return _get(myStruct);
    
    3}
    
    4
    
    5function _get(MyStruct memory myStruct) private view returns(address,address) {
    
    6    return (myStruct.addr1, myStruct.addr2);
    
    7}
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy
    
    
    1function get(uint id) returns(address,address) {
    
    2    return _get(myStructs[id].addr1, myStructs[id].addr2);
    
    3}
    
    4
    
    5function _get(address addr1, address addr2) private view returns(address,address) {
    
    6    return (addr1, addr2);
    
    7}
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

... pass the required parameters directly. In this example we saved another
**0.1kb**.

### Declare correct visibility for functions and variables

  * Functions or variables that are only called from the outside? Declare them as `external` instead of `public`.
  * Functions or variables only called from within the contract? Declare them as `private` or `internal` instead of `public`.

### Remove modifiers

Modifiers, especially when used intensely, could have a significant impact on
the contract size. Consider removing them and instead use functions.

    
    
    1modifier checkStuff() {}
    
    2
    
    3function doSomething() checkStuff {}
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy
    
    
    1function checkStuff() private {}
    
    2
    
    3function doSomething() { checkStuff(); }
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Those tips should help you to significantly reduce the contract size. Once
again, I cannot stress enough, always focus on splitting contracts if possible
for the biggest impact.

p

Last edit: [@pettinarip(opens in a new tab)](https://github.com/pettinarip),
November 23, 2023

See contributors

### Was this tutorial helpful?

YesNo

  * [Edit page(opens in a new tab)](https://github.com/ethereum/ethereum-org-website/tree/dev/public/content/developers/tutorials/downsizing-contracts-to-fight-the-contract-size-limit/index.md)
  * On this page

    * Why is there a limit?
    * Taking on the fight
    * Big impact
      * Separate your contracts
      * Libraries
      * Proxies
    * Medium impact
      * Remove functions
      * Avoid additional variables
      * Shorten error message
      * Use custom errors instead of error messages
      * Consider a low run value in the optimizer
    * Small impact
      * Avoid passing structs to functions
      * Declare correct visibility for functions and variables
      * Remove modifiers

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

