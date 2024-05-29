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

# [How to use the Required Memo token extension](/ru/developers/guides/token-
extensions/required-memo)

updated 7 декабря 2023 г.

[beginner](/ru/developers/guides?difficulty=beginner)[token
2022](/ru/developers/guides?tags=token%202022)[token
extensions](/ru/developers/guides?tags=token%20extensions)

[![How to use the Required Memo token
extension](https://solana.com/_next/image?url=%2Fopengraph%2Fdevelopers%2Fguides%2Ftoken-
extensions%2Frequired-memo&w=3840&q=75)](/ru/developers/guides/token-
extensions/required-memo)

The `MemoTransfer` extension enforces that every incoming transfer to a Token
Account is accompanied by a [memo](https://spl.solana.com/memo) instruction.
This memo instruction records a message in the transaction's program logs.
This feature is particularly useful for adding context to transactions, making
it easier to understand their purpose when reviewing the transaction logs
later.

In this guide, we'll walk through an example of using Solana Playground. Here
is the [final script](https://beta.solpg.io/65724a91fb53fa325bfd0c54).

## Getting Started #

Start by opening this Solana Playground
[link](https://beta.solpg.io/656e19acfb53fa325bfd0c46) with the following
starter code.

    
    
    // Client
    console.log("My address:", pg.wallet.publicKey.toString());
    const balance = await pg.connection.getBalance(pg.wallet.publicKey);
    console.log(`My balance: ${balance / web3.LAMPORTS_PER_SOL} SOL`);

If it is your first time using Solana Playground, you'll first need to create
a Playground Wallet and fund the wallet with devnet SOL.

Info

If you do not have a Playground wallet, you may see a type error within the
editor on all declarations of `pg.wallet.publicKey`. This type error will
clear after you create a Playground wallet.

To get devnet SOL, run the `solana airdrop` command in the Playground's
terminal, or visit this [devnet faucet](https://faucet.solana.com/).

    
    
    solana airdrop 5

Once you've created and funded the Playground wallet, click the "Run" button
to run the starter code.

## Add Dependencies #

Let's start by setting up our script. We'll be using the `@solana/web3.js`,
`@solana/spl-token`, and `@solana/spl-memo` libraries.

Replace the starter code with the following:

    
    
    import {
      Connection,
      Keypair,
      SystemProgram,
      Transaction,
      clusterApiUrl,
      sendAndConfirmTransaction,
      TransactionInstruction,
      PublicKey,
    } from "@solana/web3.js";
    import {
      ExtensionType,
      TOKEN_2022_PROGRAM_ID,
      createEnableRequiredMemoTransfersInstruction,
      createInitializeAccountInstruction,
      createMint,
      disableRequiredMemoTransfers,
      enableRequiredMemoTransfers,
      getAccountLen,
      createAccount,
      mintTo,
      createTransferInstruction,
    } from "@solana/spl-token";
    import { createMemoInstruction } from "@solana/spl-memo";
     
    // Playground wallet
    const payer = pg.wallet.keypair;
     
    // Connection to devnet cluster
    const connection = new Connection(clusterApiUrl("devnet"), "confirmed");
     
    // Transaction to send
    let transaction: Transaction;
    // Transaction signature returned from sent transaction
    let transactionSignature: string;

## Mint Setup #

We'll first need to create a new Mint Account before we can create Token
Accounts.

    
    
    // Authority that can mint new tokens
    const mintAuthority = pg.wallet.publicKey;
    // Decimals for Mint Account
    const decimals = 2;
     
    // Create Mint Account
    const mint = await createMint(
      connection,
      payer, // Payer of the transaction and initialization fees
      mintAuthority, // Mint Authority
      null, // Optional Freeze Authority
      decimals, // Decimals of Mint
      undefined, // Optional keypair
      undefined, // Options for confirming the transaction
      TOKEN_2022_PROGRAM_ID, // Token Extension Program ID
    );

## Memo Transfer Token Account #

Next, let's build a transaction to enable the `MemoTransfer` extension for a
new Token Account.

First, let's generate a new keypair to use as the address of the Token
Account.

    
    
    // Random keypair to use as owner of Token Account
    const tokenAccountKeypair = Keypair.generate();
    // Address for Token Account
    const tokenAccount = tokenAccountKeypair.publicKey;

Next, let's determine the size of the new Token Account and calculate the
minimum lamports needed for rent exemption.

    
    
    // Size of Token Account with extension
    const accountLen = getAccountLen([ExtensionType.MemoTransfer]);
    // Minimum lamports required for Token Account
    const lamports = await connection.getMinimumBalanceForRentExemption(accountLen);

With Token Extensions, the size of the Token Account will vary based on the
extensions enabled.

## Build Instructions #

Next, let's build the set of instructions to:

  * Create a new account
  * Initialize the Token Account data
  * Enable the `MemoTransfer` extension

First, build the instruction to invoke the System Program to create an account
and assign ownership to the Token Extensions Program.

    
    
    // Instruction to invoke System Program to create new account
    const createAccountInstruction = SystemProgram.createAccount({
      fromPubkey: payer.publicKey, // Account that will transfer lamports to created account
      newAccountPubkey: tokenAccount, // Address of the account to create
      space: accountLen, // Amount of bytes to allocate to the created account
      lamports, // Amount of lamports transferred to created account
      programId: TOKEN_2022_PROGRAM_ID, // Program assigned as owner of created account
    });

Next, build the instruction to initialize the Token Account data.

    
    
    // Instruction to initialize Token Account data
    const initializeAccountInstruction = createInitializeAccountInstruction(
      tokenAccount, // Token Account Address
      mint, // Mint Account
      payer.publicKey, // Token Account Owner
      TOKEN_2022_PROGRAM_ID, // Token Extension Program ID
    );

Lastly, build the instruction to enable the `MemoTransfer` extension for the
Token Account.

    
    
    // Instruction to initialize the MemoTransfer Extension
    const enableRequiredMemoTransfersInstruction =
      createEnableRequiredMemoTransfersInstruction(
        tokenAccount, // Token Account address
        payer.publicKey, // Token Account Owner
        undefined, // Additional signers
        TOKEN_2022_PROGRAM_ID, // Token Program ID
      );

## Send Transaction #

Next, let's add the instructions to a new transaction and send it to the
network. This will create a Token Account with the `MemoTransfer` extension
enabled.

    
    
    // Add instructions to new transaction
    transaction = new Transaction().add(
      createAccountInstruction,
      initializeAccountInstruction,
      enableRequiredMemoTransfersInstruction,
    );
     
    // Send transaction
    transactionSignature = await sendAndConfirmTransaction(
      connection,
      transaction,
      [payer, tokenAccountKeypair], // Signers
    );
     
    console.log(
      "\nCreate Token Account:",
      `https://solana.fm/tx/${transactionSignature}?cluster=devnet-solana`,
    );

Run the script by clicking the `Run` button. You can then inspect the
transaction details on SolanaFM.

## Create and Fund Token Account #

Next, let's set up another Token Account to demonstrate the functionality of
the `MemoTransfer` extension.

First, create a `sourceTokenAccount` owned by the Playground wallet.

    
    
    // Create Token Account for Playground wallet
    const sourceTokenAccount = await createAccount(
      connection,
      payer, // Payer to create Token Account
      mint, // Mint Account address
      payer.publicKey, // Token Account owner
      undefined, // Optional keypair, default to Associated Token Account
      undefined, // Confirmation options
      TOKEN_2022_PROGRAM_ID, // Token Extension Program ID
    );

Next, mint 2 tokens to the `sourceTokenAccount` to fund it.

    
    
    // Mint tokens to sourceTokenAccount
    transactionSignature = await mintTo(
      connection,
      payer, // Transaction fee payer
      mint, // Mint Account address
      sourceTokenAccount, // Mint to
      mintAuthority, // Mint Authority address
      200, // Amount
      undefined, // Additional signers
      undefined, // Confirmation options
      TOKEN_2022_PROGRAM_ID, // Token Extension Program ID
    );
     
    console.log(
      "\nMint Tokens:",
      `https://solana.fm/tx/${transactionSignature}?cluster=devnet-solana`,
    );

## Transfer and Memo Instruction #

Next, let's prepare the token transfer and memo instructions.

First, build the instruction to transfer tokens from the `sourceTokenAccount`
to the `tokenAccount` which has the `MemoTransfer` extension enabled.

    
    
    // Instruction to transfer tokens
    const transferInstruction = createTransferInstruction(
      sourceTokenAccount, // Source Token Account
      tokenAccount, // Destination Token Account
      payer.publicKey, // Source Token Account owner
      100, // Amount
      undefined, // Additional signers
      TOKEN_2022_PROGRAM_ID, // Token Extension Program ID
    );

Next, build the memo instruction. The message will be included in the program
logs of the transaction the instruction is added to.

    
    
    // Message for the memo
    const message = "Hello, Solana";
    // Instruction to add memo
    const memoInstruction = new TransactionInstruction({
      keys: [{ pubkey: payer.publicKey, isSigner: true, isWritable: true }],
      data: Buffer.from(message, "utf-8"),
      programId: new PublicKey("MemoSq4gqABAXKb96qnH8TysNcWxMyWCqXgDLGmfcHr"),
    });

Alternatively, you can create the instruction using the `@solana/spl-memo`
library:

    
    
    // Message for the memo
    const message = "Hello, Solana";
    // Instruction to add memo
    const memoInstruction = createMemoInstruction(message, [payer.publicKey]);

## Attempt Transfer without Memo #

To demonstrate the functionality of the `MemoTransfer` extension, let's first
attempt to send a token transfer without a memo.

    
    
    try {
      // Attempt to transfer without memo
      transaction = new Transaction().add(transferInstruction);
     
      // Send transaction
      await sendAndConfirmTransaction(
        connection,
        transaction,
        [payer], // Signers
      );
    } catch (error) {
      console.log("\nExpect Error:", error);
    }

Run the script by clicking the `Run` button. You can then inspect the error in
the Playground terminal. You should see a message similar to the following:

    
    
    Expect Error: { [Error: failed to send transaction: Transaction simulation failed: Error processing Instruction 0: custom program error: 0x24]
      logs:
       [ 'Program TokenzQdBNbLqP5VEhdkAS6EPFLC1PHnBqCXEpPxuEb invoke [1]',
         'Program log: Instruction: Transfer',
         'Program log: Error: No memo in previous instruction; required for recipient to receive a transfer',
         'Program TokenzQdBNbLqP5VEhdkAS6EPFLC1PHnBqCXEpPxuEb consumed 6571 of 200000 compute units',
         'Program TokenzQdBNbLqP5VEhdkAS6EPFLC1PHnBqCXEpPxuEb failed: custom program error: 0x24' ] }

## Transfer with Memo #

Next, send a token transfer with the memo instruction included on the
transaction.

    
    
    // Add instructions to new transaction
    transaction = new Transaction().add(memoInstruction, transferInstruction);
     
    // Send transaction
    transactionSignature = await sendAndConfirmTransaction(
      connection,
      transaction,
      [payer], // Signers
    );
     
    console.log(
      "\nTransfer with Memo:",
      `https://solana.fm/tx/${transactionSignature}?cluster=devnet-solana`,
    );

Run the script by clicking the `Run` button. You can then inspect the
transaction details on SolanaFM.

## Enable and Disable Memo Transfer #

The `MemoTransfer` extension can also be freely enabled or disabled by the
Token Account owner.

To enable the `MemoTransfer` extension, use the `enableRequiredMemoTransfers`
instruction.

    
    
    // Enable Required Memo Transfers
    transactionSignature = await enableRequiredMemoTransfers(
      connection, // Connection to use
      payer, // Payer of the transaction fee
      tokenAccount, // Token Account to modify
      payer.publicKey, // Owner of Token Account
      undefined, // Additional signers
      undefined, // Confirmation options
      TOKEN_2022_PROGRAM_ID, // Token Extension Program ID
    );
     
    console.log(
      "\nEnable Required Memo Transfers:",
      `https://solana.fm/tx/${transactionSignature}?cluster=devnet-solana`,
    );

To disable the `MemoTransfer` extension, use the
`disableRequiredMemoTransfers` instruction.

    
    
    // Disable Required Memo Transfers
    transactionSignature = await disableRequiredMemoTransfers(
      connection, // Connection to use
      payer, // Payer of the transaction fee
      tokenAccount, // Token Account to modify
      payer.publicKey, // Owner of Token Account
      undefined, // Additional signers
      undefined, // Confirmation options
      TOKEN_2022_PROGRAM_ID, // Token Extension Program ID
    );
     
    console.log(
      "\nDisable Required Memo Transfers:",
      `https://solana.fm/tx/${transactionSignature}?cluster=devnet-solana`,
    );

Once the `MemoTransfer` extension is disabled, transactions to transfer tokens
without a memo instruction will complete successfully.

    
    
    // Add instructions to new transaction
    transaction = new Transaction().add(transferInstruction);
     
    // Send transaction
    transactionSignature = await sendAndConfirmTransaction(
      connection,
      transaction,
      [payer], // Signers
    );
     
    console.log(
      "\nTransfer without Memo:",
      `https://solana.fm/tx/${transactionSignature}?cluster=devnet-solana`,
    );

Run the script by clicking the `Run` button. You can then inspect the
transaction details on SolanaFM.

## Conclusion #

The `MemoTransfer` extension ensures every incoming transfer to a Token
Account includes a memo. By requiring a memo instruction with each transfer, a
message is recorded in the transaction's program logs. This feature is
especially useful for understanding the purpose of transactions when reviewing
logs at a later time.

[Previous« How to use the Reallocate instruction](/ru/developers/guides/token-
extensions/reallocate)[NextHow to use the Transfer Fee extension
»](/ru/developers/guides/token-extensions/transfer-fee)

##### Table of Contents

  * [Getting Started](/ru/developers/guides/token-extensions/required-memo#getting-started)
  * [Add Dependencies](/ru/developers/guides/token-extensions/required-memo#add-dependencies)
  * [Mint Setup](/ru/developers/guides/token-extensions/required-memo#mint-setup)
  * [Memo Transfer Token Account](/ru/developers/guides/token-extensions/required-memo#memo-transfer-token-account)
  * [Build Instructions](/ru/developers/guides/token-extensions/required-memo#build-instructions)
  * [Send Transaction](/ru/developers/guides/token-extensions/required-memo#send-transaction)
  * [Create and Fund Token Account](/ru/developers/guides/token-extensions/required-memo#create-and-fund-token-account)
  * [Transfer and Memo Instruction](/ru/developers/guides/token-extensions/required-memo#transfer-and-memo-instruction)
  * [Attempt Transfer without Memo](/ru/developers/guides/token-extensions/required-memo#attempt-transfer-without-memo)
  * [Transfer with Memo](/ru/developers/guides/token-extensions/required-memo#transfer-with-memo)
  * [Enable and Disable Memo Transfer](/ru/developers/guides/token-extensions/required-memo#enable-and-disable-memo-transfer)
  * [Conclusion](/ru/developers/guides/token-extensions/required-memo#conclusion)

[Scroll to Top](/ru/developers/guides/token-extensions/required-memo#)

[Edit Page](https://github.com/solana-foundation/developer-
content/tree/main/content/guides/token-extensions/required-memo.md)

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

