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

  * [Rust Crates](/ru/docs/clients/rust#rust-crates)

[Scroll to Top](/ru/docs/clients/rust#)

[Edit Page](https://github.com/solana-foundation/developer-
content/tree/main/docs/clients/rust.md)

[Home](/ru)>[Solana Documentation](/ru/docs)>Solana Clients

# [Rust Client for Solana](/ru/docs/clients/rust)

Solana's Rust crates are [published to
crates.io](https://crates.io/search?q=solana-) and can be found [on
docs.rs](https://docs.rs/releases/search?query=solana-) with the `solana-`
prefix.

Hello World: Get started with Solana development

To quickly get started with Solana development and build your first Rust
program, take a look at these detailed quick start guides:

  * [Build and deploy your first Solana program using only your browser](/ru/developers/guides/getstarted/hello-world-in-your-browser). No installation needed.
  * [Setup your local environment](/ru/developers/guides/getstarted/setup-local-development) and use the local test validator.

## Rust Crates #

The following are the most important and commonly used Rust crates for Solana
development:

  * [`solana-program`](https://docs.rs/solana-program) — Imported by programs running on Solana, compiled to SBF. This crate contains many fundamental data types and is re-exported from [`solana-sdk`](https://docs.rs/solana-sdk), which cannot be imported from a Solana program.

  * [`solana-sdk`](https://docs.rs/solana-sdk) — The basic off-chain SDK, it re-exports [`solana-program`](https://docs.rs/solana-program) and adds more APIs on top of that. Most Solana programs that do not run on-chain will import this.

  * [`solana-client`](https://docs.rs/solana-client) — For interacting with a Solana node via the [JSON RPC API](/ru/docs/rpc).

  * [`solana-cli-config`](https://docs.rs/solana-cli-config) — Loading and saving the Solana CLI configuration file.

  * [`solana-clap-utils`](https://docs.rs/solana-clap-utils) — Routines for setting up a CLI, using [`clap`](https://docs.rs/clap), as used by the main Solana CLI. Includes functions for loading all types of signers supported by the CLI.

[Previous« State Compression](/ru/docs/advanced/state-
compression)[NextJavaScript / TypeScript »](/ru/docs/clients/javascript)

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

