This website uses cookies to offer you a better browsing experience. Find out
more on how we use cookies.

Opt-out[Details](/vi/privacy-policy#collection-of-information)

Accept

[![Solana](/_next/static/media/logotype-dark.f79d530d.svg)](/vi)

  * Tìm hiểu
  * Developers
  * Solutions
  * Network
  * Cộng đồng 

Search```K`

[Documentation](/vi/docs)[RPC
API](/vi/docs/rpc)[Cookbook](/vi/developers/cookbook)[Guides](/vi/developers/guides)[Terminology](/vi/docs/terminology)

##### Table of Contents

  * [What is a Wallet](/vi/docs/intro/wallets#what-is-a-wallet)
  * [Keypair](/vi/docs/intro/wallets#keypair)
  * [Public key](/vi/docs/intro/wallets#public-key)
  * [Secret key](/vi/docs/intro/wallets#secret-key)
  * [Security](/vi/docs/intro/wallets#security)
  * [Supported Wallets](/vi/docs/intro/wallets#supported-wallets)

[Scroll to Top](/vi/docs/intro/wallets#)

[Edit Page](https://github.com/solana-foundation/developer-
content/tree/main/docs/intro/wallets.md)

[Home](/vi)>[Solana Documentation](/vi/docs)>Introduction

# [Solana Wallet Guide](/vi/docs/intro/wallets)

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

A [_keypair_](/vi/docs/terminology#keypair) is a securely generated [_secret
key_](/vi/docs/intro/wallets#secret-key) and its cryptographically-derived
[_public key_](/vi/docs/intro/wallets#public-key). A secret key and its
corresponding public key are together known as a _keypair_. A wallet contains
a collection of one or more keypairs and provides some means to interact with
them.

### Public key #

The [_public key_](/vi/docs/terminology#public-key-pubkey) (commonly shortened
to _pubkey_) is known as the wallet's _receiving address_ or simply its
_address_. The wallet address **may be shared and displayed freely**. When
another party is going to send some amount of cryptocurrency to a wallet, they
need to know the wallet's receiving address. Depending on a blockchain's
implementation, the address can also be used to view certain information about
a wallet, such as viewing the balance, but has no ability to change anything
about the wallet or withdraw any tokens.

### Secret key #

The [_secret key_](/vi/docs/terminology#private-key) (also referred to as
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
Ecosystem](/vi/ecosystem/explore?categories=wallet) page.

For advanced users or developers, the [command-line
wallets](https://docs.solanalabs.com/cli/wallets) may be more appropriate, as
new features on the Solana blockchain will always be supported on the command
line first before being integrated into third-party solutions.

[Previous« Overview](/vi/docs/intro/overview)[NextIntro to Development
»](/vi/docs/intro/dev)

  * [Solana Documentation](/vi/docs)

    * [JSON RPC Methods](/vi/docs/rpc)
    * [Terminology](/vi/docs/terminology)
  * Introduction

    * [Overview](/vi/docs/intro/overview)
    * [Wallets](/vi/docs/intro/wallets)
    * [Intro to Development](/vi/docs/intro/dev)
  * Core Concepts

    * [Solana Account Model](/vi/docs/core/accounts)
    * [Transactions and Instructions](/vi/docs/core/transactions)
    * [Fees on Solana](/vi/docs/core/fees)
    * [Programs on Solana](/vi/docs/core/programs)
    * [Program Derived Address](/vi/docs/core/pda)
    * [Cross Program Invocation](/vi/docs/core/cpi)
    * [Tokens on Solana](/vi/docs/core/tokens)
    * [Clusters & Endpoints](/vi/docs/core/clusters)
  * Advanced Concepts

    * [Versioned Transactions](/vi/docs/advanced/versions)
    * [Address Lookup Tables](/vi/docs/advanced/lookup-tables)
    * [Confirmation & Expiration](/vi/docs/advanced/confirmation)
    * [Retrying Transactions](/vi/docs/advanced/retry)
    * [State Compression](/vi/docs/advanced/state-compression)
  * Solana Clients

    * [Rust](/vi/docs/clients/rust)
    * [JavaScript / TypeScript](/vi/docs/clients/javascript)
    * [Web3.js API Examples](/vi/docs/clients/javascript-reference)
  * [Economics](/vi/docs/economics)

    * Inflation
      * [Proposed Inflation Schedule](/vi/docs/economics/inflation/inflation-schedule)
      * [Inflation Terminology](/vi/docs/economics/inflation/terminology)
    * [Staking](/vi/docs/economics/staking)
      * [Stake Accounts](/vi/docs/economics/staking/stake-accounts)
      * [Stake Programming](/vi/docs/economics/staking/stake-programming)
  * Developing Programs

    * [Overview](/vi/docs/programs/overview)
    * [Debugging Programs](/vi/docs/programs/debugging)
    * [Deploying Programs](/vi/docs/programs/deploying)
    * [Program Examples](/vi/docs/programs/examples)
    * [FAQ](/vi/docs/programs/faq)
    * [Developing with C](/vi/docs/programs/lang-c)
    * [Developing with Rust](/vi/docs/programs/lang-rust)
    * [Limitations](/vi/docs/programs/limitations)
  * More Information

    * [Add Solana to Your Exchange](/vi/docs/more/exchange)

Managed by

[](/vi)

[](/youtube)[](/twitter)[](/discord)[](/reddit)[](/github)[](/telegram)

© 2024 Solana Foundation. All rights reserved.

Solana

  * [Trợ cấp](https://solana.org/grants)
  * [Solana Break](https://break.solana.com/)
  * [Media Kit](/vi/branding)
  * [Nghề nghiệp ](https://jobs.solana.com/)
  * [Từ chối](/vi/tos)
  * [Privacy Policy](/vi/privacy-policy)

Get Connected

  * [Hệ sinh thái](/vi/ecosystem)
  * [Blog](/vi/news)
  * [Bản tin](/vi/newsletter)

vi

© 2024 Solana Foundation. All rights reserved.

