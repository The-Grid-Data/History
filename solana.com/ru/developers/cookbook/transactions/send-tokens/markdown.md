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

[Home](/ru)>[Solana Cookbook](/ru/developers/cookbook)>Transactions

[Edit Page](https://github.com/solana-foundation/developer-
content/tree/main/content/cookbook/transactions/send-tokens.md)

# [How to Send Tokens](/ru/developers/cookbook/transactions/send-tokens)

Use the [Token Program](https://spl.solana.com/token) to transfer SPL Tokens.
In order to send a SPL token, you need to know its SPL token account address.
You can both get the address and send tokens with the following example.

send-tokens.ts

    
    
    import {
      Connection,
      clusterApiUrl,
      Keypair,
      LAMPORTS_PER_SOL,
      Transaction,
      sendAndConfirmTransaction,
    } from "@solana/web3.js";
    import {
      createMint,
      getOrCreateAssociatedTokenAccount,
      mintTo,
      createTransferInstruction,
    } from "@solana/spl-token";
     
    (async () => {
      // Connect to cluster
      const connection = new Connection(clusterApiUrl("devnet"), "confirmed");
     
      // Generate a new wallet keypair and airdrop SOL
      const fromWallet = Keypair.generate();
      const fromAirdropSignature = await connection.requestAirdrop(
        fromWallet.publicKey,
        LAMPORTS_PER_SOL,
      );
      // Wait for airdrop confirmation
      await connection.confirmTransaction(fromAirdropSignature);
     
      // Generate a new wallet to receive newly minted token
      const toWallet = Keypair.generate();
     
      // Create new token mint
      const mint = await createMint(
        connection,
        fromWallet,
        fromWallet.publicKey,
        null,
        9,
      );
     
      // Get the token account of the fromWallet Solana address, if it does not exist, create it
      const fromTokenAccount = await getOrCreateAssociatedTokenAccount(
        connection,
        fromWallet,
        mint,
        fromWallet.publicKey,
      );
     
      //get the token account of the toWallet Solana address, if it does not exist, create it
      const toTokenAccount = await getOrCreateAssociatedTokenAccount(
        connection,
        fromWallet,
        mint,
        toWallet.publicKey,
      );
     
      // Minting 1 new token to the "fromTokenAccount" account we just returned/created
      await mintTo(
        connection,
        fromWallet,
        mint,
        fromTokenAccount.address,
        fromWallet.publicKey,
        1000000000, // it's 1 token, but in lamports
        [],
      );
     
      // Add token transfer instructions to transaction
      const transaction = new Transaction().add(
        createTransferInstruction(
          fromTokenAccount.address,
          toTokenAccount.address,
          fromWallet.publicKey,
          1,
        ),
      );
     
      // Sign transaction, broadcast, and confirm
      await sendAndConfirmTransaction(connection, transaction, [fromWallet]);
    })();

[Previous« How to Send SOL](/ru/developers/cookbook/transactions/send-
sol)[NextHow to Calculate Transaction Cost
»](/ru/developers/cookbook/transactions/calculate-cost)

  * [Solana Cookbook](/ru/developers/cookbook)

    * Wallets
      * [How to Create a Keypair](/ru/developers/cookbook/wallets/create-keypair)
      * [How to Restore a Keypair](/ru/developers/cookbook/wallets/restore-keypair)
      * [How to Verify a Keypair](/ru/developers/cookbook/wallets/verify-keypair)
      * [How to Validate a Public Key](/ru/developers/cookbook/wallets/check-publickey)
      * [How to Generate Mnemonics for Keypairs](/ru/developers/cookbook/wallets/generate-mnemonic)
      * [How to Restore a Keypair from a Mnemonic](/ru/developers/cookbook/wallets/restore-from-mnemonic)
      * [How to Generate a Vanity Address](/ru/developers/cookbook/wallets/generate-vanity-address)
      * [How to Sign and Verify a Message](/ru/developers/cookbook/wallets/sign-message)
      * [How to Connect a Wallet with React](/ru/developers/cookbook/wallets/connect-wallet-react)
    * Transactions
      * [How to Send SOL](/ru/developers/cookbook/transactions/send-sol)
      * [How to Send Tokens](/ru/developers/cookbook/transactions/send-tokens)
      * [How to Calculate Transaction Cost](/ru/developers/cookbook/transactions/calculate-cost)
      * [How to Add a Memo to a Transaction](/ru/developers/cookbook/transactions/add-memo)
      * [How to Add Priority Fees to a Transaction](/ru/developers/cookbook/transactions/add-priority-fees)
      * [How to Optimize Compute Requested](/ru/developers/cookbook/transactions/optimize-compute)
    * Accounts
      * [How to Create an Account](/ru/developers/cookbook/accounts/create-account)
      * [How to Calculate Account Creation Cost](/ru/developers/cookbook/accounts/calculate-rent)
      * [How to Create a PDA's Account](/ru/developers/cookbook/accounts/create-pda-account)
      * [How to Sign with a PDA's Account](/ru/developers/cookbook/accounts/sign-with-pda)
      * [How to Close an Account](/ru/developers/cookbook/accounts/close-account)
      * [How to Get Account Balance](/ru/developers/cookbook/accounts/get-account-balance)

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

