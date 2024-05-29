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

[Scroll to Top](/vi/docs/economics/inflation/inflation-schedule#)

[Edit Page](https://github.com/solana-foundation/developer-
content/tree/main/docs/economics/inflation/inflation-schedule.md)

[Home](/vi)>[Solana
Documentation](/vi/docs)>[Economics](/vi/docs/economics)>Inflation

# [Proposed Inflation Schedule](/vi/docs/economics/inflation/inflation-
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

[Previous« Economics](/vi/docs/economics)[NextInflation Terminology
»](/vi/docs/economics/inflation/terminology)

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

