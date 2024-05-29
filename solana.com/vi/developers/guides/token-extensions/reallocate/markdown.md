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

[Home](/vi)>[Developers](/vi/developers)>[Guides](/vi/developers/guides)

# [How to use the Reallocate instruction](/vi/developers/guides/token-
extensions/reallocate)

updated 7 tháng 12, 2023

[beginner](/vi/developers/guides?difficulty=beginner)[token
2022](/vi/developers/guides?tags=token%202022)[token
extensions](/vi/developers/guides?tags=token%20extensions)

[![How to use the Reallocate
instruction](https://solana.com/_next/image?url=%2Fopengraph%2Fdevelopers%2Fguides%2Ftoken-
extensions%2Freallocate&w=3840&q=75)](/vi/developers/guides/token-
extensions/reallocate)

To enable additional extensions on existing Token Accounts created via the
Token Extension program, additional space must first be reallocated to
accommodate the extra data required by these extensions. This can be done
using the `reallocate` instruction.

For example, this allows existing Token Accounts can be updated to enable the
[`MemoTransfer`](/vi/developers/guides/token-extensions/required-memo) and
`CpiGuard` extensions.

In this guide, we'll walk through an example of using Solana Playground. Here
is the [final script](https://beta.solpg.io/65723a50fb53fa325bfd0c52).

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
      Transaction,
      clusterApiUrl,
      sendAndConfirmTransaction,
    } from "@solana/web3.js";
    import {
      ExtensionType,
      TOKEN_2022_PROGRAM_ID,
      createAccount,
      createMint,
      createReallocateInstruction,
      createEnableRequiredMemoTransfersInstruction,
    } from "@solana/spl-token";
     
    // Playground wallet
    const payer = pg.wallet.keypair;
     
    // Connection to devnet cluster
    const connection = new Connection(clusterApiUrl("devnet"), "confirmed");
     
    // Transaction signature returned from sent transaction
    let transactionSignature: string;

## Create Mint and Token Account #

First, we'll need to create a new Mint Account.

    
    
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

Next, let's create a Token Account with no extensions enabled.

    
    
    // Create Token Account for Playground wallet
    const tokenAccount = await createAccount(
      connection,
      payer, // Payer to create Token Account
      mint, // Mint Account address
      payer.publicKey, // Token Account owner
      undefined, // Optional keypair, default to Associated Token Account
      undefined, // Confirmation options
      TOKEN_2022_PROGRAM_ID, // Token Extension Program ID
    );

## Build Instructions #

Next, let's build a transaction to enable the `MemoTransfer` extensions for an
existing Token Account.

First, build the instruction to reallocate the Token Account with enough space
for the specified extension. The Token Extensions Program includes a
[reallocate instruction](https://github.com/solana-labs/solana-program-
library/blob/master/token/program-2022/src/extension/reallocate.rs#L24) that
automatically calculates the space and lamports required.

    
    
    // Extensions to reallocate data for
    const extensions = [ExtensionType.MemoTransfer];
    // Instruction to reallocate Token Account data
    const reallocateInstruction = createReallocateInstruction(
      tokenAccount, // Token Account address
      payer.publicKey, // Payer to reallocate data
      extensions, // Extensions to reallocate for
      payer.publicKey, // Token Account owner
      undefined, // Additional signers
      TOKEN_2022_PROGRAM_ID, // Token Extension Program ID
    );

Next, build the instruction to enable the `MemoTransfer` extension for the
Token Account.

    
    
    // Instruction to initialize the MemoTransfer Extension
    const enableRequiredMemoTransfersInstruction =
      createEnableRequiredMemoTransfersInstruction(
        tokenAccount, // Token Account address
        payer.publicKey, // Token Account Owner
        undefined, // Additional signers
        TOKEN_2022_PROGRAM_ID, // Token Extension Program ID
      );

## Send Transaction #

Next, let's add the instructions to a new transaction and send it to the
network. This will update the Token Account with the `MemoTransfer` extension
enabled.

    
    
    // Add instructions to new transaction
    const transaction = new Transaction().add(
      reallocateInstruction,
      enableRequiredMemoTransfersInstruction,
    );
     
    // Send Transaction
    transactionSignature = await sendAndConfirmTransaction(
      connection,
      transaction,
      [payer],
    );
     
    console.log(
      "\nReallocate:",
      `https://solana.fm/tx/${transactionSignature}?cluster=devnet-solana`,
    );

Run the script by clicking the `Run` button. You can then inspect the
transaction details on SolanaFM.

## Conclusion #

The reallocate instruction on the Token Extensions program offers a flexible
way to update existing Token Accounts with additional functionalities. This
instruction is useful for token owners who may not have foreseen the need for
certain extensions initially, but find themselves requiring these additional
features at a later time.

[Previous« How to use the Permanent Delegate
extension](/vi/developers/guides/token-extensions/permanent-delegate)[NextHow
to use the Required Memo token extension »](/vi/developers/guides/token-
extensions/required-memo)

##### Table of Contents

  * [Getting Started](/vi/developers/guides/token-extensions/reallocate#getting-started)
  * [Add Dependencies](/vi/developers/guides/token-extensions/reallocate#add-dependencies)
  * [Create Mint and Token Account](/vi/developers/guides/token-extensions/reallocate#create-mint-and-token-account)
  * [Build Instructions](/vi/developers/guides/token-extensions/reallocate#build-instructions)
  * [Send Transaction](/vi/developers/guides/token-extensions/reallocate#send-transaction)
  * [Conclusion](/vi/developers/guides/token-extensions/reallocate#conclusion)

[Scroll to Top](/vi/developers/guides/token-extensions/reallocate#)

[Edit Page](https://github.com/solana-foundation/developer-
content/tree/main/content/guides/token-extensions/reallocate.md)

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

![](https://t.co/1/i/adsct?bci=4&eci=3&event=%7B%7D&event_id=5e9a2ade-668a-4111-af1c-8acfdfd2c748&integration=gtm&p_id=Twitter&p_user_id=0&pl_id=4b901ff7-c14f-4b56-a11a-61c6c2194956&tw_document_href=https%3A%2F%2Fsolana.com%2Fvi%2Fdevelopers%2Fguides%2Ftoken-
extensions%2Freallocate&tw_iframe_status=0&txn_id=o6jgu&type=javascript&version=2.3.30)![](https://analytics.twitter.com/1/i/adsct?bci=4&eci=3&event=%7B%7D&event_id=5e9a2ade-668a-4111-af1c-8acfdfd2c748&integration=gtm&p_id=Twitter&p_user_id=0&pl_id=4b901ff7-c14f-4b56-a11a-61c6c2194956&tw_document_href=https%3A%2F%2Fsolana.com%2Fvi%2Fdevelopers%2Fguides%2Ftoken-
extensions%2Freallocate&tw_iframe_status=0&txn_id=o6jgu&type=javascript&version=2.3.30)

