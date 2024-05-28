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

  * [Rust libraries](/de/docs/programs/limitations#rust-libraries)
  * [Compute budget](/de/docs/programs/limitations#compute-budget)
  * [Call stack depth - `CallDepthExceeded` error](/de/docs/programs/limitations#call-stack-depth-calldepthexceeded-error)
  * [CPI call depth - `CallDepth` error](/de/docs/programs/limitations#cpi-call-depth-calldepth-error)
  * [Float Rust types support](/de/docs/programs/limitations#float-rust-types-support)
  * [Static writable data](/de/docs/programs/limitations#static-writable-data)
  * [Signed division](/de/docs/programs/limitations#signed-division)

[Scroll to Top](/de/docs/programs/limitations#)

[Edit Page](https://github.com/solana-foundation/developer-
content/tree/main/docs/programs/limitations.md)

[Home](/de)>[Solana Dokumentation](/de/docs)>Developing Programs

# [Limitations](/de/docs/programs/limitations)

Developing programs on the Solana blockchain have some inherent limitation
associated with them. Below is a list of common limitation that you may run
into.

## Rust libraries #

Since Rust based on-chain programs must run be deterministic while running in
a resource-constrained, single-threaded environment, they have some
limitations on various libraries.

See [Developing with Rust - Restrictions](/de/docs/programs/lang-
rust#restrictions) for a detailed breakdown these restrictions and
limitations.

## Compute budget #

To prevent abuse of the blockchain's computational resources, each transaction
is allocated a [compute budget](/de/docs/terminology#compute-budget).
Exceeding this compute budget will result in the transaction failing.

See the [computational constraints](/de/docs/core/fees#compute-budget)
documentation for more specific details.

## Call stack depth - `CallDepthExceeded` error #

Solana programs are constrained to run quickly, and to facilitate this, the
program's call stack is limited to a max depth of **64 frames**.

When a program exceeds the allowed call stack depth limit, it will receive the
`CallDepthExceeded` error.

## CPI call depth - `CallDepth` error #

Cross-program invocations allow programs to invoke other programs directly,
but the depth is constrained currently to `4`.

When a program exceeds the allowed [cross-program invocation call
depth](/de/docs/core/cpi), it will receive a `CallDepth` error

## Float Rust types support #

Programs support a limited subset of Rust's float operations. If a program
attempts to use a float operation that is not supported, the runtime will
report an unresolved symbol error.

Float operations are performed via software libraries, specifically LLVM's
float built-ins. Due to the software emulated, they consume more compute units
than integer operations. In general, fixed point operations are recommended
where possible.

The [Solana Program Library math](https://github.com/solana-labs/solana-
program-library/tree/master/libraries/math) tests will report the performance
of some math operations. To run the test, sync the repo and run:

    
    
    cargo test-sbf -- --nocapture --test-threads=1

Recent results show the float operations take more instructions compared to
integers equivalents. Fixed point implementations may vary but will also be
less than the float equivalents:

    
    
              u64   f32
    Multiply    8   176
    Divide      9   219

## Static writable data #

Program shared objects do not support writable shared data. Programs are
shared between multiple parallel executions using the same shared read-only
code and data. This means that developers should not include any static
writable or global variables in programs. In the future a copy-on-write
mechanism could be added to support writable data.

## Signed division #

The SBF instruction set does not support [signed
division](https://www.kernel.org/doc/html/latest/bpf/bpf_design_QA.Html#q-why-
there-is-no-bpf-sdiv-for-signed-divide-operation). Adding a signed division
instruction is a consideration.

[Previous« Developing with Rust](/de/docs/programs/lang-rust)[NextAdd Solana
to Your Exchange »](/de/docs/more/exchange)

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

