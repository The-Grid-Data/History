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

  * [Key Points](/ru/docs/core/accounts#key-points)
  * [Account](/ru/docs/core/accounts#account)
  * [AccountInfo](/ru/docs/core/accounts#accountinfo)
  * [Native Programs](/ru/docs/core/accounts#native-programs)
  * [System Program](/ru/docs/core/accounts#system-program)
  * [BPFLoader Program](/ru/docs/core/accounts#bpfloader-program)
  * [Sysvar Accounts](/ru/docs/core/accounts#sysvar-accounts)
  * [Custom Programs](/ru/docs/core/accounts#custom-programs)
  * [Program Account](/ru/docs/core/accounts#program-account)
  * [Data Account](/ru/docs/core/accounts#data-account)

[Scroll to Top](/ru/docs/core/accounts#)

[Edit Page](https://github.com/solana-foundation/developer-
content/tree/main/docs/core/accounts.md)

[Home](/ru)>[Solana Documentation](/ru/docs)>Core Concepts

# [Solana Account Model](/ru/docs/core/accounts)

On Solana, all data is stored in what are referred to as "accounts”. The way
data is organized on Solana resembles a [key-value
store](https://en.wikipedia.org/wiki/Key%E2%80%93value_database), where each
entry in the database is called an "account".

![Accounts](https://solana-developer-
content.vercel.app/assets/docs/core/accounts/accounts.svg)Accounts

## Key Points #

  * Accounts can store up to 10MB of data, which can consist of either executable program code or program state.

  * Accounts require a rent deposit in SOL, proportional to the amount of data stored, which is fully refundable when the account is closed.

  * Every account has a program "owner". Only the program that owns an account can modify it data or deduct its lamport balance. However, anyone can increase the balance.

  * Programs (smart contracts) are stateless accounts that store executable code.

  * Data accounts are created by programs to store and manage program state.

  * Native programs are built-in programs included with the Solana runtime.

  * Sysvar accounts are special accounts that store network cluster state.

## Account #

Each account is identifiable by its unique address, represented as 32 bytes in
the format of an [Ed25519](https://ed25519.cr.yp.to/) `PublicKey`. You can
think of the address as the unique identifier for the account.

![Account Address](https://solana-developer-
content.vercel.app/assets/docs/core/accounts/account-address.svg)Account
Address

This relationship between the account and its address can be thought of as a
key-value pair, where the address serves as the key to locate the
corresponding on-chain data of the account.

### AccountInfo #

Accounts have a [max size of 10MB](https://github.com/solana-
labs/solana/blob/27eff8408b7223bb3c4ab70523f8a8dca3ca6645/sdk/program/src/system_instruction.rs#L85)
(10 Mega Bytes) and the data stored on every account on Solana has the
following structure known as the [AccountInfo](https://github.com/solana-
labs/solana/blob/27eff8408b7223bb3c4ab70523f8a8dca3ca6645/sdk/program/src/account_info.rs#L19).

![AccountInfo](https://solana-developer-
content.vercel.app/assets/docs/core/accounts/accountinfo.svg)AccountInfo

The `AccountInfo` for each account includes the following fields:

  * `data`: A byte array that stores the state of an account. If the account is a program (smart contract), this stores executable program code. This field is often referred to as the "account data".
  * `executable`: A boolean flag that indicates if the account is a program.
  * `lamports`: A numeric representation of the account's balance in [lamports](/ru/docs/terminology#lamport), the smallest unit of SOL (1 SOL = 1 billion lamports).
  * `owner`: Specifies the public key (program ID) of the program that owns the account.

As a key part of the Solana Account Model, every account on Solana has a
designated "owner", specifically a program. Only the program designated as the
owner of an account can modify the data stored on the account or deduct the
lamport balance. It's important to note that while only the owner may deduct
the balance, anyone can increase the balance.

Info

To store data on-chain, a certain amount of SOL must be transferred to an
account. The amount transferred is proportional to the size of the data stored
on the account. This concept is commonly referred to as “rent”. However, you
can think of "rent" more like a "deposit" because the SOL allocated to an
account can be fully recovered when the account is closed.

## Native Programs #

Solana contains a small handful of native programs that are part of the
validator implementation and provide various core functionalities for the
network. You can find the full list of native programs
[here](https://docs.solanalabs.com/runtime/programs).

When developing custom programs on Solana, you will commonly interact with two
native programs, the System Program and the BPF Loader.

### System Program #

By default, all new accounts are owned by the [System
Program](https://github.com/solana-
labs/solana/tree/27eff8408b7223bb3c4ab70523f8a8dca3ca6645/programs/system/src).
The System Program performs several key tasks such as:

  * [New Account Creation](https://github.com/solana-labs/solana/blob/27eff8408b7223bb3c4ab70523f8a8dca3ca6645/programs/system/src/system_processor.rs#L145): Only the System Program can create new accounts.
  * [Space Allocation](https://github.com/solana-labs/solana/blob/27eff8408b7223bb3c4ab70523f8a8dca3ca6645/programs/system/src/system_processor.rs#L70): Sets the byte capacity for the data field of each account.
  * [Assign Program Ownership](https://github.com/solana-labs/solana/blob/27eff8408b7223bb3c4ab70523f8a8dca3ca6645/programs/system/src/system_processor.rs#L112): Once the System Program creates an account, it can reassign the designated program owner to a different program account. This is how custom programs take ownership of new accounts created by the System Program.

On Solana, a "wallet" is simply an account owned by the System Program. The
lamport balance of the wallet is the amount of SOL owned by the account.

![System Account](https://solana-developer-
content.vercel.app/assets/docs/core/accounts/system-account.svg)System Account

Info

Only accounts owned by the System Program can be used as transaction fee
payers.

### BPFLoader Program #

The [BPF Loader](https://github.com/solana-
labs/solana/tree/27eff8408b7223bb3c4ab70523f8a8dca3ca6645/programs/bpf_loader/src)
is the program designated as the "owner" of all other programs on the network,
excluding Native Programs. It is responsible for deploying, upgrading, and
executing custom programs.

## Sysvar Accounts #

Sysvar accounts are special accounts located at predefined addresses that
provide access to cluster state data. These accounts are dynamically updated
with data about the network cluster. You can find the full list of Sysvar
Accounts [here](https://docs.solanalabs.com/runtime/sysvars).

## Custom Programs #

On Solana, “smart contracts” are referred to as
[programs](/ru/docs/core/programs). A program is an account that contains
executable code and is indicated by an “executable” flag that is set to true.

For a more detailed explanation of the program deployment process, refer to
the [Deploying Programs](/ru/docs/programs/deploying) page of this
documentation.

### Program Account #

When new programs are [deployed](https://github.com/solana-
labs/solana/blob/27eff8408b7223bb3c4ab70523f8a8dca3ca6645/programs/bpf_loader/src/lib.rs#L498)
on Solana, technically three separate accounts are created:

  * **Program Account** : The main account representing an on-chain program. This account stores the address of an executable data account (which stores the compiled program code) and the update authority for the program (address authorized to make changes to the program).
  * **Program Executable Data Account** : An account that contains the executable byte code of the program.
  * **Buffer Account** : A temporary account that stores byte code while a program is being actively deployed or upgraded. Once the process is complete, the data is transferred to the Program Executable Data Account and the buffer account is closed.

For example, here are links to the Solana Explorer for the Token Extensions
[Program
Account](https://explorer.solana.com/address/TokenzQdBNbLqP5VEhdkAS6EPFLC1PHnBqCXEpPxuEb)
and its corresponding [Program Executable Data
Account](https://explorer.solana.com/address/DoU57AYuPFu2QU514RktNPG22QhApEjnKxnBcu4BHDTY).

![Program and Executable Data Accounts](https://solana-developer-
content.vercel.app/assets/docs/core/accounts/program-account-
expanded.svg)Program and Executable Data Accounts

For simplicity, you can think of the "Program Account" as the program itself.

![Program Account](https://solana-developer-
content.vercel.app/assets/docs/core/accounts/program-account-
simple.svg)Program Account

Info

The address of the "Program Account" is commonly referred to as the “Program
ID”, which is used to invoke the program.

### Data Account #

Solana programs are "stateless", meaning that program accounts only contain
the program's executable byte code. To store and modify additional data, new
accounts must be created. These accounts are commonly referred to as “data
accounts”.

Data accounts can store any arbitrary data as defined in the owner program's
code.

![Data Account](https://solana-developer-
content.vercel.app/assets/docs/core/accounts/data-account.svg)Data Account

Note that only the [System Program](/ru/docs/core/accounts#system-program) can
create new accounts. Once the System Program creates an account, it can then
transfer ownership of the new account to another program.

In other words, creating a data account for a custom program requires two
steps:

  1. Invoke the System Program to create an account, which then transfers ownership to a custom program
  2. Invoke the custom program, which now owns the account, to then initialize the account data as defined in the program code

This data account creation process is often abstracted as a single step, but
it's helpful to understand the underlying process.

[Previous« Intro to Development](/ru/docs/intro/dev)[NextTransactions and
Instructions »](/ru/docs/core/transactions)

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

