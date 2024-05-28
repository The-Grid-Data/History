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

[Scroll to Top](/de/docs/economics/staking/stake-programming#)

[Edit Page](https://github.com/solana-foundation/developer-
content/tree/main/docs/economics/staking/stake-programming.md)

[Home](/de)>[Solana
Dokumentation](/de/docs)>[Economics](/de/docs/economics)>[Staking](/de/docs/economics/staking)

# [Stake Programming](/de/docs/economics/staking/stake-programming)

To maximize stake distribution, decentralization, and censorship resistance on
the Solana network, staking can be performed programmatically. The team and
community have developed several on-chain and off-chain programs to make
stakes easier to manage.

#### Stake-o-matic aka Auto-delegation Bots #

This off-chain program manages a large population of validators staked by a
central authority. The Solana Foundation uses an auto-delegation bot to
regularly delegate its stake to "non-delinquent" validators that meet
specified performance requirements.

#### Stake Pools #

This on-chain program pools together SOL to be staked by a manager, allowing
SOL holders to stake and earn rewards without managing stakes. Users deposit
SOL in exchange for SPL tokens (staking derivatives) that represent their
ownership in the stake pool. The pool manager stakes deposited SOL according
to their strategy, perhaps using a variant of an auto-delegation bot as
described above. As stakes earn rewards, the pool and pool tokens grow
proportionally in value. Finally, pool token holders can send SPL tokens back
to the stake pool to redeem SOL, thereby participating in decentralization
with much less work required. More information can be found at the [SPL stake
pool documentation](https://spl.solana.com/stake-pool).

[Previous« Stake Accounts](/de/docs/economics/staking/stake-
accounts)[NextOverview »](/de/docs/programs/overview)

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

