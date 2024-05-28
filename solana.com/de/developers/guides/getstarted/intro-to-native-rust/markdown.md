This website uses cookies to offer you a better browsing experience. Find out
more on how we use cookies.

Opt-out[Details](/de/privacy-policy#collection-of-information)

Accept

[![Solana](/_next/static/media/logotype-dark.f79d530d.svg)](/de)

  * Learn
  * Developers
  * Solutions
  * Network
  * Community

Search```K`

[Documentation](/de/docs)[RPC
API](/de/docs/rpc)[Cookbook](/de/developers/cookbook)[Guides](/de/developers/guides)[Terminology](/de/docs/terminology)

[Home](/de)>[Developers](/de/developers)>[Guides](/de/developers/guides)

# [How to write a Native Rust Program](/de/developers/guides/getstarted/intro-
to-native-rust)

updated 24\. April 2024

[beginner](/de/developers/guides?difficulty=beginner)[rust](/de/developers/guides?tags=rust)

[![How to write a Native Rust
Program](https://solana.com/_next/image?url=%2Fopengraph%2Fdevelopers%2Fguides%2Fgetstarted%2Fintro-
to-native-rust&w=3840&q=75)](/de/developers/guides/getstarted/intro-to-native-
rust)

To write Solana programs without leveraging the Anchor framework, we use the
[`solana_program`](https://docs.rs/solana-program/latest/solana_program/)
crate. This is the base library for writing on-chain programs in Rust.

For beginners, it is recommended to start with the [Anchor
framework](/de/developers/guides/getstarted/intro-to-anchor).

## Program #

Below is a simple Solana program with a single instruction that creates a new
account. We'll walk through it to explain the basic structure of a Solana
program. Here is the program on [Solana
Playground](https://beta.solpg.io/661058a6cffcf4b13384d02a).

lib.rs

    
    
    use borsh::{BorshDeserialize, BorshSerialize};
    use solana_program::{
        account_info::{next_account_info, AccountInfo},
        entrypoint,
        entrypoint::ProgramResult,
        msg,
        program::invoke,
        pubkey::Pubkey,
        rent::Rent,
        system_instruction::create_account,
        sysvar::Sysvar,
    };
     
    entrypoint!(process_instruction);
     
    pub fn process_instruction(
        program_id: &Pubkey,
        accounts: &[AccountInfo],
        instruction_data: &[u8],
    ) -> ProgramResult {
        let instruction = Instructions::try_from_slice(instruction_data)?;
        match instruction {
            Instructions::Initialize { data } => process_initialize(program_id, accounts, data),
        }
    }
     
    pub fn process_initialize(
        program_id: &Pubkey,
        accounts: &[AccountInfo],
        data: u64,
    ) -> ProgramResult {
        let accounts_iter = &mut accounts.iter();
     
        let new_account = next_account_info(accounts_iter)?;
        let signer = next_account_info(accounts_iter)?;
        let system_program = next_account_info(accounts_iter)?;
     
        let account_data = NewAccount { data };
        let size = account_data.try_to_vec()?.len();
        let lamports = (Rent::get()?).minimum_balance(size);
     
        invoke(
            &create_account(
                signer.key,
                new_account.key,
                lamports,
                size as u64,
                program_id,
            ),
            &[signer.clone(), new_account.clone(), system_program.clone()],
        )?;
     
        account_data.serialize(&mut *new_account.data.borrow_mut())?;
        msg!("Changed data to: {:?}!", data);
        Ok(())
    }
     
    #[derive(BorshSerialize, BorshDeserialize)]
    pub enum Instructions {
        Initialize { data: u64 },
    }
     
    #[derive(BorshSerialize, BorshDeserialize, Debug)]
    pub struct NewAccount {
        pub data: u64,
    }
     

### Entrypoint #

Every Solana program includes a single [entrypoint](https://github.com/solana-
labs/solana/blob/27eff8408b7223bb3c4ab70523f8a8dca3ca6645/sdk/program/src/entrypoint.rs#L125)
used to invoke the program. The
[`process_instruction`](https://github.com/solana-
labs/solana/blob/27eff8408b7223bb3c4ab70523f8a8dca3ca6645/sdk/program/src/entrypoint.rs#L28-L29)
function is then used to process the data passed into the entrypoint. This
function requires the following parameters:

  * `program_id` \- Address of the currently executing program
  * `accounts` \- Array of accounts needed to execute an instruction.
  * `instruction_data` \- Serialized data specific to an instruction.

    
    
    entrypoint!(process_instruction);
     
    pub fn process_instruction(
        program_id: &Pubkey,
        accounts: &[AccountInfo],
        instruction_data: &[u8],
    ) -> ProgramResult {
        ...
    }

These parameters correspond to the details required for every
[instruction](/de/docs/core/transactions#instruction) on a transaction.

### Instructions #

While there is only one entrypoint, program execution can follow different
paths depending on the `instruction_data`. It is common to define instructions
as variants within an [enum](https://doc.rust-lang.org/book/ch06-01-defining-
an-enum.html), where each variant represents a distinct instruction on the
program.

    
    
    #[derive(BorshSerialize, BorshDeserialize)]
    pub enum Instructions {
        Initialize { data: u64 },
    }

The `instruction_data` passed into the entrypoint is deserialized to determine
its corresponding enum variant.

    
    
    pub fn process_instruction(
        program_id: &Pubkey,
        accounts: &[AccountInfo],
        instruction_data: &[u8],
    ) -> ProgramResult {
        let instruction = Instructions::try_from_slice(instruction_data)?;
        match instruction {
            Instructions::Initialize { data } => process_initialize(program_id, accounts, data),
        }
    }

A [match](https://doc.rust-lang.org/book/ch06-02-match.html) statement is then
used to invoke the function including the logic to process the identified
instruction. These functions are often called [instruction
handlers](/de/docs/terminology#instruction-handler).

    
    
    pub fn process_instruction(
        program_id: &Pubkey,
        accounts: &[AccountInfo],
        instruction_data: &[u8],
    ) -> ProgramResult {
        let instruction = Instructions::try_from_slice(instruction_data)?;
        match instruction {
            Instructions::Initialize { data } => process_initialize(program_id, accounts, data),
        }
    }
     
    pub fn process_initialize(
        program_id: &Pubkey,
        accounts: &[AccountInfo],
        data: u64,
    ) -> ProgramResult {
        ...
        Ok(())
    }

### Process Instruction #

For every instruction on a program, there exists a specific instruction
handler function that implements the logic required to execute that
instruction.

    
    
    pub fn process_initialize(
        program_id: &Pubkey,
        accounts: &[AccountInfo],
        data: u64,
    ) -> ProgramResult {
        let accounts_iter = &mut accounts.iter();
     
        let new_account = next_account_info(accounts_iter)?;
        let signer = next_account_info(accounts_iter)?;
        let system_program = next_account_info(accounts_iter)?;
     
        let account_data = NewAccount { data };
        let size = account_data.try_to_vec()?.len();
        let lamports = (Rent::get()?).minimum_balance(size);
     
        invoke(
            &create_account(
                signer.key,
                new_account.key,
                lamports,
                size as u64,
                program_id,
            ),
            &[signer.clone(), new_account.clone(), system_program.clone()],
        )?;
     
        account_data.serialize(&mut *new_account.data.borrow_mut())?;
        msg!("Changed data to: {:?}!", data);
        Ok(())
    }

To access the accounts provided to the program, use an
[iterator](https://doc.rust-lang.org/book/ch13-02-iterators.html) to iterate
over the list of accounts passed into the entrypoint through the `accounts`
argument. The [`next_account_info`](https://github.com/solana-
labs/solana/blob/27eff8408b7223bb3c4ab70523f8a8dca3ca6645/sdk/program/src/account_info.rs#L326)
function is used to access the next item in the iterator.

    
    
    let accounts_iter = &mut accounts.iter();
     
    let new_account = next_account_info(accounts_iter)?;
    let signer = next_account_info(accounts_iter)?;
    let system_program = next_account_info(accounts_iter)?;

Creating a new account requires invoking the
[`create_account`](https://github.com/solana-
labs/solana/blob/27eff8408b7223bb3c4ab70523f8a8dca3ca6645/programs/system/src/system_processor.rs#L145)
instruction on the [System Program](/de/docs/core/accounts#system-program).
When the System Program creates a new account, it can reassign the program
owner of the new account.

In this example, we use a [Cross Program Invocation](/de/docs/core/cpi) to
invoke the System Program, creating a new account with the executing program
as the `owner`. As part of the [Solana Account
Model](/de/docs/core/accounts#accountinfo), only the program designated as the
`owner` of an account is allowed to modify the data on the account.

    
    
    let account_data = NewAccount { data };
    let size = account_data.try_to_vec()?.len();
    let lamports = (Rent::get()?).minimum_balance(size);
     
    invoke(
        &create_account(
            signer.key,      // payer
            new_account.key, // new account address
            lamports,        // rent
            size as u64,     // space
            program_id,      // program owner address
        ),
        &[signer.clone(), new_account.clone(), system_program.clone()],
    )?;

After the account has been successfully created, the final step is to
serialize data into the new account's `data` field. This effectively
initializes the account data, storing the `data` passed into the program
entrypoint.

    
    
    account_data.serialize(&mut *new_account.data.borrow_mut())?;

### State #

Structs are used to define the format of a custom data account type for a
program. Serialization and deserialization of account data is commonly done
using [Borsh](https://borsh.io/).

In this example, the `NewAccount` struct defines the structure of the data to
store in a new account.

    
    
    #[derive(BorshSerialize, BorshDeserialize, Debug)]
    pub struct NewAccount {
        pub data: u64,
    }

All Solana accounts include a [`data`](/de/docs/core/accounts#accountinfo)
field that can be used to store any arbitrary data as a byte array. This
flexibility enables programs to create and store customized data structures
within new accounts.

In the `process_initialize` function, the data passed into the entrypoint is
used to create an instance of the `NewAccount` struct. This instance is
serialized and stored in the data field of the newly created account.

    
    
    pub fn process_initialize(
        program_id: &Pubkey,
        accounts: &[AccountInfo],
        data: u64,
    ) -> ProgramResult {
     
        let account_data = NewAccount { data };
     
        invoke(
            ...
        )?;
     
        account_data.serialize(&mut *new_account.data.borrow_mut())?;
        msg!("Changed data to: {:?}!", data);
        Ok(())
    }
    ...
     
    #[derive(BorshSerialize, BorshDeserialize, Debug)]
    pub struct NewAccount {
        pub data: u64,
    }

## Client #

Interacting with Solana programs written in native Rust involves directly
building the [`TransactionInstruction`](https://solana-labs.github.io/solana-
web3.js/classes/TransactionInstruction.html).

Similarly, fetching and deserializing account data requires creating a schema
compatible with the on-chain program's data structures.

Info

There are multiple client languages supported. You can find details for
[Rust](/de/docs/clients/rust) and
[Javascript/Typescript](/de/docs/clients/rust) under the Solana Clients of the
documentation.

Below, we'll walk through an example demonstrating how to invoke the
`initialize` instruction from the program above.

native.test.ts

    
    
    describe("Test", () => {
      it("Initialize", async () => {
        // Generate keypair for the new account
        const newAccountKp = new web3.Keypair();
     
        const instructionIndex = 0;
        const data = 42;
     
        // Create instruction data buffer
        const instructionData = Buffer.alloc(1 + 8);
        instructionData.writeUInt8(instructionIndex, 0);
        instructionData.writeBigUInt64LE(BigInt(data), 1);
     
        const instruction = new web3.TransactionInstruction({
          keys: [
            {
              pubkey: newAccountKp.publicKey,
              isSigner: true,
              isWritable: true,
            },
            {
              pubkey: pg.wallet.publicKey,
              isSigner: true,
              isWritable: true,
            },
            {
              pubkey: web3.SystemProgram.programId,
              isSigner: false,
              isWritable: false,
            },
          ],
          programId: pg.PROGRAM_ID,
          data: instructionData,
        });
     
        const transaction = new web3.Transaction().add(instruction);
     
        const txHash = await web3.sendAndConfirmTransaction(
          pg.connection,
          transaction,
          [pg.wallet.keypair, newAccountKp],
        );
        console.log(`Use 'solana confirm -v ${txHash}' to see the logs`);
     
        // Fetch Account
        const newAccount = await pg.connection.getAccountInfo(
          newAccountKp.publicKey,
        );
     
        // Deserialize Account Data
        const deserializedAccountData = borsh.deserialize(
          AccountDataSchema,
          AccountData,
          newAccount.data,
        );
     
        console.log(Number(deserializedAccountData.data));
      });
    });
     
    class AccountData {
      data = 0;
      constructor(fields: { data: number }) {
        if (fields) {
          this.data = fields.data;
        }
      }
    }
     
    const AccountDataSchema = new Map([
      [AccountData, { kind: "struct", fields: [["data", "u64"]] }],
    ]);

### Invoke Instructions #

To invoke an instruction, you must manually construct a
`TransactionInstruction` that corresponds with the on-chain program. This
involves specifying:

  * The program ID for the program being invoked
  * The `AccountMeta` for each account required by the instruction
  * The instruction data buffer required by the instruction

    
    
    // Generate keypair for the new account
    const newAccountKp = new web3.Keypair();
     
    const instructionIndex = 0;
    const data = 42;
     
    // Create instruction data buffer
    const instructionData = Buffer.alloc(1 + 8);
    instructionData.writeUInt8(instructionIndex, 0);
    instructionData.writeBigUInt64LE(BigInt(data), 1);
     
    const instruction = new web3.TransactionInstruction({
      keys: [
        {
          pubkey: newAccountKp.publicKey,
          isSigner: true,
          isWritable: true,
        },
        {
          pubkey: pg.wallet.publicKey,
          isSigner: true,
          isWritable: true,
        },
        {
          pubkey: web3.SystemProgram.programId,
          isSigner: false,
          isWritable: false,
        },
      ],
      programId: pg.PROGRAM_ID,
      data: instructionData,
    });

First, create a new keypair. The publickey from this keypair will be used as
the address for the new account created by the `initialize` instruction.

    
    
    // Generate keypair for the new account
    const newAccountKp = new web3.Keypair();

Before building the instruction, prepare the instruction data buffer that the
instruction expects. In this example, the buffer's first byte identifies the
instruction to invoke on the program. The additional 8 bytes are allocated for
the `u64` type data, which is required by the `initialize` instruction.

    
    
    const instructionIndex = 0;
    const data = 42;
     
    // Create instruction data buffer
    const instructionData = Buffer.alloc(1 + 8);
    instructionData.writeUInt8(instructionIndex, 0);
    instructionData.writeBigUInt64LE(BigInt(data), 1);

After creating the instruction data buffer, use it to construct the
`TransactionInstruction`. This involves specifying the program ID and defining
the [`AccountMeta`](/de/docs/core/transactions#accountmeta) for each account
involved in the instruction. This means specifying whether each account is
writable and if it is required as a signer on the transaction.

    
    
    const instruction = new web3.TransactionInstruction({
      keys: [
        {
          pubkey: newAccountKp.publicKey,
          isSigner: true,
          isWritable: true,
        },
        {
          pubkey: pg.wallet.publicKey,
          isSigner: true,
          isWritable: true,
        },
        {
          pubkey: web3.SystemProgram.programId,
          isSigner: false,
          isWritable: false,
        },
      ],
      programId: pg.PROGRAM_ID,
      data: instructionData,
    });

Finally, add the instruction to a new transaction and send it to be processed
by the network.

    
    
    const transaction = new web3.Transaction().add(instruction);
     
    const txHash = await web3.sendAndConfirmTransaction(
      pg.connection,
      transaction,
      [pg.wallet.keypair, newAccountKp],
    );
    console.log(`Use 'solana confirm -v ${txHash}' to see the logs`);

### Fetch Accounts #

To fetch and deserialize the account data, you need to first create a scheme
to match the expected on-chain account data.

    
    
    class AccountData {
      data = 0;
      constructor(fields: { data: number }) {
        if (fields) {
          this.data = fields.data;
        }
      }
    }
     
    const AccountDataSchema = new Map([
      [AccountData, { kind: "struct", fields: [["data", "u64"]] }],
    ]);

Then fetch the `AccountInfo` for the account using its address.

    
    
    const newAccount = await pg.connection.getAccountInfo(newAccountKp.publicKey);

Lastly, deserialize the `AccountInfo`'s `data` field using the predefined
schema.

    
    
    const deserializedAccountData = borsh.deserialize(
      AccountDataSchema,
      AccountData,
      newAccount.data,
    );
     
    console.log(Number(deserializedAccountData.data));

[Previous« Getting Started with the Anchor
Framework](/de/developers/guides/getstarted/intro-to-anchor)[NextSetup, build,
and deploy a Solana program locally in Rust
»](/de/developers/guides/getstarted/local-rust-hello-world)

##### Table of Contents

  * [Program](/de/developers/guides/getstarted/intro-to-native-rust#program)
  * [Entrypoint](/de/developers/guides/getstarted/intro-to-native-rust#entrypoint)
  * [Instructions](/de/developers/guides/getstarted/intro-to-native-rust#instructions)
  * [Process Instruction](/de/developers/guides/getstarted/intro-to-native-rust#process-instruction)
  * [State](/de/developers/guides/getstarted/intro-to-native-rust#state)
  * [Client](/de/developers/guides/getstarted/intro-to-native-rust#client)
  * [Invoke Instructions](/de/developers/guides/getstarted/intro-to-native-rust#invoke-instructions)
  * [Fetch Accounts](/de/developers/guides/getstarted/intro-to-native-rust#fetch-accounts)

[Scroll to Top](/de/developers/guides/getstarted/intro-to-native-rust#)

[Edit Page](https://github.com/solana-foundation/developer-
content/tree/main/content/guides/getstarted/intro-to-native-rust.md)

Managed by

[](/de)

[](/youtube)[](/twitter)[](/discord)[](/reddit)[](/github)[](/telegram)

© 2024 Solana Foundation. All rights reserved.

Solana

  * [Fördermittel](https://solana.org/grants)
  * [Break Solana](https://break.solana.com/)
  * [Media Kit](/de/branding)
  * [Karriere](https://jobs.solana.com/)
  * [Haftungsausschluss](/de/tos)
  * [Privacy Policy](/de/privacy-policy)

Get Connected

  * [Ökosystem](/de/ecosystem)
  * [Blog](/de/news)
  * [Newsletter](/de/newsletter)

de

© 2024 Solana Foundation. All rights reserved.

