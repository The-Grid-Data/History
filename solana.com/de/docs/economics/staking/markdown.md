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

  * [How do I stake my SOL tokens](/de/docs/economics/staking#how-do-i-stake-my-sol-tokens)
  * [Stake Account Details](/de/docs/economics/staking#stake-account-details)

[Scroll to Top](/de/docs/economics/staking#)

[Edit Page](https://github.com/solana-foundation/developer-
content/tree/main/docs/economics/staking/index.md)

[Home](/de)>[Solana Dokumentation](/de/docs)>[Economics](/de/docs/economics)

# [Staking on Solana](/de/docs/economics/staking)

 _Note before reading: All references to increases in values are in absolute
terms with regards to balance of SOL. This document makes no suggestion as to
the monetary value of SOL at any time._

By staking your SOL tokens, you help secure the network and [earn
rewards](https://docs.solanalabs.com/implemented-proposals/staking-rewards)
while doing so.

You can stake by delegating your tokens to validators who process transactions
and run the network.

Delegating stake is a shared-risk shared-reward financial model that may
provide returns to holders of tokens delegated for a long period. This is
achieved by aligning the financial incentives of the token-holders
(delegators) and the validators to whom they delegate.

The more stake delegated to a validator, the more often this validator is
chosen to write new transactions to the ledger. The more transactions the
validator writes, the more rewards the validator and its delegators earn.
Validators who configure their systems to be able to process more transactions
earn proportionally more rewards and because they keep the network running as
fast and as smoothly as possible.

Validators incur costs by running and maintaining their systems, and this is
passed on to delegators in the form of a fee collected as a percentage of
rewards earned. This fee is known as a _commission_. Since validators earn
more rewards the more stake is delegated to them, they may compete with one
another to offer the lowest commission for their services.

You risk losing tokens when staking through a process known as _slashing_.
Slashing involves the removal and destruction of a portion of a validator's
delegated stake in response to intentional malicious behavior, such as
creating invalid transactions or censoring certain types of transactions or
network participants.

When a validator is slashed, all token holders who have delegated stake to
that validator lose a portion of their delegation. While this means an
immediate loss for the token holder, it also is a loss of future rewards for
the validator due to their reduced total delegation. More details on the
slashing roadmap can be found
[here](https://docs.solanalabs.com/proposals/optimistic-confirmation-and-
slashing#slashing-roadmap).

Rewards and slashing align validator and token holder interests which helps
keep the network secure, robust and performant.

## How do I stake my SOL tokens? #

You can stake SOL by moving your tokens into a wallet that supports staking.
The wallet provides steps to create a stake account and do the delegation.

#### Supported Wallets #

Many web and mobile wallets support Solana staking operations. Please check
with your favorite wallet's maintainers regarding status

#### Solana command line tools #

  * Solana command line tools can perform all stake operations in conjunction with a CLI-generated keypair file wallet, a paper wallet, or with a connected Ledger Nano. [Staking commands using the Solana Command Line Tools](https://docs.solanalabs.com/cli/examples/delegate-stake).

#### Create a Stake Account #

Follow the wallet's instructions for creating a staking account. This account
will be of a different type than one used to simply send and receive tokens.

#### Select a Validator #

Follow the wallet's instructions for selecting a validator. You can get
information about potentially performant validators from the links below. The
Solana Foundation does not recommend any particular validator.

The site solanabeach.io is built and maintained by one of our validators,
Staking Facilities. It provides a some high-level graphical information about
the network as a whole, as well as a list of each validator and some recent
performance statistics about each one.

  * <https://solanabeach.io>

To view block production statistics, use the Solana command-line tools:

  * `solana validators`
  * `solana block-production`

The Solana team does not make recommendations on how to interpret this
information. Do your own due diligence.

#### Delegate your Stake #

Follow the wallet's instructions for delegating your stake to your chosen
validator.

## Stake Account Details #

For more information about the operations and permissions associated with a
stake account, please see [Stake Accounts](/de/docs/economics/staking/stake-
accounts)

[Previous« Inflation
Terminology](/de/docs/economics/inflation/terminology)[NextStake Accounts
»](/de/docs/economics/staking/stake-accounts)

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

