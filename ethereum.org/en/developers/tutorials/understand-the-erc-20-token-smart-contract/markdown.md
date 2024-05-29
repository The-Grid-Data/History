Skip to main content

[](/en/)

  * Learn
  * Use
  * Build
  * Participate
  * Research

Search```K`

Languages EN

# Understand the ERC-20 token smart contract

smart contractstokenssolidityerc-20

Beginner

![✍️](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/270d.svg)jdourlens

![📚](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4da.svg)[EthereumDev(opens
in a new tab)](https://ethereumdev.io/understand-the-erc20-token-smart-
contract/)

![📆](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4c6.svg)
April 5, 2020

![⏱️](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/23f1.svg)5
minute read minute read

comp-tutorial-metadata-tip-author 0x19dE91Af973F404EDF5B4c093983a7c6E3EC8ccE

On this page

  * Getters
  * Functions
  * Events
  * A basic implementation of ERC-20 tokens

One of the most significant [smart contract
standards](/en/developers/docs/standards/) on Ethereum is known as
[ERC-20](/en/developers/docs/standards/tokens/erc-20/), which has emerged as
the technical standard used for all smart contracts on the Ethereum blockchain
for fungible token implementations.

ERC-20 defines a common list of rules that all fungible Ethereum tokens should
adhere to. Consequently, this token standard empowers developers of all types
to accurately predict how new tokens will function within the larger Ethereum
system. This simplifies and eases developers’ tasks, because they can proceed
with their work, knowing that each and every new project won’t need to be
redone every time a new token is released, as long as the token follows the
rules.

Here is, presented as an interface, the functions an ERC-20 must implement. If
you’re not sure about what is an interface: check our article about [OOP
programming in Solidity(opens in a new
tab)](https://ethereumdev.io/inheritance-in-solidity-contracts-are-classes/).

    
    
    1pragma solidity ^0.6.0;
    
    2
    
    3interface IERC20 {
    
    4
    
    5    function totalSupply() external view returns (uint256);
    
    6    function balanceOf(address account) external view returns (uint256);
    
    7    function allowance(address owner, address spender) external view returns (uint256);
    
    8
    
    9    function transfer(address recipient, uint256 amount) external returns (bool);
    
    10    function approve(address spender, uint256 amount) external returns (bool);
    
    11    function transferFrom(address sender, address recipient, uint256 amount) external returns (bool);
    
    12
    
    13
    
    14    event Transfer(address indexed from, address indexed to, uint256 value);
    
    15    event Approval(address indexed owner, address indexed spender, uint256 value);
    
    16}
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Here is a line-by-line explainer of what every function is for. After this
we’ll present a simple implementation of the ERC-20 token.

## Getters

    
    
    1function totalSupply() external view returns (uint256);
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Returns the amount of tokens in existence. This function is a getter and does
not modify the state of the contract. Keep in mind that there are no floats in
Solidity. Therefore most tokens adopt 18 decimals and will return the total
supply and other results as followed 1000000000000000000 for 1 token. Not
every token has 18 decimals and this is something you really need to watch for
when dealing with tokens.

    
    
    1function balanceOf(address account) external view returns (uint256);
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Returns the amount of tokens owned by an address (`account`). This function is
a getter and does not modify the state of the contract.

    
    
    1function allowance(address owner, address spender) external view returns (uint256);
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

The ERC-20 standard allows an address to give an allowance to another address
to be able to retrieve tokens from it. This getter returns the remaining
number of tokens that the `spender` will be allowed to spend on behalf of
`owner`. This function is a getter and does not modify the state of the
contract and should return 0 by default.

## Functions

    
    
    1function transfer(address recipient, uint256 amount) external returns (bool);
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Moves the `amount` of tokens from the function caller address (`msg.sender`)
to the recipient address. This function emits the `Transfer` event defined
later. It returns true if the transfer was possible.

    
    
    1function approve(address spender, uint256 amount) external returns (bool);
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Set the amount of `allowance` the `spender` is allowed to transfer from the
function caller (`msg.sender`) balance. This function emits the Approval
event. The function returns whether the allowance was successfully set.

    
    
    1function transferFrom(address sender, address recipient, uint256 amount) external returns (bool);
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Moves the `amount` of tokens from `sender` to `recipient` using the allowance
mechanism. amount is then deducted from the caller’s allowance. This function
emits the `Transfer` event.

## Events

    
    
    1event Transfer(address indexed from, address indexed to, uint256 value);
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

This event is emitted when the amount of tokens (value) is sent from the
`from` address to the `to` address.

In the case of minting new tokens, the transfer is usually `from` the
0x00..0000 address while in the case of burning tokens the transfer is `to`
0x00..0000.

    
    
    1event Approval(address indexed owner, address indexed spender, uint256 value);
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

This event is emitted when the amount of tokens (`value`) is approved by the
`owner` to be used by the `spender`.

## A basic implementation of ERC-20 tokens

Here is the most simple code to base your ERC-20 token from:

    
    
    1pragma solidity ^0.8.0;
    
    2
    
    3interface IERC20 {
    
    4
    
    5    function totalSupply() external view returns (uint256);
    
    6    function balanceOf(address account) external view returns (uint256);
    
    7    function allowance(address owner, address spender) external view returns (uint256);
    
    8
    
    9    function transfer(address recipient, uint256 amount) external returns (bool);
    
    10    function approve(address spender, uint256 amount) external returns (bool);
    
    11    function transferFrom(address sender, address recipient, uint256 amount) external returns (bool);
    
    12
    
    13
    
    14    event Transfer(address indexed from, address indexed to, uint256 value);
    
    15    event Approval(address indexed owner, address indexed spender, uint256 value);
    
    16}
    
    17
    
    18
    
    19contract ERC20Basic is IERC20 {
    
    20
    
    21    string public constant name = "ERC20Basic";
    
    22    string public constant symbol = "ERC";
    
    23    uint8 public constant decimals = 18;
    
    24
    
    25
    
    26    mapping(address => uint256) balances;
    
    27
    
    28    mapping(address => mapping (address => uint256)) allowed;
    
    29
    
    30    uint256 totalSupply_ = 10 ether;
    
    31
    
    32
    
    33   constructor() {
    
    34    balances[msg.sender] = totalSupply_;
    
    35    }
    
    36
    
    37    function totalSupply() public override view returns (uint256) {
    
    38    return totalSupply_;
    
    39    }
    
    40
    
    41    function balanceOf(address tokenOwner) public override view returns (uint256) {
    
    42        return balances[tokenOwner];
    
    43    }
    
    44
    
    45    function transfer(address receiver, uint256 numTokens) public override returns (bool) {
    
    46        require(numTokens <= balances[msg.sender]);
    
    47        balances[msg.sender] = balances[msg.sender]-numTokens;
    
    48        balances[receiver] = balances[receiver]+numTokens;
    
    49        emit Transfer(msg.sender, receiver, numTokens);
    
    50        return true;
    
    51    }
    
    52
    
    53    function approve(address delegate, uint256 numTokens) public override returns (bool) {
    
    54        allowed[msg.sender][delegate] = numTokens;
    
    55        emit Approval(msg.sender, delegate, numTokens);
    
    56        return true;
    
    57    }
    
    58
    
    59    function allowance(address owner, address delegate) public override view returns (uint) {
    
    60        return allowed[owner][delegate];
    
    61    }
    
    62
    
    63    function transferFrom(address owner, address buyer, uint256 numTokens) public override returns (bool) {
    
    64        require(numTokens <= balances[owner]);
    
    65        require(numTokens <= allowed[owner][msg.sender]);
    
    66
    
    67        balances[owner] = balances[owner]-numTokens;
    
    68        allowed[owner][msg.sender] = allowed[owner][msg.sender]-numTokens;
    
    69        balances[buyer] = balances[buyer]+numTokens;
    
    70        emit Transfer(owner, buyer, numTokens);
    
    71        return true;
    
    72    }
    
    73}
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Another excellent implementation of the ERC-20 token standard is the
[OpenZeppelin ERC-20 implementation(opens in a new
tab)](https://github.com/OpenZeppelin/openzeppelin-
contracts/tree/master/contracts/token/ERC20).

n

Last edit: [@nhsz(opens in a new tab)](https://github.com/nhsz), August 15,
2023

See contributors

### Was this tutorial helpful?

YesNo

  * [Edit page(opens in a new tab)](https://github.com/ethereum/ethereum-org-website/tree/dev/public/content/developers/tutorials/understand-the-erc-20-token-smart-contract/index.md)
  * On this page

    * Getters
    * Functions
    * Events
    * A basic implementation of ERC-20 tokens

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

