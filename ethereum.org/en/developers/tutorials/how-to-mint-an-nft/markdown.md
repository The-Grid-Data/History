Skip to main content

[](/en/)

  * Learn
  * Use
  * Build
  * Participate
  * Research

Search```K`

Languages EN

# How to Mint an NFT (Part 2/3 of NFT Tutorial Series)

ERC-721alchemysoliditysmart contracts

Beginner

![✍️](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/270d.svg)Sumi
Mudgil

![📆](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4c6.svg)
April 22, 2021

![⏱️](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/23f1.svg)9
minute read minute read

On this page

  * Step 1: Install Web3
  * Step 2: Create a mint-nft.js file
  * Step 3: Grab your contract ABI
  * Step 4: Configure the metadata for your NFT using IPFS
  * Step 5: Create an instance of your contract
  * Step 6: Update the .env file
  * Step 7: Create your transaction
  * Step 8: Sign the transaction
  * Step 9: Call mintNFT and run node mint-nft.js

[Beeple(opens in a new
tab)](https://www.nytimes.com/2021/03/11/arts/design/nft-auction-christies-
beeple.html): $69 Million [3LAU(opens in a new
tab)](https://www.forbes.com/sites/abrambrown/2021/03/03/3lau-nft-nonfungible-
tokens-justin-blau/?sh=5f72ef64643b): $11 Million [Grimes(opens in a new
tab)](https://www.theguardian.com/music/2021/mar/02/grimes-sells-digital-art-
collection-non-fungible-tokens): $6 Million

All of them minted their NFTs using Alchemy’s powerful API. In this tutorial,
we’ll teach you how to do the same in <10 minutes.

“Minting an NFT” is the act of publishing a unique instance of your ERC-721
token on the blockchain. Using our smart contract from [Part 1 of this NFT
tutorial series](/en/developers/tutorials/how-to-write-and-deploy-an-nft/),
let’s flex our Web3 skills and mint an NFT. At the end of this tutorial,
you’ll be able to mint as many NFTs as your heart (and wallet) desires!

Let’s get started!

## Step 1: Install Web3

If you followed the first tutorial on creating your NFT smart contract, you
already have experience using Ethers.js. Web3 is similar to Ethers, as it is a
library used to make creating requests to the Ethereum blockchain easier. In
this tutorial we’ll be using [Alchemy Web3(opens in a new
tab)](https://docs.alchemyapi.io/alchemy/documentation/alchemy-web3), which is
an enhanced Web3 library that offers automatic retries and robust WebSocket
support.

In your project home directory run:

    
    
    1npm install @alch/alchemy-web3

## Step 2: Create a `mint-nft.js`file

Inside your scripts directory, create a `mint-nft.js` file and add the
following lines of code:

    
    
    1require("dotenv").config()
    
    2const API_URL = process.env.API_URL
    
    3const { createAlchemyWeb3 } = require("@alch/alchemy-web3")
    
    4const web3 = createAlchemyWeb3(API_URL)
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

## Step 3: Grab your contract ABI

Our contract ABI (Application Binary Interface) is the interface to interact
with our smart contract. You can learn more about Contract ABIs [here(opens in
a new tab)](https://docs.alchemyapi.io/alchemy/guides/eth_getlogs#what-are-ab-
is). Hardhat automatically generates an ABI for us and saves it in the
`MyNFT.json` file. In order to use this we’ll need to parse out the contents
by adding the following lines of code to our `mint-nft.js` file:

    
    
    1const contract = require("../artifacts/contracts/MyNFT.sol/MyNFT.json")
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

If you want to see the ABI you can print it to your console:

    
    
    1console.log(JSON.stringify(contract.abi))
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

To run `mint-nft.js` and see your ABI printed to the console navigate to your
terminal and run:

    
    
    1node scripts/mint-nft.js
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

## Step 4: Configure the metadata for your NFT using IPFS

If you remember from our tutorial in Part 1, our `mintNFT` smart contract
function takes in a tokenURI parameter that should resolve to a JSON document
describing the NFT's metadata— which is really what brings the NFT to life,
allowing it to have configurable properties, such as a name, description,
image, and other attributes.

> _Interplanetary File System (IPFS) is a decentralized protocol and peer-to-
> peer network for storing and sharing data in a distributed file system._

We will use Pinata, a convenient IPFS API and toolkit, to store our NFT asset
and metadata to ensure our NFT is truly decentralized. If you don’t have a
Pinata account, sign up for a free account [here(opens in a new
tab)](https://app.pinata.cloud) and complete the steps to verify your email.

Once you’ve created an account:

  * Navigate to the “Files” page and click the blue "Upload" button at the top-left of the page.

  * Upload an image to Pinata — this will be the image asset for your NFT. Feel free to name the asset whatever you wish

  * After you upload, you'll see the file info in the table on the "Files" page. You'll also see a CID column. You can copy the CID by clicking the copy button next to it. You can view your upload at: `https://gateway.pinata.cloud/ipfs/<CID>`. You can find the image we used on IPFS [here(opens in a new tab)](https://gateway.pinata.cloud/ipfs/QmZdd5KYdCFApWn7eTZJ1qgJu18urJrP9Yh1TZcZrZxxB5), for example.

For the more visual learners, the steps above are summarized here:

[![How to upload your image to Pinata](/content/developers/tutorials/how-to-
mint-an-nft/instructionsPinata.gif)](/content/developers/tutorials/how-to-
mint-an-nft/instructionsPinata.gif)

Now, we’re going to want to upload one more document to Pinata. But before we
do that, we need to create it!

In your root directory, make a new file called `nft-metadata.json` and add the
following json code:

    
    
    1{
    
    2  "attributes": [
    
    3    {
    
    4      "trait_type": "Breed",
    
    5      "value": "Maltipoo"
    
    6    },
    
    7    {
    
    8      "trait_type": "Eye color",
    
    9      "value": "Mocha"
    
    10    }
    
    11  ],
    
    12  "description": "The world's most adorable and sensitive pup.",
    
    13  "image": "ipfs://QmWmvTJmJU3pozR9ZHFmQC2DNDwi2XJtf3QGyYiiagFSWb",
    
    14  "name": "Ramses"
    
    15}
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Feel free to change the data in the json. You can remove or add to the
attributes section. Most importantly, make sure image field points to the
location of your IPFS image — otherwise, your NFT will include a photo of a
(very cute!) dog.

Once you’re done editing the JSON file, save it and upload it to Pinata,
following the same steps we did for uploading the image.

[![How to upload your nft-metadata.json to
Pinata](/content/developers/tutorials/how-to-mint-an-
nft/uploadPinata.gif)](/content/developers/tutorials/how-to-mint-an-
nft/uploadPinata.gif)

## Step 5: Create an instance of your contract

Now, to interact with our contract, we need to create an instance of it in our
code. To do so we’ll need our contract address which we can get from the
deployment or [Etherscan(opens in a new tab)](https://sepolia.etherscan.io/)
by looking up the address you used to deploy the contract.

[![View your contract address on
Etherscan](/_next/image/?url=%2Fcontent%2Fdevelopers%2Ftutorials%2Fhow-to-
mint-an-nft%2Fview-contract-
etherscan.png&w=1920&q=75)](/content/developers/tutorials/how-to-mint-an-
nft/view-contract-etherscan.png)

In the above example, our contract address is
0x5a738a5c5fe46a1fd5ee7dd7e38f722e2aef7778.

Next we will use the Web3 [contract method(opens in a new
tab)](https://docs.web3js.org/api/web3-eth-contract/class/Contract) to create
our contract using the ABI and address. In your `mint-nft.js` file, add the
following:

    
    
    1const contractAddress = "0x5a738a5c5fe46a1fd5ee7dd7e38f722e2aef7778"
    
    2
    
    3const nftContract = new web3.eth.Contract(contract.abi, contractAddress)
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

## Step 6: Update the `.env`file

Now, in order to create and send transactions to the Ethereum chain, we’ll use
your public ethereum account address to get the account nonce (will explain
below).

Add your public key to your `.env` file — if you completed part 1 of the
tutorial, our `.env` file should now look like this:

    
    
    1API_URL = "https://eth-sepolia.g.alchemy.com/v2/your-api-key"
    
    2PRIVATE_KEY = "your-private-account-address"
    
    3PUBLIC_KEY = "your-public-account-address"
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

## Step 7: Create your transaction

First, let’s define a function named `mintNFT(tokenData)` and create our
transaction by doing the following:

  1. Grab your _PRIVATE_KEY_ and _PUBLIC_KEY_ from the `.env` file.

  2. Next, we’ll need to figure out the account nonce. The nonce specification is used to keep track of the number of transactions sent from your address — which we need for security purposes and to prevent [replay attacks(opens in a new tab)](https://docs.alchemyapi.io/resources/blockchain-glossary#account-nonce). To get the number of transactions sent from your address, we use [getTransactionCount(opens in a new tab)](https://docs.alchemyapi.io/documentation/alchemy-api-reference/json-rpc#eth_gettransactioncount).

  3. Finally we’ll set up our transaction with the following info:

  * `'from': PUBLIC_KEY` — The origin of our transaction is our public address

  * `'to': contractAddress` — The contract we wish to interact with and send the transaction

  * `'nonce': nonce` — The account nonce with the number of transactions sent from our address

  * `'gas': estimatedGas` — The estimated gas needed to complete the transaction

  * `'data': nftContract.methods.mintNFT(PUBLIC_KEY, md).encodeABI()` — The computation we wish to perform in this transaction — which in this case is minting a NFT

Your `mint-nft.js` file should look like this now:

    
    
    1   require('dotenv').config();
    
    2   const API_URL = process.env.API_URL;
    
    3   const PUBLIC_KEY = process.env.PUBLIC_KEY;
    
    4   const PRIVATE_KEY = process.env.PRIVATE_KEY;
    
    5
    
    6   const { createAlchemyWeb3 } = require("@alch/alchemy-web3");
    
    7   const web3 = createAlchemyWeb3(API_URL);
    
    8
    
    9   const contract = require("../artifacts/contracts/MyNFT.sol/MyNFT.json");
    
    10   const contractAddress = "0x5a738a5c5fe46a1fd5ee7dd7e38f722e2aef7778";
    
    11   const nftContract = new web3.eth.Contract(contract.abi, contractAddress);
    
    12
    
    13   async function mintNFT(tokenURI) {
    
    14     const nonce = await web3.eth.getTransactionCount(PUBLIC_KEY, 'latest'); //get latest nonce
    
    15
    
    16   //the transaction
    
    17     const tx = {
    
    18       'from': PUBLIC_KEY,
    
    19       'to': contractAddress,
    
    20       'nonce': nonce,
    
    21       'gas': 500000,
    
    22       'data': nftContract.methods.mintNFT(PUBLIC_KEY, tokenURI).encodeABI()
    
    23     };
    
    24   }​
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

## Step 8: Sign the transaction

Now that we’ve created our transaction, we need to sign it in order to send it
off. Here is where we’ll use our private key.

`web3.eth.sendSignedTransaction` will give us the transaction hash, which we
can use to make sure our transaction was mined and didn't get dropped by the
network. You'll notice in the transaction signing section, we've added some
error checking so we know if our transaction successfully went through.

    
    
    1require("dotenv").config()
    
    2const API_URL = process.env.API_URL
    
    3const PUBLIC_KEY = process.env.PUBLIC_KEY
    
    4const PRIVATE_KEY = process.env.PRIVATE_KEY
    
    5
    
    6const { createAlchemyWeb3 } = require("@alch/alchemy-web3")
    
    7const web3 = createAlchemyWeb3(API_URL)
    
    8
    
    9const contract = require("../artifacts/contracts/MyNFT.sol/MyNFT.json")
    
    10const contractAddress = "0x5a738a5c5fe46a1fd5ee7dd7e38f722e2aef7778"
    
    11const nftContract = new web3.eth.Contract(contract.abi, contractAddress)
    
    12
    
    13async function mintNFT(tokenURI) {
    
    14  const nonce = await web3.eth.getTransactionCount(PUBLIC_KEY, "latest") //get latest nonce
    
    15
    
    16  //the transaction
    
    17  const tx = {
    
    18    from: PUBLIC_KEY,
    
    19    to: contractAddress,
    
    20    nonce: nonce,
    
    21    gas: 500000,
    
    22    data: nftContract.methods.mintNFT(PUBLIC_KEY, tokenURI).encodeABI(),
    
    23  }
    
    24
    
    25  const signPromise = web3.eth.accounts.signTransaction(tx, PRIVATE_KEY)
    
    26  signPromise
    
    27    .then((signedTx) => {
    
    28      web3.eth.sendSignedTransaction(
    
    29        signedTx.rawTransaction,
    
    30        function (err, hash) {
    
    31          if (!err) {
    
    32            console.log(
    
    33              "The hash of your transaction is: ",
    
    34              hash,
    
    35              "\nCheck Alchemy's Mempool to view the status of your transaction!"
    
    36            )
    
    37          } else {
    
    38            console.log(
    
    39              "Something went wrong when submitting your transaction:",
    
    40              err
    
    41            )
    
    42          }
    
    43        }
    
    44      )
    
    45    })
    
    46    .catch((err) => {
    
    47      console.log(" Promise failed:", err)
    
    48    })
    
    49}
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

## Step 9: Call `mintNFT` and run node `mint-nft.js`

Remember the `metadata.json` you uploaded to Pinata? Get its hashcode from
Pinata and pass the following as parameter to the function `mintNFT`
`https://gateway.pinata.cloud/ipfs/<metadata-hash-code>`

Here’s how to get the hashcode:

[![How to get your nft metadata hashcode on
Pinata](/content/developers/tutorials/how-to-mint-an-
nft/metadataPinata.gif)](/content/developers/tutorials/how-to-mint-an-
nft/metadataPinata.gif)_How to get your nft metadata hashcode on Pinata_

> Double check that the hashcode you copied links to your **metadata.json** by
> loading `https://gateway.pinata.cloud/ipfs/<metadata-hash-code>` into a
> separate window. The page should look similar to the screenshot below:

[![Your page should display the json
metadata](/_next/image/?url=%2Fcontent%2Fdevelopers%2Ftutorials%2Fhow-to-mint-
an-nft%2FmetadataJSON.png&w=1920&q=75)](/content/developers/tutorials/how-to-
mint-an-nft/metadataJSON.png)_Your page should display the json metadata_

Altogether, your code should look something like this:

    
    
    1require("dotenv").config()
    
    2const API_URL = process.env.API_URL
    
    3const PUBLIC_KEY = process.env.PUBLIC_KEY
    
    4const PRIVATE_KEY = process.env.PRIVATE_KEY
    
    5
    
    6const { createAlchemyWeb3 } = require("@alch/alchemy-web3")
    
    7const web3 = createAlchemyWeb3(API_URL)
    
    8
    
    9const contract = require("../artifacts/contracts/MyNFT.sol/MyNFT.json")
    
    10const contractAddress = "0x5a738a5c5fe46a1fd5ee7dd7e38f722e2aef7778"
    
    11const nftContract = new web3.eth.Contract(contract.abi, contractAddress)
    
    12
    
    13async function mintNFT(tokenURI) {
    
    14  const nonce = await web3.eth.getTransactionCount(PUBLIC_KEY, "latest") //get latest nonce
    
    15
    
    16  //the transaction
    
    17  const tx = {
    
    18    from: PUBLIC_KEY,
    
    19    to: contractAddress,
    
    20    nonce: nonce,
    
    21    gas: 500000,
    
    22    data: nftContract.methods.mintNFT(PUBLIC_KEY, tokenURI).encodeABI(),
    
    23  }
    
    24
    
    25  const signPromise = web3.eth.accounts.signTransaction(tx, PRIVATE_KEY)
    
    26  signPromise
    
    27    .then((signedTx) => {
    
    28      web3.eth.sendSignedTransaction(
    
    29        signedTx.rawTransaction,
    
    30        function (err, hash) {
    
    31          if (!err) {
    
    32            console.log(
    
    33              "The hash of your transaction is: ",
    
    34              hash,
    
    35              "\nCheck Alchemy's Mempool to view the status of your transaction!"
    
    36            )
    
    37          } else {
    
    38            console.log(
    
    39              "Something went wrong when submitting your transaction:",
    
    40              err
    
    41            )
    
    42          }
    
    43        }
    
    44      )
    
    45    })
    
    46    .catch((err) => {
    
    47      console.log("Promise failed:", err)
    
    48    })
    
    49}
    
    50
    
    51mintNFT("ipfs://QmYueiuRNmL4MiA2GwtVMm6ZagknXnSpQnB3z2gWbz36hP")
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Now, run `node scripts/mint-nft.js` to deploy your NFT. After a couple of
seconds, you should see a response like this in your terminal:

    
    
    1The hash of your transaction is: 0x301791fdf492001fcd9d5e5b12f3aa1bbbea9a88ed24993a8ab2cdae2d06e1e8
    
    2
    
    3Check Alchemy's Mempool to view the status of your transaction!

Next, visit your [Alchemy mempool(opens in a new
tab)](https://dashboard.alchemyapi.io/mempool) to see the status of your
transaction (whether it’s pending, mined, or got dropped by the network). If
your transaction got dropped, it’s also helpful to check [Sepolia
Etherscan(opens in a new tab)](https://sepolia.etherscan.io/) and search for
your transaction hash.

[![View your NFT transaction hash on
Etherscan](/_next/image/?url=%2Fcontent%2Fdevelopers%2Ftutorials%2Fhow-to-
mint-an-nft%2Fview-nft-
etherscan.png&w=1920&q=75)](/content/developers/tutorials/how-to-mint-an-
nft/view-nft-etherscan.png)_View your NFT transaction hash on Etherscan_

And that’s it! You’ve now deployed AND minted with a NFT on the Ethereum
blockchain
![🤑](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f911.svg)

Using the `mint-nft.js` you can mint as many NFTs as your heart (and wallet)
desires! Just be sure to pass in a new tokenURI describing the NFT's metadata
(otherwise, you'll just end up making a bunch of identical ones with different
IDs).

Presumably, you’d like to be able to show off your NFT in your wallet — so be
sure to check out [Part 3: How to View Your NFT in Your
Wallet](/en/developers/tutorials/how-to-view-nft-in-metamask/)!

p

Last edit: [@pettinarip(opens in a new tab)](https://github.com/pettinarip),
November 23, 2023

See contributors

### Was this tutorial helpful?

YesNo

  * [Edit page(opens in a new tab)](https://github.com/ethereum/ethereum-org-website/tree/dev/public/content/developers/tutorials/how-to-mint-an-nft/index.md)
  * On this page

    * Step 1: Install Web3
    * Step 2: Create a mint-nft.js file
    * Step 3: Grab your contract ABI
    * Step 4: Configure the metadata for your NFT using IPFS
    * Step 5: Create an instance of your contract
    * Step 6: Update the .env file
    * Step 7: Create your transaction
    * Step 8: Sign the transaction
    * Step 9: Call mintNFT and run node mint-nft.js

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

