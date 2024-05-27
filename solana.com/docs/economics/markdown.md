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

[Scroll to Top](/docs/economics#)

[Edit Page](https://github.com/solana-foundation/developer-
content/tree/main/docs/economics/index.md)

[Home](/)>[Solana Documentation](/docs)

# [Solana Economics Overview](/docs/economics)

**Subject to change.**

Solana’s crypto-economic system is designed to promote a healthy, long term
self-sustaining economy with participant incentives aligned to the security
and decentralization of the network. The main participants in this economy are
validation-clients. Their contributions to the network, state validation, and
their requisite incentive mechanisms are discussed below.

The main channels of participant remittances are referred to as protocol-based
rewards and transaction fees. Protocol-based rewards are generated from
inflationary issuances from a protocol-defined inflation schedule. These
rewards will constitute the total protocol-based reward delivered to
validation clients, the remaining sourced from transaction fees. In the early
days of the network, it is likely that protocol-based rewards, deployed based
on predefined issuance schedule, will drive the majority of participant
incentives to participate in the network.

These protocol-based rewards are calculated per epoch and distributed across
the active delegated stake and validator set (per validator commission). As
discussed further below, the per annum inflation rate is based on a pre-
determined disinflationary schedule. This provides the network with supply
predictability which supports long term economic stability and security.

Transaction fees are participant-to-participant transfers, attached to network
interactions as a motivation and compensation for the inclusion and execution
of a proposed transaction. A mechanism for long-term economic stability and
forking protection through partial burning of each transaction fee is also
discussed below.

First, an overview of the inflation design is presented. This section starts
with defining and clarifying
[Terminology](/docs/economics/inflation/terminology) commonly used
subsequently in the discussion of inflation and the related components.
Following that, we outline Solana's proposed [Inflation
Schedule](/docs/economics/inflation/inflation_schedule), i.e. the specific
parameters that uniquely parameterize the protocol-driven inflationary
issuance over time. Next is a brief section on Adjusted Staking Yield, and how
token dilution might influence staking behavior.

An overview of [Transaction Fees](/docs/core/fees#transaction-fees) on Solana
is followed by a discussion of [Storage Rent Economics](/docs/core/fees#rent)
in which we describe an implementation of storage rent to account for the
externality costs of maintaining the active state of the ledger.

[Previous« Web3.js API Examples](/docs/clients/javascript-
reference)[NextProposed Inflation Schedule
»](/docs/economics/inflation/inflation-schedule)

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

