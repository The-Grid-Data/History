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

  * [Rust libraries](/vi/docs/programs/limitations#rust-libraries)
  * [Compute budget](/vi/docs/programs/limitations#compute-budget)
  * [Call stack depth - `CallDepthExceeded` error](/vi/docs/programs/limitations#call-stack-depth-calldepthexceeded-error)
  * [CPI call depth - `CallDepth` error](/vi/docs/programs/limitations#cpi-call-depth-calldepth-error)
  * [Float Rust types support](/vi/docs/programs/limitations#float-rust-types-support)
  * [Static writable data](/vi/docs/programs/limitations#static-writable-data)
  * [Signed division](/vi/docs/programs/limitations#signed-division)

[Scroll to Top](/vi/docs/programs/limitations#)

[Edit Page](https://github.com/solana-foundation/developer-
content/tree/main/docs/programs/limitations.md)

[Home](/vi)>[Solana Documentation](/vi/docs)>Developing Programs

# [Limitations](/vi/docs/programs/limitations)

Developing programs on the Solana blockchain have some inherent limitation
associated with them. Below is a list of common limitation that you may run
into.

## Rust libraries #

Since Rust based on-chain programs must run be deterministic while running in
a resource-constrained, single-threaded environment, they have some
limitations on various libraries.

See [Developing with Rust - Restrictions](/vi/docs/programs/lang-
rust#restrictions) for a detailed breakdown these restrictions and
limitations.

## Compute budget #

To prevent abuse of the blockchain's computational resources, each transaction
is allocated a [compute budget](/vi/docs/terminology#compute-budget).
Exceeding this compute budget will result in the transaction failing.

See the [computational constraints](/vi/docs/core/fees#compute-budget)
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
depth](/vi/docs/core/cpi), it will receive a `CallDepth` error

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

[Previous« Developing with Rust](/vi/docs/programs/lang-rust)[NextAdd Solana
to Your Exchange »](/vi/docs/more/exchange)

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

