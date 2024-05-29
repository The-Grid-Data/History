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

[Home](/vi)>[Solana Cookbook](/vi/developers/cookbook)>Transactions

[Edit Page](https://github.com/solana-foundation/developer-
content/tree/main/content/cookbook/transactions/add-priority-fees.md)

# [How to Add Priority Fees to a
Transaction](/vi/developers/cookbook/transactions/add-priority-fees)

Transaction (TX) priority is achieved by paying a Prioritization Fee in
addition to the Base Fee. By default the compute budget is the product of
200,000 Compute Units (CU) * number of instructions, with a max of 1.4M CU.
The Base Fee is 5,000 Lamports per signature. A microLamport is 0.000001
Lamports.

Info

You can find a detailed guide here on [how to use priority
fees](/vi/developers/guides/advanced/how-to-use-priority-fees).

The total compute budget or Prioritization Fee for a single TX can be changed
by adding instructions from the ComputeBudgetProgram.

`ComputeBudgetProgram.setComputeUnitPrice({ microLamports: number })` will add
a Prioritization Fee above the Base Fee (5,000 Lamports). The value provided
in microLamports will be multiplied by the CU budget to determine the
Prioritization Fee in Lamports. For example, if your CU budget is 1M CU, and
you add 1 microLamport/CU, the Prioritization Fee will be 1 Lamport (1M *
0.000001). The total fee will then be 5001 Lamports.

Use `ComputeBudgetProgram.setComputeUnitLimit({ units: number })` to set the
new compute budget. The value provided will replace the default value.
Transactions should request the minimum amount of CU required for execution to
maximize throughput, or minimize fees.

add-priority-fees.ts

    
    
    import { BN } from "@coral-xyz/anchor";
    import {
      Keypair,
      Connection,
      LAMPORTS_PER_SOL,
      sendAndConfirmTransaction,
      ComputeBudgetProgram,
      SystemProgram,
      Transaction,
    } from "@solana/web3.js";
     
    (async () => {
      const payer = Keypair.generate();
      const toAccount = Keypair.generate().publicKey;
     
      const connection = new Connection("http://127.0.0.1:8899", "confirmed");
     
      const airdropSignature = await connection.requestAirdrop(
        payer.publicKey,
        LAMPORTS_PER_SOL,
      );
     
      await connection.confirmTransaction(airdropSignature);
     
      // request a specific compute unit budget
      const modifyComputeUnits = ComputeBudgetProgram.setComputeUnitLimit({
        units: 1000000,
      });
     
      // set the desired priority fee
      const addPriorityFee = ComputeBudgetProgram.setComputeUnitPrice({
        microLamports: 1,
      });
     
      // Total fee will be 5,001 Lamports for 1M CU
      const transaction = new Transaction()
        .add(modifyComputeUnits)
        .add(addPriorityFee)
        .add(
          SystemProgram.transfer({
            fromPubkey: payer.publicKey,
            toPubkey: toAccount,
            lamports: 10000000,
          }),
        );
     
      const signature = await sendAndConfirmTransaction(connection, transaction, [
        payer,
      ]);
      console.log(signature);
     
      const result = await connection.getParsedTransaction(signature);
      console.log(result);
    })();

[Previous« How to Add a Memo to a
Transaction](/vi/developers/cookbook/transactions/add-memo)[NextHow to
Optimize Compute Requested »](/vi/developers/cookbook/transactions/optimize-
compute)

  * [Solana Cookbook](/vi/developers/cookbook)

    * Wallets
      * [How to Create a Keypair](/vi/developers/cookbook/wallets/create-keypair)
      * [How to Restore a Keypair](/vi/developers/cookbook/wallets/restore-keypair)
      * [How to Verify a Keypair](/vi/developers/cookbook/wallets/verify-keypair)
      * [How to Validate a Public Key](/vi/developers/cookbook/wallets/check-publickey)
      * [How to Generate Mnemonics for Keypairs](/vi/developers/cookbook/wallets/generate-mnemonic)
      * [How to Restore a Keypair from a Mnemonic](/vi/developers/cookbook/wallets/restore-from-mnemonic)
      * [How to Generate a Vanity Address](/vi/developers/cookbook/wallets/generate-vanity-address)
      * [How to Sign and Verify a Message](/vi/developers/cookbook/wallets/sign-message)
      * [How to Connect a Wallet with React](/vi/developers/cookbook/wallets/connect-wallet-react)
    * Transactions
      * [How to Send SOL](/vi/developers/cookbook/transactions/send-sol)
      * [How to Send Tokens](/vi/developers/cookbook/transactions/send-tokens)
      * [How to Calculate Transaction Cost](/vi/developers/cookbook/transactions/calculate-cost)
      * [How to Add a Memo to a Transaction](/vi/developers/cookbook/transactions/add-memo)
      * [How to Add Priority Fees to a Transaction](/vi/developers/cookbook/transactions/add-priority-fees)
      * [How to Optimize Compute Requested](/vi/developers/cookbook/transactions/optimize-compute)
    * Accounts
      * [How to Create an Account](/vi/developers/cookbook/accounts/create-account)
      * [How to Calculate Account Creation Cost](/vi/developers/cookbook/accounts/calculate-rent)
      * [How to Create a PDA's Account](/vi/developers/cookbook/accounts/create-pda-account)
      * [How to Sign with a PDA's Account](/vi/developers/cookbook/accounts/sign-with-pda)
      * [How to Close an Account](/vi/developers/cookbook/accounts/close-account)
      * [How to Get Account Balance](/vi/developers/cookbook/accounts/get-account-balance)

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

