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

[Scroll to Top](/de/docs/economics/inflation/inflation-schedule#)

[Edit Page](https://github.com/solana-foundation/developer-
content/tree/main/docs/economics/inflation/inflation-schedule.md)

[Home](/de)>[Solana
Dokumentation](/de/docs)>[Economics](/de/docs/economics)>Inflation

# [Proposed Inflation Schedule](/de/docs/economics/inflation/inflation-
schedule)

As mentioned above, the network's _Inflation Schedule_ is uniquely described
by three parameters: _Initial Inflation Rate_ , _Disinflation Rate_ and _Long-
term Inflation Rate_. When considering these numbers, there are many factors
to take into account:

  * A large portion of the SOL issued via inflation will be distributed to stake-holders in proportion to the SOL they have staked. We want to ensure that the _Inflation Schedule_ design results in reasonable _Staking Yields_ for token holders who delegate SOL and for validation service providers (via commissions taken from _Staking Yields_).
  * The primary driver of _Staked Yield_ is the amount of SOL staked divided by the total amount of SOL (% of total SOL staked). Therefore the distribution and delegation of tokens across validators are important factors to understand when determining initial inflation parameters.
  * Yield throttling is a current area of research that would impact _staking-yields_. This is not taken into consideration in the discussion here or the modeling below.
  * Overall token issuance - i.e. what do we expect the Current Total Supply to be in 10 years, or 20 years?
  * Long-term, steady-state inflation is an important consideration not only for sustainable support for the validator ecosystem and the Solana Foundation grant programs, but also should be tuned in consideration with expected token losses and burning over time.
  * The rate at which we expect network usage to grow, as a consideration to the disinflationary rate. Over time, we plan for inflation to drop and expect that usage will grow.

Based on these considerations and the community discussions following the
initial design, the Solana Foundation proposes the following Inflation
Schedule parameters:

  * Initial Inflation Rate: 8%
  * Disinflation Rate: -15%
  * Long-term Inflation Rate: 1.5%

These parameters define the proposed _Inflation Schedule_. Below we show
implications of these parameters. These plots only show the impact of
inflation issuances given the Inflation Schedule as parameterized above. They
_do not account_ for other factors that may impact the Total Supply such as
fee/rent burning, slashing or other unforeseen future token destruction
events. Therefore, what is presented here is an **upper limit** on the amount
of SOL issued via inflation.

![Example proposed inflation schedule graph](https://solana-developer-
content.vercel.app/assets/docs/economics/proposed_inflation_schedule.png)Example
proposed inflation schedule graph

In the above graph we see the annual inflation rate percentage over time,
given the inflation parameters proposed above.

![Example proposed total supply graph](https://solana-developer-
content.vercel.app/assets/docs/economics/proposed_total_supply.png)Example
proposed total supply graph

Similarly, here we see the _Total Current Supply_ of SOL [MM] over time,
assuming an initial _Total Current Supply_ of `488,587,349 SOL` (i.e. for this
example, taking the _Total Current Supply_ as of `2020-01-25` and simulating
inflation starting from that day).

Setting aside validator uptime and commissions, the expected Staking Yield and
Adjusted Staking Yield metrics are then primarily a function of the % of total
SOL staked on the network. Therefore we can model _Staking Yield_ , if we
introduce an additional parameter _% of Staked SOL_ :

This parameter must be estimated because it is a dynamic property of the token
holders and staking incentives. The values of _% of Staked SOL_ presented here
range from 60% - 90%, which we feel covers the likely range we expect to
observe, based on feedback from the investor and validator communities as well
as what is observed on comparable Proof-of-Stake protocols.

![Example staked yields graph](https://solana-developer-
content.vercel.app/assets/docs/economics/example_staked_yields.png)Example
staked yields graph

Again, the above shows an example _Staked Yield_ that a staker might expect
over time on the Solana network with the _Inflation Schedule_ as specified.
This is an idealized _Staked Yield_ as it neglects validator uptime impact on
rewards, validator commissions, potential yield throttling and potential
slashing incidents. It additionally ignores that _% of Staked SOL_ is dynamic
by design - the economic incentives set up by this _Inflation Schedule_ are
more clearly seen when _Token Dilution_ is taken into account (see the
**Adjusted Staking Yield** section below).

[Previous« Economics](/de/docs/economics)[NextInflation Terminology
»](/de/docs/economics/inflation/terminology)

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

