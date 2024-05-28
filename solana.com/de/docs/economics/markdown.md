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

[Scroll to Top](/de/docs/economics#)

[Edit Page](https://github.com/solana-foundation/developer-
content/tree/main/docs/economics/index.md)

[Home](/de)>[Solana Dokumentation](/de/docs)

# [Solana Economics Overview](/de/docs/economics)

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
[Terminology](/de/docs/economics/inflation/terminology) commonly used
subsequently in the discussion of inflation and the related components.
Following that, we outline Solana's proposed [Inflation
Schedule](/de/docs/economics/inflation/inflation_schedule), i.e. the specific
parameters that uniquely parameterize the protocol-driven inflationary
issuance over time. Next is a brief section on Adjusted Staking Yield, and how
token dilution might influence staking behavior.

An overview of [Transaction Fees](/de/docs/core/fees#transaction-fees) on
Solana is followed by a discussion of [Storage Rent
Economics](/de/docs/core/fees#rent) in which we describe an implementation of
storage rent to account for the externality costs of maintaining the active
state of the ledger.

[Previous« Web3.js API Examples](/de/docs/clients/javascript-
reference)[NextProposed Inflation Schedule
»](/de/docs/economics/inflation/inflation-schedule)

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

