This website uses cookies to offer you a better browsing experience. Find out
more on how we use cookies.

Opt-out[Details](/privacy-policy#collection-of-information)

Accept

[![Solana](/_next/static/media/logotype-dark.f79d530d.svg)](/)

  * Learn
  * Developers
  * Solutions
  * Network
  * Community

Search```K`

[Documentation](/docs)[RPC
API](/docs/rpc)[Cookbook](/developers/cookbook)[Guides](/developers/guides)[Terminology](/docs/terminology)

##### Table of Contents

  * [Key Points](/docs/core/programs#key-points)
  * [Writing Solana Programs](/docs/core/programs#writing-solana-programs)
  * [Updating Solana Programs](/docs/core/programs#updating-solana-programs)
  * [Verifiable Programs](/docs/core/programs#verifiable-programs)
  * [Berkeley Packet Filter (BPF](/docs/core/programs#berkeley-packet-filter-bpf)

[Scroll to Top](/docs/core/programs#)

[Edit Page](https://github.com/solana-foundation/developer-
content/tree/main/docs/core/programs.md)

[Home](/)>[Solana Documentation](/docs)>Core Concepts

# [Programs](/docs/core/programs)

In the Solana ecosystem, "smart contracts" are called programs. Each
[program](/docs/core/accounts#program-account) is an on-chain account that
stores executable logic, organized into specific functions referred to as
[instructions](/docs/core/transactions#instruction).

For additional topics related to Solana programs, refer to the pages included
under the [Deploying Programs](/docs/programs) section of this documentation.

## Key Points #

  * Programs are on-chain accounts that contain executable code. This code is organized into distinct functions known as instructions.

  * Programs are stateless but can include instructions to create new accounts, which are used to store and manage program state.

  * Programs can be updated by an upgrade authority. A program becomes immutable when the upgrade authority is set to null.

  * Verifiable builds enable users to verify that on-chain programs match the publicly available source code.

## Writing Solana Programs #

Solana programs are predominantly written in the [Rust](https://doc.rust-
lang.org/book/) programming language, with two common approaches for
development:

  * [Anchor](/developers/guides/getstarted/intro-to-anchor): A framework designed for Solana program development. It provides a faster and simpler way to write programs, using Rust macros to significantly reduce boilerplate code. For beginners, it is recommended to start with the Anchor framework.

  * [Native Rust](/developers/guides/getstarted/intro-to-native-rust): This approach involves writing Solana programs in Rust without leveraging any frameworks. It offers more flexibility but comes with increased complexity.

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

[Previous« Fees on Solana](/docs/core/fees)[NextProgram Derived Address
»](/docs/core/pda)

  * [Solana Documentation](/docs)

    * [JSON RPC Methods](/docs/rpc)
    * [Terminology](/docs/terminology)
  * Introduction

    * [Overview](/docs/intro/overview)
    * [Wallets](/docs/intro/wallets)
    * [Intro to Development](/docs/intro/dev)
  * Core Concepts

    * [Solana Account Model](/docs/core/accounts)
    * [Transactions and Instructions](/docs/core/transactions)
    * [Fees on Solana](/docs/core/fees)
    * [Programs on Solana](/docs/core/programs)
    * [Program Derived Address](/docs/core/pda)
    * [Cross Program Invocation](/docs/core/cpi)
    * [Tokens on Solana](/docs/core/tokens)
    * [Clusters & Endpoints](/docs/core/clusters)
  * Advanced Concepts

    * [Versioned Transactions](/docs/advanced/versions)
    * [Address Lookup Tables](/docs/advanced/lookup-tables)
    * [Confirmation & Expiration](/docs/advanced/confirmation)
    * [Retrying Transactions](/docs/advanced/retry)
    * [State Compression](/docs/advanced/state-compression)
  * Solana Clients

    * [Rust](/docs/clients/rust)
    * [JavaScript / TypeScript](/docs/clients/javascript)
    * [Web3.js API Examples](/docs/clients/javascript-reference)
  * [Economics](/docs/economics)

    * Inflation
      * [Proposed Inflation Schedule](/docs/economics/inflation/inflation-schedule)
      * [Inflation Terminology](/docs/economics/inflation/terminology)
    * [Staking](/docs/economics/staking)
      * [Stake Accounts](/docs/economics/staking/stake-accounts)
      * [Stake Programming](/docs/economics/staking/stake-programming)
  * Developing Programs

    * [Overview](/docs/programs/overview)
    * [Debugging Programs](/docs/programs/debugging)
    * [Deploying Programs](/docs/programs/deploying)
    * [Program Examples](/docs/programs/examples)
    * [FAQ](/docs/programs/faq)
    * [Developing with C](/docs/programs/lang-c)
    * [Developing with Rust](/docs/programs/lang-rust)
    * [Limitations](/docs/programs/limitations)
  * More Information

    * [Add Solana to Your Exchange](/docs/more/exchange)

Managed by

[](/)

[](/youtube)[](/twitter)[](/discord)[](/reddit)[](/github)[](/telegram)

© 2024 Solana Foundation. All rights reserved.

Solana

  * [Grants](https://solana.org/grants)
  * [Break Solana](https://break.solana.com/)
  * [Media Kit](/branding)
  * [Careers](https://jobs.solana.com/)
  * [Disclaimer](/tos)
  * [Privacy Policy](/privacy-policy)

Get Connected

  * [Ecosystem](/ecosystem)
  * [Blog](/news)
  * [Newsletter](/newsletter)

en

© 2024 Solana Foundation. All rights reserved.

