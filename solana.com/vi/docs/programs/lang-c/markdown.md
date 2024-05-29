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

  * [Project Layout](/vi/docs/programs/lang-c#project-layout)
  * [How to Build](/vi/docs/programs/lang-c#how-to-build)
  * [How to Test](/vi/docs/programs/lang-c#how-to-test)
  * [Program Entrypoint](/vi/docs/programs/lang-c#program-entrypoint)
  * [Serialization](/vi/docs/programs/lang-c#serialization)
  * [Data Types](/vi/docs/programs/lang-c#data-types)
  * [Heap](/vi/docs/programs/lang-c#heap)
  * [Logging](/vi/docs/programs/lang-c#logging)
  * [Compute Budget](/vi/docs/programs/lang-c#compute-budget)
  * [ELF Dump](/vi/docs/programs/lang-c#elf-dump)
  * [Examples](/vi/docs/programs/lang-c#examples)

[Scroll to Top](/vi/docs/programs/lang-c#)

[Edit Page](https://github.com/solana-foundation/developer-
content/tree/main/docs/programs/lang-c.md)

[Home](/vi)>[Solana Documentation](/vi/docs)>Developing Programs

# [Developing with C](/vi/docs/programs/lang-c)

Solana supports writing on-chain programs using the C and C++ programming
languages.

## Project Layout #

C projects are laid out as follows:

    
    
    /src/<program name>
    /makefile

The `makefile` should contain the following:

    
    
    OUT_DIR := <path to place to resulting shared object>
    include ~/.local/share/solana/install/active_release/bin/sdk/sbf/c/sbf.mk

The sbf-sdk may not be in the exact place specified above but if you setup
your environment per [How to Build](/vi/docs/programs/lang-c#how-to-build)
then it should be.

## How to Build #

First setup the environment:

  * Install the latest Rust stable from <https://rustup.rs>
  * Install the latest [Solana command-line tools](https://docs.solanalabs.com/cli/install)

Then build using make:

    
    
    make -C <program directory>

## How to Test #

Solana uses the [Criterion](https://github.com/Snaipe/Criterion) test
framework and tests are executed each time the program is built [How to
Build](/vi/docs/programs/lang-c#how-to-build).

To add tests, create a new file next to your source file named `test_<program
name>.c` and populate it with criterion test cases. See the [Criterion
docs](https://criterion.readthedocs.io/en/master) for information on how to
write a test case.

## Program Entrypoint #

Programs export a known entrypoint symbol which the Solana runtime looks up
and calls when invoking a program. Solana supports multiple versions of the
SBF loader and the entrypoints may vary between them. Programs must be written
for and deployed to the same loader. For more details see the [FAQ section on
Loaders](/vi/docs/programs/faq#loaders).

Currently there are two supported loaders [SBF
Loader](https://github.com/solana-
labs/solana/blob/7ddf10e602d2ed87a9e3737aa8c32f1db9f909d8/sdk/program/src/bpf_loader.rs#L17)
and [SBF loader deprecated](https://github.com/solana-
labs/solana/blob/7ddf10e602d2ed87a9e3737aa8c32f1db9f909d8/sdk/program/src/bpf_loader_deprecated.rs#L14).

They both have the same raw entrypoint definition, the following is the raw
symbol that the runtime looks up and calls:

    
    
    extern uint64_t entrypoint(const uint8_t *input)

This entrypoint takes a generic byte array which contains the serialized
program parameters (program id, accounts, instruction data, etc...). To
deserialize the parameters each loader contains its own [helper
function](/vi/docs/programs/lang-c#serialization).

### Serialization #

Each loader provides a helper function that deserializes the program's input
parameters into C types:

  * [SBF Loader deserialization](https://github.com/solana-labs/solana/blob/d2ee9db2143859fa5dc26b15ee6da9c25cc0429c/sdk/sbf/c/inc/solana_sdk.h#L304)
  * [SBF Loader deprecated deserialization](https://github.com/solana-labs/solana/blob/8415c22b593f164020adc7afe782e8041d756ddf/sdk/sbf/c/inc/deserialize_deprecated.h#L25)

Some programs may want to perform deserialization themselves, and they can by
providing their own implementation of the [raw
entrypoint](/vi/docs/programs/lang-c#program-entrypoint). Take note that the
provided deserialization functions retain references back to the serialized
byte array for variables that the program is allowed to modify (lamports,
account data). The reason for this is that upon return the loader will read
those modifications so they may be committed. If a program implements their
own deserialization function they need to ensure that any modifications the
program wishes to commit must be written back into the input byte array.

Details on how the loader serializes the program inputs can be found in the
[Input Parameter Serialization](/vi/docs/programs/faq#input-parameter-
serialization) docs.

## Data Types #

The loader's deserialization helper function populates the
[SolParameters](https://github.com/solana-
labs/solana/blob/8415c22b593f164020adc7afe782e8041d756ddf/sdk/sbf/c/inc/solana_sdk.h#L276)
structure:

    
    
    /**
     * Structure that the program's entrypoint input data is deserialized into.
     */
    typedef struct {
      SolAccountInfo* ka; /** Pointer to an array of SolAccountInfo, must already
                              point to an array of SolAccountInfos */
      uint64_t ka_num; /** Number of SolAccountInfo entries in `ka` */
      const uint8_t *data; /** pointer to the instruction data */
      uint64_t data_len; /** Length in bytes of the instruction data */
      const SolPubkey *program_id; /** program_id of the currently executing program */
    } SolParameters;

'ka' is an ordered array of the accounts referenced by the instruction and
represented as a [SolAccountInfo](https://github.com/solana-
labs/solana/blob/8415c22b593f164020adc7afe782e8041d756ddf/sdk/sbf/c/inc/solana_sdk.h#L173)
structures. An account's place in the array signifies its meaning, for
example, when transferring lamports an instruction may define the first
account as the source and the second as the destination.

The members of the `SolAccountInfo` structure are read-only except for
`lamports` and `data`. Both may be modified by the program in accordance with
the "runtime enforcement policy". When an instruction reference the same
account multiple times there may be duplicate `SolAccountInfo` entries in the
array but they both point back to the original input byte array. A program
should handle these cases delicately to avoid overlapping read/writes to the
same buffer. If a program implements their own deserialization function care
should be taken to handle duplicate accounts appropriately.

`data` is the general purpose byte array from the [instruction's instruction
data](/vi/docs/core/transactions#instruction) being processed.

`program_id` is the public key of the currently executing program.

## Heap #

C programs can allocate memory via the system call
[`calloc`](https://github.com/solana-
labs/solana/blob/c3d2d2134c93001566e1e56f691582f379b5ae55/sdk/sbf/c/inc/solana_sdk.h#L245)
or implement their own heap on top of the 32KB heap region starting at virtual
address x300000000. The heap region is also used by `calloc` so if a program
implements their own heap it should not also call `calloc`.

## Logging #

The runtime provides two system calls that take data and log it to the program
logs.

  * [`sol_log(const char*)`](https://github.com/solana-labs/solana/blob/d2ee9db2143859fa5dc26b15ee6da9c25cc0429c/sdk/sbf/c/inc/solana_sdk.h#L128)
  * [`sol_log_64(uint64_t, uint64_t, uint64_t, uint64_t, uint64_t)`](https://github.com/solana-labs/solana/blob/d2ee9db2143859fa5dc26b15ee6da9c25cc0429c/sdk/sbf/c/inc/solana_sdk.h#L134)

The [debugging](/vi/docs/programs/debugging#logging) section has more
information about working with program logs.

## Compute Budget #

Use the system call `sol_remaining_compute_units()` to return a `u64`
indicating the number of compute units remaining for this transaction.

Use the system call [`sol_log_compute_units()`](https://github.com/solana-
labs/solana/blob/d3a3a7548c857f26ec2cb10e270da72d373020ec/sdk/sbf/c/inc/solana_sdk.h#L140)
to log a message containing the remaining number of compute units the program
may consume before execution is halted

See the [Compute Budget](/vi/docs/core/fees#compute-budget) documentation for
more information.

## ELF Dump #

The SBF shared object internals can be dumped to a text file to gain more
insight into a program's composition and what it may be doing at runtime. The
dump will contain both the ELF information as well as a list of all the
symbols and the instructions that implement them. Some of the SBF loader's
error log messages will reference specific instruction numbers where the error
occurred. These references can be looked up in the ELF dump to identify the
offending instruction and its context.

To create a dump file:

    
    
    cd <program directory>
    make dump_<program name>

## Examples #

The [Solana Program Library github](https://github.com/solana-labs/solana-
program-library/tree/master/examples/c) repo contains a collection of C
examples

[Previous« FAQ](/vi/docs/programs/faq)[NextDeveloping with Rust
»](/vi/docs/programs/lang-rust)

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

