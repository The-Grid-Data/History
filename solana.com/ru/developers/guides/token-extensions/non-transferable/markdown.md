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

# [How to use the Non-transferable extension](/ru/developers/guides/token-
extensions/non-transferable)

updated 6 декабря 2023 г.

[beginner](/ru/developers/guides?difficulty=beginner)[token
2022](/ru/developers/guides?tags=token%202022)[token
extensions](/ru/developers/guides?tags=token%20extensions)

[![How to use the Non-transferable
extension](https://solana.com/_next/image?url=%2Fopengraph%2Fdevelopers%2Fguides%2Ftoken-
extensions%2Fnon-transferable&w=3840&q=75)](/ru/developers/guides/token-
extensions/non-transferable)

The `NonTransferable` extension makes it possible to create tokens that cannot
be transferred. This enables the creation of "soul-bound" tokens, where
digital assets are intrinsically linked to an individual. While these tokens
cannot be transferred, the owner can still burn tokens and close the Token
Account. This prevents users from being "stuck" with an unwanted asset.

In this guide, we will walk through an example of creating "soul-bound" tokens
with the `NonTransferable` extension using Solana Playground. Here is the
[final script](https://beta.solpg.io/6570c54bfb53fa325bfd0c4d).

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

Let's start by setting up our script. We'll be using the `@solana/web3.js` and
`@solana/spl-token` libraries.

Replace the starter code with the following:

    
    
    import {
      Connection,
      Keypair,
      SystemProgram,
      Transaction,
      clusterApiUrl,
      sendAndConfirmTransaction,
    } from "@solana/web3.js";
    import {
      ExtensionType,
      TOKEN_2022_PROGRAM_ID,
      createInitializeMintInstruction,
      createInitializeNonTransferableMintInstruction,
      getMintLen,
      mintTo,
      createAccount,
      transfer,
      burn,
      closeAccount,
    } from "@solana/spl-token";
     
    // Playground wallet
    const payer = pg.wallet.keypair;
     
    // Connection to devnet cluster
    const connection = new Connection(clusterApiUrl("devnet"), "confirmed");
     
    // Transaction signature returned from sent transaction
    let transactionSignature: string;

## Mint Setup #

First, let's define the properties of the Mint Account we'll be creating in
the following step.

    
    
    // Generate new keypair for Mint Account
    const mintKeypair = Keypair.generate();
    // Address for Mint Account
    const mint = mintKeypair.publicKey;
    // Decimals for Mint Account
    const decimals = 2;
    // Authority that can mint new tokens
    const mintAuthority = pg.wallet.publicKey;

Next, let's determine the size of the new Mint Account and calculate the
minimum lamports needed for rent exemption.

    
    
    // Size of Mint Account with extension
    const mintLen = getMintLen([ExtensionType.NonTransferable]);
    // Minimum lamports required for Mint Account
    const lamports = await connection.getMinimumBalanceForRentExemption(mintLen);

With Token Extensions, the size of the Mint Account will vary based on the
extensions enabled.

## Build Instructions #

Next, let's build the set of instructions to:

  * Create a new account
  * Initialize the `NonTransferable` extension
  * Initialize the remaining Mint Account data

First, build the instruction to invoke the System Program to create an account
and assign ownership to the Token Extensions Program.

    
    
    // Instruction to invoke System Program to create new account
    const createAccountInstruction = SystemProgram.createAccount({
      fromPubkey: payer.publicKey, // Account that will transfer lamports to created account
      newAccountPubkey: mint, // Address of the account to create
      space: mintLen, // Amount of bytes to allocate to the created account
      lamports, // Amount of lamports transferred to created account
      programId: TOKEN_2022_PROGRAM_ID, // Program assigned as owner of created account
    });

Next, build the instruction to initialize the `NonTransferable` extension for
the Mint Account.

    
    
    // Instruction to initialize the NonTransferable Extension
    const initializeNonTransferableMintInstruction =
      createInitializeNonTransferableMintInstruction(
        mint, // Mint Account address
        TOKEN_2022_PROGRAM_ID, // Token Extension Program ID
      );

Lastly, build the instruction to initialize the rest of the Mint Account data.
This is the same as with the original Token Program.

    
    
    // Instruction to initialize Mint Account data
    const initializeMintInstruction = createInitializeMintInstruction(
      mint, // Mint Account Address
      decimals, // Decimals of Mint
      mintAuthority, // Designated Mint Authority
      null, // Optional Freeze Authority
      TOKEN_2022_PROGRAM_ID, // Token Extension Program ID
    );

## Send Transaction #

Next, let's add the instructions to a new transaction and send it to the
network. This will create a Mint Account with the `NonTransferable` extension
enabled.

    
    
    // Add instructions to new transaction
    const transaction = new Transaction().add(
      createAccountInstruction,
      initializeNonTransferableMintInstruction,
      initializeMintInstruction,
    );
     
    // Send transaction
    transactionSignature = await sendAndConfirmTransaction(
      connection,
      transaction,
      [payer, mintKeypair], // Signers
    );
     
    console.log(
      "\nCreate Mint Account:",
      `https://solana.fm/tx/${transactionSignature}?cluster=devnet-solana`,
    );

Run the script by clicking the `Run` button. You can then inspect the
transaction on the SolanaFM.

## Create Token Accounts #

Next, let's set up two Token Accounts to demonstrate the functionality of the
`NonTransferable` extension.

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

Next, generate a random keypair and use it as the owner of a
`destinationTokenAccount`.

    
    
    // Random keypair to use as owner of Token Account
    const randomKeypair = new Keypair();
    // Create Token Account for random keypair
    const destinationTokenAccount = await createAccount(
      connection,
      payer, // Payer to create Token Account
      mint, // Mint Account address
      randomKeypair.publicKey, // Token Account owner
      undefined, // Optional keypair, default to Associated Token Account
      undefined, // Confirmation options
      TOKEN_2022_PROGRAM_ID, // Token Extension Program ID
    );

Lastly, mint 1 token to the `sourceTokenAccount` to test the non-transferrable
enforcement.

    
    
    // Mint tokens to sourceTokenAccount
    transactionSignature = await mintTo(
      connection,
      payer, // Transaction fee payer
      mint, // Mint Account address
      sourceTokenAccount, // Mint to
      mintAuthority, // Mint Authority address
      100, // Amount
      undefined, // Additional signers
      undefined, // Confirmation options
      TOKEN_2022_PROGRAM_ID, // Token Extension Program ID
    );
     
    console.log(
      "\nMint Tokens:",
      `https://solana.fm/tx/${transactionSignature}?cluster=devnet-solana`,
    );

## Attempt Token Transfer #

Next, let's try to transfer tokens from the `sourceTokenAccount` to the
`destinationTokenAccount`. We expect this transaction to fail due to the
`NonTransferable` extension.

    
    
    try {
      // Attempt to Transfer tokens
      await transfer(
        connection,
        payer, // Transaction fee payer
        sourceTokenAccount, // Transfer from
        destinationTokenAccount, // Transfer to
        payer.publicKey, // Source Token Account owner
        100, // Amount
        undefined, // Additional signers
        undefined, // Confirmation options
        TOKEN_2022_PROGRAM_ID, // Token Extension Program ID
      );
    } catch (error) {
      console.log("\nExpect Error:", error);
    }

Run the script by clicking the `Run` button. You can then inspect the error in
the Playground terminal. You should see a message similar to the following:

    
    
    Expect Error: { [Error: failed to send transaction: Transaction simulation failed: Error processing Instruction 0: custom program error: 0x25]
      logs:
       [ 'Program TokenzQdBNbLqP5VEhdkAS6EPFLC1PHnBqCXEpPxuEb invoke [1]',
         'Program log: Instruction: Transfer',
         'Program log: Transfer is disabled for this mint',
         'Program TokenzQdBNbLqP5VEhdkAS6EPFLC1PHnBqCXEpPxuEb consumed 3454 of 200000 compute units',
         'Program TokenzQdBNbLqP5VEhdkAS6EPFLC1PHnBqCXEpPxuEb failed: custom program error: 0x25' ] }

## Burn Tokens and Close Token Account #

While tokens can't be transferred, they can still be burned.

    
    
    // Burn tokens
    transactionSignature = await burn(
      connection,
      payer, // Transaction fee payer
      sourceTokenAccount, // Burn from
      mint, // Mint Account address
      payer.publicKey, // Token Account owner
      100, // Amount
      undefined, // Additional signers
      undefined, // Confirmation options
      TOKEN_2022_PROGRAM_ID, // Token Extension Program ID
    );
     
    console.log(
      "\nBurn Tokens:",
      `https://solana.fm/tx/${transactionSignature}?cluster=devnet-solana`,
    );

The Token Account can then be closed to recover the SOL that was allocated to
the account. Note that the token balance must be 0.

    
    
    // Close Token Account
    transactionSignature = await closeAccount(
      connection,
      payer, // Transaction fee payer
      sourceTokenAccount, // Token Account to close
      payer.publicKey, // Account to receive lamports from closed account
      payer.publicKey, // Owner of Token Account
      undefined, // Additional signers
      undefined, // Confirmation options
      TOKEN_2022_PROGRAM_ID, // Token Extension Program ID
    );
     
    console.log(
      "\nClose Token Account:",
      `https://solana.fm/tx/${transactionSignature}?cluster=devnet-solana`,
    );

Run the script by clicking the `Run` button. You can then inspect the
transaction on the SolanaFM.

## Conclusion #

The `NonTransferable` mint extension enables the creation of "soul-bound"
tokens, ensuring that digital assets are bound to an individual account. This
feature enables a unique mechanism for digital ownership such as for personal
achievements, identity, or credentials that are inherently non-transferable.

[Previous« How to use the Mint Close Authority
extension](/ru/developers/guides/token-extensions/mint-close-
authority)[NextHow to use the Permanent Delegate extension
»](/ru/developers/guides/token-extensions/permanent-delegate)

##### Table of Contents

  * [Getting Started](/ru/developers/guides/token-extensions/non-transferable#getting-started)
  * [Add Dependencies](/ru/developers/guides/token-extensions/non-transferable#add-dependencies)
  * [Mint Setup](/ru/developers/guides/token-extensions/non-transferable#mint-setup)
  * [Build Instructions](/ru/developers/guides/token-extensions/non-transferable#build-instructions)
  * [Send Transaction](/ru/developers/guides/token-extensions/non-transferable#send-transaction)
  * [Create Token Accounts](/ru/developers/guides/token-extensions/non-transferable#create-token-accounts)
  * [Attempt Token Transfer](/ru/developers/guides/token-extensions/non-transferable#attempt-token-transfer)
  * [Burn Tokens and Close Token Account](/ru/developers/guides/token-extensions/non-transferable#burn-tokens-and-close-token-account)
  * [Conclusion](/ru/developers/guides/token-extensions/non-transferable#conclusion)

[Scroll to Top](/ru/developers/guides/token-extensions/non-transferable#)

[Edit Page](https://github.com/solana-foundation/developer-
content/tree/main/content/guides/token-extensions/non-transferable.md)

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

![](https://t.co/1/i/adsct?bci=4&eci=3&event=%7B%7D&event_id=11629258-e1cc-4a83-b393-94a90d236ec1&integration=gtm&p_id=Twitter&p_user_id=0&pl_id=576728f1-7203-4321-a883-5dc9dd18d8f6&tw_document_href=https%3A%2F%2Fsolana.com%2Fru%2Fdevelopers%2Fguides%2Ftoken-
extensions%2Fnon-
transferable&tw_iframe_status=0&txn_id=o6jgu&type=javascript&version=2.3.30)![](https://analytics.twitter.com/1/i/adsct?bci=4&eci=3&event=%7B%7D&event_id=11629258-e1cc-4a83-b393-94a90d236ec1&integration=gtm&p_id=Twitter&p_user_id=0&pl_id=576728f1-7203-4321-a883-5dc9dd18d8f6&tw_document_href=https%3A%2F%2Fsolana.com%2Fru%2Fdevelopers%2Fguides%2Ftoken-
extensions%2Fnon-
transferable&tw_iframe_status=0&txn_id=o6jgu&type=javascript&version=2.3.30)

