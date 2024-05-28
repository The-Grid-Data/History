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

[Home](/de)>[Solana Cookbook](/de/developers/cookbook)>Wallets

[Edit Page](https://github.com/solana-foundation/developer-
content/tree/main/content/cookbook/wallets/restore-keypair.md)

# [How to Restore a Keypair](/de/developers/cookbook/wallets/restore-keypair)

If you already have your secret key or bytes, you can get your Keypair from
the secret to test out your dApp.

## From Bytes #

restore-keypair-from-bytes.ts

    
    
    import { Keypair } from "@solana/web3.js";
     
    const keypair = Keypair.fromSecretKey(
      Uint8Array.from([
        174, 47, 154, 16, 202, 193, 206, 113, 199, 190, 53, 133, 169, 175, 31, 56,
        222, 53, 138, 189, 224, 216, 117, 173, 10, 149, 53, 45, 73, 251, 237, 246,
        15, 185, 186, 82, 177, 240, 148, 69, 241, 227, 167, 80, 141, 89, 240, 121,
        121, 35, 172, 247, 68, 251, 226, 218, 48, 63, 176, 109, 168, 89, 238, 135,
      ]),
    );

## From base58 String #

restore-keypair-from-base58.ts

    
    
    import { Keypair } from "@solana/web3.js";
    import * as bs58 from "bs58";
     
    const keypair = Keypair.fromSecretKey(
      bs58.decode(
        "5MaiiCavjCmn9Hs1o3eznqDEhRwxo7pXiAYez7keQUviUkauRiTMD8DrESdrNjN8zd9mTmVhRvBJeg5vhyvgrAhG",
      ),
    );

[Previous« How to Create a Keypair](/de/developers/cookbook/wallets/create-
keypair)[NextHow to Verify a Keypair
»](/de/developers/cookbook/wallets/verify-keypair)

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

