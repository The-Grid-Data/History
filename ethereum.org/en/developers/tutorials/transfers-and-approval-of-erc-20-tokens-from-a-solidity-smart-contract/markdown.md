Skip to main content

[](/en/)

  * Learn
  * Use
  * Build
  * Participate
  * Research

Search```K`

Languages EN

# Transfers and approval of ERC-20 tokens from a solidity smart contract

smart contractstokenssolidityerc-20

Intermediate

![✍️](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/270d.svg)jdourlens

![📚](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4da.svg)[EthereumDev(opens
in a new tab)](https://ethereumdev.io/transfers-and-approval-or-erc20-tokens-
from-a-solidity-smart-contract/)

![📆](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4c6.svg)
April 7, 2020

![⏱️](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/23f1.svg)7
minute read minute read

comp-tutorial-metadata-tip-author 0x19dE91Af973F404EDF5B4c093983a7c6E3EC8ccE

On this page

  * The buy function
  * The sell function

In the previous tutorial we studied [the anatomy of an ERC-20 token in
Solidity](/en/developers/tutorials/understand-the-erc-20-token-smart-
contract/) on the Ethereum blockchain. In this article we’ll see how we can
use a smart contract to interact with a token using the Solidity language.

For this smart contract, we’ll create a really dummy decentralized exchange
where a user can trade ether for our newly deployed [ERC-20
token](/en/developers/docs/standards/tokens/erc-20/).

For this tutorial we’ll use the code we wrote in the previous tutorial as a
base. Our DEX will instantiate an instance of the contract in its constructor
and perform the operations of:

  * exchanging tokens to ether
  * exchanging ether to tokens

We’ll start our Decentralized exchange code by adding our simple ERC20
codebase:

    
    
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
    
    74
    
    75
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Our new DEX smart contract will deploy the ERC-20 and get all the supplied:

    
    
    1contract DEX {
    
    2
    
    3    IERC20 public token;
    
    4
    
    5    event Bought(uint256 amount);
    
    6    event Sold(uint256 amount);
    
    7
    
    8    constructor() {
    
    9        token = new ERC20Basic();
    
    10    }
    
    11
    
    12    function buy() payable public {
    
    13        // TODO
    
    14    }
    
    15
    
    16    function sell(uint256 amount) public {
    
    17        // TODO
    
    18    }
    
    19
    
    20}
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

So we now have our DEX and it has all the token reserve available. The
contract has two functions:

  * `buy`: The user can send ether and get tokens in exchange
  * `sell`: The user can decide to send tokens to get ether back

## The buy function

Let’s code the buy function. We’ll first need to check the amount of ether the
message contains and verify that the contracts own enough tokens and that the
message has some ether in it. If the contract owns enough tokens it’ll send
the number of tokens to the user and emit the `Bought` event.

Note that if we call the require function in the case of an error the ether
sent will directly be reverted and given back to the user.

To keep things simple, we just exchange 1 token for 1 Wei.

    
    
    1function buy() payable public {
    
    2    uint256 amountTobuy = msg.value;
    
    3    uint256 dexBalance = token.balanceOf(address(this));
    
    4    require(amountTobuy > 0, "You need to send some ether");
    
    5    require(amountTobuy <= dexBalance, "Not enough tokens in the reserve");
    
    6    token.transfer(msg.sender, amountTobuy);
    
    7    emit Bought(amountTobuy);
    
    8}
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

In the case where the buy is successful we should see two events in the
transaction: The token `Transfer` and the `Bought` event.

[![Two events in the transaction: Transfer and
Bought](/_next/image/?url=%2Fcontent%2Fdevelopers%2Ftutorials%2Ftransfers-and-
approval-of-erc-20-tokens-from-a-solidity-smart-contract%2Ftransfer-and-
bought-events.png&w=1920&q=75)](/content/developers/tutorials/transfers-and-
approval-of-erc-20-tokens-from-a-solidity-smart-contract/transfer-and-bought-
events.png)

## The sell function

The function responsible for the sell will first require the user to have
approved the amount by calling the approve function beforehand. Approving the
transfer requires the ERC20Basic token instantiated by the DEX to be called by
the user. This can be achieved by first calling the DEX contract's `token()`
function to retrieve the address where DEX deployed the ERC20Basic contract
called `token`. Then we create an instance of that contract in our session and
call its `approve` function. Then we are able to call the DEX's `sell`
function and swap our tokens back for ether. For example, this is how this
looks in an interactive brownie session:

    
    
    1#### Python in interactive brownie console...
    
    2
    
    3# deploy the DEX
    
    4dex = DEX.deploy({'from':account1})
    
    5
    
    6# call the buy function to swap ether for token
    
    7# 1e18 is 1 ether denominated in wei
    
    8dex.buy({'from': account2, 1e18})
    
    9
    
    10# get the deployment address for the ERC20 token
    
    11# that was deployed during DEX contract creation
    
    12# dex.token() returns the deployed address for token
    
    13token = ERC20Basic.at(dex.token())
    
    14
    
    15# call the token's approve function
    
    16# approve the dex address as spender
    
    17# and how many of your tokens it is allowed to spend
    
    18token.approve(dex.address, 3e18, {'from':account2})
    
    19
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Then when the sell function is called, we’ll check if the transfer from the
caller address to the contract address was successful and then send the Ethers
back to the caller address.

    
    
    1function sell(uint256 amount) public {
    
    2    require(amount > 0, "You need to sell at least some tokens");
    
    3    uint256 allowance = token.allowance(msg.sender, address(this));
    
    4    require(allowance >= amount, "Check the token allowance");
    
    5    token.transferFrom(msg.sender, address(this), amount);
    
    6    payable(msg.sender).transfer(amount);
    
    7    emit Sold(amount);
    
    8}
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

If everything works you should see 2 events (a `Transfer` and `Sold`) in the
transaction and your token balance and ether balance updated.

[![Two events in the transaction: Transfer and
Sold](/_next/image/?url=%2Fcontent%2Fdevelopers%2Ftutorials%2Ftransfers-and-
approval-of-erc-20-tokens-from-a-solidity-smart-contract%2Ftransfer-and-sold-
events.png&w=1920&q=75)](/content/developers/tutorials/transfers-and-approval-
of-erc-20-tokens-from-a-solidity-smart-contract/transfer-and-sold-events.png)

From this tutorial we saw how to check the balance and allowance of an ERC-20
token and also how to call `Transfer` and `TransferFrom` of an ERC20 smart
contract using the interface.

Once you make a transaction we have a JavaScript tutorial to [wait and get
details about the transactions(opens in a new
tab)](https://ethereumdev.io/waiting-for-a-transaction-to-be-mined-on-
ethereum-with-js/) that were made to your contract and a [tutorial to decode
events generated by token transfers or any other events(opens in a new
tab)](https://ethereumdev.io/how-to-decode-event-logs-in-javascript-using-abi-
decoder/) as long as you have the ABI.

Here is the complete code for the tutorial:

    
    
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
    
    74
    
    75
    
    76contract DEX {
    
    77
    
    78    event Bought(uint256 amount);
    
    79    event Sold(uint256 amount);
    
    80
    
    81
    
    82    IERC20 public token;
    
    83
    
    84    constructor() {
    
    85        token = new ERC20Basic();
    
    86    }
    
    87
    
    88    function buy() payable public {
    
    89        uint256 amountTobuy = msg.value;
    
    90        uint256 dexBalance = token.balanceOf(address(this));
    
    91        require(amountTobuy > 0, "You need to send some ether");
    
    92        require(amountTobuy <= dexBalance, "Not enough tokens in the reserve");
    
    93        token.transfer(msg.sender, amountTobuy);
    
    94        emit Bought(amountTobuy);
    
    95    }
    
    96
    
    97    function sell(uint256 amount) public {
    
    98        require(amount > 0, "You need to sell at least some tokens");
    
    99        uint256 allowance = token.allowance(msg.sender, address(this));
    
    100        require(allowance >= amount, "Check the token allowance");
    
    101        token.transferFrom(msg.sender, address(this), amount);
    
    102        payable(msg.sender).transfer(amount);
    
    103        emit Sold(amount);
    
    104    }
    
    105
    
    106}
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

n

Last edit: [@nhsz(opens in a new tab)](https://github.com/nhsz), August 15,
2023

See contributors

### Was this tutorial helpful?

YesNo

  * [Edit page(opens in a new tab)](https://github.com/ethereum/ethereum-org-website/tree/dev/public/content/developers/tutorials/transfers-and-approval-of-erc-20-tokens-from-a-solidity-smart-contract/index.md)
  * On this page

    * The buy function
    * The sell function

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

