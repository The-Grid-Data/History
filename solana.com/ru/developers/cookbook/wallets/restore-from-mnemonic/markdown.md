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

[Home](/ru)>[Solana Cookbook](/ru/developers/cookbook)>Wallets

[Edit Page](https://github.com/solana-foundation/developer-
content/tree/main/content/cookbook/wallets/restore-from-mnemonic.md)

# [How to Restore a Keypair from a
Mnemonic](/ru/developers/cookbook/wallets/restore-from-mnemonic)

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
Keypairs](/ru/developers/cookbook/wallets/generate-mnemonic)[NextHow to
Generate a Vanity Address »](/ru/developers/cookbook/wallets/generate-vanity-
address)

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

