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

# [How to use the Interest-Bearing extension](/vi/developers/guides/token-
extensions/interest-bearing-tokens)

updated 7 tháng 12, 2023

[beginner](/vi/developers/guides?difficulty=beginner)[token
2022](/vi/developers/guides?tags=token%202022)[token
extensions](/vi/developers/guides?tags=token%20extensions)

[![How to use the Interest-Bearing
extension](https://solana.com/_next/image?url=%2Fopengraph%2Fdevelopers%2Fguides%2Ftoken-
extensions%2Finterest-bearing-
tokens&w=3840&q=75)](/vi/developers/guides/token-extensions/interest-bearing-
tokens)

The `InterestBearingConfig` extension enables developers to set an interest
rate stored directly on the Mint Account. Interest is compounded continuously,
based on the network's timestamp.

In other words, the accrued interest is simply a visual UI conversion, but the
underlying token quantity remains unchanged. This design eliminates the need
for frequent rebase or update operations to adjust for accrued interest.

Info

Note that the interest accrual is only a
[calculation](https://github.com/solana-labs/solana-program-
library/blob/master/token/program-2022/src/extension/interest_bearing_mint/mod.rs#L85),
and does not involve minting new tokens.

In this guide, we'll walk through an example of using Solana Playground. Here
is the [final script](https://beta.solpg.io/65724856fb53fa325bfd0c53).

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
      updateRateInterestBearingMint,
      createInitializeInterestBearingMintInstruction,
      createInitializeMintInstruction,
      getMintLen,
      TOKEN_2022_PROGRAM_ID,
      amountToUiAmount,
      getInterestBearingMintConfigState,
      getMint,
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
    // Authority that can update the interest rate
    const rateAuthority = pg.wallet.keypair;
    // Interest rate basis points (100 = 1%)
    // Max value = 32,767 (i16)
    const rate = 32_767;

Next, let's determine the size of the new Mint Account and calculate the
minimum lamports needed for rent exemption.

    
    
    // Size of Mint Account with extension
    const mintLen = getMintLen([ExtensionType.InterestBearingConfig]);
    // Minimum lamports required for Mint Account
    const lamports = await connection.getMinimumBalanceForRentExemption(mintLen);

With Token Extensions, the size of the Mint Account will vary based on the
extensions enabled.

## Build Instructions #

Next, let's build the set of instructions to:

  * Create a new account
  * Initialize the `InterestBearingConfig` extension
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

Next, build the instruction to initialize the `InterestBearingConfig`
extension for the Mint Account.

    
    
    // Instruction to initialize the InterestBearingConfig Extension
    const initializeInterestBearingMintInstruction =
      createInitializeInterestBearingMintInstruction(
        mint, // Mint Account address
        rateAuthority.publicKey, // Designated Rate Authority
        rate, // Interest rate basis points
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
network. This will create a Mint Account with the `InterestBearingConfig`
extension enabled.

    
    
    // Add instructions to new transaction
    const transaction = new Transaction().add(
      createAccountInstruction,
      initializeInterestBearingMintInstruction,
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

## Update Interest Rate #

The designated Rate Authority can then update the interest rate on the Mint
Account at any time.

    
    
    // New interest rate in basis points
    const updateRate = 0;
    // Update interest rate on Mint Account
    transactionSignature = await updateRateInterestBearingMint(
      connection,
      payer, // Transaction fee payer
      mint, // Mint Account Address
      rateAuthority, // Designated Rate Authority
      updateRate, // New interest rate
      undefined, // Additional signers
      undefined, // Confirmation options
      TOKEN_2022_PROGRAM_ID, // Token Extension Program ID
    );
     
    console.log(
      "\nUpdate Rate:",
      `https://solana.fm/tx/${transactionSignature}?cluster=devnet-solana`,
    );

## Fetch Interest Config State #

Next, let's check the updated interest rate by fetching the Mint Account data.

    
    
    // Fetch Mint Account data
    const mintAccount = await getMint(
      connection,
      mint, // Mint Account Address
      undefined, // Optional commitment
      TOKEN_2022_PROGRAM_ID, // Token Extension Program ID
    );
     
    // Get Interest Config for Mint Account
    const interestBearingMintConfig = await getInterestBearingMintConfigState(
      mintAccount, // Mint Account data
    );
     
    console.log(
      "\nMint Config:",
      JSON.stringify(interestBearingMintConfig, null, 2),
    );

## Calculate Accrued Interest #

Lastly, let's calculate the interest accrued for a given amount. Note that
this calculation can be performed independently for any amount, without the
need for minting tokens.

    
    
    // Wait 1 second
    sleep(1000);
     
    // Amount to convert
    const amount = 100;
    // Convert amount to UI amount with accrued interest
    const uiAmount = await amountToUiAmount(
      connection, // Connection to the Solana cluster
      payer, // Account that will transfer lamports for the transaction
      mint, // Address of the Mint account
      amount, // Amount to be converted
      TOKEN_2022_PROGRAM_ID, // Token Extension Program ID
    );
     
    console.log("\nAmount with Accrued Interest:", uiAmount);

Run the script by clicking the `Run` button. You can then inspect the
transaction details on SolanaFM and view the data logged in the Playground
terminal.

Caution

Interest is continuously compounded based on the timestamp in the network. Due
to drift that may occur in the network timestamp, the accumulated interest
could be lower than the expected value. Thankfully, this is rare.

You should see an output similar to snippet below, where the decimal values
indicate the interest that has accumulated:

    
    
    Mint Config: {
      "rateAuthority": "3z9vL1zjN6qyAFHhHQdWYRTFAcy69pJydkZmSFBKHg1R",
      "initializationTimestamp": 1702321738,
      "preUpdateAverageRate": 32767,
      "lastUpdateTimestamp": 1702321740,
      "currentRate": 0
    }
     
    Amount with Accrued Interest: 1.000000207670422

## Conclusion #

The `InterestBearingConfig` extension introduces a simple mechanism for tokens
to increase or decrease in value over time. By seamlessly integrating tools
commonly found in traditional finance, this innovation broadens Solana's
capabilities, bridging the gap between conventional financial instruments and
the world of blockchain.

[Previous« How to use the Immutable Owner
extension](/vi/developers/guides/token-extensions/immutable-owner)[NextHow to
use the Metadata Pointer extension »](/vi/developers/guides/token-
extensions/metadata-pointer)

##### Table of Contents

  * [Getting Started](/vi/developers/guides/token-extensions/interest-bearing-tokens#getting-started)
  * [Add Dependencies](/vi/developers/guides/token-extensions/interest-bearing-tokens#add-dependencies)
  * [Mint Setup](/vi/developers/guides/token-extensions/interest-bearing-tokens#mint-setup)
  * [Build Instructions](/vi/developers/guides/token-extensions/interest-bearing-tokens#build-instructions)
  * [Send Transaction](/vi/developers/guides/token-extensions/interest-bearing-tokens#send-transaction)
  * [Update Interest Rate](/vi/developers/guides/token-extensions/interest-bearing-tokens#update-interest-rate)
  * [Fetch Interest Config State](/vi/developers/guides/token-extensions/interest-bearing-tokens#fetch-interest-config-state)
  * [Calculate Accrued Interest](/vi/developers/guides/token-extensions/interest-bearing-tokens#calculate-accrued-interest)
  * [Conclusion](/vi/developers/guides/token-extensions/interest-bearing-tokens#conclusion)

[Scroll to Top](/vi/developers/guides/token-extensions/interest-bearing-
tokens#)

[Edit Page](https://github.com/solana-foundation/developer-
content/tree/main/content/guides/token-extensions/interest-bearing-tokens.md)

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

