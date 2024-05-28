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

##### Table of Contents

  * [What is a Wallet](/de/docs/intro/wallets#what-is-a-wallet)
  * [Keypair](/de/docs/intro/wallets#keypair)
  * [Public key](/de/docs/intro/wallets#public-key)
  * [Secret key](/de/docs/intro/wallets#secret-key)
  * [Security](/de/docs/intro/wallets#security)
  * [Supported Wallets](/de/docs/intro/wallets#supported-wallets)

[Scroll to Top](/de/docs/intro/wallets#)

[Edit Page](https://github.com/solana-foundation/developer-
content/tree/main/docs/intro/wallets.md)

[Home](/de)>[Solana Dokumentation](/de/docs)>Introduction

# [Solana Wallet Guide](/de/docs/intro/wallets)

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

A [_keypair_](/de/docs/terminology#keypair) is a securely generated [_secret
key_](/de/docs/intro/wallets#secret-key) and its cryptographically-derived
[_public key_](/de/docs/intro/wallets#public-key). A secret key and its
corresponding public key are together known as a _keypair_. A wallet contains
a collection of one or more keypairs and provides some means to interact with
them.

### Public key #

The [_public key_](/de/docs/terminology#public-key-pubkey) (commonly shortened
to _pubkey_) is known as the wallet's _receiving address_ or simply its
_address_. The wallet address **may be shared and displayed freely**. When
another party is going to send some amount of cryptocurrency to a wallet, they
need to know the wallet's receiving address. Depending on a blockchain's
implementation, the address can also be used to view certain information about
a wallet, such as viewing the balance, but has no ability to change anything
about the wallet or withdraw any tokens.

### Secret key #

The [_secret key_](/de/docs/terminology#private-key) (also referred to as
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
Ecosystem](/de/ecosystem/explore?categories=wallet) page.

For advanced users or developers, the [command-line
wallets](https://docs.solanalabs.com/cli/wallets) may be more appropriate, as
new features on the Solana blockchain will always be supported on the command
line first before being integrated into third-party solutions.

[Previous« Overview](/de/docs/intro/overview)[NextIntro to Development
»](/de/docs/intro/dev)

  * [Solana Dokumentation](/de/docs)

    * [JSON RPC Methods](/de/docs/rpc)
    * [Terminology](/de/docs/terminology)
  * Introduction

    * [Overview](/de/docs/intro/overview)
    * [Wallets](/de/docs/intro/wallets)
    * [Intro to Development](/de/docs/intro/dev)
  * Core Concepts

    * [Solana Account Model](/de/docs/core/accounts)
    * [Transactions and Instructions](/de/docs/core/transactions)
    * [Fees on Solana](/de/docs/core/fees)
    * [Programs on Solana](/de/docs/core/programs)
    * [Program Derived Address](/de/docs/core/pda)
    * [Cross Program Invocation](/de/docs/core/cpi)
    * [Tokens on Solana](/de/docs/core/tokens)
    * [Clusters & Endpoints](/de/docs/core/clusters)
  * Advanced Concepts

    * [Versioned Transactions](/de/docs/advanced/versions)
    * [Address Lookup Tables](/de/docs/advanced/lookup-tables)
    * [Confirmation & Expiration](/de/docs/advanced/confirmation)
    * [Retrying Transactions](/de/docs/advanced/retry)
    * [State Compression](/de/docs/advanced/state-compression)
  * Solana Clients

    * [Rust](/de/docs/clients/rust)
    * [JavaScript / TypeScript](/de/docs/clients/javascript)
    * [Web3.js API Examples](/de/docs/clients/javascript-reference)
  * [Economics](/de/docs/economics)

    * Inflation
      * [Proposed Inflation Schedule](/de/docs/economics/inflation/inflation-schedule)
      * [Inflation Terminology](/de/docs/economics/inflation/terminology)
    * [Staking](/de/docs/economics/staking)
      * [Stake Accounts](/de/docs/economics/staking/stake-accounts)
      * [Stake Programming](/de/docs/economics/staking/stake-programming)
  * Developing Programs

    * [Overview](/de/docs/programs/overview)
    * [Debugging Programs](/de/docs/programs/debugging)
    * [Deploying Programs](/de/docs/programs/deploying)
    * [Program Examples](/de/docs/programs/examples)
    * [FAQ](/de/docs/programs/faq)
    * [Developing with C](/de/docs/programs/lang-c)
    * [Developing with Rust](/de/docs/programs/lang-rust)
    * [Limitations](/de/docs/programs/limitations)
  * More Information

    * [Add Solana to Your Exchange](/de/docs/more/exchange)

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

