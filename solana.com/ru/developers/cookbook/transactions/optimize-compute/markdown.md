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
content/tree/main/content/cookbook/transactions/optimize-compute.md)

# [How to Optimize Compute
Requested](/ru/developers/cookbook/transactions/optimize-compute)

Optimizing the Compute Requested on a transaction is important to ensure that
the transaction is both processed in a timely manner as well as to avoid
paying too much in priority fees.

For more information about requesting optimal compute, [check out the full
guide](/ru/developers/guides/advanced/how-to-request-optimal-compute). You can
also find more information about [using priority
fees](/ru/developers/guides/advanced/how-to-use-priority-fees) in this
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
Transaction](/ru/developers/cookbook/transactions/add-priority-fees)[NextHow
to Create an Account »](/ru/developers/cookbook/accounts/create-account)

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

