Skip to main content

[](/en/)

  * Learn
  * Use
  * Build
  * Participate
  * Research

Search```K`

Languages EN

# Calling a smart contract from JavaScript

transactionsfrontendJavaScriptweb3.js

Beginner

![✍️](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/270d.svg)jdourlens

![📚](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4da.svg)[EthereumDev(opens
in a new tab)](https://ethereumdev.io/calling-a-smart-contract-from-
javascript/)

![📆](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4c6.svg)
April 19, 2020

![⏱️](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/23f1.svg)3
minute read minute read

comp-tutorial-metadata-tip-author 0x19dE91Af973F404EDF5B4c093983a7c6E3EC8ccE

On this page

  * Call: Reading value from a smart contract
  * Send: Sending a transaction to a smart contract function

In this tutorial we’ll see how to call a [smart
contract](/en/developers/docs/smart-contracts/) function from JavaScript.
First is reading the state of a smart contract (e.g. the balance of an ERC20
holder), then we’ll modify the state of the blockchain by making a token
transfer. You should already be familiar with [setting up a JS environment to
interact with the blockchain](/en/developers/tutorials/set-up-web3js-to-use-
ethereum-in-javascript/).

For this example we’ll play with the DAI token, for testing purpose we’ll fork
the blockchain using ganache-cli and unlock an address that already has a lot
of DAI:

    
    
    ganache-cli -f https://mainnet.infura.io/v3/[YOUR INFURA KEY] -d -i 66 1 --unlock 0x4d10ae710Bd8D1C31bd7465c8CBC3add6F279E81

To interact with a smart contract we’ll need its address and ABI:

    
    
    1const ERC20TransferABI = [
    
    2  {
    
    3    constant: false,
    
    4    inputs: [
    
    5      {
    
    6        name: "_to",
    
    7        type: "address",
    
    8      },
    
    9      {
    
    10        name: "_value",
    
    11        type: "uint256",
    
    12      },
    
    13    ],
    
    14    name: "transfer",
    
    15    outputs: [
    
    16      {
    
    17        name: "",
    
    18        type: "bool",
    
    19      },
    
    20    ],
    
    21    payable: false,
    
    22    stateMutability: "nonpayable",
    
    23    type: "function",
    
    24  },
    
    25  {
    
    26    constant: true,
    
    27    inputs: [
    
    28      {
    
    29        name: "_owner",
    
    30        type: "address",
    
    31      },
    
    32    ],
    
    33    name: "balanceOf",
    
    34    outputs: [
    
    35      {
    
    36        name: "balance",
    
    37        type: "uint256",
    
    38      },
    
    39    ],
    
    40    payable: false,
    
    41    stateMutability: "view",
    
    42    type: "function",
    
    43  },
    
    44]
    
    45
    
    46const DAI_ADDRESS = "0x6b175474e89094c44da98b954eedeac495271d0f"
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

For this project we stripped the complete ERC20 ABI to just keep the
`balanceOf` and `transfer` function but you can find [the full ERC20 ABI
here(opens in a new tab)](https://ethereumdev.io/abi-for-erc20-contract-on-
ethereum/).

We then need to instantiate our smart contract:

    
    
    1const web3 = new Web3("http://localhost:8545")
    
    2
    
    3const daiToken = new web3.eth.Contract(ERC20TransferABI, DAI_ADDRESS)
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

We’ll also set up two addresses:

  * the one who will receive the transfer and
  * the one we already unlocked that will send it:

    
    
    1const senderAddress = "0x4d10ae710Bd8D1C31bd7465c8CBC3add6F279E81"
    
    2const receiverAddress = "0x19dE91Af973F404EDF5B4c093983a7c6E3EC8ccE"
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

In the next part we’ll call the `balanceOf` function to retrieve the current
amount of tokens both addresses hold.

## Call: Reading value from a smart contract

The first example will call a “constant” method and execute its smart contract
method in the EVM without sending any transaction. For this we’ll read the
ERC20 balance of an address. [Read our article about ERC20
tokens](/en/developers/tutorials/understand-the-erc-20-token-smart-contract/).

You can access an instantiated smart contract methods that you provided the
ABI for as follows: `yourContract.methods.methodname`. By using the `call`
function you’ll receive the result of executing the function.

    
    
    1daiToken.methods.balanceOf(senderAddress).call(function (err, res) {
    
    2  if (err) {
    
    3    console.log("An error occurred", err)
    
    4    return
    
    5  }
    
    6  console.log("The balance is: ", res)
    
    7})
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Remember that DAI ERC20 has 18 decimals which means you need to remove 18
zeros to get the correct amount. uint256 are returned as strings as JavaScript
does not handle big numeric values. If you’re not sure [how to deal with big
numbers in JS check our tutorial about bignumber.js(opens in a new
tab)](https://ethereumdev.io/how-to-deal-with-big-numbers-in-javascript/).

## Send: Sending a transaction to a smart contract function

For the second example we’ll call the transfer function of the DAI smart
contract to send 10 DAI to our second address. The transfer function accepts
two parameters: the recipient address and the amount of token to transfers:

    
    
    1daiToken.methods
    
    2  .transfer(receiverAddress, "100000000000000000000")
    
    3  .send({ from: senderAddress }, function (err, res) {
    
    4    if (err) {
    
    5      console.log("An error occurred", err)
    
    6      return
    
    7    }
    
    8    console.log("Hash of the transaction: " + res)
    
    9  })
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

The call function returns the hash of the transaction that will be mined into
the blockchain. On Ethereum, transaction hashes are predictable - that’s how
we can get the hash of the transaction before it is executed ([learn how
hashes are calculated here(opens in a new
tab)](https://ethereum.stackexchange.com/questions/45648/how-to-calculate-the-
assigned-txhash-of-a-transaction)).

As the function only submits the transaction to the blockchain, we can’t see
the result until we know when it is mined and included in the blockchain. In
the next tutorial we’ll learn [how to wait for a transaction to be executed on
the blockchain by knowing its hash(opens in a new
tab)](https://ethereumdev.io/waiting-for-a-transaction-to-be-mined-on-
ethereum-with-js/).

p

Last edit: [@pettinarip(opens in a new tab)](https://github.com/pettinarip),
November 23, 2023

See contributors

### Was this tutorial helpful?

YesNo

  * [Edit page(opens in a new tab)](https://github.com/ethereum/ethereum-org-website/tree/dev/public/content/developers/tutorials/calling-a-smart-contract-from-javascript/index.md)
  * On this page

    * Call: Reading value from a smart contract
    * Send: Sending a transaction to a smart contract function

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

