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

[Scroll to Top](/ru/docs/economics#)

[Edit Page](https://github.com/solana-foundation/developer-
content/tree/main/docs/economics/index.md)

[Home](/ru)>[Solana Documentation](/ru/docs)

# [Solana Economics Overview](/ru/docs/economics)

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
[Terminology](/ru/docs/economics/inflation/terminology) commonly used
subsequently in the discussion of inflation and the related components.
Following that, we outline Solana's proposed [Inflation
Schedule](/ru/docs/economics/inflation/inflation_schedule), i.e. the specific
parameters that uniquely parameterize the protocol-driven inflationary
issuance over time. Next is a brief section on Adjusted Staking Yield, and how
token dilution might influence staking behavior.

An overview of [Transaction Fees](/ru/docs/core/fees#transaction-fees) on
Solana is followed by a discussion of [Storage Rent
Economics](/ru/docs/core/fees#rent) in which we describe an implementation of
storage rent to account for the externality costs of maintaining the active
state of the ledger.

[Previous« Web3.js API Examples](/ru/docs/clients/javascript-
reference)[NextProposed Inflation Schedule
»](/ru/docs/economics/inflation/inflation-schedule)

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

