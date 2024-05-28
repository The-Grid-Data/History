This website uses cookies to offer you a better browsing experience. Find out
more on how we use cookies.

Opt-out[Details](/privacy-policy#collection-of-information)

Accept

[![Solana](/_next/static/media/logotype.e4df684f.svg)](/)

  * Learn
  * Developers
  * Solutions
  * Network
  * Community

Search```K`

[Documentation](/docs)[RPC
API](/docs/rpc)[Cookbook](/developers/cookbook)[Guides](/developers/guides)[Terminology](/docs/terminology)

# EVM vs. SVM: Smart Contracts

Learn the differences between Ethereum and Solana smart contracts.

**Table of Contents**

  

Native programs and the Solana Program Library (SPL)

Writing Programs

Deploying Programs

Summary

You can write and deploy programs on the Solana blockchain. **Programs,** also
known as **smart contracts** in other protocols, serve as the foundation for
on-chain activities ranging from DeFi and NFTs to social media and games.

  * Programs process instructions received from users or other programs.
  * All programs do not maintain state. In other words, the data used by programs is sent to separate accounts through instructions.
  * The program itself is stored in an `executable` checked account.
  * All programs are owned by the BPF Loader and executed by the Solana Runtime.
  * Developers typically write programs in Rust or C++. However, any language targeting LLVM and BPF backend can be chosen.
  * All programs have a single entry point where instruction processing occurs (i.e., `process_instruction`). The following parameters are always included:
  * program_id: pubkey,
  * accounts: array,
  * instruction_data: byte array

Unlike most other blockchains, Solana completely separates data and code. All
data that programs interact with is stored in separate accounts and is called
through instructions.

This model allows for comprehensive single programs to operate through various
accounts without the need for additional deployments. A common example of this
pattern can be seen between Native and SPL Programs.

## Native programs and the Solana Program Library (SPL)

Solana has many programs that serve as core building blocks for on-chain
interactions.

These programs are divided into Native Programs and Solana Program Library
(SPL) Programs.

Native Programs provide the foundational functionality required to operate
validators. One of the most well-known programs among these is the System
Program, responsible for managing new accounts and transferring SOL between
two groups.

SPL Programs support various on-chain activities, including token creation,
exchange, lending, stake pool generation, and on-chain name services. The SPL
Token Program can be invoked directly through the CLI. Other programs, like
the Associated Token Account Program, are typically configured as custom
program

## **Writing Programs**

Programs are typically developed in Rust and C++. However, you can develop in
any language targeting LLVM and BPF backend. Recent efforts by Neon Labs and
Solang make EVM compatibility possible, allowing developers to write programs
in Solidity.

Most Rust-based programs follow the architecture below:

File | Description  
---|---  
`lib.rs` | Registering modules  
`entrypoint.rs` | Entrypoint to the program  
`instruction.rs` | Program API, (de)serializing instruction data  
`processor.rs` | Program logic  
`state.rs` | Program objects, (de)serializing state  
`error.rs` | Program-specific errors  
  
Recently, Anchor has emerged as a framework for developing programs. Anchor
reduces boilerplate and simplifies (de)serialization handling, similar to Ruby
on Rails but for Rust-based programs. Programs are typically developed and
tested in the Localhost and Devnet environments before being deployed to
Testnet and Mainnet.

Solana supports the following environments:

Cluster Environment | RPC Connection URL  
---|---  
Mainnet-beta  | https://api.mainnet-beta.solana.com  
Testnet | https://api.testnet.solana.com  
Devnet | https://api.devtnet.solana.com  
Localhost | Default port: 8899 (e.g., http://localhost:8899)  
  
Once deployed to an environment, clients can interact with on-chain programs
through RPC connections to each cluster.

## Deploying Programs

Developers can deploy programs via the CLI as follows:

`solana program deploy <PROGRAM_FILEPATH>`

When a program is deployed, it is compiled into an ELP shared object
(including BPF bytecode) and uploaded to the Solana cluster. Programs exist
inside an account except when they are marked as executable and allocated to
the BPF Loader. The account's address is used as the` program_id` to reference
the program in all transactions.

Solana supports multiple BPF Loaders, including the recent Upgradable BPF
Loader. BPF Loaders are responsible for managing program accounts and making
this possible through the program_id for clients.

All programs have a single entry point where instruction processing occurs
(i.e., process_instruction). The parameters always include:

  * program_id: pubkey
  * accounts: array
  * instruction_data: byte array

Once called, programs are executed by the Solana Runtime.

### Summary

  * The Program in Solana corresponds to 'Executable account' on the Solana blockchain.
  * The concept of smart contracts in Ethereum aligns with the concept of programs in Solana.
  * Solana enables anyone to issue tokens without the need to deploy additional contracts.

EVM TO SVM

[Home](/developers/evm-to-svm)[Next: Client differences](/developers/evm-to-
svm/client-differences)

## Start building on Solana

[![](/_next/image?url=https%3A%2F%2Fcdn.builder.io%2Fapi%2Fv1%2Fimage%2Fassets%252Fce0c7323a97a4d91bd0baa7490ec9139%252Fdfb1773873354d118d134beca2334288&w=3840&q=75)![](/_next/image?url=https%3A%2F%2Fcdn.builder.io%2Fapi%2Fv1%2Fimage%2Fassets%252Fce0c7323a97a4d91bd0baa7490ec9139%252Fdfb1773873354d118d134beca2334288&w=3840&q=75)Intro
to Solana Development](/developers/guides/getstarted/hello-world-in-your-
browser)

[![](/_next/image?url=https%3A%2F%2Fcdn.builder.io%2Fapi%2Fv1%2Fimage%2Fassets%252Fce0c7323a97a4d91bd0baa7490ec9139%252Fdfb1773873354d118d134beca2334288&w=3840&q=75)![](/_next/image?url=https%3A%2F%2Fcdn.builder.io%2Fapi%2Fv1%2Fimage%2Fassets%252Fce0c7323a97a4d91bd0baa7490ec9139%252Fdfb1773873354d118d134beca2334288&w=3840&q=75)
Intro to Solana Development](/developers/guides/getstarted/hello-world-in-
your-
browser)[![](/_next/image?url=https%3A%2F%2Fcdn.builder.io%2Fapi%2Fv1%2Fimage%2Fassets%252Fce0c7323a97a4d91bd0baa7490ec9139%252Fdfb1773873354d118d134beca2334288&w=3840&q=75)![](/_next/image?url=https%3A%2F%2Fcdn.builder.io%2Fapi%2Fv1%2Fimage%2Fassets%252Fce0c7323a97a4d91bd0baa7490ec9139%252Fdfb1773873354d118d134beca2334288&w=3840&q=75)
Solana Development
Course](https://www.soldev.app/course)[![](/_next/image?url=https%3A%2F%2Fcdn.builder.io%2Fapi%2Fv1%2Fimage%2Fassets%252Fce0c7323a97a4d91bd0baa7490ec9139%252Fdfb1773873354d118d134beca2334288&w=3840&q=75)![](/_next/image?url=https%3A%2F%2Fcdn.builder.io%2Fapi%2Fv1%2Fimage%2Fassets%252Fce0c7323a97a4d91bd0baa7490ec9139%252Fdfb1773873354d118d134beca2334288&w=3840&q=75)
Solana
Bootcamp](https://youtu.be/0P8JeL3TURU?feature=shared)[![](/_next/image?url=https%3A%2F%2Fcdn.builder.io%2Fapi%2Fv1%2Fimage%2Fassets%252Fce0c7323a97a4d91bd0baa7490ec9139%252Fdfb1773873354d118d134beca2334288&w=3840&q=75)![](/_next/image?url=https%3A%2F%2Fcdn.builder.io%2Fapi%2Fv1%2Fimage%2Fassets%252Fce0c7323a97a4d91bd0baa7490ec9139%252Fdfb1773873354d118d134beca2334288&w=3840&q=75)
More Solana Developer Tools](/developers)

![](https://cdn.builder.io/api/v1/pixel?apiKey=ce0c7323a97a4d91bd0baa7490ec9139)

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

