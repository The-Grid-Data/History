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

  * [Key Points](/ru/docs/core/cpi#key-points)
  * [How to write a CPI](/ru/docs/core/cpi#how-to-write-a-cpi)
  * [Basic CPI](/ru/docs/core/cpi#basic-cpi)
  * [CPI with PDA Signer](/ru/docs/core/cpi#cpi-with-pda-signer)

[Scroll to Top](/ru/docs/core/cpi#)

[Edit Page](https://github.com/solana-foundation/developer-
content/tree/main/docs/core/cpi.md)

[Home](/ru)>[Solana Documentation](/ru/docs)>Core Concepts

# [Cross Program Invocation (CPI)](/ru/docs/core/cpi)

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
  * The programs can "sign" on behalf of the [PDAs](/ru/docs/core/pda) derived from its program ID

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
[instruction](/ru/docs/core/transactions#instruction) to add to a transaction.
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
the [Basic CPI guide](/ru/developers/guides/getstarted/how-to-cpi) for further
details.

### CPI with PDA Signer #

The [`invoke_signed`](https://github.com/solana-
labs/solana/blob/27eff8408b7223bb3c4ab70523f8a8dca3ca6645/sdk/program/src/program.rs#L247)
function is used when making a CPI that requires PDA signers. The seeds used
to derive the signer PDAs are passed into the `invoke_signed` function as
`signer_seeds`.

You can reference the [Program Derived Address](/ru/docs/core/pda) page for
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

While PDAs have [no private keys](/ru/docs/core/pda#what-is-a-pda), they can
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
guide](/ru/developers/guides/getstarted/how-to-cpi-with-signer) for further
details.

[Previous« Program Derived Address](/ru/docs/core/pda)[NextTokens on Solana
»](/ru/docs/core/tokens)

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

