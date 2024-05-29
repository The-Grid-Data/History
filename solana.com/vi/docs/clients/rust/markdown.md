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

  * [Rust Crates](/vi/docs/clients/rust#rust-crates)

[Scroll to Top](/vi/docs/clients/rust#)

[Edit Page](https://github.com/solana-foundation/developer-
content/tree/main/docs/clients/rust.md)

[Home](/vi)>[Solana Documentation](/vi/docs)>Solana Clients

# [Rust Client for Solana](/vi/docs/clients/rust)

Solana's Rust crates are [published to
crates.io](https://crates.io/search?q=solana-) and can be found [on
docs.rs](https://docs.rs/releases/search?query=solana-) with the `solana-`
prefix.

Hello World: Get started with Solana development

To quickly get started with Solana development and build your first Rust
program, take a look at these detailed quick start guides:

  * [Build and deploy your first Solana program using only your browser](/vi/developers/guides/getstarted/hello-world-in-your-browser). No installation needed.
  * [Setup your local environment](/vi/developers/guides/getstarted/setup-local-development) and use the local test validator.

## Rust Crates #

The following are the most important and commonly used Rust crates for Solana
development:

  * [`solana-program`](https://docs.rs/solana-program) — Imported by programs running on Solana, compiled to SBF. This crate contains many fundamental data types and is re-exported from [`solana-sdk`](https://docs.rs/solana-sdk), which cannot be imported from a Solana program.

  * [`solana-sdk`](https://docs.rs/solana-sdk) — The basic off-chain SDK, it re-exports [`solana-program`](https://docs.rs/solana-program) and adds more APIs on top of that. Most Solana programs that do not run on-chain will import this.

  * [`solana-client`](https://docs.rs/solana-client) — For interacting with a Solana node via the [JSON RPC API](/vi/docs/rpc).

  * [`solana-cli-config`](https://docs.rs/solana-cli-config) — Loading and saving the Solana CLI configuration file.

  * [`solana-clap-utils`](https://docs.rs/solana-clap-utils) — Routines for setting up a CLI, using [`clap`](https://docs.rs/clap), as used by the main Solana CLI. Includes functions for loading all types of signers supported by the CLI.

[Previous« State Compression](/vi/docs/advanced/state-
compression)[NextJavaScript / TypeScript »](/vi/docs/clients/javascript)

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

