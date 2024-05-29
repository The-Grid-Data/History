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
content/tree/main/content/cookbook/transactions/calculate-cost.md)

# [How to Calculate Transaction
Cost](/vi/developers/cookbook/transactions/calculate-cost)

The number of signatures a transaction requires are used to calculate the
transaction cost. As long as you are not creating an account, this will be the
base transaction cost. To find out more about costs to create an account,
check out [calculating rent costs](/vi/developers/cookbook/accounts/calculate-
rent).

calculate-cost.ts

    
    
    import {
      clusterApiUrl,
      Connection,
      Keypair,
      Message,
      SystemProgram,
      SYSTEM_INSTRUCTION_LAYOUTS,
      Transaction,
    } from "@solana/web3.js";
    import bs58 from "bs58";
     
    (async () => {
      // Connect to cluster
      const connection = new Connection(clusterApiUrl("devnet"), "confirmed");
     
      const payer = Keypair.generate();
      const recipient = Keypair.generate();
     
      const type = SYSTEM_INSTRUCTION_LAYOUTS.Transfer;
      const data = Buffer.alloc(type.layout.span);
      const layoutFields = Object.assign({ instruction: type.index });
      type.layout.encode(layoutFields, data);
     
      const recentBlockhash = await connection.getLatestBlockhash();
     
      const messageParams = {
        accountKeys: [
          payer.publicKey.toString(),
          recipient.publicKey.toString(),
          SystemProgram.programId.toString(),
        ],
        header: {
          numReadonlySignedAccounts: 0,
          numReadonlyUnsignedAccounts: 1,
          numRequiredSignatures: 1,
        },
        instructions: [
          {
            accounts: [0, 1],
            data: bs58.encode(data),
            programIdIndex: 2,
          },
        ],
        recentBlockhash: recentBlockhash.blockhash,
      };
     
      const message = new Message(messageParams);
     
      const fees = await connection.getFeeForMessage(message);
      console.log(`Estimated SOL transfer cost: ${fees.value} lamports`);
      // Estimated SOL transfer cost: 5000 lamports
    })();

[Previous« How to Send Tokens](/vi/developers/cookbook/transactions/send-
tokens)[NextHow to Add a Memo to a Transaction
»](/vi/developers/cookbook/transactions/add-memo)

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

