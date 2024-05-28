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

  * [Rust libraries](/ru/docs/programs/limitations#rust-libraries)
  * [Compute budget](/ru/docs/programs/limitations#compute-budget)
  * [Call stack depth - `CallDepthExceeded` error](/ru/docs/programs/limitations#call-stack-depth-calldepthexceeded-error)
  * [CPI call depth - `CallDepth` error](/ru/docs/programs/limitations#cpi-call-depth-calldepth-error)
  * [Float Rust types support](/ru/docs/programs/limitations#float-rust-types-support)
  * [Static writable data](/ru/docs/programs/limitations#static-writable-data)
  * [Signed division](/ru/docs/programs/limitations#signed-division)

[Scroll to Top](/ru/docs/programs/limitations#)

[Edit Page](https://github.com/solana-foundation/developer-
content/tree/main/docs/programs/limitations.md)

[Home](/ru)>[Solana Documentation](/ru/docs)>Developing Programs

# [Limitations](/ru/docs/programs/limitations)

Developing programs on the Solana blockchain have some inherent limitation
associated with them. Below is a list of common limitation that you may run
into.

## Rust libraries #

Since Rust based on-chain programs must run be deterministic while running in
a resource-constrained, single-threaded environment, they have some
limitations on various libraries.

See [Developing with Rust - Restrictions](/ru/docs/programs/lang-
rust#restrictions) for a detailed breakdown these restrictions and
limitations.

## Compute budget #

To prevent abuse of the blockchain's computational resources, each transaction
is allocated a [compute budget](/ru/docs/terminology#compute-budget).
Exceeding this compute budget will result in the transaction failing.

See the [computational constraints](/ru/docs/core/fees#compute-budget)
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
depth](/ru/docs/core/cpi), it will receive a `CallDepth` error

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

[Previous« Developing with Rust](/ru/docs/programs/lang-rust)[NextAdd Solana
to Your Exchange »](/ru/docs/more/exchange)

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

