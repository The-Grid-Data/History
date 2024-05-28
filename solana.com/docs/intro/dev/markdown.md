This website uses cookies to offer you a better browsing experience. Find out
more on how we use cookies.

Opt-out[Details](/privacy-policy#collection-of-information)

Accept

[![Solana](/_next/static/media/logotype-dark.f79d530d.svg)](/)

  * Learn
  * Developers
  * Solutions
  * Network
  * Community

Search```K`

[Documentation](/docs)[RPC
API](/docs/rpc)[Cookbook](/developers/cookbook)[Guides](/developers/guides)[Terminology](/docs/terminology)

##### Table of Contents

  * [High Level Developer Overview](/docs/intro/dev#high-level-developer-overview)
  * [What You'll Need Get Started](/docs/intro/dev#what-you-ll-need-get-started)
  * [Client-side Development](/docs/intro/dev#client-side-development)
  * [Onchain Program Development](/docs/intro/dev#onchain-program-development)
  * [Developer Environments](/docs/intro/dev#developer-environments)
  * [Build by Example](/docs/intro/dev#build-by-example)
  * [Getting Support](/docs/intro/dev#getting-support)
  * [Next steps](/docs/intro/dev#next-steps)

[Scroll to Top](/docs/intro/dev#)

[Edit Page](https://github.com/solana-foundation/developer-
content/tree/main/docs/intro/dev.md)

[Home](/)>[Solana Documentation](/docs)>Introduction

# [Getting Started with Solana Development](/docs/intro/dev)

Welcome to the Solana developer docs!

This page has everything you need to know to get started with Solana
development, including basic requirements, how Solana development works, and
the tools you'll need to get started.

## High Level Developer Overview #

Development on Solana can be broken down into two main parts:

  1. **Onchain Program Development** : This is where you create and deploy custom programs directly to the blockchain. Once deployed, anyone who knows how to communicate with them can use them. You can write these programs in Rust, C, or C++. Rust has the most support for onchain program development today.
  2. **Client Development** : This is where you write software (called decentralized applications, or dApps) that communicates with onchain programs. Your apps can submit transactions to perform actions onchain. Client development can be written in any programming language.

The "glue" between the client side and the onchain side is the [Solana JSON
RPC API](/docs/rpc). The client-side sends RPC requests to the Solana network
to interact with onchain programs. This is very similar to normal development
between a frontend and backend. The major difference with working on Solana is
that the backend is a global permissionless blockchain. This means that anyone
can interact with your onchain program without the need of issuing API keys or
any other form of permission.

![How clients work with the Solana blockchain](https://solana-developer-
content.vercel.app/assets/docs/intro/developer_flow.png)How clients work with
the Solana blockchain

Solana development is a bit different from other blockchains because of its
highly composable onchain programs. This means you can build on top of any
program already deployed, and often you can do so without needing to do any
custom onchain program development. For example, if you wanted to work with
tokens, you could use the [Token Program](/docs/core/tokens) that is already
deployed on the network. All development on your application would be client-
side in your language of choice.

Developers looking to build on Solana will find that the development stack is
very similar to any other development stack. The main difference is that
you'll be working with a blockchain and have to think about how users
potentially interact with your application onchain instead of just on the
frontend. Developing on Solana still has CI/CD pipelines, testing, debugging
tools, a frontend and backend, and anything you'd find in a normal development
flow.

## What You'll Need Get Started #

To get started with Solana development, you'll need different tools based on
whether you are developing for client-side, onchain programs, or both.

### Client-side Development #

If you're developing onchain apps, you should know Rust.

If you're developing on the client-side, you can work with any programming
language you're comfortable with. Solana has community-contributed SDKs to
help developers interact with the Solana network in most popular languages :

Language| SDK  
---|---  
RUST| [solana_sdk](https://docs.rs/solana-sdk/latest/solana_sdk/)  
Typescript| [@solana/web3.js](https://github.com/solana-labs/solana-web3.js)  
Python| [solders](https://github.com/kevinheavey/solders)  
Java| [solanaj](https://github.com/skynetcap/solanaj)  
C++| [solcpp](https://github.com/mschneider/solcpp)  
Go| [solana-go](https://github.com/gagliardetto/solana-go)  
Kotlin| [solanaKT](https://github.com/metaplex-foundation/SolanaKT)  
Dart| [solana](https://github.com/espresso-cash/espresso-cash-
public/tree/master/packages/solana)  
  
You'll also need a connection with an RPC to interact with the network. You
can either work with a [RPC infrastructure provider](/rpc) or [run your own
RPC node](https://docs.solanalabs.com/operations/setup-an-rpc-node).

To quickly get started with a front-end for your application, you can generate
a customizable Solana scaffold by typing the following into your CLI:

    
    
    npx create-solana-dapp <project-name>

This will create a new project with all the necessary files and basic
configuration to get started building on Solana. The scaffold will include
both an example frontend and an onchain program template (if you selected
one). You can read the [`create-solana-dapp` docs](https://github.com/solana-
developers/create-solana-dapp?tab=readme-ov-file#create-solana-dapp) to learn
more.

### Onchain Program Development #

Onchain program development consists of either writing programs in Rust, C, or
C++. First you'll need to make sure you have Rust installed on your machine.
You can do this with the following command:

    
    
    curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh

You'll then need to have the [Solana CLI
installed](https://docs.solanalabs.com/cli/install) to compile and deploy your
programs. You can install the Solana CLI by running the following command:

    
    
    sh -c "$(curl -sSfL https://release.solana.com/stable/install)"

Using the Solana CLI, it is recommended to run a local validator for testing
your program. To run a local validator after installing the Solana CLI, run
the following command:

    
    
    solana-test-validator

This will start a local validator on your machine that you can use to test
your programs. You can [read more about local development in this
guide](/developers/guides/getstarted/setup-local-development).

When building onchain programs, you have a choice to either build with native
Rust (ie, without a framework) or use the Anchor framework. Anchor is a
framework that makes it easier to build on Solana by providing a higher-level
API for developers. Think of Anchor like building with React for your websites
instead of raw Javascript and HTML. While Javascript and HTML give you more
control over your website, React accelerates your development and makes
developing easy. You can read more about [Anchor](https://www.anchor-
lang.com/) on their website.

You'll need a way to test your program. There are a few different ways to test
your program based on your language preference:

  * [solana-program-test](https://docs.rs/solana-program-test/latest/solana_program_test/) \- Testing framework built in Rust
  * [solana-bankrun](https://kevinheavey.github.io/solana-bankrun/) \- Testing framework built for writing Typescript tests
  * [bankrun](https://kevinheavey.github.io/solders/tutorials/bankrun.html) \- Testing framework built for writing Python tests

If you do not want to develop your programs locally, there's also the [online
IDE Solana Playground](https://beta.solpg.io). Solana Playground allows you to
write, test, and deploy programs on Solana. You can get started with Solana
Playground by [following our guide](/developers/guides/getstarted/hello-world-
in-your-browser).

### Developer Environments #

Choosing the right environment based on your work is very important. On
Solana, there are a few different network environments (called clusters) to
facilitate mature testing and CI/CD practices:

  * **Mainnet Beta** : The production network where all the action happens. Transactions cost real money here.
  * **Devnet** : The quality assurance network were you deploy your programs to test before deploying to production. Think "staging environment".
  * **Local** : The local network that you run on your machine using `solana-test-validator` to test your programs. This should be your first choice when developing programs.

## Build by Example #

While you get started building on Solana, there's a few more resources
available to help accelerate your journey:

  * [Solana Cookbook](/developers/cookbook): A collection of references and code snippets to help you build on Solana.
  * [Solana Program Examples](https://github.com/solana-developers/program-examples): A repository of example programs providing building blocks for different actions on your programs.
  * [Guides](/developers/guides): Tutorials and guides to walk you through building on Solana.

## Getting Support #

The best support you can find is on [Solana
StackExchange](https://solana.stackexchange.com/). Search for your question
there first - there's a good chance there will already be a question asked by
someone else, with an answer. If it's not there, add a new question! Remember
to include as much detail as you can in your question, and please use text
(not screenshots) to show error messages, so other people with the same
problem can find your question!

## Next steps #

You're now ready to get started building on Solana!

  * [Deploy your first Solana program in the browser](/developers/guides/getstarted/hello-world-in-your-browser)
  * [Setup your local development environment](/developers/guides/getstarted/setup-local-development)
  * [Get started building programs locally with Rust](/developers/guides/getstarted/local-rust-hello-world)
  * [Overview of writing Solana programs](/docs/programs)

[Previous« Wallets](/docs/intro/wallets)[NextSolana Account Model
»](/docs/core/accounts)

  * [Solana Documentation](/docs)

    * [JSON RPC Methods](/docs/rpc)
    * [Terminology](/docs/terminology)
  * Introduction

    * [Overview](/docs/intro/overview)
    * [Wallets](/docs/intro/wallets)
    * [Intro to Development](/docs/intro/dev)
  * Core Concepts

    * [Solana Account Model](/docs/core/accounts)
    * [Transactions and Instructions](/docs/core/transactions)
    * [Fees on Solana](/docs/core/fees)
    * [Programs on Solana](/docs/core/programs)
    * [Program Derived Address](/docs/core/pda)
    * [Cross Program Invocation](/docs/core/cpi)
    * [Tokens on Solana](/docs/core/tokens)
    * [Clusters & Endpoints](/docs/core/clusters)
  * Advanced Concepts

    * [Versioned Transactions](/docs/advanced/versions)
    * [Address Lookup Tables](/docs/advanced/lookup-tables)
    * [Confirmation & Expiration](/docs/advanced/confirmation)
    * [Retrying Transactions](/docs/advanced/retry)
    * [State Compression](/docs/advanced/state-compression)
  * Solana Clients

    * [Rust](/docs/clients/rust)
    * [JavaScript / TypeScript](/docs/clients/javascript)
    * [Web3.js API Examples](/docs/clients/javascript-reference)
  * [Economics](/docs/economics)

    * Inflation
      * [Proposed Inflation Schedule](/docs/economics/inflation/inflation-schedule)
      * [Inflation Terminology](/docs/economics/inflation/terminology)
    * [Staking](/docs/economics/staking)
      * [Stake Accounts](/docs/economics/staking/stake-accounts)
      * [Stake Programming](/docs/economics/staking/stake-programming)
  * Developing Programs

    * [Overview](/docs/programs/overview)
    * [Debugging Programs](/docs/programs/debugging)
    * [Deploying Programs](/docs/programs/deploying)
    * [Program Examples](/docs/programs/examples)
    * [FAQ](/docs/programs/faq)
    * [Developing with C](/docs/programs/lang-c)
    * [Developing with Rust](/docs/programs/lang-rust)
    * [Limitations](/docs/programs/limitations)
  * More Information

    * [Add Solana to Your Exchange](/docs/more/exchange)

Managed by

[](/)

[](/youtube)[](/twitter)[](/discord)[](/reddit)[](/github)[](/telegram)

© 2024 Solana Foundation. All rights reserved.

Solana

  * [Grants](https://solana.org/grants)
  * [Break Solana](https://break.solana.com/)
  * [Media Kit](/branding)
  * [Careers](https://jobs.solana.com/)
  * [Disclaimer](/tos)
  * [Privacy Policy](/privacy-policy)

Get Connected

  * [Ecosystem](/ecosystem)
  * [Blog](/news)
  * [Newsletter](/newsletter)

en

© 2024 Solana Foundation. All rights reserved.

