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
content/tree/main/content/cookbook/wallets/sign-message.md)

# [How to Sign and Verify a Message](/vi/developers/cookbook/wallets/sign-
message)

The primary function of a keypair is to sign messages and enable verification
of the signature. Verification of a signature allows the recipient to be sure
that the data was signed by the owner of a specific private key.

To do so, we can use the [TweetNaCl](https://www.npmjs.com/package/tweetnacl)
crypto library:

sign-message.ts

    
    
    import { Keypair } from "@solana/web3.js";
    import nacl from "tweetnacl";
    import { decodeUTF8 } from "tweetnacl-util";
     
    const keypair = Keypair.fromSecretKey(
      Uint8Array.from([
        174, 47, 154, 16, 202, 193, 206, 113, 199, 190, 53, 133, 169, 175, 31, 56,
        222, 53, 138, 189, 224, 216, 117, 173, 10, 149, 53, 45, 73, 251, 237, 246,
        15, 185, 186, 82, 177, 240, 148, 69, 241, 227, 167, 80, 141, 89, 240, 121,
        121, 35, 172, 247, 68, 251, 226, 218, 48, 63, 176, 109, 168, 89, 238, 135,
      ]),
    );
     
    const message = "The quick brown fox jumps over the lazy dog";
    const messageBytes = decodeUTF8(message);
     
    const signature = nacl.sign.detached(messageBytes, keypair.secretKey);
    const result = nacl.sign.detached.verify(
      messageBytes,
      signature,
      keypair.publicKey.toBytes(),
    );
     
    console.log(result);

[Previous« How to Generate a Vanity
Address](/vi/developers/cookbook/wallets/generate-vanity-address)[NextHow to
Connect a Wallet with React »](/vi/developers/cookbook/wallets/connect-wallet-
react)

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

