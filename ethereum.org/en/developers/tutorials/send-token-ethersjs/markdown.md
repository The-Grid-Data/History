Skip to main content

[](/en/)

  * Learn
  * Use
  * Build
  * Participate
  * Research

Search```K`

Languages EN

# Sending Tokens Using ethers.js

ETHERS.JSERC-20TOKENS

Beginner

![✍️](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/270d.svg)Kim
YongJun

![📆](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4c6.svg)
April 6, 2021

![⏱️](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/23f1.svg)2
minute read minute read

On this page

  * Send Token Using ethers.js(5.0)
    * In This Tutorial You'll Learn How To
    * To-Get-Started
    * Installing
    * Parameters
  * Notice
  * Sending Procedures
    * 1\. Connect to network (testnet)
    * 2\. Create wallet
    * 3\. Connect Wallet to net
    * 4\. Get current gas price
    * 5\. Define Transaction
    * Transaction parameters
    * 6\. Transfer
  * How to use it
    * Success!
  * send_token()

## Send Token Using ethers.js(5.0)

### In This Tutorial You'll Learn How To

  * Import ethers.js
  * Transfer token
  * Set gas price according to the network traffic situation

### To-Get-Started

To get started, we must first import the ethers.js library into our javascript
Include ethers.js(5.0)

### Installing

    
    
    1/home/ricmoo> npm install --save ethers

ES6 in the Browser

    
    
    1<script type="module">
    
    2  import { ethers } from "https://cdn.ethers.io/lib/ethers-5.0.esm.min.js"
    
    3  // Your code here...
    
    4</script>

ES3(UMD) in the Browser

    
    
    1<script
    
    2  src="https://cdn.ethers.io/lib/ethers-5.0.umd.min.js"
    
    3  type="application/javascript"
    
    4></script>

### Parameters

  1. **`contract_address`** : Token contract address (contract address is needed when the token you want to transfer is not ether)
  2. **`send_token_amount`** : The amount you want to send to the receiver
  3. **`to_address`** : The receiver's address
  4. **`send_account`** : The sender's address
  5. **`private_key`** : Private key of the sender to sign the transaction and actually transfer the tokens

## Notice

`signTransaction(tx)` is removed because `sendTransaction()` does it
internally.

## Sending Procedures

### 1\. Connect to network (testnet)

#### Set Provider (Infura)

Connect to Ropsten testnet

    
    
    1window.ethersProvider = new ethers.providers.InfuraProvider("ropsten")

### 2\. Create wallet

    
    
    1let wallet = new ethers.Wallet(private_key)

### 3\. Connect Wallet to net

    
    
    1let walletSigner = wallet.connect(window.ethersProvider)

### 4\. Get current gas price

    
    
    1window.ethersProvider.getGasPrice() // gasPrice

### 5\. Define Transaction

These variables defined below are dependent on `send_token()`

### Transaction parameters

  1. **`send_account`** : address of the token sender
  2. **`to_address`** : address of the token receiver
  3. **`send_token_amount`** : the amount of tokens to send
  4. **`gas_limit`** : gas limit
  5. **`gas_price`** : gas price

See below for how to use

    
    
    1const tx = {
    
    2  from: send_account,
    
    3  to: to_address,
    
    4  value: ethers.utils.parseEther(send_token_amount),
    
    5  nonce: window.ethersProvider.getTransactionCount(send_account, "latest"),
    
    6  gasLimit: ethers.utils.hexlify(gas_limit), // 100000
    
    7  gasPrice: gas_price,
    
    8}

### 6\. Transfer

    
    
    1walletSigner.sendTransaction(tx).then((transaction) => {
    
    2  console.dir(transaction)
    
    3  alert("Send finished!")
    
    4})

## How to use it

    
    
    1let private_key =
    
    2  "41559d28e936dc92104ff30691519693fc753ffbee6251a611b9aa1878f12a4d"
    
    3let send_token_amount = "1"
    
    4let to_address = "0x4c10D2734Fb76D3236E522509181CC3Ba8DE0e80"
    
    5let send_address = "0xda27a282B5B6c5229699891CfA6b900A716539E6"
    
    6let gas_limit = "0x100000"
    
    7let wallet = new ethers.Wallet(private_key)
    
    8let walletSigner = wallet.connect(window.ethersProvider)
    
    9let contract_address = ""
    
    10window.ethersProvider = new ethers.providers.InfuraProvider("ropsten")
    
    11
    
    12send_token(
    
    13  contract_address,
    
    14  send_token_amount,
    
    15  to_address,
    
    16  send_address,
    
    17  private_key
    
    18)
    
    Show all

### Success!

[![image of transaction done
successfully](/_next/image/?url=%2Fcontent%2Fdevelopers%2Ftutorials%2Fsend-
token-ethersjs%2Fsuccessful-
transaction.png&w=1920&q=75)](/content/developers/tutorials/send-token-
ethersjs/successful-transaction.png)

## send_token()

    
    
    1function send_token(
    
    2  contract_address,
    
    3  send_token_amount,
    
    4  to_address,
    
    5  send_account,
    
    6  private_key
    
    7) {
    
    8  let wallet = new ethers.Wallet(private_key)
    
    9  let walletSigner = wallet.connect(window.ethersProvider)
    
    10
    
    11  window.ethersProvider.getGasPrice().then((currentGasPrice) => {
    
    12    let gas_price = ethers.utils.hexlify(parseInt(currentGasPrice))
    
    13    console.log(`gas_price: ${gas_price}`)
    
    14
    
    15    if (contract_address) {
    
    16      // general token send
    
    17      let contract = new ethers.Contract(
    
    18        contract_address,
    
    19        send_abi,
    
    20        walletSigner
    
    21      )
    
    22
    
    23      // How many tokens?
    
    24      let numberOfTokens = ethers.utils.parseUnits(send_token_amount, 18)
    
    25      console.log(`numberOfTokens: ${numberOfTokens}`)
    
    26
    
    27      // Send tokens
    
    28      contract.transfer(to_address, numberOfTokens).then((transferResult) => {
    
    29        console.dir(transferResult)
    
    30        alert("sent token")
    
    31      })
    
    32    } // ether send
    
    33    else {
    
    34      const tx = {
    
    35        from: send_account,
    
    36        to: to_address,
    
    37        value: ethers.utils.parseEther(send_token_amount),
    
    38        nonce: window.ethersProvider.getTransactionCount(
    
    39          send_account,
    
    40          "latest"
    
    41        ),
    
    42        gasLimit: ethers.utils.hexlify(gas_limit), // 100000
    
    43        gasPrice: gas_price,
    
    44      }
    
    45      console.dir(tx)
    
    46      try {
    
    47        walletSigner.sendTransaction(tx).then((transaction) => {
    
    48          console.dir(transaction)
    
    49          alert("Send finished!")
    
    50        })
    
    51      } catch (error) {
    
    52        alert("failed to send!!")
    
    53      }
    
    54    }
    
    55  })
    
    56}
    
    Show all

p

Last edit: [@pettinarip(opens in a new tab)](https://github.com/pettinarip),
December 4, 2023

See contributors

### Was this tutorial helpful?

YesNo

  * [Edit page(opens in a new tab)](https://github.com/ethereum/ethereum-org-website/tree/dev/public/content/developers/tutorials/send-token-ethersjs/index.md)
  * On this page

    * Send Token Using ethers.js(5.0)
      * In This Tutorial You'll Learn How To
      * To-Get-Started
      * Installing
      * Parameters
    * Notice
    * Sending Procedures
      * 1\. Connect to network (testnet)
      * 2\. Create wallet
      * 3\. Connect Wallet to net
      * 4\. Get current gas price
      * 5\. Define Transaction
      * Transaction parameters
      * 6\. Transfer
    * How to use it
      * Success!
    * send_token()

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

