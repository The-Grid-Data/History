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

  * [Key Points](/docs/core/cpi#key-points)
  * [How to write a CPI](/docs/core/cpi#how-to-write-a-cpi)
  * [Basic CPI](/docs/core/cpi#basic-cpi)
  * [CPI with PDA Signer](/docs/core/cpi#cpi-with-pda-signer)

[Scroll to Top](/docs/core/cpi#)

[Edit Page](https://github.com/solana-foundation/developer-
content/tree/main/docs/core/cpi.md)

[Home](/)>[Solana Documentation](/docs)>Core Concepts

# [Cross Program Invocation (CPI)](/docs/core/cpi)

A Cross Program Invocation (CPI) refers to when one program invokes the
instructions of another program. This mechanism allows for the composability
of Solana programs.

You can think of instructions as API endpoints that a program exposes to the
network and a CPI as one API internally invoking another API.

![Cross Program Invocation](https://solana-developer-
content.vercel.app/assets/docs/core/cpi/cpi.svg)Cross Program Invocation

When a program initiates a Cross Program Invocation (CPI) to another program:

  * The signer privileges from the initial transaction invoking the caller program (A) extend to the callee (B) program
  * The callee (B) program can make further CPIs to other programs, up to a maximum depth of 4 (ex. B->C, C->D)
  * The programs can "sign" on behalf of the [PDAs](/docs/core/pda) derived from its program ID

Info

The Solana program runtime defines a constant called
[`max_invoke_stack_height`](https://github.com/solana-
labs/solana/blob/27eff8408b7223bb3c4ab70523f8a8dca3ca6645/program-
runtime/src/compute_budget.rs#L31-L35), which is set to a [value of
5](https://github.com/solana-
labs/solana/blob/27eff8408b7223bb3c4ab70523f8a8dca3ca6645/program-
runtime/src/compute_budget.rs#L138). This represents the maximum height of the
program instruction invocation stack. The stack height begins at 1 for
transaction instructions, increases by 1 each time a program invokes another
instruction. This setting effectively limits invocation depth for CPIs to 4.

## Key Points #

  * CPIs enable Solana program instructions to directly invoke instructions on another program.

  * Signer privileges from a caller program are extended to the callee program.

  * When making a CPI, programs can "sign" on behalf of PDAs derived from their own program ID.

  * The callee program can make additional CPIs to other programs, up to a maximum depth of 4.

## How to write a CPI #

Writing an instruction for a CPI follows the same pattern as building an
[instruction](/docs/core/transactions#instruction) to add to a transaction.
Under the hood, each CPI instruction must specify the following information:

  * **Program address** : Specifies the program being invoked
  * **Accounts** : Lists every account the instruction reads from or writes to, including other programs
  * **Instruction Data** : Specifies which instruction on the program to invoke, plus any additional data required by the instruction (function arguments)

Depending on the program you are making the call to, there may be crates
available with helper functions for building the instruction. Programs then
execute CPIs using either one of the following functions from the
`solana_program` crate:

  * `invoke` \- used when there are no PDA signers
  * `invoke_signed` \- used when the caller program needs to sign with a PDA derived from its program ID

### Basic CPI #

The [`invoke`](https://github.com/solana-
labs/solana/blob/27eff8408b7223bb3c4ab70523f8a8dca3ca6645/sdk/program/src/program.rs#L132)
function is used when making a CPI that does not require PDA signers. When
making CPIs, signers provided to the caller program automatically extend to
the callee program.

    
    
    pub fn invoke(
        instruction: &Instruction,
        account_infos: &[AccountInfo<'_>]
    ) -> Result<(), ProgramError>

Here is an example program on [Solana
Playground](https://beta.solpg.io/github.com/ZYJLiu/doc-
examples/tree/main/cpi-invoke) that makes a CPI using the `invoke` function to
call the transfer instruction on the System Program. You can also reference
the [Basic CPI guide](/developers/guides/getstarted/how-to-cpi) for further
details.

### CPI with PDA Signer #

The [`invoke_signed`](https://github.com/solana-
labs/solana/blob/27eff8408b7223bb3c4ab70523f8a8dca3ca6645/sdk/program/src/program.rs#L247)
function is used when making a CPI that requires PDA signers. The seeds used
to derive the signer PDAs are passed into the `invoke_signed` function as
`signer_seeds`.

You can reference the [Program Derived Address](/docs/core/pda) page for
details on how PDAs are derived.

    
    
    pub fn invoke_signed(
        instruction: &Instruction,
        account_infos: &[AccountInfo<'_>],
        signers_seeds: &[&[&[u8]]]
    ) -> Result<(), ProgramError>

The runtime uses the privileges granted to the caller program to determine
what privileges can be extended to the callee. Privileges in this context
refer to signers and writable accounts. For example, if the instruction the
caller is processing contains a signer or writable account, then the caller
can invoke an instruction that also contains that signer and/or writable
account.

While PDAs have [no private keys](/docs/core/pda#what-is-a-pda), they can
still act as a signer in an instruction via a CPI. To verify that a PDA is
derived from the calling program, the seeds used to generate the PDA must be
included as `signers_seeds`.

When the CPI is processed, the Solana runtime [internally calls
`create_program_address`](https://github.com/solana-
labs/solana/blob/27eff8408b7223bb3c4ab70523f8a8dca3ca6645/programs/bpf_loader/src/syscalls/cpi.rs#L550)
using the `signers_seeds` and the `program_id` of the calling program. If a
valid PDA is found, the address is [added as a valid
signer](https://github.com/solana-
labs/solana/blob/27eff8408b7223bb3c4ab70523f8a8dca3ca6645/programs/bpf_loader/src/syscalls/cpi.rs#L552).

Here is an example program on [Solana
Playground](https://beta.solpg.io/github.com/ZYJLiu/doc-
examples/tree/main/cpi-invoke-signed) that makes a CPI using the
`invoke_signed` function to call the transfer instruction on the System
Program with a PDA signer. You can reference the [CPI with PDA Signer
guide](/developers/guides/getstarted/how-to-cpi-with-signer) for further
details.

[Previous« Program Derived Address](/docs/core/pda)[NextTokens on Solana
»](/docs/core/tokens)

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

