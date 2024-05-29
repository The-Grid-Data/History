Skip to main content

[](/en/)

  * Learn
  * Use
  * Build
  * Participate
  * Research

Search```K`

Languages EN

# Deploying your first smart contract

smart contractsremixsoliditydeploying

Beginner

![✍️](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/270d.svg)jdourlens

![📚](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4da.svg)[EthereumDev(opens
in a new tab)](https://ethereumdev.io/deploying-your-first-smart-contract/)

![📆](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4c6.svg)
April 3, 2020

![⏱️](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/23f1.svg)4
minute read minute read

comp-tutorial-metadata-tip-author 0x19dE91Af973F404EDF5B4c093983a7c6E3EC8ccE

On this page

  * Writing our contract
  * Deploying our contract

I guess you are as excited as us to [deploy](/en/developers/docs/smart-
contracts/deploying/) and interact with your first [smart
contract](/en/developers/docs/smart-contracts/) on the Ethereum blockchain.

Don’t worry, as it’s our first smart contract, we’ll deploy it on a [local
test network](/en/developers/docs/networks/) so it does not cost anything for
you to deploy and play as much as you’d like with it.

## Writing our contract

First step is to [visit Remix(opens in a new
tab)](https://remix.ethereum.org/) and create a new file. On the upper left
part of the Remix interface add a new file and enter the file name you want.

[![Adding a new file in the Remix
interface](/_next/image/?url=%2Fcontent%2Fdevelopers%2Ftutorials%2Fdeploying-
your-first-smart-
contract%2Fremix.png&w=1920&q=75)](/content/developers/tutorials/deploying-
your-first-smart-contract/remix.png)

In the new file, we’ll paste the following code.

    
    
    1// SPDX-License-Identifier: MIT
    
    2pragma solidity >=0.5.17;
    
    3
    
    4contract Counter {
    
    5
    
    6    // Public variable of type unsigned int to keep the number of counts
    
    7    uint256 public count = 0;
    
    8
    
    9    // Function that increments our counter
    
    10    function increment() public {
    
    11        count += 1;
    
    12    }
    
    13
    
    14    // Not necessary getter to get the count value
    
    15    function getCount() public view returns (uint256) {
    
    16        return count;
    
    17    }
    
    18
    
    19}
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

If you’re used to programming you can easily guess what this program does.
Here is an explainer line by line:

  * Line 4: We define a contract with the name `Counter`.
  * Line 7: Our contract stores one unsigned integer named `count` starting at 0.
  * Line 10: The first function will modify the state of the contract and `increment()` our variable `count`.
  * Line 15: The second function is just a getter to be able to read the value of the `count` variable outside of the smart contract. Note that, as we defined our `count` variable as public this is not necessary but is shown as an example.

This is all for our first simple smart contract. As you may know, it looks
like a class from OOP (Object-Oriented Programming) languages like Java or
C++. It’s now time to play with our contract.

## Deploying our contract

As we wrote our very first smart contract, we’ll now deploy it to the
blockchain to be able to play with it.

[Deploying the smart contract on the blockchain](/en/developers/docs/smart-
contracts/deploying/) is actually just sending a transaction containing the
code of the compiled smart contract without specifying any recipients.

We’ll first [compile the contract](/en/developers/docs/smart-
contracts/compiling/) by clicking on the compile icon on the left hand side:

[![The compile icon in the Remix
toolbar](/_next/image/?url=%2Fcontent%2Fdevelopers%2Ftutorials%2Fdeploying-
your-first-smart-contract%2Fremix-compile-
button.png&w=750&q=75)](/content/developers/tutorials/deploying-your-first-
smart-contract/remix-compile-button.png)

Then click on the compile button:

[![The compile button in the Remix solidity
compiler](/_next/image/?url=%2Fcontent%2Fdevelopers%2Ftutorials%2Fdeploying-
your-first-smart-contract%2Fremix-
compile.png&w=1080&q=75)](/content/developers/tutorials/deploying-your-first-
smart-contract/remix-compile.png)

You can choose to select the “Auto compile” option so the contract will always
be compiled when you save the content on the text editor.

Then navigate to the "deploy and run transactions" screen:

[![The deploy icon in the Remix
toolbar](/_next/image/?url=%2Fcontent%2Fdevelopers%2Ftutorials%2Fdeploying-
your-first-smart-contract%2Fremix-
deploy.png&w=1200&q=75)](/content/developers/tutorials/deploying-your-first-
smart-contract/remix-deploy.png)

Once you are on the "deploy and run transactions" screen, double check that
your contract name appears and click on Deploy. As you can see on the top of
the page, the current environment is “JavaScript VM” that means that we’ll
deploy and interact with our smart contract on a local test blockchain to be
able to test faster and without any fees.

[![The deploy button in the Remix solidity
compiler](/_next/image/?url=%2Fcontent%2Fdevelopers%2Ftutorials%2Fdeploying-
your-first-smart-contract%2Fremix-deploy-
button.png&w=1920&q=75)](/content/developers/tutorials/deploying-your-first-
smart-contract/remix-deploy-button.png)

Once you've clicked the “Deploy” button, you’ll see your contract appear on
the bottom. Click the arrow on the left to expand it so we’ll see the content
of our contract. This is our variable `counter`, our `increment()` function
and the getter `getCounter()`.

If you click on the `count` or `getCount` button, it will actually retrieve
the content of the contract’s `count` variable and display it. As we did not
called the `increment` function yet, it should display 0.

[![The function button in the Remix solidity
compiler](/_next/image/?url=%2Fcontent%2Fdevelopers%2Ftutorials%2Fdeploying-
your-first-smart-contract%2Fremix-function-
button.png&w=750&q=75)](/content/developers/tutorials/deploying-your-first-
smart-contract/remix-function-button.png)

Let’s now call the `increment` function by clicking on the button. You’ll see
logs of the transactions that are made appearing on the bottom of the window.
You’ll see that the logs are different when you’re pressing the button to
retrieve the data instead of the `increment` button. It’s because reading data
on the blockchain does not need any transactions (writing) or fees. Because
only modifying the state of the blockchain requires to make a transaction:

[![A log of
transactions](/_next/image/?url=%2Fcontent%2Fdevelopers%2Ftutorials%2Fdeploying-
your-first-smart-contract%2Ftransaction-
log.png&w=1920&q=75)](/content/developers/tutorials/deploying-your-first-
smart-contract/transaction-log.png)

After pressing the increment button that will generate a transaction to call
our `increment()` function if we click back on the count or getCount buttons
we’ll read the newly updated state of our smart contract with the count
variable being bigger than 0.

[![Newly updated state of the smart
contract](/_next/image/?url=%2Fcontent%2Fdevelopers%2Ftutorials%2Fdeploying-
your-first-smart-contract%2Fupdated-
state.png&w=750&q=75)](/content/developers/tutorials/deploying-your-first-
smart-contract/updated-state.png)

In the next tutorial, we’ll cover [how you can add events to your smart
contracts](/en/developers/tutorials/logging-events-smart-contracts/). Logging
events is a convenient way to debug your smart contract and understand what is
happening while calling a function.

l

Last edit: [@lukassim(opens in a new tab)](https://github.com/lukassim), April
26, 2024

See contributors

### Was this tutorial helpful?

YesNo

  * [Edit page(opens in a new tab)](https://github.com/ethereum/ethereum-org-website/tree/dev/public/content/developers/tutorials/deploying-your-first-smart-contract/index.md)
  * On this page

    * Writing our contract
    * Deploying our contract

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

