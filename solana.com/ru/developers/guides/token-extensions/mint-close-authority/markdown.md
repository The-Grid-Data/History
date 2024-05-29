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

# [How to use the Mint Close Authority extension](/ru/developers/guides/token-
extensions/mint-close-authority)

updated 5 декабря 2023 г.

[beginner](/ru/developers/guides?difficulty=beginner)[token
2022](/ru/developers/guides?tags=token%202022)[token
extensions](/ru/developers/guides?tags=token%20extensions)

[![How to use the Mint Close Authority
extension](https://solana.com/_next/image?url=%2Fopengraph%2Fdevelopers%2Fguides%2Ftoken-
extensions%2Fmint-close-authority&w=3840&q=75)](/ru/developers/guides/token-
extensions/mint-close-authority)

With the original SPL token program, there was no option to close Mint
Accounts owned by the Token Program and reclaim the SOL allocated to these
accounts.

The `MintCloseAuthority` extension introduces a solution to this limitation by
allowing a designated Close Authority to close a Mint Account if the supply of
the mint is 0. This feature provides a mechanism to recover SOL allocated to
Mint Accounts that are no longer in use.

In this guide, we'll walk through an example of using Solana Playground. Here
is the [final script](https://beta.solpg.io/65700c73fb53fa325bfd0c4a).

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
      closeAccount,
      createInitializeMintCloseAuthorityInstruction,
      createInitializeMintInstruction,
      getMintLen,
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
    // Authority that can close the Mint Account
    const closeAuthority = pg.wallet.publicKey;

Next, let's determine the size of the new Mint Account and calculate the
minimum lamports needed for rent exemption.

    
    
    // Size of Mint Account with extension
    const mintLen = getMintLen([ExtensionType.MintCloseAuthority]);
    // Minimum lamports required for Mint Account
    const lamports = await connection.getMinimumBalanceForRentExemption(mintLen);

With Token Extensions, the size of the Mint Account will vary based on the
extensions enabled.

## Build Instructions #

Next, let's build the set of instructions to:

  * Create a new account
  * Initialize the `MintCloseAuthority` extension
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

Next, build the instruction to initialize the `MintCloseAuthority` extension
for the Mint Account.

    
    
    // Instruction to initialize the MintCloseAuthority Extension
    const initializeMintCloseAuthorityInstruction =
      createInitializeMintCloseAuthorityInstruction(
        mint, // Mint Account address
        closeAuthority, // Designated Close Authority
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
network. This will create a Mint Account with the `MintCloseAuthority`
extension enabled.

    
    
    // Add instructions to new transaction
    const transaction = new Transaction().add(
      createAccountInstruction,
      initializeMintCloseAuthorityInstruction,
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
transaction details on SolanaFM.

## Close Mint Account #

With the `MintCloseAuthority` extension enabled, the Close Authority can close
the Mint Account to reclaim the lamports from the account.

    
    
    // Send transaction to close Mint Account
    transactionSignature = await closeAccount(
      connection,
      payer, // Transaction fee payer
      mint, // Mint Account address
      payer.publicKey, // Account to receive lamports from closed account
      closeAuthority, // Close Authority for Mint Account
      undefined, // Additional signers
      undefined, // Confirmation options
      TOKEN_2022_PROGRAM_ID, // Token Extension Program ID
    );
     
    console.log(
      "\nClose Mint Account:",
      `https://solana.fm/tx/${transactionSignature}?cluster=devnet-solana`,
    );

Run the script by clicking the `Run` button. You can then inspect the
transaction details on the SolanaFM.

## Conclusion #

The `MintCloseAuthority` extension enables developers to reclaim SOL that
otherwise would have been permanently locked in a Mint Account. This feature
is particularly useful for applications or games involving single-use NFTs
that are meant to be burned. It ensures that the SOL allocated to Mint
Accounts which are no longer used can be reclaimed and reused.

[Previous« How to use the Metadata Pointer
extension](/ru/developers/guides/token-extensions/metadata-pointer)[NextHow to
use the Non-transferable extension »](/ru/developers/guides/token-
extensions/non-transferable)

##### Table of Contents

  * [Getting Started](/ru/developers/guides/token-extensions/mint-close-authority#getting-started)
  * [Add Dependencies](/ru/developers/guides/token-extensions/mint-close-authority#add-dependencies)
  * [Mint Setup](/ru/developers/guides/token-extensions/mint-close-authority#mint-setup)
  * [Build Instructions](/ru/developers/guides/token-extensions/mint-close-authority#build-instructions)
  * [Send Transaction](/ru/developers/guides/token-extensions/mint-close-authority#send-transaction)
  * [Close Mint Account](/ru/developers/guides/token-extensions/mint-close-authority#close-mint-account)
  * [Conclusion](/ru/developers/guides/token-extensions/mint-close-authority#conclusion)

[Scroll to Top](/ru/developers/guides/token-extensions/mint-close-authority#)

[Edit Page](https://github.com/solana-foundation/developer-
content/tree/main/content/guides/token-extensions/mint-close-authority.md)

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

