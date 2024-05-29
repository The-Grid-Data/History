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

[Home](/ru)>[Developers](/ru/developers)>[Guides](/ru/developers/guides)

# [Getting started with Solana with Rust
Experience](/ru/developers/guides/getstarted/rust-to-solana)

updated 21 мая 2024 г.

[Intro](/ru/developers/guides?difficulty=Intro)[rust](/ru/developers/guides?tags=rust)[solana](/ru/developers/guides?tags=solana)[anchor](/ru/developers/guides?tags=anchor)

[![Getting started with Solana with Rust
Experience](https://solana.com/_next/image?url=%2Fopengraph%2Fdevelopers%2Fguides%2Fgetstarted%2Frust-
to-solana&w=3840&q=75)](/ru/developers/guides/getstarted/rust-to-solana)

Developers looking to get into Solana development who already know Rust have a
great head start. Rust is an officially supported language for writing onchain
programs for the Solana Blockchain. However, several key differences in the
language's usage could otherwise be confusing.

This guide will walk through several of those differences, specifically the
setup details, restrictions, macro changes, and compute limits. Additionally,
this guide will cover the development environments and frameworks needed to
start with Solana.

By the end of this guide, Rust developers will understand the differences they
need to know to start their Solana journeys.

## Understanding the Core Differences #

First, note that this guide aims at understanding the differences in using
Rust as a language when working with Solana. It won’t cover [Blockchain or
Solana basics](/ru/learn/blockchain-basics).

It also won’t cover core Solana concepts that must be understood in order to
program in Solana, such as:

  * [Programs](/ru/docs/core/programs) \- Solana’s version of smart contracts
  * [Accounts](/ru/docs/core/accounts) \- A record in the Solana ledger that either holds data (a data account) or is an executable program
  * Various [fees](/ru/docs/core/fees#why-pay-transaction-fees) \- Such as base fee, priority fee, and rent
  * [Transactions](/ru/docs/core/transactions) \- Interactions with the network that contain instructions, signatures, and more.

For more information on those core concepts, check out the [Solana developer
documentation](/ru/docs).

Let’s now look at the differences in **project setup**.

## Key Setup Details #

Onchain programs for Solana in Rust are still Rust programs at heart. They
still follow the standard Rust project with a `/src` folder and `Cargo.toml`
file in the root. That said, there are several key differences.

### Project Dependencies #

To get started, the [solana-program crate](https://crates.io/crates/solana-
program) is required for every onchain Solana program written with Rust. This
is the base library for all onchain Rust programs. The library defines macros
for the required **program entrypoint** _(see below)_ , **core data types** ,
**logging macros** , and more.

### Program Entrypoint #

Instead of a `main` function, Solana programs use the `entrypoint!` macro.
This symbol is exported and then called by the Solana runtime when the program
runs. The entrypoint macro calls a given function, which must have the
following type signature:

    
    
    pub fn process_instruction( program_id: &Pubkey, accounts: &[AccountInfo],
    instruction_data: &[u8], ) -> ProgramResult {
     
            //program code goes here
     
        }

These three parameters are passed to every onchain program:

  1. The `program_id` is the public key of the current program.
  2. The `accounts` are all accounts that are required to process the instruction.
  3. The `instruction_data` is data specific to that instruction.

Every program must then call the `entrypoint!` macro on the instruction, as
follows:

    
    
    entrypoint!(process_instruction);

### Building and Testing #

After [installing the Solana command-line
tools](/ru/developers/guides/getstarted/setup-local-development#3-install-the-
solana-cli), projects can be built to target host machines as normal with
`cargo build`.

However, to target the Solana runtime, use `cargo build-bpf` or `cargo build-
spf` which will compile the program to the bytecode necessary to run it on the
Solana runtime.

Unit testing can be achieved via `cargo test` with standard `#test`
attributes. For more integrated testing, the [solana-program-
test](https://crates.io/crates/solana-program-test) crate provides a local
Solana runtime instance which can be used in conjunction with outside tests
sending transactions.

Finally, a full test cluster can be started with the [solana-test-
validator](https://docs.solanalabs.com/cli/examples/test-validator), installed
along with the Solana CLI. This creates a fully featured test cluster on a
local machine, which can then deploy programs and run tests.

## Understanding Restrictions #

While most standard Rust crates are available in the Solana runtime, and
third-party crates are supported as well, there are several limitations. Since
the Solana runtime has resource constraints and must run deterministically,
here are the differences to be aware of:

### Package Limitations #

The following packages are unavailable:

  * rand
  * std::fs
  * std::net
  * std::future
  * std::process
  * std::sync
  * std::task
  * std::thread
  * std::time

The following packages have limited functionality:

  * std::hash
  * std::os

### Rand Dependencies #

Because programs must run deterministically, the `rand` crate is not
available. Using an additional crate that depends on `rand` will also cause
compile errors.

However, if the crate used simply depends on `rand` but does not actually
generate random numbers, then it is possible to work around this by adding the
following to the program’s Cargo.toml:

    
    
    [dependencies]
    getrandom = { version = "0.1.14", features = ["dummy"] }

### Macro Changes #

Several standard macros have been replaced or have modified behavior to be
aware of. First, the `println!` has been replaced with the computationally
simpler `msg!` macro. The `msg!` macro outputs to the program logs, and it can
be used as follows:

    
    
    msg!("Your message");
    msg!(0_64, 1_64, 2_64);
    msg!("Your variable: {:?}", variable);

The `panic!`, `assert!`, and any internal panics are also output to the
program logs by default. However, this can be modified with a custom panic
handler.

As a better alternative to `panic!`, error handling should be used:

    
    
    #[error_code]
    pub enum MyErrors {
        CustomError,
    }
     
    #[program]
    pub mod anchor_error_test {
        use super::*;
     
        pub fn initialize(ctx: Context<Initialize>) -> Result<()> {
            //panic!("PANIC");
            return Err(MyErrors::CustomError.into());
     
            Ok(())
        }
    }

## Compute Budget #

As a Rust developer, efficient computing is nothing new. What may be different
is that in Solana, each transaction has a fixed [compute
budget](/ru/developers/guides/advanced/how-to-request-optimal-compute) that it
must not surpass. When transactions exceed the compute budget, they are halted
and return an error.

Programs can access the number of remaining compute units via the
`sol_remaining_compute_units` system call, and can log the remaining number of
compute units with `sol_log_compute_units`.

## Learning the Development Environment and Frameworks #

While the Solana CLI and the `solana_program` crate are all that is needed to
get started, there are a couple of helpful tools which can accelerate
learning.

![Network Diagram](https://solana-developer-
content.vercel.app/assets/guides/rust-to-solana/network-diagram.png)Network
Diagram

### Solana Playground #

The [Solana Playground](https://beta.solpg.io/) is a browser-based IDE that
allows developers to develop and deploy Solana programs.

![Solana Playground](https://solana-developer-
content.vercel.app/assets/guides/rust-to-solana/solana-playground.png)Solana
Playground

It’s the easiest way to begin developing with Solana, and it supports
building, testing, and deploying Solana Rust programs. Additionally, a number
of built-in tutorials are available to guide learning.

The Solana Playground allows developers to get started immediately without
setting up a local environment.

### Using Anchor #

[Anchor](https://www.anchor-lang.com/) is a framework that seeks to accelerate
the building of secure Solana programs. It can help by handling standard
boilerplate code, speeding up the development cycle. Additionally, it provides
some security checks by default, making Solana programs more secure.

To create a new program, simply [create a new Anchor
project](/ru/developers/guides/getstarted/intro-to-anchor) in the Solana
playground.

Alternatively, [install the Anchor CLI](https://www.anchor-
lang.com/docs/installation) locally, and then use `anchor init <project-name>`
to create a new Anchor project.

## Creating Off-chain Programs #

So far, this guide has covered the key details of developing **onchain Solana
programs** in Rust. However, it’s also possible to develop **off-chain Solana
clients** in Rust. This can be done by using the [solana_sdk
crate](https://docs.rs/solana-sdk/latest/solana_sdk/). This contains the
[solana_client crate](https://docs.rs/solana-client/latest/solana_client/)
that allows Rust programs to interact with a Solana node via the [JSON RPC
API](/ru/docs/rpc).

Another option is to use the [anchor_client crate](https://docs.rs/anchor-
client/latest/anchor_client/) which interacts with Solana programs written in
Anchor via RPC. Alternatively, consider writing onchain programs in Rust, and
off-chain [clients in JS/TS](/ru/de/docs/clients/javascript-reference).

## Wrap Up #

This guide has covered the basics of developing for Solana with Rust, from
setup details and restrictions to development environments and frameworks.

For more Rust-related Solana resources, check out the [Developing with Rust
page](/ru/docs/programs/lang-rust).

For other Solana program examples written with Rust, check out these [examples
on GitHub](https://github.com/solana-labs/solana-program-
library/tree/master/examples/rust).

To view several example solana programs, check out the [Solana Program
Examples on Github](/ru/docs/programs/examples).

[Previous« Setup, build, and deploy a Solana program locally in
Rust](/ru/developers/guides/getstarted/local-rust-hello-world)[NextSetup local
development and install the Solana CLI
»](/ru/developers/guides/getstarted/setup-local-development)

##### Table of Contents

  * [Understanding the Core Differences](/ru/developers/guides/getstarted/rust-to-solana#understanding-the-core-differences)
  * [Key Setup Details](/ru/developers/guides/getstarted/rust-to-solana#key-setup-details)
  * [Project Dependencies](/ru/developers/guides/getstarted/rust-to-solana#project-dependencies)
  * [Program Entrypoint](/ru/developers/guides/getstarted/rust-to-solana#program-entrypoint)
  * [Building and Testing](/ru/developers/guides/getstarted/rust-to-solana#building-and-testing)
  * [Understanding Restrictions](/ru/developers/guides/getstarted/rust-to-solana#understanding-restrictions)
  * [Package Limitations](/ru/developers/guides/getstarted/rust-to-solana#package-limitations)
  * [Rand Dependencies](/ru/developers/guides/getstarted/rust-to-solana#rand-dependencies)
  * [Macro Changes](/ru/developers/guides/getstarted/rust-to-solana#macro-changes)
  * [Compute Budget](/ru/developers/guides/getstarted/rust-to-solana#compute-budget)
  * [Learning the Development Environment and Frameworks](/ru/developers/guides/getstarted/rust-to-solana#learning-the-development-environment-and-frameworks)
  * [Solana Playground](/ru/developers/guides/getstarted/rust-to-solana#solana-playground)
  * [Using Anchor](/ru/developers/guides/getstarted/rust-to-solana#using-anchor)
  * [Creating Off-chain Programs](/ru/developers/guides/getstarted/rust-to-solana#creating-off-chain-programs)
  * [Wrap Up](/ru/developers/guides/getstarted/rust-to-solana#wrap-up)

[Scroll to Top](/ru/developers/guides/getstarted/rust-to-solana#)

[Edit Page](https://github.com/solana-foundation/developer-
content/tree/main/content/guides/getstarted/rust-to-solana.md)

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
