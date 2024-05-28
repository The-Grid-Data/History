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

  * [Key Points](/vi/docs/core/transactions#key-points)
  * [Basic Example](/vi/docs/core/transactions#basic-example)
  * [Simple SOL Transfer](/vi/docs/core/transactions#simple-sol-transfer)
  * [Transaction](/vi/docs/core/transactions#transaction)
  * [Transaction Size](/vi/docs/core/transactions#transaction-size)
  * [Message Header](/vi/docs/core/transactions#message-header)
  * [Compact-Array Format](/vi/docs/core/transactions#compact-array-format)
  * [Array of Account Addresses](/vi/docs/core/transactions#array-of-account-addresses)
  * [Recent Blockhash](/vi/docs/core/transactions#recent-blockhash)
  * [Array of Instructions](/vi/docs/core/transactions#array-of-instructions)
  * [Example Transaction Structure](/vi/docs/core/transactions#example-transaction-structure)
  * [Instruction](/vi/docs/core/transactions#instruction)
  * [AccountMeta](/vi/docs/core/transactions#accountmeta)
  * [Example Instruction Structure](/vi/docs/core/transactions#example-instruction-structure)
  * [Expanded Example](/vi/docs/core/transactions#expanded-example)
  * [Manual SOL Transfer](/vi/docs/core/transactions#manual-sol-transfer)

[Scroll to Top](/vi/docs/core/transactions#)

[Edit Page](https://github.com/solana-foundation/developer-
content/tree/main/docs/core/transactions.md)

[Home](/vi)>[Solana Documentation](/vi/docs)>Core Concepts

# [Transactions and Instructions](/vi/docs/core/transactions)

On Solana, we send [transactions](/vi/docs/core/transactions#transaction) to
interactions with the network. Transactions include one or more
[instructions](/vi/docs/core/transactions#instruction), each representing a
specific operation to be processed. The execution logic for instructions is
stored on [programs](/vi/docs/core/programs) deployed to the Solana network,
where each program stores its own set of instructions.

Below are key details about how transactions are executed:

  * Execution Order: If a transaction includes multiple instructions, the instructions are processed in the order they are added to the transaction.
  * Atomicity: A transaction is atomic, meaning it either fully completes with all instructions successfully processed, or fails altogether. If any instruction within the transaction fails, none of the instructions are executed.

For simplicity, a transaction can be thought of as a request to process one or
multiple instructions.

![Transaction Simplified](https://solana-developer-
content.vercel.app/assets/docs/core/transactions/transaction-
simple.svg)Transaction Simplified

You can imagine a transaction as an envelope, where each instruction is a
document that you fill out and place inside the envelope. We then mail out the
envelope to process the documents, just like sending a transaction on the
network to process our instructions.

## Key Points #

  * Solana transactions consist of instructions that interact with various programs on the network, where each instruction represents a specific operation.

  * Each instruction specifies the program to execute the instruction, the accounts required by the instruction, and the data required for the instruction's execution.

  * Instructions within a transaction are processed in the order they are listed.

  * Transactions are atomic, meaning either all instructions process successfully, or the entire transaction fails.

  * The maximum size of a transaction is 1232 bytes.

## Basic Example #

Below is a diagram representing a transaction with a single instruction to
transfer SOL from a sender to a receiver.

Individual "wallets" on Solana are accounts owned by the [System
Program](/vi/docs/core/accounts#system-program). As part of the [Solana
Account Model](/vi/docs/core/accounts), only the program that owns an account
is allowed to modify the data on the account.

Therefore, transferring SOL from a "wallet" account requires sending a
transaction to invoke the transfer instruction on the System Program.

![SOL Transfer](https://solana-developer-
content.vercel.app/assets/docs/core/transactions/sol-transfer.svg)SOL Transfer

The sender account must be included as a signer (`is_signer`) on the
transaction to approve the deduction of their lamport balance. Both the sender
and recipient accounts must be mutable (`is_writable`) because the instruction
modifies the lamport balance for both accounts.

Once the transaction is sent, the System Program is invoked to process the
transfer instruction. The System Program then updates the lamport balances of
both the sender and recipient accounts accordingly.

![SOL Transfer Process](https://solana-developer-
content.vercel.app/assets/docs/core/transactions/sol-transfer-process.svg)SOL
Transfer Process

### Simple SOL Transfer #

Here is a [Solana Playground](https://beta.solpg.io/656a0ea7fb53fa325bfd0c3e)
example of how to build a SOL transfer instruction using the
`SystemProgram.transfer` method:

    
    
    // Define the amount to transfer
    const transferAmount = 0.01; // 0.01 SOL
     
    // Create a transfer instruction for transferring SOL from wallet_1 to wallet_2
    const transferInstruction = SystemProgram.transfer({
      fromPubkey: sender.publicKey,
      toPubkey: receiver.publicKey,
      lamports: transferAmount * LAMPORTS_PER_SOL, // Convert transferAmount to lamports
    });
     
    // Add the transfer instruction to a new transaction
    const transaction = new Transaction().add(transferInstruction);

Run the script and inspect the transaction details logged to the console. In
the sections below, we'll walk through the details of what's happening under
the hood.

## Transaction #

A Solana [transaction](https://github.com/solana-
labs/solana/blob/27eff8408b7223bb3c4ab70523f8a8dca3ca6645/sdk/src/transaction/mod.rs#L173)
consists of:

  1. [Signatures](https://github.com/solana-labs/solana/blob/27eff8408b7223bb3c4ab70523f8a8dca3ca6645/sdk/src/signature.rs#L27): An array of signatures included on the transaction.
  2. [Message](https://github.com/solana-labs/solana/blob/27eff8408b7223bb3c4ab70523f8a8dca3ca6645/sdk/program/src/message/legacy.rs#L110): List of instructions to be processed atomically.

![Transaction Format](https://solana-developer-
content.vercel.app/assets/docs/core/transactions/tx_format.png)Transaction
Format

The structure of a transaction message comprises of:

  * [Message Header](/vi/docs/core/transactions#message-header): Specifies the number of signer and read-only account.
  * [Account Addresses](/vi/docs/core/transactions#array-of-account-addresses): An array of account addresses required by the instructions on the transaction.
  * [Recent Blockhash](/vi/docs/core/transactions#recent-blockhash): Acts as a timestamp for the transaction.
  * [Instructions](/vi/docs/core/transactions#array-of-instructions): An array of instructions to be executed.

![Transaction Message](https://solana-developer-
content.vercel.app/assets/docs/core/transactions/legacy_message.png)Transaction
Message

### Transaction Size #

The Solana network adheres to a maximum transmission unit (MTU) size of 1280
bytes, consistent with the [IPv6
MTU](https://en.wikipedia.org/wiki/IPv6_packet) size constraints to ensure
fast and reliable transmission of cluster information over UDP. After
accounting for the necessary headers (40 bytes for IPv6 and 8 bytes for the
fragment header), [1232 bytes remain available for packet
data](https://github.com/solana-
labs/solana/blob/27eff8408b7223bb3c4ab70523f8a8dca3ca6645/sdk/src/packet.rs#L16-L21),
such as serialized transactions.

This means that the total size of a Solana transaction is limited to 1232
bytes. The combination of the signatures and the message cannot exceed this
limit.

  * Signatures: Each signature requires 64 bytes. The number of signatures can vary, depending on the transaction's requirements.
  * Message: The message includes instructions, accounts, and additional metadata, with each account requiring 32 bytes. The combined size of the accounts plus metadata can vary, depending on the instructions included in the transaction.

![Transaction Format](https://solana-developer-
content.vercel.app/assets/docs/core/transactions/issues_with_legacy_txs.png)Transaction
Format

### Message Header #

The [message header](https://github.com/solana-
labs/solana/blob/27eff8408b7223bb3c4ab70523f8a8dca3ca6645/sdk/program/src/message/mod.rs#L96)
specifies the privileges of accounts included in the transaction's account
address array. It is comprised of three bytes, each containing a u8 integer,
which collectively specify:

  1. The number of required signatures for the transaction.
  2. The number of read-only account addresses that require signatures.
  3. The number of read-only account addresses that do not require signatures.

![Message Header](https://solana-developer-
content.vercel.app/assets/docs/core/transactions/message_header.png)Message
Header

### Compact-Array Format #

A compact array in the context of a transaction message refers to an array
serialized in the following format:

  1. The length of the array, encoded as [compact-u16](https://github.com/solana-labs/solana/blob/27eff8408b7223bb3c4ab70523f8a8dca3ca6645/sdk/program/src/short_vec.rs).
  2. The individual items of the array listed sequentially after the encoded length.

![Compact array format](https://solana-developer-
content.vercel.app/assets/docs/core/transactions/compact_array_format.png)Compact
array format

This encoding method is used to specify the lengths of both the [Account
Addresses](/vi/docs/core/transactions#array-of-account-addresses) and
[Instructions](/vi/docs/core/transactions#array-of-instructions) arrays within
a transaction message.

### Array of Account Addresses #

A transaction message includes an array containing all the [account
addresses](https://github.com/solana-
labs/solana/blob/27eff8408b7223bb3c4ab70523f8a8dca3ca6645/sdk/program/src/message/legacy.rs#L119)
needed for the instructions within the transaction.

This array starts with a [compact-u16](/vi/docs/core/transactions#compact-
array-format) encoding of the number of account addresses, followed by the
addresses ordered by the privileges for the accounts. The metadata in the
message header is used to determine the number of accounts in each section.

  * Accounts that are writable and signers
  * Accounts that are read-only and signers
  * Accounts that are writable and not signers
  * Accounts that are read-only and not signers

![Compact array of account addresses](https://solana-developer-
content.vercel.app/assets/docs/core/transactions/compat_array_of_account_addresses.png)Compact
array of account addresses

### Recent Blockhash #

All transactions include a [recent blockhash](https://github.com/solana-
labs/solana/blob/27eff8408b7223bb3c4ab70523f8a8dca3ca6645/sdk/program/src/message/legacy.rs#L122)
to act as a timestamp for the transaction. The blockhash is used to prevent
duplications and eliminate stale transactions.

The maximum age of a transaction's blockhash is 150 blocks (~1 minute assuming
400ms block times). If a transaction's blockhash is 150 blocks older than the
latest blockhash, it is considered expired. This means that transactions not
processed within a specific timeframe will never be executed.

You can use the [`getLatestBlockhash`](/vi/docs/rpc/http/getlatestblockhash)
RPC method to get the current blockhash and last block height at which the
blockhash will be valid. Here is an example on [Solana
Playground](https://beta.solpg.io/661a06e1cffcf4b13384d046).

### Array of Instructions #

A transaction message includes an array of all
[instructions](https://github.com/solana-
labs/solana/blob/27eff8408b7223bb3c4ab70523f8a8dca3ca6645/sdk/program/src/message/legacy.rs#L128)
requesting to be processed. Instructions within a transaction message are in
the format of [CompiledInstruction](https://github.com/solana-
labs/solana/blob/27eff8408b7223bb3c4ab70523f8a8dca3ca6645/sdk/program/src/instruction.rs#L633).

Much like the array of account addresses, this compact array starts with a
[compact-u16](/vi/docs/core/transactions#compact-array-format) encoding of the
number of instructions, followed by an array of instructions. Each instruction
in the array specifies the following information:

  1. **Program ID** : Identifies an on-chain program that will process the instruction. This is represented as an u8 index pointing to an account address within the account addresses array.
  2. **Compact array of account address indexes** : Array of u8 indexes pointing to the account addresses array for each account required by the instruction.
  3. **Compact array of opaque u8 data** : A u8 byte array specific to the program invoked. This data specifies the instruction to invoke on the program along with any additional data that the instruction requires (such as function arguments).

![Compact array of Instructions](https://solana-developer-
content.vercel.app/assets/docs/core/transactions/compact_array_of_ixs.png)Compact
array of Instructions

### Example Transaction Structure #

Below is an example of the structure of a transaction including a single [SOL
transfer](/vi/docs/core/transactions#basic-example) instruction. It shows the
message details including the header, account keys, blockhash, and the
instructions, along with the signature for the transaction.

  * `header`: Includes data used to specify the read/write and signer privileges in the `accountKeys` array.

  * `accountKeys`: Array including account addresses for all instructions on the transaction.

  * `recentBlockhash`: The blockhash included on the transaction when the transaction was created.

  * `instructions`: Array including all the instructions on the transaction. Each `account` and `programIdIndex` in an instruction references the `accountKeys` array by index.

  * `signatures`: Array including signatures for all accounts required as signers by the instructions on the transaction. A signature is created by signing the transaction message using the corresponding private key for an account.

    
    
    "transaction": {
        "message": {
          "header": {
            "numReadonlySignedAccounts": 0,
            "numReadonlyUnsignedAccounts": 1,
            "numRequiredSignatures": 1
          },
          "accountKeys": [
            "3z9vL1zjN6qyAFHhHQdWYRTFAcy69pJydkZmSFBKHg1R",
            "5snoUseZG8s8CDFHrXY2ZHaCrJYsW457piktDmhyb5Jd",
            "11111111111111111111111111111111"
          ],
          "recentBlockhash": "DzfXchZJoLMG3cNftcf2sw7qatkkuwQf4xH15N5wkKAb",
          "instructions": [
            {
              "accounts": [
                0,
                1
              ],
              "data": "3Bxs4NN8M2Yn4TLb",
              "programIdIndex": 2,
              "stackHeight": null
            }
          ],
          "indexToProgramIds": {}
        },
        "signatures": [
          "5LrcE2f6uvydKRquEJ8xp19heGxSvqsVbcqUeFoiWbXe8JNip7ftPQNTAVPyTK7ijVdpkzmKKaAQR7MWMmujAhXD"
        ]
      }

## Instruction #

An [instruction](https://github.com/solana-
labs/solana/blob/27eff8408b7223bb3c4ab70523f8a8dca3ca6645/sdk/program/src/instruction.rs#L329)
is a request to process a specific action on-chain and is the smallest
contiguous unit of execution logic in a
[program](/vi/docs/core/accounts#program-account).

When building an instruction to add to a transaction, each instruction must
include the following information:

  * **Program address** : Specifies the program being invoked.
  * **Accounts** : Lists every account the instruction reads from or writes to, including other programs, using the `AccountMeta` struct.
  * **Instruction Data** : A byte array that specifies which [instruction handler](/vi/docs/terminology#instruction-handler) on the program to invoke, plus any additional data required by the instruction handler (function arguments).

![Transaction Instruction](https://solana-developer-
content.vercel.app/assets/docs/core/transactions/instruction.svg)Transaction
Instruction

### AccountMeta #

For every account required by an instruction, the following info must be
specified:

  * `pubkey`: The on-chain address of an account
  * `is_signer`: Specify if the account is required as a signer on the transaction
  * `is_writable`: Specify if the account data will be modified

This information is referred to as the
[AccountMeta](https://github.com/solana-
labs/solana/blob/27eff8408b7223bb3c4ab70523f8a8dca3ca6645/sdk/program/src/instruction.rs#L539).

![AccountMeta](https://solana-developer-
content.vercel.app/assets/docs/core/transactions/accountmeta.svg)AccountMeta

By specifying all accounts required by an instruction, and whether each
account is writable, transactions can be processed in parallel.

For example, two transactions that do not include any accounts that write to
the same state can be executed at the same time.

### Example Instruction Structure #

Below is an example of the structure of a [SOL
transfer](/vi/docs/core/transactions#basic-examples) instruction which details
the account keys, program ID, and data required by the instruction.

  * `keys`: Includes the `AccountMeta` for each account required by an instruction.
  * `programId`: The address of the program which contains the execution logic for the instruction invoked.
  * `data`: The instruction data for the instruction as a buffer of bytes

    
    
    {
      "keys": [
        {
          "pubkey": "3z9vL1zjN6qyAFHhHQdWYRTFAcy69pJydkZmSFBKHg1R",
          "isSigner": true,
          "isWritable": true
        },
        {
          "pubkey": "BpvxsLYKQZTH42jjtWHZpsVSa7s6JVwLKwBptPSHXuZc",
          "isSigner": false,
          "isWritable": true
        }
      ],
      "programId": "11111111111111111111111111111111",
      "data": [2,0,0,0,128,150,152,0,0,0,0,0]
    }

## Expanded Example #

The details for building program instructions are often abstracted away by
client libraries. However, if one is not available, you can always fall back
to manually building the instruction.

### Manual SOL Transfer #

Here is a [Solana Playground](https://beta.solpg.io/656a102efb53fa325bfd0c3f)
example of how to manually build the a SOL transfer instruction:

    
    
    // Define the amount to transfer
    const transferAmount = 0.01; // 0.01 SOL
     
    // Instruction index for the SystemProgram transfer instruction
    const transferInstructionIndex = 2;
     
    // Create a buffer for the data to be passed to the transfer instruction
    const instructionData = Buffer.alloc(4 + 8); // uint32 + uint64
    // Write the instruction index to the buffer
    instructionData.writeUInt32LE(transferInstructionIndex, 0);
    // Write the transfer amount to the buffer
    instructionData.writeBigUInt64LE(BigInt(transferAmount * LAMPORTS_PER_SOL), 4);
     
    // Manually create a transfer instruction for transferring SOL from sender to receiver
    const transferInstruction = new TransactionInstruction({
      keys: [
        { pubkey: sender.publicKey, isSigner: true, isWritable: true },
        { pubkey: receiver.publicKey, isSigner: false, isWritable: true },
      ],
      programId: SystemProgram.programId,
      data: instructionData,
    });
     
    // Add the transfer instruction to a new transaction
    const transaction = new Transaction().add(transferInstruction);

Under the hood, the [simple example](/vi/docs/core/transactions#simple-sol-
transfer) using the `SystemProgram.transfer` method is functionally equivalent
to the more verbose example above. The `SystemProgram.transfer` method simply
abstracts away the details of creating the instruction data buffer and
`AccountMeta` for each account required by the instruction.

[Previous« Solana Account Model](/vi/docs/core/accounts)[NextFees on Solana
»](/vi/docs/core/fees)

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
