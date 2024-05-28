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

[Home](/de)>[Solana Cookbook](/de/developers/cookbook)>Transactions

[Edit Page](https://github.com/solana-foundation/developer-
content/tree/main/content/cookbook/transactions/optimize-compute.md)

# [How to Optimize Compute
Requested](/de/developers/cookbook/transactions/optimize-compute)

Optimizing the Compute Requested on a transaction is important to ensure that
the transaction is both processed in a timely manner as well as to avoid
paying too much in priority fees.

For more information about requesting optimal compute, [check out the full
guide](/de/developers/guides/advanced/how-to-request-optimal-compute). You can
also find more information about [using priority
fees](/de/developers/guides/advanced/how-to-use-priority-fees) in this
detailed guide.

optimize-compute.ts

    
    
    // import { ... } from "@solana/web3.js"
     
    async function buildOptimalTransaction(
      connection: Connection,
      instructions: Array<TransactionInstruction>,
      signer: Signer,
      lookupTables: Array<AddressLookupTableAccount>,
    ) {
      const [microLamports, units, recentBlockhash] = await Promise.all([
        100 /* Get optimal priority fees - https://solana.com/developers/guides/advanced/how-to-use-priority-fees*/,
        getSimulationComputeUnits(
          connection,
          instructions,
          signer.publicKey,
          lookupTables,
        ),
        connection.getLatestBlockhash(),
      ]);
     
      instructions.unshift(
        ComputeBudgetProgram.setComputeUnitPrice({ microLamports }),
      );
      if (units) {
        // probably should add some margin of error to units
        instructions.unshift(ComputeBudgetProgram.setComputeUnitLimit({ units }));
      }
      return {
        transaction: new VersionedTransaction(
          new TransactionMessage({
            instructions,
            recentBlockhash: recentBlockhash.blockhash,
            payerKey: signer.publicKey,
          }).compileToV0Message(lookupTables),
        ),
        recentBlockhash,
      };
    }

[Previous« How to Add Priority Fees to a
Transaction](/de/developers/cookbook/transactions/add-priority-fees)[NextHow
to Create an Account »](/de/developers/cookbook/accounts/create-account)

  * [Solana Cookbook](/de/developers/cookbook)

    * Wallets
      * [How to Create a Keypair](/de/developers/cookbook/wallets/create-keypair)
      * [How to Restore a Keypair](/de/developers/cookbook/wallets/restore-keypair)
      * [How to Verify a Keypair](/de/developers/cookbook/wallets/verify-keypair)
      * [How to Validate a Public Key](/de/developers/cookbook/wallets/check-publickey)
      * [How to Generate Mnemonics for Keypairs](/de/developers/cookbook/wallets/generate-mnemonic)
      * [How to Restore a Keypair from a Mnemonic](/de/developers/cookbook/wallets/restore-from-mnemonic)
      * [How to Generate a Vanity Address](/de/developers/cookbook/wallets/generate-vanity-address)
      * [How to Sign and Verify a Message](/de/developers/cookbook/wallets/sign-message)
      * [How to Connect a Wallet with React](/de/developers/cookbook/wallets/connect-wallet-react)
    * Transactions
      * [How to Send SOL](/de/developers/cookbook/transactions/send-sol)
      * [How to Send Tokens](/de/developers/cookbook/transactions/send-tokens)
      * [How to Calculate Transaction Cost](/de/developers/cookbook/transactions/calculate-cost)
      * [How to Add a Memo to a Transaction](/de/developers/cookbook/transactions/add-memo)
      * [How to Add Priority Fees to a Transaction](/de/developers/cookbook/transactions/add-priority-fees)
      * [How to Optimize Compute Requested](/de/developers/cookbook/transactions/optimize-compute)
    * Accounts
      * [How to Create an Account](/de/developers/cookbook/accounts/create-account)
      * [How to Calculate Account Creation Cost](/de/developers/cookbook/accounts/calculate-rent)
      * [How to Create a PDA's Account](/de/developers/cookbook/accounts/create-pda-account)
      * [How to Sign with a PDA's Account](/de/developers/cookbook/accounts/sign-with-pda)
      * [How to Close an Account](/de/developers/cookbook/accounts/close-account)
      * [How to Get Account Balance](/de/developers/cookbook/accounts/get-account-balance)

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

