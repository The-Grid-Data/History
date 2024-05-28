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

  * [What is a Wallet](/ru/docs/intro/wallets#what-is-a-wallet)
  * [Keypair](/ru/docs/intro/wallets#keypair)
  * [Public key](/ru/docs/intro/wallets#public-key)
  * [Secret key](/ru/docs/intro/wallets#secret-key)
  * [Security](/ru/docs/intro/wallets#security)
  * [Supported Wallets](/ru/docs/intro/wallets#supported-wallets)

[Scroll to Top](/ru/docs/intro/wallets#)

[Edit Page](https://github.com/solana-foundation/developer-
content/tree/main/docs/intro/wallets.md)

[Home](/ru)>[Solana Documentation](/ru/docs)>Introduction

# [Solana Wallet Guide](/ru/docs/intro/wallets)

This document describes the different wallet options that are available to
users of Solana who want to be able to send, receive and interact with SOL
tokens on the Solana blockchain.

## What is a Wallet? #

A crypto wallet is a device or application that stores a collection of keys
and can be used to send, receive, and track ownership of cryptocurrencies.
Wallets can take many forms. A wallet might be a directory or file in your
computer's file system, a piece of paper, or a specialized device called a
_hardware wallet_. There are also various smartphone apps and computer
programs that provide a user-friendly way to create and manage wallets.

### Keypair #

A [_keypair_](/ru/docs/terminology#keypair) is a securely generated [_secret
key_](/ru/docs/intro/wallets#secret-key) and its cryptographically-derived
[_public key_](/ru/docs/intro/wallets#public-key). A secret key and its
corresponding public key are together known as a _keypair_. A wallet contains
a collection of one or more keypairs and provides some means to interact with
them.

### Public key #

The [_public key_](/ru/docs/terminology#public-key-pubkey) (commonly shortened
to _pubkey_) is known as the wallet's _receiving address_ or simply its
_address_. The wallet address **may be shared and displayed freely**. When
another party is going to send some amount of cryptocurrency to a wallet, they
need to know the wallet's receiving address. Depending on a blockchain's
implementation, the address can also be used to view certain information about
a wallet, such as viewing the balance, but has no ability to change anything
about the wallet or withdraw any tokens.

### Secret key #

The [_secret key_](/ru/docs/terminology#private-key) (also referred to as
_private key_) is required to digitally sign any transactions to send
cryptocurrencies to another address or to make any changes to the wallet. The
secret key **must never be shared**. If someone gains access to the secret key
to a wallet, they can withdraw all the tokens it contains. If the secret key
for a wallet is lost, any tokens that have been sent to that wallet's address
are **permanently lost**.

## Security #

Different wallet solutions offer different approaches to keypair security,
interacting with the keypair, and signing transactions to use/spend the
tokens. Some are easier to use than others. Some store and back up secret keys
more securely. Solana supports multiple types of wallets so you can choose the
right balance of security and convenience.

**If you want to be able to receive SOL tokens on the Solana blockchain, you
first will need to create a wallet.**

## Supported Wallets #

Several browser and mobile app based wallets support Solana. Find some options
that might be right for you on the [Solana
Ecosystem](/ru/ecosystem/explore?categories=wallet) page.

For advanced users or developers, the [command-line
wallets](https://docs.solanalabs.com/cli/wallets) may be more appropriate, as
new features on the Solana blockchain will always be supported on the command
line first before being integrated into third-party solutions.

[Previous« Overview](/ru/docs/intro/overview)[NextIntro to Development
»](/ru/docs/intro/dev)

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

