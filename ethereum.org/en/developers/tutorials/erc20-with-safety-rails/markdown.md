Skip to main content

[](/en/)

  * Learn
  * Use
  * Build
  * Participate
  * Research

Search```K`

Languages EN

# ERC-20 with Safety Rails

erc-20

Beginner

![✍️](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/270d.svg)Ori
Pomerantz

![📆](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4c6.svg)
August 15, 2022

![⏱️](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/23f1.svg)8
minute read minute read

On this page

  * Introduction
  * Creating an ERC-20 contract
  * Common mistakes
    * The mistakes
    * Preventing transfers
    * Coding the requirements
  * Administrative access
    * Freezing and thawing contracts
    * Asset cleanup
  * Conclusion

## Introduction

One of the great things about Ethereum is that there is no central authority
that can modify or undo your transactions. One of the great problems with
Ethereum is that there is no central authority with the power to undo user
mistakes or illicit transactions. In this article you learn about some of the
common mistakes that users commit with
[ERC-20](/en/developers/docs/standards/tokens/erc-20/) tokens, as well as how
to create ERC-20 contracts that help users to avoid those mistakes, or that
give a central authority some power (for example to freeze accounts).

Note that while we will use the [OpenZeppelin ERC-20 token contract(opens in a
new tab)](https://github.com/OpenZeppelin/openzeppelin-
contracts/tree/master/contracts/token/ERC20), this article does not explain it
in great details. You can find this information
[here](/en/developers/tutorials/erc20-annotated-code/).

If you want to see the complete source code:

  1. Open the [Remix IDE(opens in a new tab)](https://remix.ethereum.org/).
  2. Click the clone github icon ([![clone github icon](/_next/image/?url=%2Fcontent%2Fdevelopers%2Ftutorials%2Ferc20-with-safety-rails%2Ficon-clone.png&w=48&q=75)](/content/developers/tutorials/erc20-with-safety-rails/icon-clone.png)).
  3. Clone the github repository `https://github.com/qbzzt/20220815-erc20-safety-rails`.
  4. Open **contracts > erc20-safety-rails.sol**.

## Creating an ERC-20 contract

Before we can add the safety rail functionality we need an ERC-20 contract. In
this article we'll use [the OpenZeppelin Contracts Wizard(opens in a new
tab)](https://docs.openzeppelin.com/contracts/5.x/wizard). Open it in another
browser and follow these instructions:

  1. Select **ERC20**.

  2. Enter these settings:

Parameter| Value  
---|---  
Name| SafetyRailsToken  
Symbol| SAFE  
Premint| 1000  
Features| None  
Access Control| Ownable  
Upgradability| None  
  
  3. Scroll up and click **Open in Remix** (for Remix) or **Download** to use a different environment. I'm going to assume you're using Remix, if you use something else just make the appropriate changes.

  4. We now have a fully functional ERC-20 contract. You can expand `.deps` > `npm` to see the imported code.

  5. Compile, deploy, and play with the contract to see that it functions as an ERC-20 contract. If you need to learn how to use Remix, [use this tutorial(opens in a new tab)](https://remix.ethereum.org/?#activate=udapp,solidity,LearnEth).

## Common mistakes

### The mistakes

Users sometimes send tokens to the wrong address. While we cannot read their
minds to know what they meant to do, there are two error types that happen a
lot and are easy to detect:

  1. Sending the tokens to the contract's own address. For example, [Optimism's OP token(opens in a new tab)](https://optimism.mirror.xyz/qvd0WfuLKnePm1Gxb9dpGchPf5uDz5NSMEFdgirDS4c) managed to accumulate [over 120,000(opens in a new tab)](https://optimistic.etherscan.io/address/0x4200000000000000000000000000000000000042#tokentxns) OP tokens in less than two months. This represents a significant amount of wealth that presumably people just lost.

  2. Sending the tokens to an empty address, one that doesn't correspond to an [externally owned account](/en/developers/docs/accounts/#externally-owned-accounts-and-key-pairs) or a [smart contract](/en/developers/docs/smart-contracts/). While I don't have statistics on how often this happens, [one incident could have cost 20,000,000 tokens(opens in a new tab)](https://gov.optimism.io/t/message-to-optimism-community-from-wintermute/2595).

### Preventing transfers

The OpenZeppelin ERC-20 contract includes [a hook,
`_beforeTokenTransfer`(opens in a new
tab)](https://github.com/OpenZeppelin/openzeppelin-
contracts/blob/master/contracts/token/ERC20/ERC20.sol#L364-L368), that is
called before a token is transferred. By default this hook does not do
anything, but we can hang our own functionality on it, such as checks that
revert if there's a problem.

To use the hook, add this function after the constructor:

    
    
    1    function _beforeTokenTransfer(address from, address to, uint256 amount)
    
    2        internal virtual
    
    3        override(ERC20)
    
    4    {
    
    5        super._beforeTokenTransfer(from, to, amount);
    
    6    }
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Some parts of this function may be new if you aren't very familiar with
Solidity:

    
    
    1        internal virtual
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

The `virtual` keyword means that just as we inherited functionality from
`ERC20` and overrode this function, other contracts can inherit from us and
override this function.

    
    
    1        override(ERC20)
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

We have to specify explicitly that we're [overriding(opens in a new
tab)](https://docs.soliditylang.org/en/v0.8.15/contracts.html#function-
overriding) the ERC20 token definition of `_beforeTokenTransfer`. In general,
explicit definitions are a lot better, from the security standpoint, than
implicit ones - you cannot forget that you've done something if it's right in
front of you. That is also the reason we need to specify which superclass's
`_beforeTokenTransfer` we are overriding.

    
    
    1        super._beforeTokenTransfer(from, to, amount);
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

This line calls the `_beforeTokenTransfer` function of the contract or
contracts from which we inherited which have it. In this case, that is only
`ERC20`, `Ownable` does not have this hook. Even though currently
`ERC20._beforeTokenTransfer` doesn't do anything, we call it in case
functionality is added in the future (and we then decide to redeploy the
contract, because contracts don't change after deployment).

### Coding the requirements

We want to add these requirements to the function:

  * The `to` address cannot equal `address(this)`, the address of the ERC-20 contract itself.
  * The `to` address cannot be empty, it has to be either:
    * An externally owned account (EOA). We can't check if an address is an EOA directly, but we can check an address's ETH balance. EOAs almost always have a balance, even if they are no longer used - it's difficult to clear them to the last wei.
    * A smart contract. Testing if an address is a smart contract is a bit harder. There is an opcode that checks the external code length, called [`EXTCODESIZE`(opens in a new tab)](https://www.evm.codes/#3b), but it is not available directly in Solidity. We have to use [Yul(opens in a new tab)](https://docs.soliditylang.org/en/v0.8.15/yul.html), which is EVM assembly, for it. There are other values we could use from Solidity ([`<address>.code` and `<address>.codehash`(opens in a new tab)](https://docs.soliditylang.org/en/v0.8.15/units-and-global-variables.html#members-of-address-types)), but they cost more.

Lets go over the new code line by line:

    
    
    1        require(to != address(this), "Can't send tokens to the contract address");
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

This is the first requirement, check that `to` and `this(address)` are not the
same thing.

    
    
    1        bool isToContract;
    
    2        assembly {
    
    3           isToContract := gt(extcodesize(to), 0)
    
    4        }
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

This is how we check if an address is a contract. We cannot receive output
directly from Yul, so instead we define a variable to hold the result
(`isToContract` in this case). The way Yul works is that every opcode is
considered a function. So first we call [`EXTCODESIZE`(opens in a new
tab)](https://www.evm.codes/#3b) to get the contract size, and then use
[`GT`(opens in a new tab)](https://www.evm.codes/#11) to check it is not zero
(we are dealing with unsigned integers, so of course it can't be negative). We
then write the result to `isToContract`.

    
    
    1        require(to.balance != 0 || isToContract, "Can't send tokens to an empty address");
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

And finally, we have the actual check for empty addresses.

## Administrative access

Sometimes it is useful to have an administrator that can undo mistakes. To
reduce the potential for abuse, this administrator can be a [multisig(opens in
a new tab)](https://blog.logrocket.com/security-choices-multi-signature-
wallets/) so multiple people have to agree on an action. In this article we'll
have two administrative features:

  1. Freezing and unfreezing accounts. This can be useful, for example, when an account might be compromised.

  2. Asset cleanup.

Sometimes frauds send fraudulent tokens to the real token's contract to gain
legitimacy. For example, [see here(opens in a new
tab)](https://optimistic.etherscan.io/token/0x2348b1a1228ddcd2db668c3d30207c3e1852fbbe?a=0x4200000000000000000000000000000000000042).
The legitimate ERC-20 contract is [0x4200....0042(opens in a new
tab)](https://optimistic.etherscan.io/address/0x4200000000000000000000000000000000000042).
The scam that pretends to be it is [0x234....bbe(opens in a new
tab)](https://optimistic.etherscan.io/address/0x2348b1a1228ddcd2db668c3d30207c3e1852fbbe).

It is also possible that people send legitimate ERC-20 tokens to our contract
by mistake, which is another reason to want to have a way to get them out.

OpenZeppelin provides two mechanisms to enable administrative access:

  * [`Ownable`(opens in a new tab)](https://docs.openzeppelin.com/contracts/4.x/access-control#ownership-and-ownable) contracts have a single owner. Functions that have the `onlyOwner` [modifier(opens in a new tab)](https://www.tutorialspoint.com/solidity/solidity_function_modifiers.htm) can only be called by that owner. Owners can transfer ownership to somebody else or renounce it completely. The rights of all other accounts are typically identical.
  * [`AccessControl`(opens in a new tab)](https://docs.openzeppelin.com/contracts/4.x/access-control#role-based-access-control) contracts have [role based access control (RBAC)(opens in a new tab)](https://en.wikipedia.org/wiki/Role-based_access_control).

For the sake of simplicity, in this article we use `Ownable`.

### Freezing and thawing contracts

Freezing and thawing contracts requires several changes:

  * A [mapping(opens in a new tab)](https://www.tutorialspoint.com/solidity/solidity_mappings.htm) from addresses to [booleans(opens in a new tab)](https://en.wikipedia.org/wiki/Boolean_data_type) to keep track of which addresses are frozen. All values are initially zero, which for boolean values is interpreted as false. This is what we want because by default accounts are not frozen.
    
        1    mapping(address => bool) public frozenAccounts;
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

  * [Events(opens in a new tab)](https://www.tutorialspoint.com/solidity/solidity_events.htm) to inform anybody interested when an account is frozen or thawed. Technically speaking events are not required for these actions, but it helps off chain code to be able to listen to these events and know what is happening. It's considered good manners for a smart contract to emit them when something that miught be relevant to somebody else happens.

The events are indexed so will be possible to search for all the times an
account has been frozen or thawed.

    
        1  // When accounts are frozen or unfrozen
    
    2  event AccountFrozen(address indexed _addr);
    
    3  event AccountThawed(address indexed _addr);
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

  * Functions for freezing and thawing accounts. These two functions are nearly identical, so we'll only go over the freeze function.
    
        1    function freezeAccount(address addr)
    
    2      public
    
    3      onlyOwner
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Functions marked [`public`(opens in a new
tab)](https://www.tutorialspoint.com/solidity/solidity_contracts.htm) can be
called from other smart contracts or directly by a transaction.

    
        1  {
    
    2      require(!frozenAccounts[addr], "Account already frozen");
    
    3      frozenAccounts[addr] = true;
    
    4      emit AccountFrozen(addr);
    
    5  }  // freezeAccount
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

If the account is already frozen, revert. Otherwise, freeze it and `emit` an
event.

  * Change `_beforeTokenTransfer` to prevent money being moved from a frozen account. Note that money can still be transferred into the frozen account.
    
        1     require(!frozenAccounts[from], "The account is frozen");
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

### Asset cleanup

To release ERC-20 tokens held by this contract we need to call a function on
the token contract to which they belong, either [`transfer`(opens in a new
tab)](https://eips.ethereum.org/EIPS/eip-20#transfer) or [`approve`(opens in a
new tab)](https://eips.ethereum.org/EIPS/eip-20#approve). There's no point
wasting gas in this case on allowances, we might as well transfer directly.

    
    
    1    function cleanupERC20(
    
    2        address erc20,
    
    3        address dest
    
    4    )
    
    5        public
    
    6        onlyOwner
    
    7    {
    
    8        IERC20 token = IERC20(erc20);
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

This is the syntax to create an object for a contract when we receive the
address. We can do this because we have the definition for ERC20 tokens as
part of the source code (see line 4), and that file includes [the definition
for IERC20(opens in a new tab)](https://github.com/OpenZeppelin/openzeppelin-
contracts/blob/master/contracts/token/ERC20/IERC20.sol), the interface for an
OpenZeppelin ERC-20 contract.

    
    
    1        uint balance = token.balanceOf(address(this));
    
    2        token.transfer(dest, balance);
    
    3    }
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

This is a cleanup function, so presumably we don't want to leave any tokens.
Instead of getting the balance from the user manually, we might as well
automate the process.

## Conclusion

This is not a perfect solution - there is no perfect solution for the "user
made a mistake" problem. However, using these kinds of checks can at least
prevent some mistakes. The ability to freeze accounts, while dangerous, can be
used to limit the damage of certain hacks by denying the hacker the stolen
funds.

o

Last edit: [@omahs(opens in a new tab)](https://github.com/omahs), February
17, 2024

See contributors

### Was this tutorial helpful?

YesNo

  * [Edit page(opens in a new tab)](https://github.com/ethereum/ethereum-org-website/tree/dev/public/content/developers/tutorials/erc20-with-safety-rails/index.md)
  * On this page

    * Introduction
    * Creating an ERC-20 contract
    * Common mistakes
      * The mistakes
      * Preventing transfers
      * Coding the requirements
    * Administrative access
      * Freezing and thawing contracts
      * Asset cleanup
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

