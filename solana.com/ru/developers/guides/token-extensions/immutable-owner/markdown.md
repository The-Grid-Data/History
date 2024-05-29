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

# [How to use the Immutable Owner extension](/ru/developers/guides/token-
extensions/immutable-owner)

updated 6 декабря 2023 г.

[beginner](/ru/developers/guides?difficulty=beginner)[token
2022](/ru/developers/guides?tags=token%202022)[token
extensions](/ru/developers/guides?tags=token%20extensions)

[![How to use the Immutable Owner
extension](https://solana.com/_next/image?url=%2Fopengraph%2Fdevelopers%2Fguides%2Ftoken-
extensions%2Fimmutable-owner&w=3840&q=75)](/ru/developers/guides/token-
extensions/immutable-owner)

With the Token Program, the `SetAuthority` instruction can be used to change a
Token Account's owner to another account. The `ImmutableOwner` extension
ensures that ownership of a Token Account cannot be reassigned.

In this guide, we WILL walk through an example of using Solana Playground.
Here is the [final script](https://beta.solpg.io/65710736fb53fa325bfd0c4f).

## Understanding the Implications #

So, why is this important? The addresses for Associated Token Accounts are
derived based on the owner and the mint. This makes it easy to find the
related Token Account for a specific owner.

If the owner of an existing Associated Token Account is changed, users may
unintentionally transfer funds to an account under the assumption that it
belongs to the original owner.

With Token Extensions, Associated Token Accounts have the `ImmutableOwner`
extension enabled by default, preventing the ownership from being changed.

The `ImmutableOwner` extension can also be enabled for any new Token Account
created by the Token Extension program.

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
      clusterApiUrl,
      sendAndConfirmTransaction,
      Connection,
      Keypair,
      SystemProgram,
      Transaction,
    } from "@solana/web3.js";
    import {
      createAssociatedTokenAccount,
      createMint,
      createInitializeImmutableOwnerInstruction,
      createInitializeAccountInstruction,
      getAccountLen,
      ExtensionType,
      TOKEN_2022_PROGRAM_ID,
      setAuthority,
      AuthorityType,
    } from "@solana/spl-token";
     
    // Playground wallet
    const payer = pg.wallet.keypair;
     
    // Connection to devnet cluster
    const connection = new Connection(clusterApiUrl("devnet"), "confirmed");
     
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

## Associated Token Account #

The `ImmutableOwner` extension is enabled by default for Associated Token
Accounts created for Mint Accounts that are owned by the Token Extension
Program.

Let's demonstrate this concept by creating an Associated Token Account for the
Playground wallet.

    
    
    // Create Associated Token Account for Playground wallet
    const associatedTokenAccount = await createAssociatedTokenAccount(
      connection,
      payer, // Payer to create Token Account
      mint, // Mint Account address
      payer.publicKey, // Token Account owner
      undefined, // Confirmation options
      TOKEN_2022_PROGRAM_ID, // Token Extension Program ID
    );

Attempting to change the owner of the Associated Token Account will result in
an error.

    
    
    try {
      // Attempt to change owner of Associated Token Account
      await setAuthority(
        connection, // Connection to use
        payer, // Payer of the transaction fee
        associatedTokenAccount, // Associated Token Account
        payer.publicKey, // Owner of the Associated Token Account
        AuthorityType.AccountOwner, // Type of Authority
        new Keypair().publicKey, // New Account Owner
        undefined, // Additional signers
        undefined, // Confirmation options
        TOKEN_2022_PROGRAM_ID, // Token Extension Program ID
      );
    } catch (error) {
      console.log("\nExpect Error:", error);
    }

Run the script by clicking the `Run` button. You can then inspect the error in
the Playground terminal. You should see a message similar to the following:

    
    
    Expect Error: { [Error: failed to send transaction: Transaction simulation failed: Error processing Instruction 0: custom program error: 0x22]
      logs:
       [ 'Program TokenzQdBNbLqP5VEhdkAS6EPFLC1PHnBqCXEpPxuEb invoke [1]',
         'Program log: Instruction: SetAuthority',
         'Program log: The owner authority cannot be changed',
         'Program TokenzQdBNbLqP5VEhdkAS6EPFLC1PHnBqCXEpPxuEb consumed 3057 of 200000 compute units',
         'Program TokenzQdBNbLqP5VEhdkAS6EPFLC1PHnBqCXEpPxuEb failed: custom program error: 0x22' ] }

### Immutable Owner Token Account #

Next, let's build a transaction to enable the `ImmutableOwner` extension for a
new Token Account. Note that this can only be done for new Token Accounts.

First, let's generate a new keypair to use as the address of the Token
Account.

    
    
    // Random keypair to use as owner of Token Account
    const tokenAccountKeypair = Keypair.generate();
    // Address for Token Account
    const tokenAccount = tokenAccountKeypair.publicKey;

Next, let's determine the size of the new Token Account and calculate the
minimum lamports needed for rent exemption.

    
    
    // Size of Token Account with extension
    const accountLen = getAccountLen([ExtensionType.ImmutableOwner]);
    // Minimum lamports required for Token Account
    const lamports = await connection.getMinimumBalanceForRentExemption(accountLen);

With Token Extensions, the size of the Token Account will vary based on the
extensions enabled.

## Build Instructions #

Next, let's build the set of instructions to:

  * Create a new account
  * Initialize the `ImmutableOwner` extension
  * Initialize the remaining Token Account data

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

Next, build the instruction to initialize the `ImmutableOwner` extension for
the Token Account.

    
    
    // Instruction to initialize the ImmutableOwner Extension
    const initializeImmutableOwnerInstruction =
      createInitializeImmutableOwnerInstruction(
        tokenAccount, // Token Account address
        TOKEN_2022_PROGRAM_ID, // Token Extension Program ID
      );

Lastly, build the instruction to initialize the rest of the Token Account
data.

    
    
    // Instruction to initialize Token Account data
    const initializeAccountInstruction = createInitializeAccountInstruction(
      tokenAccount, // Token Account Address
      mint, // Mint Account
      payer.publicKey, // Token Account Owner
      TOKEN_2022_PROGRAM_ID, // Token Extension Program ID
    );

## Send Transaction #

Next, let's add the instructions to a new transaction and send it to the
network. This will create a Token Account with the `ImmutableOwner` extension
enabled.

    
    
    // Add instructions to new transaction
    const transaction = new Transaction().add(
      createAccountInstruction,
      initializeImmutableOwnerInstruction,
      initializeAccountInstruction,
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

If you attempt to change the owner of the Token Account, then you should see
the same error as before.

    
    
    try {
      // Attempt to change owner of Token Account
      await setAuthority(
        connection, // Connection to use
        payer, // Payer of the transaction fee
        tokenAccount, // Token Account
        payer.publicKey, // Owner of the Token Account
        AuthorityType.AccountOwner, // Type of Authority
        new Keypair().publicKey, // New Account Owner
        undefined, // Additional signers
        undefined, // Confirmation options
        TOKEN_2022_PROGRAM_ID, // Token Extension Program ID
      );
    } catch (error) {
      console.log("\nExpect Error:", error);
    }

## Conclusion #

The `ImmutableOwner` extension prevents a vulnerability that was previously
possible by reassigning the owner of Associated Token Accounts. This security
feature can also be applied to any new Token Account, guarding against
unintended ownership changes.

[Previous« Getting Started with Token Extensions](/ru/developers/guides/token-
extensions/getting-started)[NextHow to use the Interest-Bearing extension
»](/ru/developers/guides/token-extensions/interest-bearing-tokens)

##### Table of Contents

  * [Understanding the Implications](/ru/developers/guides/token-extensions/immutable-owner#understanding-the-implications)
  * [Getting Started](/ru/developers/guides/token-extensions/immutable-owner#getting-started)
  * [Add Dependencies](/ru/developers/guides/token-extensions/immutable-owner#add-dependencies)
  * [Mint Setup](/ru/developers/guides/token-extensions/immutable-owner#mint-setup)
  * [Associated Token Account](/ru/developers/guides/token-extensions/immutable-owner#associated-token-account)
  * [Immutable Owner Token Account](/ru/developers/guides/token-extensions/immutable-owner#immutable-owner-token-account)
  * [Build Instructions](/ru/developers/guides/token-extensions/immutable-owner#build-instructions)
  * [Send Transaction](/ru/developers/guides/token-extensions/immutable-owner#send-transaction)
  * [Conclusion](/ru/developers/guides/token-extensions/immutable-owner#conclusion)

[Scroll to Top](/ru/developers/guides/token-extensions/immutable-owner#)

[Edit Page](https://github.com/solana-foundation/developer-
content/tree/main/content/guides/token-extensions/immutable-owner.md)

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

