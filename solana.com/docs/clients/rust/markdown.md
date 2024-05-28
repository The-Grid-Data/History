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

  * [Rust Crates](/docs/clients/rust#rust-crates)

[Scroll to Top](/docs/clients/rust#)

[Edit Page](https://github.com/solana-foundation/developer-
content/tree/main/docs/clients/rust.md)

[Home](/)>[Solana Documentation](/docs)>Solana Clients

# [Rust Client for Solana](/docs/clients/rust)

Solana's Rust crates are [published to
crates.io](https://crates.io/search?q=solana-) and can be found [on
docs.rs](https://docs.rs/releases/search?query=solana-) with the `solana-`
prefix.

Hello World: Get started with Solana development

To quickly get started with Solana development and build your first Rust
program, take a look at these detailed quick start guides:

  * [Build and deploy your first Solana program using only your browser](/developers/guides/getstarted/hello-world-in-your-browser). No installation needed.
  * [Setup your local environment](/developers/guides/getstarted/setup-local-development) and use the local test validator.

## Rust Crates #

The following are the most important and commonly used Rust crates for Solana
development:

  * [`solana-program`](https://docs.rs/solana-program) — Imported by programs running on Solana, compiled to SBF. This crate contains many fundamental data types and is re-exported from [`solana-sdk`](https://docs.rs/solana-sdk), which cannot be imported from a Solana program.

  * [`solana-sdk`](https://docs.rs/solana-sdk) — The basic off-chain SDK, it re-exports [`solana-program`](https://docs.rs/solana-program) and adds more APIs on top of that. Most Solana programs that do not run on-chain will import this.

  * [`solana-client`](https://docs.rs/solana-client) — For interacting with a Solana node via the [JSON RPC API](/docs/rpc).

  * [`solana-cli-config`](https://docs.rs/solana-cli-config) — Loading and saving the Solana CLI configuration file.

  * [`solana-clap-utils`](https://docs.rs/solana-clap-utils) — Routines for setting up a CLI, using [`clap`](https://docs.rs/clap), as used by the main Solana CLI. Includes functions for loading all types of signers supported by the CLI.

[Previous« State Compression](/docs/advanced/state-compression)[NextJavaScript
/ TypeScript »](/docs/clients/javascript)

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

