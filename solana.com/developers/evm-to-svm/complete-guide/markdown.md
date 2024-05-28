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

# A Complete Guide to Solana Development for Ethereum Developers

**Table of Contents**

  

What makes Solana different from Ethereum?

Account Model

What are the benefits of the Solana Account Model?

Local Fee Markets

How do fees work on Solana?

How do transactions work on Solana?

What are the limitations of transactions on Solana?

Where is the Mempool?

Where can I find the smart contract code?

What are the differences in developer environment?

Programming languages

Where are the tools I’m familiar with from EVM?

What's different with smart contract development?

How do I build my EVM project on Solana?

![](https://cdn.builder.io/api/v1/image/assets%2Fce0c7323a97a4d91bd0baa7490ec9139%2Ff1d4c0384bf94fd4bd51807305310e9e?width=593)

In this article, we dive into the key differences between developing on
Ethereum and Solana, guiding you through how to build on Solana. Coming from
Ethereum, Solana will look and feel much different and have a diverse toolset
to use as you develop. This article will arm you with all the tools necessary
to build on Solana from an Ethereum background.

## What makes Solana different from Ethereum?

### Account Model

When developing on Solana, the most significant difference will run into is
the account model design. It is helpful to understand why Solana’s account
model was designed differently. Unlike Ethereum, Solana is designed to take
advantage of the multiple cores in high-end machines. There is a trend in
computing resources where the amount of available cores increases over time
and becomes cheaper for people to purchase. Considering this, the account
model is designed to leverage multiple cores, creating a system that
parallelizes the transactions with each other. This parallelization creates
further optimizations, such as local fee markets and faster throughput, which
we will explore later.

So what is meant by the “account model”? On Solana, accounts are like objects
containing some arbitrary data and specific rules for modification. Everything
is an account on Solana, including smart contracts. Like Ethereum, each
account has an address identifier to help locate an account. However, unlike
Ethereum, where each smart contract is an account with the execution logic and
storage tied together, Solana’s smart contracts are entirely stateless.

Smart contracts on Solana carry no state of their own and must have the state
passed to them to execute on. To illustrate this, let’s take a look at two
smart contracts for a counter, one in Solidity on Ethereum and one using Rust
on Solana.

**Ethereum Counter Smart Contract**

`contract Counter { `

`int private count = 0; `

`function incrementCounter() public `

`{ count += 1; `

`} `

`function getCount() public constant returns (int) { `

`return count; `

`} `

`}`

**Solana Counter Program**

sdffsd

Hello! Use the editor to add your copy!

**Node storing all data and participating in consensus**

  * **Ethereum:** Archive Node
  * **Solana:** [n/a]

**Node storing some data and participating in consensus**

  * **Ethereum:** Full Node
  * **Solana:** Consensus Node

**Node storing some data and not participating in consensus**

  * **Ethereum:** Light Node
  * **Solana:** RPC Node

`#[program]`

`pub mod counter_anchor {`

`use super::*;`

  

`pub fn initialize_counter(_ctx: Context<InitializeCounter>) -> Result<()> {`

`Ok(())`

` }`

  

`pub fn increment(ctx: Context<Increment>) -> Result<()> {`

` ctx.accounts.counter.count =
ctx.accounts.counter.count.checked_add(1).unwrap();`

`Ok(())`

` }`

`}`

  

`#[derive(Accounts)]`

`pub struct InitializeCounter<'info> {`

` #[account(mut)]`

` pub payer: Signer<'info>,`

` #[account(`

` init,`

` space = 8 + Counter::INIT_SPACE,`

` payer = payer`

` )]`

` pub counter: Account<'info, Counter>,`

` pub system_program: Program<'info, System>,`

`}`

  

`#[derive(Accounts)]`

`pub struct Increment<'info> {`

` #[account(mut)]`

` pub counter: Account<'info, Counter>,`

`}`

  

`#[account]`

`#[derive(InitSpace)]`

`pub struct Counter {`

` count: u64,`

`}`

While in Solidity, you have `int private count = 0;`, you have a struct within
the Rust smart contract stating `initialize_counter`. This initial counter
creates an account with a `count` of 0, which you then can pass this account
to `increment` to add to the `count`. This is not to have state within the
smart contract itself.

There are separate accounts that store the data outside of the program. To
execute the logic in a program, you would pass the account you want to perform
on. In the case of this `counter` program, you pass a `counter `account to the
program when calling the` increment` function, and the program will increment
the value in the `counter` account.

![](https://cdn.builder.io/api/v1/image/assets%2Fce0c7323a97a4d91bd0baa7490ec9139%2Fc213f02517a64dfbadfb56e05c51128c?width=1216)

### What are the benefits of the Solana Account Model?

One of the most significant benefits of the Solana Account Model is program
reusability.

Take ERC20 for example. ERC20 defines an interface specification on Ethereum
for tokens. Every time someone wants to make a new token, the developer will
have to redeploy the ERC20 smart contract onto Ethereum with its specified
values, incurring the high cost of the redeployment.

Solana is different. You do not have to redeploy another smart contract onto
the blockchain when creating new tokens. Instead, you create a new account,
known as the mint account, off of the Solana Token Program, where the account
defines a set of values to give the number of tokens in circulation, decimal
points, who can mint more tokens, and who can freeze tokens.

![](https://cdn.builder.io/api/v1/image/assets%2Fce0c7323a97a4d91bd0baa7490ec9139%2F67649c6ad3464fa1b07b3bdabce52c8c?width=1216)

You do not need to write any Rust or smart contracts to deploy a new token on
Solana. Send a transaction to the Token Program to create a new token in your
language of choice, and the token will then appear in your wallet. With the
Solana Program Library CLI, you can do this in a single command:

`$ spl-token create-token`

### Local Fee Markets

Another fortunate side effect of having the Solana account model is the
ability to model fees based on state contention. As mentioned earlier,
transactions can be executed in parallel. However, they are only executed in
parallel based on what accounts are being written to. For example, let's say
there is a popular NFT mint going on Solana. Typically, this popularity would
increase the prices for everyone using the chain, but instead, everyone not
participating in the NFT mint is unaffected.

As the name suggests, fee markets are local per account. If you're sending a
transfer of USDC to someone while everyone else is minting the hottest new
NFT, you will be unaffected and continue paying the low fee you're used to on
Solana. This works with any application in Solana, avoiding the common global
fee market you're used to on Ethereum while lowering everyone's cost.

### How do fees work on Solana?

Fees on Solana are broken up into a few categories: Base Fee, Priority Fee,
and Rent.

The Base Fee can be calculated based on the number of signatures in a
transaction. Each signature costs 5000 lamports (0.000000001
[sol](/docs/terminology#sol) = 1 lamport). If your transaction requires 5
signatures, the base fee would be 25000 lamports. This base fee adds economic
backpressure to the cluster's signature verification, which is one of the more
compute-intensive actions. Half of the base fees are burnt, and half are
rewarded to the validators.

The Priority Fee is an optional fee that anyone can add to a transaction to
give priority over other transactions executing at the same time. Priority fee
is measured based on the amount of compute units used in a transaction.
Compute units are similar to Gas on Ethereum, a simple measurement of
computing resources required for a transaction. Like Ethereum, the priority of
your transaction is calculated based on the product of the compute unit price
and the compute units used, or `priority fee = compute units * compute unit
price`. Like base fees, half of priority fees are burnt, and half are rewarded
to the validators.

The final fee, Rent, is more of a deposit than a fee. When you create accounts
or allocate space on the network, you must deposit some SOL for the network to
keep your account. Rent is calculated based on the number of bytes stored on
the network, and an additional base fee is charged for allocating space. It is
important to note that Rent fees are not lost; they can be collected if you
close the account and allow the allocated space to be recollected by the
cluster.

### How do transactions work on Solana?

With each fee being paid when executing a transaction, it is good to
understand how transactions work. A transaction consists of four parts:

  * one or more instructions
  * an array of accounts to read or write from
  * one or more signatures
  * recent blockhash or nonce

An [instruction](/docs/terminology#instruction) is the smallest execution
logic on Solana. Instructions are a call to update the global Solana state.
Instructions invoke programs that make calls to the Solana runtime to update
the state (for example, calling the token program to transfer tokens from your
account to another account). You can think of an instruction like a function
call on an Ethereum smart contract.

A significant difference between Ethereum and Solana is the number of function
calls in a single transaction due to the number of instructions. Having
multiple instructions per transaction benefits developers as they do not have
to create custom smart contracts to chain functions in a single transaction.
Each instruction can be a separate function call, done in order in the
transaction. Transactions are atomic, meaning if any of these instructions
fails, the whole transaction will fail, and you will only pay the transaction
fee. This is like failing a transaction due to not setting the correct
slippage on Ethereum.

Another key difference to remember would be the use of a recent blockhash
instead of an incremental nonce for transactions. When a wallet wants to make
a transaction, a recent blockhash will be pulled from the cluster to create a
valid transaction. This recent blockhash only makes the transaction valid for
150 blocks after the recent blockhash was retrieved. This prevents long-living
transaction signatures from being executed at a much later date.

### What are the limitations of transactions on Solana?

Like Ethereum gas limitations, there are specific compute unit limitations on
transactions for Solana. Each limitation can be found below:

| Ethereum | Solana  
---|---|---  
Single Transaction Compute Cap  |  30,000,000  |  1,400,000 Compute Units   
Block Compute Cap  |  30,000,000 Gas  |  48,000,000 Compute Units   
  
Solana has a [few additional caps](/ru/docs/programs/limitations) placed on
transactions. Each account referenced may be at most 12,000,000 compute units
used per block. This cap prevents people from write-locking a single account
too many times in a single block, further preventing the local fee markets
from being overrun by one account.

Another limit on transactions is the depth of instruction calls you can make
in a single instruction. This limit is currently set to 4, meaning you can
only call instructions at a depth of 4 before the transaction would revert.
This makes re-entrancy issues nonexistent on Solana compared to something
you’d have to worry about on Ethereum.

### Where is the Mempool?

Unlike Ethereum, Mempools don’t exist on Solana. Solana validators forward
transactions to up to the following four leaders on the leader schedule. While
Solana doesn’t have a mempool, it still has priority fees to help order
transactions. Not having a mempool forces the transactions to hop from leader
to leader until blockhash expiration, but it reduces the overhead of gossip
communicating the mempool across the cluster.

### Where can I find smart contract code?

In the EVM world, most are familiar with finding smart contract code on
Etherscan when viewing the smart contract address. However, viewing smart
contract code on an explorer in the Solana ecosystem is relatively new and
needs to be established compared to EVM standards. At the time of writing,
[Solana.fm](http://Solana.fm) is the only explorer that supports viewing smart
contract code based on [verifiable builds](https://github.com/otter-
sec/solana_verified_programs_api).

You can find the smart contract code by visiting a smart contract address the
explorer. For example, going to the [Pheonix smart
contract](https://solana.fm/address/PhoeNiXZ8ByJGLkxNfZRnkUfjvmuYqLR89jjFHGqdXY),
you can find the smart contract’s code [under the verification
tab](https://solana.fm/address/PhoeNiXZ8ByJGLkxNfZRnkUfjvmuYqLR89jjFHGqdXY/verification).
From here, you can analyze the code and understand if the smart contract is
something you want to interact with.

## What are the differences in the developer environment?

### Programming languages

EVM primarily uses Solidity to write smart contracts, while Solana uses Rust.
There is a framework called the [Anchor framework](https://www.anchor-
lang.com/) that allows you to build in Rust with many of the tools you are
familiar with from EVM, but it is still Rust. If you want to stick with
Solidity while building on Solana, a project named
[Neon](https://neonevm.org/) enables using Solidity. Neon comes with many of
the tools you are familiar with, such as using Foundry or Hardhat during
development. Using Neon may get you up and running faster, building on Solana,
but you would need more composability outside of the Neon ecosystem with other
Solana projects.

Like Ethereum, on the client side, you can find comparable SDKs for all your
favorite programming languages on Solana.

Language | SDK  
---|---  
Javascript  |  [solana/web3.js](https://github.com/solana-labs/solana-web3.js)  
Rust  |  [solana_sdk](https://docs.rs/solana-sdk/latest/solana_sdk/)  
Python  |  [solana-py](https://github.com/michaelhly/solana-py)  
Java  |  [solanaj](https://github.com/skynetcap/solanaj)  
C++  |  [solcpp](https://github.com/mschneider/solcpp)  
C#  |  [Solnet](https://github.com/bmresearch/Solnet)  
GoLang  |  [solana-go](https://github.com/gagliardetto/solana-go)  
  
### Where are the tools I’m familiar with from EVM?

As you migrate from EVM to building on Solana, you may be looking for the
tools you are familiar with. Currently, the Solana ecosystem does not have
tooling equal to Foundry but has a decent amount of other equivalents to the
tools you are used to.

Tool | Solana Equivalent  
---|---  
HardHat | [Solana Test Validator](https://docs.solana.com/developing/test-validator)  
Brownie | [Program-test](https://docs.rs/solana-program-test/latest/solana_program_test/),  
[BankRun.js](https://kevinheavey.github.io/solana-bankrun/)  
Ethers, Wagmi | [@solana/web.js](https://www.npmjs.com/package/@solana/web3.js)  
Remix | [Solana Playground](https://beta.solpg.io/)  
ABI | Anchor Framework's IDL  
Etherscan | [SolanaFM](https://solana.fm/),  
[XRay](https://xray.helius.xyz/)  
scaffold-eth | [create-solana-dapp](https://github.com/solana-developers/create-solana-dapp)  
  
### What’s different with smart contract development?

There are several things to take note of when you are building programs on
Solana or migrating your Ethereum smart contract over.

For example, if you are looking for mapping like you are used to using on
Ethereum smart contracts, this type does not directly exist on Solana.
Instead, you use program-derived addresses, or PDA for short. Like mapping,
program-derived addresses can give you the ability to create a map from a key
or account to a value stored on-chain. The way you map is different from that
of Ethereum.

Let’s say you want to map user accounts to their balance on-chain. In
Solidity, you do something like the following:

`mapping(address => uint) public balances;`

With program derived addresses, you instead have to do the following:

**Client:**

`const [BALANCE_PDA] = await anchor.web3.PublicKey.findProgramAddress(`

`[Buffer.from("BALANCE"), pg.wallet.publicKey.toBuffer()],`

`pg.program.programId`

`);`

**Program:**

`#[derive(Accounts)]`

`#[instruction(restaurant: String)]`

`pub struct BalanceAccounts<'info> {`

` #[account(`

` init_if_needed,`

` payer = signer,`

` space = 500,`

` seeds = [balance.as_bytes().as_ref(), signer.key().as_ref()],`

` bump`

` )]`

` pub balance: Account<'info,BalanceAccount>,`

` #[account(mut)]`

` pub signer: Signer<'info>,`

` pub system_program: Program<'info, System>,`

`}`

`#[account]`

`pub struct BalanceAccount {`

` pub balance: u8`

`}`

The map's key is derived from the combination of the "balance" string and the
signer's public key, while the program derived address provides the location
to look up the map's value. Program derived addresses have more functionality
than just providing a map; we can [learn about that
later](https://solanacookbook.com/core-concepts/pdas.html#facts).

In Solidity, the ability to upgrade your smart contracts using proxy contracts
has become the norm. On Solana, programs are default upgradable without any
special work involved. Each smart contract can be upgraded by a CLI command
`solana program deploy <program_filepath`. While programs are default
upgradable, you can still demote their status to immutable with `solana
program set-upgrade-authority <program_address> --final`. Once immutable, the
program will be flagged as not upgradable on the explorers.

![](https://cdn.builder.io/api/v1/image/assets%2Fce0c7323a97a4d91bd0baa7490ec9139%2F169d65c59d4443ff9229e76bbcf69697?width=400)

A common thing you do when writing a solidity smart contract is check for
either `msg.sender` or `tx.origin`. There isnʼt an equivalent on Solana
because each transaction can have multiple signers. Also the person sending
the transaction is not necessarily the one who signed the transaction because
you have someone else pay for your transactions.

Let’s take a look at this basic Solana Program:

`#[program]`

`pub mod gettingSigners {`

` use super::*;`

  

` pub fn initialize(ctx: Context<Initialize>) -> Result<()> {`

` let the_signer: &mut Signer = &mut ctx.accounts.the_signer;`

  

` msg!("The signer: {:?}", *the_signer.key);`

  

` Ok(())`

` }`

`}`

  

`#[derive(Accounts)]`

`pub struct Initialize<'info> {`

` #[account(mut)]`

` pub the_signer: Signer<'info>,`

`}`

This will output a signer of the transaction as part of your program logs. As
mentioned before, you can have multiple signers:

`#[program]`

`pub mod gettingSigners {`

` use super::*;`

  

` pub fn initialize(ctx: Context<Initialize>) -> Result<()> {`

` let the_signer: &mut Signer = &mut ctx.accounts.first_signer;`

  

` msg!("The signer: {:?}", *the_signer.key);`

  

` Ok(())`

` }`

`}`

  

`#[derive(Accounts)]`

`pub struct Initialize<'info> {`

` #[account(mut)]`

` pub first_signer: Signer<'info>,`

` pub second_signer: Signer<'info>,`

` `

`}`

The above example shows that this specific program has multiple signers,
first_signer and second_signer. We cannot necessarily tell which one is the
payer, but we know both have signed the transaction. You can learn more about
[getting signers on Rareskills](https://www.rareskills.io/post/msg-sender-
solana).

## How do I build my EVM project on Solana?

Let’s take a simple project built in Solidity and go through the process of
building the same project on Solana. A common first project you run into is a
voting project. The Solidity smart contract would look like this:

`pragma solidity ^0.6.4;`

  

`contract Voting {`

` mapping (bytes32 => uint256) public votesReceived;`

` `

` bytes32[] public candidateList;`

  

` constructor(bytes32[] memory candidateNames) public {`

` candidateList = candidateNames;`

` }`

  

` function voteForCandidate(bytes32 candidate) public {`

` require(validCandidate(candidate));`

` votesReceived[candidate] += 1;`

` }`

  

` function totalVotesFor(bytes32 candidate) view public returns (uint256) {`

` require(validCandidate(candidate));`

` return votesReceived[candidate];`

` }`

  

` function validCandidate(bytes32 candidate) view public returns (bool) {`

` for(uint i = 0; i < candidateList.length; i++) {`

` if (candidateList[i] == candidate) {`

` return true;`

` }`

` }`

` return false;`

` }`

`}`

We quickly noticed a few things that were not available in Solana programs.
View functions and `mapping` need to be done differently. Let’s start building
this program on Solana!

Let’s create our very basic Solana program shell:

`use anchor_lang::prelude::*;`

  

`declare_id!("6voY4gV7kzuGr4hE2xjZnkdagFGNhEe8WonZ8UtdPWig");`

  

`#[program]`

`pub mod voting {`

` use super::*;`

  

` pub fn init_candidate(ctx: Context<InitializeCandidate>) -> Result<()> {`

` Ok(())`

` }`

  

` pub fn vote_for_candidate(ctx: Context<VoteCandidate>) -> Result<()> {`

` Ok(())`

` }`

`}`

  

`#[derive(Accounts)]`

`pub struct InitializeCandidate{}`

  

`#[derive(Accounts)]`

`pub struct VoteCandidate{}`

We have two functions in our voting program, `init_candidate` and
`vote_for_candidate`. The `init_candidate` function maps directly to our
constructor in the Solidity smart contract, while `vote_for_candidate` maps
one-to-one with voteForCandidate in Solidity.

One problem with `init_candidate` today is that it can be called by anyone
permissionless, unlike the contructor in Solidity only being called by the
contract deployer. To solve this, we will employ a similar feature to
`onlyOwner `from Solidity. We set a specific address on the Solana program
that is the only one that can execute the instruction.

Let’s say our publicKey is `8os8PKYmeVjU1mmwHZZNTEv5hpBXi5VvEKGzykduZAik`. By
adding a reference to this publicKey in the Solana program and requiring the
signer to match, we effectively emulate both `onlyOwner` and the constructor.

`use anchor_lang::prelude::*;`

  

`declare_id!("6voY4gV7kzuGr4hE2xjZnkdagFGNhEe8WonZ8UtdPWig");`

  

`const OWNER: &str = "8os8PKYmeVjU1mmwHZZNTEv5hpBXi5VvEKGzykduZAik";`

  

`#[program]`

`pub mod voting {`

` use super::*;`

  

` #[access_control(check(&ctx))]`

` pub fn init_candidate(ctx: Context<InitializeCandidate>) -> Result<()> {`

` Ok(())`

` }`

  

` pub fn vote_for_candidate(ctx: Context<VoteCandidate>) -> Result<()> {`

` Ok(())`

` }`

`}`

  

`#[derive(Accounts)]`

`pub struct InitializeCandidate<'info> {`

` #[account(mut)]`

` pub payer: Signer<'info>,`

`}`

  

`#[derive(Accounts)]`

`pub struct VoteCandidate {}`

  

`fn check(ctx: &Context<InitializeCandidate>) -> Result<()> {`

` // Check if signer === owner`

` require_keys_eq!(`

` ctx.accounts.payer.key(),`

` OWNER.parse::<Pubkey>().unwrap(),`

` OnlyOwnerError::NotOwner`

` );`

  

` Ok(())`

`}`

  

`#[error_code]`

`pub enum OnlyOwnerError {`

` #[msg("Only owner can call this function!")]`

` NotOwner,`

`}`

We added an access control function `check` that will check if the signer of
`init_candidate` matches the address listed in the smart contract. If the
signer does not match, the `OnlyOwnerError `will be thrown, and the
transaction will fail.

Let’s move on to the next bit in the Solidity smart contract, `candidateList
`and `votesReceived`. While you can use a `Vec` in a Solana program similar to
`bytes32[]`, managing the payments for changing the size can be a bit of a
hassle. Instead, we will utilize Program Derived Addresses given specific
candidate name, with the value found at that address being the `votesReceived
`by the candidate.

To use Program Derived Accounts in a Solana Program, you use `seeds` and
`bump` in the account. First, let’s create the account to track
`votesReceived`.

`#[account]`

`#[derive(InitSpace)]`

`pub struct Candidate {`

` pub votes_received: u8,`

`}`

`#[account]` denotes the struct as a Solana account, while the
`#[derive(InitSpace)] `is a useful macro for auto-calculating the space
required to allocate for `Candidate`. The` votes_received` can hold a count
just like `votesReceived` in the Solidity smart contract.

Expanding the `InitializeCandidate` and `VoteCandidate`, we get the following:

`#[derive(Accounts)]`

`#[instruction(_candidate_Name: String)]`

`pub struct InitializeCandidate<'info> {`

` #[account(mut)]`

` pub payer: Signer<'info>,`

  

` #[account(`

` init,`

` space = 8 + Candidate::INIT_SPACE,`

` payer = payer,`

` seeds = [_candidate_Name.as_bytes().as_ref()],`

` bump,`

` )]`

` pub candidate: Account<'info, Candidate>,`

` pub system_program: Program<'info, System>,`

`}`

  

`#[derive(Accounts)]`

`#[instruction(_candidate_Name: String)]`

`pub struct VoteCandidate<'info> {`

  

` #[account(`

` mut,`

` seeds = [_candidate_Name.as_bytes().as_ref()],`

` bump,`

` )]`

` pub candidate: Account<'info, Candidate>,`

`}`

Wow, that’s a lot of new code in the accounts. Let’s unpack it.

First you’ll notice `#[instruction(_candidate_Name: String)]`. This means the
context for `InitializeCandidate` expects a string `_candidate_name` to be
passed into the instruction. We can see later this is used in `seeds =
[_candidate_name.as_bytes().as_ref()]`. This means that the seed of the PDA
will be `_candidate_Name`, and the value stored at the PDA will be the
candidate’s `votes_received`.

Next you may have some questions on `space = 8 + Candidate::INIT_SPACE`. The
`Candidate::INIT_SPACE` is how big the `Candidate` account is + `8`, `8` being
the bytes added at the beginning of Anchor framework accounts for security
checks. `pub system_program: Program<'info, System>`, is required when you’re
creating an account, which is denoted by `init`. This means that any time an
instruction using the `InitializeCandidate` context is called, the instruction
will try to create a candidate account.

Now let’s add the business logic found in `voteForCandidate` from the Solidity
smart contract.

`pub fn vote_for_candidate(ctx: Context<VoteCandidate>, _candidate_name:
String) -> Result<()> {`

` ctx.accounts.candidate.votes_received += 1;`

` Ok(())`

`}`

Here we take an additional parameter discussed earlier, `_candidate_name `.
This will help match to the exact account we’re referencing for the candidate.
We then increment the votes by 1 for that candidate.

That’s all we need to complete on the Solana program side, with the final
Solana program looking like this:

`use anchor_lang::prelude::*;`

  

`declare_id!("6voY4gV7kzuGr4hE2xjZnkdagFGNhEe8WonZ8UtdPWig");`

  

`const OWNER: &str = "8os8PKYmeVjU1mmwHZZNTEv5hpBXi5VvEKGzykduZAik";`

  

`#[program]`

`pub mod voting {`

` use super::*;`

  

` #[access_control(check(&ctx))]`

` pub fn init_candidate(ctx: Context<InitializeCandidate>, _candidate_name:
String) -> Result<()> {`

` Ok(())`

` }`

  

` pub fn vote_for_candidate(ctx: Context<VoteCandidate>, _candidate_name:
String) -> Result<()> {`

` ctx.accounts.candidate.votes_received += 1;`

` Ok(())`

` }`

`}`

  

`#[derive(Accounts)]`

`#[instruction(_candidate_name: String)]`

`pub struct InitializeCandidate<'info> {`

` #[account(mut)]`

` pub payer: Signer<'info>,`

  

` #[account(`

` init,`

` space = 8 + Candidate::INIT_SPACE,`

` payer = payer,`

` seeds = [_candidate_name.as_bytes().as_ref()],`

` bump,`

` )]`

` pub candidate: Account<'info, Candidate>,`

` pub system_program: Program<'info, System>,`

`}`

  

`#[derive(Accounts)]`

`#[instruction(_candidate_name: String)]`

`pub struct VoteCandidate<'info> {`

` #[account(`

` mut,`

` seeds = [_candidate_name.as_bytes().as_ref()],`

` bump,`

` )]`

` pub candidate: Account<'info, Candidate>,`

`}`

  

`#[account]`

`#[derive(InitSpace)]`

`pub struct Candidate {`

` pub votes_received: u8,`

`}`

  

`fn check(ctx: &Context<InitializeCandidate>) -> Result<()> {`

` // Check if signer === owner`

` require_keys_eq!(`

` ctx.accounts.payer.key(),`

` OWNER.parse::<Pubkey>().unwrap(),`

` OnlyOwnerError::NotOwner`

` );`

  

` Ok(())`

`}`

  

`#[error_code]`

`pub enum OnlyOwnerError {`

` #[msg("Only owner can call this function!")]`

` NotOwner,`

`}`

Now you might think, “But wait, what about `totalVotesFor` and
`validCandidate` from the Solidity smart contract?” `validCandidate` is
already accounted for because `vote_for_candidate` will fail if you pass an
account that does not exist. `totalVotesFor` can be done client-side with
Typescript and does not need to exist within the Solana program.

Now that we’ve built the Solana program, let’s interact with it.

Loading the program into [Solana
Playground](https://beta.solpg.io/65dc240ccffcf4b13384cf71), I can build and
deploy it to Devnet. Once you build and deploy the program, you’ll find that
you can run tests with the instructions on the test tab.

![](https://cdn.builder.io/api/v1/image/assets%2Fce0c7323a97a4d91bd0baa7490ec9139%2F0ca7cec6395f41a6b6f8314fd3c3c1e9?width=500)

This is akin to using Remix to test your Solidity smart contract. Opening up
`initCandidate` and entering the name `John Smith` as the candidate name, we
now have to generate the PDA for `John Smith`. Click on the candidate account
finder and select `From seed`. Select the custom String and input `John
Smith`, and finally click `generate`. Congratulations, you just found your PDA
for `John Smith`! Now hit `Test` to execute the instruction.

If all is successful, you should see the following program logs on the test
transaction.

![](https://cdn.builder.io/api/v1/image/assets%2Fce0c7323a97a4d91bd0baa7490ec9139%2F7f382a94721e484aa57ae08c2f4391b9?width=700)

Now let’s vote for `John Smith `! Opening up the `voteForCandidate`
instruction, type in `John Smith` and generate the same PDA again. Hit `Test`
to vote for your first candidate!

![](https://cdn.builder.io/api/v1/image/assets%2Fce0c7323a97a4d91bd0baa7490ec9139%2F914ca3ebc38945be808993711af801e6?width=700)

Now that you’ve voted, how can you check how many votes the candidate has?
Head on over to `Candidate` under `Accounts` on the test tab and hit the
button `Fetch All`. This will grab all valid candidates and their votes. From
there you’ll receive an array of the candidates, their account addresses, and
their votes.

![](https://cdn.builder.io/api/v1/image/assets%2Fce0c7323a97a4d91bd0baa7490ec9139%2F4930bf05e3e9451b93bd895750065759?width=500)

Congratulations! You just took the voting Solidity smart contract and
translated into a Solana program. You can use a lot of the same techniques on
other Solidity smart contracts to build what you have on EVM on Solana. If
you’re interested to learn more about Solana, [check out the
documentation](/docs) and get started today.

EVM TO SVM

[Home](/developers/evm-to-svm)[Next: Consensus](/developers/evm-to-
svm/consensus)

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

