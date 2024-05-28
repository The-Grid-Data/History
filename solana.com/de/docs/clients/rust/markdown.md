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

  * [Rust Crates](/de/docs/clients/rust#rust-crates)

[Scroll to Top](/de/docs/clients/rust#)

[Edit Page](https://github.com/solana-foundation/developer-
content/tree/main/docs/clients/rust.md)

[Home](/de)>[Solana Dokumentation](/de/docs)>Solana Clients

# [Rust Client for Solana](/de/docs/clients/rust)

Solana's Rust crates are [published to
crates.io](https://crates.io/search?q=solana-) and can be found [on
docs.rs](https://docs.rs/releases/search?query=solana-) with the `solana-`
prefix.

Hello World: Get started with Solana development

To quickly get started with Solana development and build your first Rust
program, take a look at these detailed quick start guides:

  * [Build and deploy your first Solana program using only your browser](/de/developers/guides/getstarted/hello-world-in-your-browser). No installation needed.
  * [Setup your local environment](/de/developers/guides/getstarted/setup-local-development) and use the local test validator.

## Rust Crates #

The following are the most important and commonly used Rust crates for Solana
development:

  * [`solana-program`](https://docs.rs/solana-program) — Imported by programs running on Solana, compiled to SBF. This crate contains many fundamental data types and is re-exported from [`solana-sdk`](https://docs.rs/solana-sdk), which cannot be imported from a Solana program.

  * [`solana-sdk`](https://docs.rs/solana-sdk) — The basic off-chain SDK, it re-exports [`solana-program`](https://docs.rs/solana-program) and adds more APIs on top of that. Most Solana programs that do not run on-chain will import this.

  * [`solana-client`](https://docs.rs/solana-client) — For interacting with a Solana node via the [JSON RPC API](/de/docs/rpc).

  * [`solana-cli-config`](https://docs.rs/solana-cli-config) — Loading and saving the Solana CLI configuration file.

  * [`solana-clap-utils`](https://docs.rs/solana-clap-utils) — Routines for setting up a CLI, using [`clap`](https://docs.rs/clap), as used by the main Solana CLI. Includes functions for loading all types of signers supported by the CLI.

[Previous« State Compression](/de/docs/advanced/state-
compression)[NextJavaScript / TypeScript »](/de/docs/clients/javascript)

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

