This website uses cookies to offer you a better browsing experience. Find out
more on how we use cookies.

Opt-out[Details](/ru/privacy-policy#collection-of-information)

Accept

[![Solana](/_next/static/media/logotype-dark.f79d530d.svg)](/ru)

  * Узнать больше
  * Developers
  * Solutions
  * Network
  * Сообщество

Search```K`

[Documentation](/ru/docs)[RPC
API](/ru/docs/rpc)[Cookbook](/ru/developers/cookbook)[Guides](/ru/developers/guides)[Terminology](/ru/docs/terminology)

##### Table of Contents

  * [On-chain program development lifecycle](/ru/docs/programs/overview#on-chain-program-development-lifecycle)
  * [1) Setup your development environment](/ru/docs/programs/overview#1-setup-your-development-environment)
  * [2\. Write your program](/ru/docs/programs/overview#2-write-your-program)
  * [3\. Compile the program](/ru/docs/programs/overview#3-compile-the-program)
  * [4\. Generate the program's public address](/ru/docs/programs/overview#4-generate-the-program-s-public-address)
  * [5\. Deploying the program](/ru/docs/programs/overview#5-deploying-the-program)
  * [Support languages](/ru/docs/programs/overview#support-languages)
  * [Example programs](/ru/docs/programs/overview#example-programs)
  * [Limitations](/ru/docs/programs/overview#limitations)
  * [Frequently asked questions](/ru/docs/programs/overview#frequently-asked-questions)

[Scroll to Top](/ru/docs/programs/overview#)

[Edit Page](https://github.com/solana-foundation/developer-
content/tree/main/docs/programs/overview.md)

[Home](/ru)>[Solana Documentation](/ru/docs)>Developing Programs

# [Overview of Developing On-chain Programs](/ru/docs/programs/overview)

Developers can write and deploy their own programs to the Solana blockchain.
This process can be broadly summarized into a few key steps.

Hello World: Get started with Solana development

To quickly get started with Solana development and build your first Rust
program, take a look at these detailed quick start guides:

  * [Build and deploy your first Solana program using only your browser](/ru/developers/guides/getstarted/hello-world-in-your-browser). No installation needed.
  * [Setup your local environment](/ru/developers/guides/getstarted/setup-local-development) and use the local test validator.

## On-chain program development lifecycle #

  1. Setup your development environment
  2. Write your program
  3. Compile the program
  4. Generate the program's public address
  5. Deploy the program

### 1) Setup your development environment #

The most robust way of getting started with Solana development, is [installing
the Solana CLI](https://docs.solanalabs.com/cli/install) tools on your local
computer. This will allow you to have the most powerful development
environment.

Some developers may also opt for using [Solana
Playground](https://beta.solpg.io/), a browser based IDE. It will let you
write, build, and deploy on-chain programs. All from your browser. No
installation needed.

### 2\. Write your program #

Writing Solana programs is most commonly done so using the Rust language.
These Rust programs are effectively the same as creating a traditional [Rust
library](https://doc.rust-lang.org/rust-by-example/crates/lib.html).

Info

You can read more about other [supported
languages](/ru/docs/programs/overview#support-languages) below.

### 3\. Compile the program #

Once the program is written, it must be complied down to [Berkley Packet
Filter](/ru/docs/programs/faq#berkeley-packet-filter-bpf) byte-code that will
then be deployed to the blockchain.

### 4\. Generate the program's public address #

Using the [Solana CLI](https://docs.solanalabs.com/cli/install), the developer
will generate a new unique [Keypair](/ru/docs/terminology#keypair) for the new
program. The public address (aka [Pubkey](/ru/docs/terminology#public-key-
pubkey)) from this Keypair will be used on-chain as the program's public
address (aka [`programId`](/ru/docs/terminology#program-id)).

### 5\. Deploying the program #

Then again using the CLI, the compiled program can be deployed to the selected
blockchain cluster by creating many transactions containing the program's
byte-code. Due to the transaction memory size limitations, each transaction
effectively sends small chunks of the program to the blockchain in a rapid-
fire manner.

Once the entire program has been sent to the blockchain, a final transaction
is sent to write all of the buffered byte-code to the program's data account.
This either mark the new program as `executable`, or complete the process to
upgrade an existing program (if it already existed).

## Support languages #

Solana programs are typically written in the [Rust
language](/ru/docs/programs/lang-rust), but [C/C++](/ru/docs/programs/lang-c)
are also supported.

There are also various community driven efforts to enable writing on-chain
programs using other languages, including:

  * Python via [Seahorse](https://seahorse.dev/) (that acts as a wrapper the Rust based Anchor framework)

## Example programs #

You can also explore the [Program Examples](/ru/docs/programs/examples) for
examples of on-chain programs.

## Limitations #

As you dive deeper into program development, it is important to understand
some of the important limitations associated with on-chain programs.

Read more details on the [Limitations](/ru/docs/programs/limitations) page

## Frequently asked questions #

Discover many of the [frequently asked questions](/ru/docs/programs/faq) other
developers have about writing/understanding Solana programs.

[Previous« Stake Programming](/ru/docs/economics/staking/stake-
programming)[NextDebugging Programs »](/ru/docs/programs/debugging)

  * [Solana Documentation](/ru/docs)

    * [JSON RPC Methods](/ru/docs/rpc)
    * [Terminology](/ru/docs/terminology)
  * Introduction

    * [Overview](/ru/docs/intro/overview)
    * [Wallets](/ru/docs/intro/wallets)
    * [Intro to Development](/ru/docs/intro/dev)
  * Core Concepts

    * [Solana Account Model](/ru/docs/core/accounts)
    * [Transactions and Instructions](/ru/docs/core/transactions)
    * [Fees on Solana](/ru/docs/core/fees)
    * [Programs on Solana](/ru/docs/core/programs)
    * [Program Derived Address](/ru/docs/core/pda)
    * [Cross Program Invocation](/ru/docs/core/cpi)
    * [Tokens on Solana](/ru/docs/core/tokens)
    * [Clusters & Endpoints](/ru/docs/core/clusters)
  * Advanced Concepts

    * [Versioned Transactions](/ru/docs/advanced/versions)
    * [Address Lookup Tables](/ru/docs/advanced/lookup-tables)
    * [Confirmation & Expiration](/ru/docs/advanced/confirmation)
    * [Retrying Transactions](/ru/docs/advanced/retry)
    * [State Compression](/ru/docs/advanced/state-compression)
  * Solana Clients

    * [Rust](/ru/docs/clients/rust)
    * [JavaScript / TypeScript](/ru/docs/clients/javascript)
    * [Web3.js API Examples](/ru/docs/clients/javascript-reference)
  * [Economics](/ru/docs/economics)

    * Inflation
      * [Proposed Inflation Schedule](/ru/docs/economics/inflation/inflation-schedule)
      * [Inflation Terminology](/ru/docs/economics/inflation/terminology)
    * [Staking](/ru/docs/economics/staking)
      * [Stake Accounts](/ru/docs/economics/staking/stake-accounts)
      * [Stake Programming](/ru/docs/economics/staking/stake-programming)
  * Developing Programs

    * [Overview](/ru/docs/programs/overview)
    * [Debugging Programs](/ru/docs/programs/debugging)
    * [Deploying Programs](/ru/docs/programs/deploying)
    * [Program Examples](/ru/docs/programs/examples)
    * [FAQ](/ru/docs/programs/faq)
    * [Developing with C](/ru/docs/programs/lang-c)
    * [Developing with Rust](/ru/docs/programs/lang-rust)
    * [Limitations](/ru/docs/programs/limitations)
  * More Information

    * [Add Solana to Your Exchange](/ru/docs/more/exchange)

Managed by

[](/ru)

[](/youtube)[](/twitter)[](/discord)[](/reddit)[](/github)[](/telegram)

© 2024 Solana Foundation. All rights reserved.

Solana

  * [Гранты](https://solana.org/grants)
  * [Break Solana](https://break.solana.com/)
  * [Media Kit](/ru/branding)
  * [Вакансии](https://jobs.solana.com/)
  * [Отказ от ответственности](/ru/tos)
  * [Privacy Policy](/ru/privacy-policy)

Get Connected

  * [проектов и их число растёт](/ru/ecosystem)
  * [Блог](/ru/news)
  * [Рассылка](/ru/newsletter)

ru

© 2024 Solana Foundation. All rights reserved.

