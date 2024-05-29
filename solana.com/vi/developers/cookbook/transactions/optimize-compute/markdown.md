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
content/tree/main/content/cookbook/transactions/optimize-compute.md)

# [How to Optimize Compute
Requested](/vi/developers/cookbook/transactions/optimize-compute)

Optimizing the Compute Requested on a transaction is important to ensure that
the transaction is both processed in a timely manner as well as to avoid
paying too much in priority fees.

For more information about requesting optimal compute, [check out the full
guide](/vi/developers/guides/advanced/how-to-request-optimal-compute). You can
also find more information about [using priority
fees](/vi/developers/guides/advanced/how-to-use-priority-fees) in this
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
Transaction](/vi/developers/cookbook/transactions/add-priority-fees)[NextHow
to Create an Account »](/vi/developers/cookbook/accounts/create-account)

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

