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

[Home](/vi)>[Solana Cookbook](/vi/developers/cookbook)>Wallets

[Edit Page](https://github.com/solana-foundation/developer-
content/tree/main/content/cookbook/wallets/check-publickey.md)

# [How to Validate a Public Key](/vi/developers/cookbook/wallets/check-
publickey)

In certain special cases (e.g. a Program Derived Address), public keys may not
have a private key associated with them. You can check this by looking to see
if the public key lies on the ed25519 curve. Only public keys that lie on the
curve can be controlled by users with wallets.

check-public-key.ts

    
    
    import { PublicKey } from "@solana/web3.js";
     
    // Note that Keypair.generate() will always give a public key that is valid for users
     
    // Valid public key
    const key = new PublicKey("5oNDL3swdJJF1g9DzJiZ4ynHXgszjAEpUkxVYejchzrY");
    // Lies on the ed25519 curve and is suitable for users
    console.log(PublicKey.isOnCurve(key.toBytes()));
     
    // Valid public key
    const offCurveAddress = new PublicKey(
      "4BJXYkfvg37zEmBbsacZjeQDpTNx91KppxFJxRqrz48e",
    );
     
    // Not on the ed25519 curve, therefore not suitable for users
    console.log(PublicKey.isOnCurve(offCurveAddress.toBytes()));
     
    // Not a valid public key
    const errorPubkey = new PublicKey("testPubkey");

[Previous« How to Verify a Keypair](/vi/developers/cookbook/wallets/verify-
keypair)[NextHow to Generate Mnemonics for Keypairs
»](/vi/developers/cookbook/wallets/generate-mnemonic)

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

