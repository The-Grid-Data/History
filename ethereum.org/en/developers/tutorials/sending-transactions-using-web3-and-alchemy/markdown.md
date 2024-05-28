Skip to main content

[](/en/)

  * Learn
  * Use
  * Build
  * Participate
  * Research

Search```K`

Languages EN

# Sending Transactions Using Web3

transactionsweb3.jsalchemy

Beginner

![✍️](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/270d.svg)Elan
Halpern

![📚](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4da.svg)[Alchemy
docs(opens in a new tab)](https://docs.alchemy.com/alchemy/tutorials/sending-
txs)

![📆](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4c6.svg)
November 4, 2020

![⏱️](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/23f1.svg)10
minute read minute read

On this page

  * The Basics
    * 1\. Alchemy does not store your private keys
    * 2\. What is a “signer”?
    * 3\. Why do I need to sign my transactions?
    * 4\. How do I protect my private key?
    * 5\. What is the difference between eth_sendTransaction and eth_sendRawTransaction?
    * 6\. What is the web3 library?
    * 7\. How to send secure, gas-optimized, and private transactions? {how-to-send-secure-gas-optimized-and-private-transactions}
  * Steps to Sending your Transaction
    * 1\. Create an Alchemy app on the Sepolia testnet
    * 2\. Request ETH from the Sepolia faucet
    * 3\. Create a new project directory and cd into it
    * 4\. Install Alchemy Web3 (or any web3 library)
    * 5\. Install dotenv
    * 6\. Create the .env file
    * 7\. Create sendTx.js file
    * 8\. Run the code using node sendTx.js
    * 9\. See your transaction in the Mempool

This is a beginner friendly guide to sending Ethereum transactions using Web3.
There are three main steps in order to send a transaction to the Ethereum
blockchain: create, sign, and broadcast. We’ll go through all three, hopefully
answering any questions you might have! In this tutorial, we'll be using
[Alchemy(opens in a new tab)](https://www.alchemy.com/) to send our
transactions to the Ethereum chain. You can [create a free Alchemy account
here(opens in a new tab)](https://auth.alchemyapi.io/signup).

**NOTE:** This guide is for signing your transactions on the _backend_ for
your app. If you want to integrate signing your transactions on the frontend,
check out integrating [Web3 with a browser provider(opens in a new
tab)](https://docs.alchemy.com/reference/api-overview#with-a-browser-
provider).

## The Basics

Like most blockchain developers when they first start, you might have done
some research on how to send a transaction (something that should be pretty
simple) and ran into a plethora of guides, each saying different things and
leaving you a bit overwhelmed and confused. If you’re in that boat, don’t
worry; we all were at some point! So, before we start, let’s get a few things
straight:

### 1.Alchemy does not store your private keys

  * This means that Alchemy cannot sign and send transactions on your behalf. The reason for this is security purposes. Alchemy will never ask you to share your private key, and you should never share your private key with a hosted node (or anyone for that matter).
  * You can read from the blockchain using Alchemy’s core API, but to write to it you’ll need to use something else to sign your transactions before sending them through Alchemy (this is the same for any other [node service](/en/developers/docs/nodes-and-clients/nodes-as-a-service/)).

### 2.What is a “signer”?

  * Signers will sign transactions for you using your private key. In this tutorial we’ll be using [Alchemy web3(opens in a new tab)](https://docs.alchemyapi.io/alchemy/documentation/alchemy-web3) to sign our transaction, but you could also use any other web3 library.
  * On the frontend, a good example of a signer would be [MetaMask(opens in a new tab)](https://metamask.io/), which will sign and send transactions on your behalf.

### 3.Why do I need to sign my transactions?

  * Every user that wants to send a transaction on the Ethereum network must sign the transaction (using their private key), in order to validate that the origin of the transaction is who it claims to be.
  * It is super important to protect this private key, since having access to it grants full control over your Ethereum account, allowing you (or anyone with access) to perform transactions on your behalf.

### 4.How do I protect my private key?

  * There are many ways to protect your private key and to use it to send off transactions. In this tutorial we will be using a `.env` file. However, you could also use a separate provider that stores private keys, use a keystore file, or other options.

### 5. What is the difference between `eth_sendTransaction` and
`eth_sendRawTransaction`?

`eth_sendTransaction` and `eth_sendRawTransaction` are both Ethereum API
functions which broadcast a transaction to the Ethereum network so it will be
added to a future block. They differ in how they handle signing of the
transactions.

  * [`eth_sendTransaction`(opens in a new tab)](https://docs.web3js.org/api/web3-eth/function/sendTransaction) is used for sending _unsigned_ transactions, which means the node you are sending to must manage your private key so it can sign the transaction before broadcasting it to the chain. Since Alchemy doesn't hold user's private keys, they do not support this method.
  * [`eth_sendRawTransaction`(opens in a new tab)](https://docs.alchemyapi.io/documentation/alchemy-api-reference/json-rpc#eth_sendrawtransaction) is used to broadcast transactions that have already been signed. This means you first have to use [`signTransaction(tx, private_key)`(opens in a new tab)](https://docs.web3js.org/api/web3-eth-accounts/function/signTransaction), then pass in the result into `eth_sendRawTransaction`.

When using web3, `eth_sendRawTransaction` is accessed by calling the function
[web3.eth.sendSignedTransaction(opens in a new
tab)](https://docs.web3js.org/api/web3-eth/function/sendSignedTransaction).

This is what we will be using in this tutorial.

### 6.What is the web3 library?

  * Web3.js is a wrapper library around the standard JSON-RPC calls that is quite common to use in Ethereum development.
  * There are many web3 libraries for different languages. In this tutorial we’ll be using [Alchemy Web3(opens in a new tab)](https://docs.alchemy.com/reference/api-overview) which is written in JavaScript. You can check out other options [here(opens in a new tab)](https://docs.alchemyapi.io/guides/getting-started#other-web3-libraries) like [ethers.js(opens in a new tab)](https://docs.ethers.org/v5/).

Okay, now that we have a few of these questions out of the way, let’s move on
to the tutorial. Feel free to ask questions anytime in the Alchemy
[discord(opens in a new tab)](https://discord.gg/gWuC7zB)!

### 7. How to send secure, gas-optimized, and private transactions? {how-to-
send-secure-gas-optimized-and-private-transactions}

  * [Alchemy has a suite of Transact APIs(opens in a new tab)](https://docs.alchemy.com/reference/transact-api-quickstart). You can use these to send reinforced transactions, simulate transactions before they happen, send private transactions, and send gas-optimized transactions
  * You can also use the [Notify API(opens in a new tab)](https://docs.alchemy.com/docs/alchemy-notify) to be alerted when your transaction is pulled from the mempool and added to the chain

**NOTE:** This guide requires an Alchemy account, an Ethereum address or
MetaMask wallet, NodeJs, and npm installed. If not, follow these steps:

  1. [Create a free Alchemy account(opens in a new tab)](https://auth.alchemyapi.io/signup)
  2. [Create MetaMask account(opens in a new tab)](https://metamask.io/) (or get an Ethereum address)
  3. [Follow these steps to install NodeJs and NPM(opens in a new tab)](https://docs.alchemy.com/alchemy/guides/alchemy-for-macs)

## Steps to Sending your Transaction

### 1.Create an Alchemy app on the Sepolia testnet

Navigate to your [Alchemy Dashboard(opens in a new
tab)](https://dashboard.alchemyapi.io/) and create a new app, choosing Sepolia
(or any other testnet) for your network.

### 2.Request ETH from the Sepolia faucet

Follow the instructions on the [Alchemy Sepolia faucet(opens in a new
tab)](https://www.sepoliafaucet.com/) to receive ETH. Make sure to include
your **Sepolia** Ethereum address (from MetaMask) and not another network.
After following the instructions, double-check that you’ve received the ETH in
your wallet.

### 3. Create a new project directory and `cd`into it

Create a new project directory from the command line (terminal for macs) and
navigate into it:

    
    
    1mkdir sendtx-example
    
    2cd sendtx-example

### 4.Install Alchemy Web3 (or any web3 library)

Run the following command in your project directory to install [Alchemy
Web3(opens in a new tab)](https://docs.alchemy.com/reference/api-overview):

Note, if you'd like to use the ethers.js library, [follow the instructions
here(opens in a new tab)](https://docs.alchemy.com/docs/how-to-send-
transactions-on-ethereum).

    
    
    1npm install @alch/alchemy-web3

### 5.Install dotenv

We’ll use a `.env` file to safely store our API key and private key.

    
    
    1npm install dotenv --save

### 6. Create the `.env`file

Create a `.env` file in your project directory and add the following
(replacing “`your-api-url`" and "`your-private-key`")

  * To find your Alchemy API URL, navigate to the app details page of the app you just created on your dashboard, click “View Key” in the top right corner, and grab the HTTP URL.
  * To find your private key using MetaMask, check out this [guide(opens in a new tab)](https://metamask.zendesk.com/hc/en-us/articles/360015289632-How-to-Export-an-Account-Private-Key).

    
    
    1API_URL = "your-api-url"
    
    2PRIVATE_KEY = "your-private-key"

Don't commit `.env`! Please make sure never to share or expose your `.env`
file with anyone, as you are compromising your secrets in doing so. If you are
using version control, add your `.env` to a [gitignore(opens in a new
tab)](https://git-scm.com/docs/gitignore) file.

### 7. Create `sendTx.js`file

Great, now that we have our sensitive data protected in a `.env` file, let’s
start coding. For our send transaction example, we’ll be sending ETH back to
the Sepolia faucet.

Create a `sendTx.js` file, which is where we will configure and send our
example transaction, and add the following lines of code to it:

    
    
    1async function main() {
    
    2    require('dotenv').config();
    
    3    const { API_URL, PRIVATE_KEY } = process.env;
    
    4    const { createAlchemyWeb3 } = require("@alch/alchemy-web3");
    
    5    const web3 = createAlchemyWeb3(API_URL);
    
    6    const myAddress = '0x610Ae88399fc1687FA7530Aac28eC2539c7d6d63' //TODO: replace this address with your own public address
    
    7
    
    8    const nonce = await web3.eth.getTransactionCount(myAddress, 'latest'); // nonce starts counting from 0
    
    9
    
    10    const transaction = {
    
    11     'to': '0x31B98D14007bDEe637298086988A0bBd31184523', // faucet address to return eth
    
    12     'value': 1000000000000000000, // 1 ETH
    
    13     'gas': 30000,
    
    14     'nonce': nonce,
    
    15     // optional data field to send message or execute smart contract
    
    16    };
    
    17
    
    18    const signedTx = await web3.eth.accounts.signTransaction(transaction, PRIVATE_KEY);
    
    19
    
    20    web3.eth.sendSignedTransaction(signedTx.rawTransaction, function(error, hash) {
    
    21    if (!error) {
    
    22      console.log("🎉 The hash of your transaction is: ", hash, "\n Check Alchemy's Mempool to view the status of your transaction!");
    
    23    } else {
    
    24      console.log("❗Something went wrong while submitting your transaction:", error)
    
    25    }
    
    26   });
    
    27}
    
    28
    
    29main();
    
    Show all

Be sure to replace the address on **line 6** with your own public address.

Now, before we jump into running this code, let's talk about some of the
components here.

  * `nonce` : The nonce specification is used to keep track of the number of transactions sent from your address. We need this for security purposes and to prevent [replay attacks(opens in a new tab)](https://docs.alchemyapi.io/resources/blockchain-glossary#account-nonce). To get the number of transactions sent from your address we use [getTransactionCount(opens in a new tab)](https://docs.alchemyapi.io/documentation/alchemy-api-reference/json-rpc#eth_gettransactioncount).
  * `transaction`: The transaction object has a few aspects we need to specify
    * `to`: This is the address we want to send ETH to. In this case, we are sending ETH back to the [Sepolia faucet(opens in a new tab)](https://sepoliafaucet.com/) we initially requested from.
    * `value`: This is the amount we wish to send, specified in Wei where 10^18 Wei = 1 ETH
    * `gas`: There are many ways to determine the right amount of gas to include with your transaction. Alchemy even has a [gas price webhook(opens in a new tab)](https://docs.alchemyapi.io/guides/alchemy-notify#address-activity-1) to notify you when the gas price falls within a certain threshold. For Mainnet transactions, it's good practice to check a gas estimator like [ETH Gas Station(opens in a new tab)](https://ethgasstation.info/) to determine the right amount of gas to include. 21000 is the minimum amount of gas an operation on Ethereum will use, so to ensure our transaction will be executed we put 30000 here.
    * `nonce`: see above nonce definition. Nonce starts counting from zero.
    * [OPTIONAL] data: Used for sending additional information with your transfer, or calling a smart contract, not required for balance transfers, check out the note below.
  * `signedTx`: To sign our transaction object we will use the `signTransaction` method with our `PRIVATE_KEY`
  * `sendSignedTransaction`: Once we have a signed transaction, we can send it off to be included in a subsequent block by using `sendSignedTransaction`

**A Note on data** There are a two main types of transactions that can be sent
in Ethereum.

  * Balance transfer: Send ETH from one address to another. No data field required, however, if you'd like to send additional information alongside your transaction, you can include that information in HEX format in this field.
    * For example, let's say we wanted to write the hash of an IPFS document to the Ethereum chain in order to give it an immutable timestamp. Our data field should then look like data: `web3.utils.toHex(‘IPFS hash‘)`. And now anyone can query the chain and see when that document was added.
  * Smart contract transaction: Execute some smart contract code on the chain. In this case, the data field should contain the smart function you wish to execute, alongside any parameters.
    * For a practical example, check out Step 8 in this [Hello World Tutorial(opens in a new tab)](https://docs.alchemyapi.io/alchemy/tutorials/hello-world-smart-contract#step-8-create-the-transaction).

### 8. Run the code using `node sendTx.js`

Navigate back to your terminal or command line and run:

    
    
    1node sendTx.js

### 9.See your transaction in the Mempool

Open up the [Mempool page(opens in a new
tab)](https://dashboard.alchemyapi.io/mempool) in your Alchemy dashboard and
filter by the app you created to find your transaction. This is where we can
watch our transaction transition from pending state to mined state (if
successful) or dropped state if unsuccessful. Make sure to keep it on “All” so
that you capture “mined”, “pending”, and “dropped” transactions. You can also
search for your transaction by looking for transactions sent to address
`0x31b98d14007bdee637298086988a0bbd31184523` .

To view the details of your transaction once you’ve found it, select the tx
hash, which should take you to a view that looks like this:

[![Mempool watcher
screenshot](/_next/image/?url=%2Fcontent%2Fdevelopers%2Ftutorials%2Fsending-
transactions-using-web3-and-
alchemy%2Fmempool.png&w=1920&q=75)](/content/developers/tutorials/sending-
transactions-using-web3-and-alchemy/mempool.png)

From there you can view your transaction on Etherscan by clicking on the icon
circled in red!

**Yippieeee! You just sent your first Ethereum transaction using Alchemy 🎉**

 _For feedback and suggestions about this guide, please message Elan on
Alchemy’s[Discord(opens in a new tab)](https://discord.gg/A39JVCM)!_

_Originally published at<https://docs.alchemyapi.io/tutorials/sending-
transactions-using-web3-and-alchemy>[(opens in a new
tab)](https://docs.alchemyapi.io/tutorials/sending-transactions-using-
web3-and-alchemy)_

n

Last edit: [@nhsz(opens in a new tab)](https://github.com/nhsz), August 15,
2023

See contributors

### Was this tutorial helpful?

YesNo

  * [Edit page(opens in a new tab)](https://github.com/ethereum/ethereum-org-website/tree/dev/public/content/developers/tutorials/sending-transactions-using-web3-and-alchemy/index.md)
  * On this page

    * The Basics
      * 1\. Alchemy does not store your private keys
      * 2\. What is a “signer”?
      * 3\. Why do I need to sign my transactions?
      * 4\. How do I protect my private key?
      * 5\. What is the difference between eth_sendTransaction and eth_sendRawTransaction?
      * 6\. What is the web3 library?
      * 7\. How to send secure, gas-optimized, and private transactions? {how-to-send-secure-gas-optimized-and-private-transactions}
    * Steps to Sending your Transaction
      * 1\. Create an Alchemy app on the Sepolia testnet
      * 2\. Request ETH from the Sepolia faucet
      * 3\. Create a new project directory and cd into it
      * 4\. Install Alchemy Web3 (or any web3 library)
      * 5\. Install dotenv
      * 6\. Create the .env file
      * 7\. Create sendTx.js file
      * 8\. Run the code using node sendTx.js
      * 9\. See your transaction in the Mempool

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

