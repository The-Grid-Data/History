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
content/tree/main/content/cookbook/wallets/restore-from-mnemonic.md)

# [How to Restore a Keypair from a
Mnemonic](/vi/developers/cookbook/wallets/restore-from-mnemonic)

Many wallet extensions use mnemonics to represent their secret keys. You can
convert the mnemonic to Keypairs for local testing.

## Restoring BIP39 format mnemonics #

restore-bip39-mnemonic.ts

    
    
    import { Keypair } from "@solana/web3.js";
    import * as bip39 from "bip39";
     
    const mnemonic =
      "pill tomorrow foster begin walnut borrow virtual kick shift mutual shoe scatter";
     
    // arguments: (mnemonic, password)
    const seed = bip39.mnemonicToSeedSync(mnemonic, "");
    const keypair = Keypair.fromSeed(seed.slice(0, 32));
     
    console.log(`${keypair.publicKey.toBase58()}`);
     
    // output: 5ZWj7a1f8tWkjBESHKgrLmXshuXxqeY9SYcfbshpAqPG

## Restoring BIP44 formant mnemonics #

restore-bip44-mnemonic.ts

    
    
    import { Keypair } from "@solana/web3.js";
    import { HDKey } from "micro-ed25519-hdkey";
    import * as bip39 from "bip39";
     
    const mnemonic =
      "neither lonely flavor argue grass remind eye tag avocado spot unusual intact";
     
    // arguments: (mnemonic, password)
    const seed = bip39.mnemonicToSeedSync(mnemonic, "");
    const hd = HDKey.fromMasterSeed(seed.toString("hex"));
     
    for (let i = 0; i < 10; i++) {
      const path = `m/44'/501'/${i}'/0'`;
      const keypair = Keypair.fromSeed(hd.derive(path).privateKey);
      console.log(`${path} => ${keypair.publicKey.toBase58()}`);
    }

[Previous« How to Generate Mnemonics for
Keypairs](/vi/developers/cookbook/wallets/generate-mnemonic)[NextHow to
Generate a Vanity Address »](/vi/developers/cookbook/wallets/generate-vanity-
address)

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

