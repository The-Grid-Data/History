This website uses cookies to offer you a better browsing experience. Find out
more on how we use cookies.

Opt-out[Details](/de/privacy-policy#collection-of-information)

Accept

[![Solana](/_next/static/media/logotype-dark.f79d530d.svg)](/de)

  * Learn
  * Developers
  * Solutions
  * Network
  * Community

Search```K`

[Documentation](/de/docs)[RPC
API](/de/docs/rpc)[Cookbook](/de/developers/cookbook)[Guides](/de/developers/guides)[Terminology](/de/docs/terminology)

[Home](/de)>[Developers](/de/developers)>[Guides](/de/developers/guides)

# [How to get Solana devnet SOL (including airdrops and
faucets)](/de/developers/guides/getstarted/solana-token-airdrop-and-faucets)

updated 29\. Juli 2023

[intro](/de/developers/guides?difficulty=intro)[faucet](/de/developers/guides?tags=faucet)

[![How to get Solana devnet SOL \(including airdrops and
faucets\)](https://solana.com/_next/image?url=%2Fopengraph%2Fdevelopers%2Fguides%2Fgetstarted%2Fsolana-
token-airdrop-and-
faucets&w=3840&q=75)](/de/developers/guides/getstarted/solana-token-airdrop-
and-faucets)

## How to get Solana devnet SOL (including airdrops and faucets) #

This is a collection of the different ways for developers to acquire SOL on
Solana's testing networks, the Solana devnet and testnet.

## 1\. Solana Airdrop #

_Available on Devnet and Testnet_

This is the base way of acquiring SOL, but it can be subject to rate limits
when there is a high number of airdrops.

Here are three different ways of requesting airdrops with it:

### Using the Solana CLI: #

    
    
    solana airdrop 2

### Using web3.js: #

    
    
    const connection = new Connection("https://api.devnet.solana.com");
    connection.requestAirdrop();

See more: [`requestAirdrop()`](https://solana-labs.github.io/solana-
web3.js/classes/Connection.html#requestAirdrop) documentation inside web3.js.

## 2\. Web Faucet #

_Available for Devnet_

  1. [faucet.solana.com](https://faucet.solana.com) \- A public web faucet hosted by the Solana Foundation
  2. [SolFaucet.com](https://solfaucet.com/) \- Web UI for airdrops from the public RPC endpoints
  3. [QuickNode](https://faucet.quicknode.com/solana/devnet) \- A web faucet operated by QuickNode

_Available for Testnet_

  1. [faucet.solana.com](https://faucet.solana.com) \- A public web faucet hosted by the Solana Foundation
  2. [SolFaucet.com](https://solfaucet.com/) \- Web UI for airdrops from the public RPC endpoints
  3. [QuickNode](https://faucet.quicknode.com/solana/testnet) \- A web faucet operated by QuickNode
  4. [TestnetFaucet.org](https://testnetfaucet.org) \- A web faucet with a rate limit separate than the public RPC endpoints, operated by [@Ferric](https://twitter.com/ferric)

## 3) RPC Provider Faucets #

_Available for Devnet_

RPC Providers can opt in to distributing devnet SOL via their devnet
Validators.

Info

If you are an RPC Provider and want to distribute SOL please [get in touch
here](https://c852ena8x5c.typeform.com/to/cUj1iRhS).

Currently supported:

  1. [Helius](https://www.helius.dev/)
  2. [QuickNode](https://faucet.quicknode.com/solana/devnet)
  3. [Triton](https://triton.one/)

### Using the Solana CLI #

Specify your [Cluster](https://docs.solana.com/clusters) to be your RPC
provider's URL:

    
    
    solana config set --url <your RPC url>

Then you can request an airdrop like you would in the first option in this
guide:

    
    
    solana airdrop 2

### Using Web3.js #

    
    
    const connection = new Connection("your RPC url");
    connection.requestAirdrop();

## 4\. Proof of work Faucet #

_Available for Devnet_

This is a proof of work Faucet where devnet SOL can be distributed to you
thanks to your computing power.

**Install the Devnet POW Crate:**

    
    
    cargo install devnet-pow

**Start mining devnet SOL**

    
    
    devnet-pow mine

_⚠️ The[POW Faucet](https://github.com/jarry-xiao/proof-of-work-faucet) is
maintained by Ellipsis Labs_

## 5\. Discord Faucets #

Various Discord communities have setup devnet SOL Faucets as BOTs.

Community| Usage| Link  
---|---|---  
The 76 Devs| Run `!gibsol` in the BOT commands channel.| [Join
Server](https://discord.gg/RrChGyDeRv)  
The LamportDAO| Run `/drop <address> <amount>` in the BOT commands channel.|
[Join Server](https://discord.gg/JBVrJgtFkq)  
  
## 6\. Reuse devnet SOL #

The most sustainable way to save SOL is to reuse it. With the Solana CLI you
can show and close all previous buffer accounts with the following command:

    
    
    solana program show --buffers

What's a buffer account?

Buffer accounts are automatically created when you deploy a program. All the
program's data is transferred into this account during the deployment. When
its done, the data of your program is replaced with the new data.

Normally, these buffer accounts are closed automatically. In the event they
are not, you can close them manually to reclaim the SOL in them using the
following command:

    
    
    solana program close <buffer account>

You can also the `show` subcommand to show all programs you deployed have
already deployed to your currently selected cluster:

    
    
    solana program show --programs

You can then close each program with the `close` subcommand to close them and
retrieve the SOL you used to deploy them:

    
    
    solana program close <program id>

You can then use that SOL to deploy new programs.

Caution

You will **NOT** able to use the same program id again once you closed the
program. So make sure are closing the right program and that you will not need
that id anymore.

If you get rate limited by the RPC endpoint your Solana CLI is configured to
use, you can add `-u "urlToYourRpc"` to the any of these command to use a
different RPC endpoint.

[Previous« Setup local development and install the Solana
CLI](/de/developers/guides/getstarted/setup-local-development)[NextWallets
Explained »](/de/developers/guides/intro/wallets-explained)

##### Table of Contents

  * [How to get Solana devnet SOL (including airdrops and faucets](/de/developers/guides/getstarted/solana-token-airdrop-and-faucets#how-to-get-solana-devnet-sol-including-airdrops-and-faucets)
  * [1\. Solana Airdrop](/de/developers/guides/getstarted/solana-token-airdrop-and-faucets#1-solana-airdrop)
  * [Using the Solana CLI](/de/developers/guides/getstarted/solana-token-airdrop-and-faucets#using-the-solana-cli)
  * [Using web3.js](/de/developers/guides/getstarted/solana-token-airdrop-and-faucets#using-web3-js)
  * [2\. Web Faucet](/de/developers/guides/getstarted/solana-token-airdrop-and-faucets#2-web-faucet)
  * [3) RPC Provider Faucets](/de/developers/guides/getstarted/solana-token-airdrop-and-faucets#3-rpc-provider-faucets)
  * [Using the Solana CLI](/de/developers/guides/getstarted/solana-token-airdrop-and-faucets#using-the-solana-cli)
  * [Using Web3.js](/de/developers/guides/getstarted/solana-token-airdrop-and-faucets#using-web3-js)
  * [4\. Proof of work Faucet](/de/developers/guides/getstarted/solana-token-airdrop-and-faucets#4-proof-of-work-faucet)
  * [5\. Discord Faucets](/de/developers/guides/getstarted/solana-token-airdrop-and-faucets#5-discord-faucets)
  * [6\. Reuse devnet SOL](/de/developers/guides/getstarted/solana-token-airdrop-and-faucets#6-reuse-devnet-sol)

[Scroll to Top](/de/developers/guides/getstarted/solana-token-airdrop-and-
faucets#)

[Edit Page](https://github.com/solana-foundation/developer-
content/tree/main/content/guides/getstarted/solana-token-airdrop-and-
faucets.md)

Managed by

[](/de)

[](/youtube)[](/twitter)[](/discord)[](/reddit)[](/github)[](/telegram)

© 2024 Solana Foundation. All rights reserved.

Solana

  * [Fördermittel](https://solana.org/grants)
  * [Break Solana](https://break.solana.com/)
  * [Media Kit](/de/branding)
  * [Karriere](https://jobs.solana.com/)
  * [Haftungsausschluss](/de/tos)
  * [Privacy Policy](/de/privacy-policy)

Get Connected

  * [Ökosystem](/de/ecosystem)
  * [Blog](/de/news)
  * [Newsletter](/de/newsletter)

de

© 2024 Solana Foundation. All rights reserved.

