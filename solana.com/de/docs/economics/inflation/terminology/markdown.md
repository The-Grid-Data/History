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

  * [Total Current Supply [SOL](/de/docs/economics/inflation/terminology#total-current-supply-sol)
  * [Inflation Rate](/de/docs/economics/inflation/terminology#inflation-rate)
  * [Inflation Schedule](/de/docs/economics/inflation/terminology#inflation-schedule)
  * [Effective Inflation Rate](/de/docs/economics/inflation/terminology#effective-inflation-rate)
  * [Staking Yield](/de/docs/economics/inflation/terminology#staking-yield)
  * [Token Dilution](/de/docs/economics/inflation/terminology#token-dilution)
  * [Adjusted Staking Yield](/de/docs/economics/inflation/terminology#adjusted-staking-yield)

[Scroll to Top](/de/docs/economics/inflation/terminology#)

[Edit Page](https://github.com/solana-foundation/developer-
content/tree/main/docs/economics/inflation/terminology.md)

[Home](/de)>[Solana
Dokumentation](/de/docs)>[Economics](/de/docs/economics)>Inflation

# [Inflation Related Terminology](/de/docs/economics/inflation/terminology)

Many terms are thrown around when discussing inflation and the related
components (e.g. rewards/yield/interest), we try to define and clarify some
commonly used concept here:

### Total Current Supply [SOL] #

The total amount of tokens (locked or unlocked) that have been generated (via
genesis block or protocol inflation) minus any tokens that have been burnt
(via transaction fees or other mechanism) or slashed. At network launch,
500,000,000 SOL were instantiated in the genesis block. Since then the Total
Current Supply has been reduced by the burning of transaction fees and a
planned token reduction event. Solana’s _Total Current Supply_ can be found at
<https://explorer.solana.com/supply>

### Inflation Rate [%] #

The Solana protocol will automatically create new tokens on a predetermined
inflation schedule (discussed below). The _Inflation Rate [%]_ is the
annualized growth rate of the _Total Current Supply_ at any point in time.

### Inflation Schedule #

A deterministic description of token issuance over time. The Solana Foundation
is proposing a disinflationary _Inflation Schedule_. I.e. Inflation starts at
its highest value, the rate reduces over time until stabilizing at a
predetermined long-term inflation rate (see discussion below). This schedule
is completely and uniquely parameterized by three numbers:

  * **Initial Inflation Rate [%]** : The starting _Inflation Rate_ for when inflation is first enabled. Token issuance rate can only decrease from this point.
  * **Disinflation Rate [%]** : The rate at which the _Inflation Rate_ is reduced.
  * **Long-term Inflation Rate [%]** : The stable, long-term _Inflation Rate_ to be expected.

### Effective Inflation Rate [%] #

The inflation rate actually observed on the Solana network after accounting
for other factors that might decrease the _Total Current Supply_. Note that it
is not possible for tokens to be created outside of what is described by the
_Inflation Schedule_.

  * While the _Inflation Schedule_ determines how the protocol issues SOL, this neglects the concurrent elimination of tokens in the ecosystem due to various factors. The primary token burning mechanism is the burning of a portion of each transaction fee. $50%$ of each transaction fee is burned, with the remaining fee retained by the validator that processes the transaction.
  * Additional factors such as loss of private keys and slashing events should also be considered in a holistic analysis of the _Effective Inflation Rate_. For example, it’s estimated that $10-20%$ of all BTC have been lost and are unrecoverable and that networks may experience similar yearly losses at the rate of $1-2%$.

### Staking Yield [%] #

The rate of return (aka _interest_) earned on SOL staked on the network. It is
often quoted as an annualized rate (e.g. "the network _staking yield_ is
currently $10%$ per year").

  * _Staking yield_ is of great interest to validators and token holders who wish to delegate their tokens to avoid token dilution due to inflation (the extent of which is discussed below).
  * $100%$ of inflationary issuances are to be distributed to staked token-holders in proportion to their staked SOL and to validators who charge a commission on the rewards earned by their delegated SOL.
    * There may be future consideration for an additional split of inflation issuance with the introduction of _Archivers_ into the economy. _Archivers_ are network participants who provide a decentralized storage service and should also be incentivized with token distribution from inflation issuances for this service. - Similarly, early designs specified a fixed percentage of inflationary issuance to be delivered to the Foundation treasury for operational expenses and future grants. However, inflation will be launching without any portion allocated to the Foundation.
  * _Staking yield_ can be calculated from the _Inflation Schedule_ along with the fraction of the _Total Current Supply_ that is staked at any given time. The explicit relationship is given by:

### Token Dilution [%] #

Dilution is defined here as the change in proportional representation of a set
of tokens within a larger set due to the introduction of new tokens. In
practical terms, we discuss the dilution of staked or un-staked tokens due to
the introduction and distribution of inflation issuance across the network. As
will be shown below, while dilution impacts every token holder, the _relative_
dilution between staked and un-staked tokens should be the primary concern to
un-staked token holders. Staking tokens, which will receive their proportional
distribution of inflation issuance, should assuage any dilution concerns for
staked token holders. I.e. dilution from 'inflation' is offset by the
distribution of new tokens to staked token holders, nullifying the 'dilutive'
effects of the inflation for that group.

### Adjusted Staking Yield [%] #

A complete appraisal of earning potential from staking tokens should take into
account staked _Token Dilution_ and its impact on the _Staking Yield_. For
this, we define the _Adjusted Staking Yield_ as the change in fractional token
supply ownership of staked tokens due to the distribution of inflation
issuance. I.e. the positive dilutive effects of inflation.

[Previous« Proposed Inflation
Schedule](/de/docs/economics/inflation/inflation-schedule)[NextStaking
»](/de/docs/economics/staking)

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
