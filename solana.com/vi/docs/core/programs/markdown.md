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

  * [Key Points](/vi/docs/core/programs#key-points)
  * [Writing Solana Programs](/vi/docs/core/programs#writing-solana-programs)
  * [Updating Solana Programs](/vi/docs/core/programs#updating-solana-programs)
  * [Verifiable Programs](/vi/docs/core/programs#verifiable-programs)
  * [Berkeley Packet Filter (BPF](/vi/docs/core/programs#berkeley-packet-filter-bpf)

[Scroll to Top](/vi/docs/core/programs#)

[Edit Page](https://github.com/solana-foundation/developer-
content/tree/main/docs/core/programs.md)

[Home](/vi)>[Solana Documentation](/vi/docs)>Core Concepts

# [Programs](/vi/docs/core/programs)

In the Solana ecosystem, "smart contracts" are called programs. Each
[program](/vi/docs/core/accounts#program-account) is an on-chain account that
stores executable logic, organized into specific functions referred to as
[instructions](/vi/docs/core/transactions#instruction).

For additional topics related to Solana programs, refer to the pages included
under the [Deploying Programs](/vi/docs/programs) section of this
documentation.

## Key Points #

  * Programs are on-chain accounts that contain executable code. This code is organized into distinct functions known as instructions.

  * Programs are stateless but can include instructions to create new accounts, which are used to store and manage program state.

  * Programs can be updated by an upgrade authority. A program becomes immutable when the upgrade authority is set to null.

  * Verifiable builds enable users to verify that on-chain programs match the publicly available source code.

## Writing Solana Programs #

Solana programs are predominantly written in the [Rust](https://doc.rust-
lang.org/book/) programming language, with two common approaches for
development:

  * [Anchor](/vi/developers/guides/getstarted/intro-to-anchor): A framework designed for Solana program development. It provides a faster and simpler way to write programs, using Rust macros to significantly reduce boilerplate code. For beginners, it is recommended to start with the Anchor framework.

  * [Native Rust](/vi/developers/guides/getstarted/intro-to-native-rust): This approach involves writing Solana programs in Rust without leveraging any frameworks. It offers more flexibility but comes with increased complexity.

## Updating Solana Programs #

On-chain programs can be [directly modified](https://github.com/solana-
labs/solana/blob/27eff8408b7223bb3c4ab70523f8a8dca3ca6645/programs/bpf_loader/src/lib.rs#L675)
by an account designated as the "upgrade authority", which is typically the
account that originally deployed the program.

If the [upgrade authority](https://github.com/solana-
labs/solana/blob/27eff8408b7223bb3c4ab70523f8a8dca3ca6645/programs/bpf_loader/src/lib.rs#L865)
is revoked and set to `None`, the program becomes immutable and can no longer
be updated.

## Verifiable Programs #

Ensuring the integrity and verifiability of on-chain code is essential. A
verifiable build ensures that the executable code deployed on-chain can be
independently verified to match its public source code by any third party.
This process enhances transparency and trust, making it possible to detect
discrepancies between the source code and the deployed program.

The Solana developer community has introduced tools to support verifiable
builds, enabling both developers and users to verify that on-chain programs
accurately reflect their publicly shared source code.

  * **Searching for Verified Programs** : To quickly check for verified programs, users can search for a program address on the [SolanaFM](https://solana.fm/) Explorer and navigate to the "Verification" tab. View an example of a verified program [here](https://solana.fm/address/PhoeNiXZ8ByJGLkxNfZRnkUfjvmuYqLR89jjFHGqdXY).

  * **Verification Tools** : The [Solana Verifiable Build CLI](https://github.com/Ellipsis-Labs/solana-verifiable-build) by Ellipsis Labs enables users to independently verify on-chain programs against published source code.

  * **Support for Verifiable Builds in Anchor** : Anchor provides built-in support for verifiable builds. Details can be found in the [Anchor documentation](https://www.anchor-lang.com/docs/verifiable-builds).

## Berkeley Packet Filter (BPF) #

Solana leverages the [LLVM compiler infrastructure](https://llvm.org/) to
compile programs into [Executable and Linkable Format
(ELF)](https://en.wikipedia.org/wiki/Executable_and_Linkable_Format) files.
These files include a modified version of [Berkeley Packet Filter
(eBPF)](https://en.wikipedia.org/wiki/EBPF) bytecode for Solana programs,
known as "Solana Bytecode Format" (sBPF).

The use of LLVM enables Solana to potentially support any programming language
that can compile to LLVM's BPF backend. This significantly enhances the
flexibility of Solana as a development platform.

[Previous« Fees on Solana](/vi/docs/core/fees)[NextProgram Derived Address
»](/vi/docs/core/pda)

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

