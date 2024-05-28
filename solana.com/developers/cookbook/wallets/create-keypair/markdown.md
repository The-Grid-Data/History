This website uses cookies to offer you a better browsing experience. Find out
more on how we use cookies.

Opt-out[Details](/privacy-policy#collection-of-information)

Accept

[![Solana](/_next/static/media/logotype-dark.f79d530d.svg)](/)

  * Learn
  * Developers
  * Solutions
  * Network
  * Community

Search```K`

[Documentation](/docs)[RPC
API](/docs/rpc)[Cookbook](/developers/cookbook)[Guides](/developers/guides)[Terminology](/docs/terminology)

[Home](/)>[Solana Cookbook](/developers/cookbook)>Wallets

[Edit Page](https://github.com/solana-foundation/developer-
content/tree/main/content/cookbook/wallets/create-keypair.md)

# [How to Create a Keypair](/developers/cookbook/wallets/create-keypair)

Any transaction on the Solana blockchain requires a keypair or wallet. If you
are [connecting to a wallet](/developers/cookbook/wallets/connect-wallet-
react), you do not need to worry about the keypair. Otherwise a keypair must
be generated for signing transactions.

    
    
    import { Keypair } from "@solana/web3.js";
     
    const keypair = Keypair.generate();

[Previous« Solana Cookbook](/developers/cookbook)[NextHow to Restore a Keypair
»](/developers/cookbook/wallets/restore-keypair)

  * [Solana Cookbook](/developers/cookbook)

    * Wallets
      * [How to Create a Keypair](/developers/cookbook/wallets/create-keypair)
      * [How to Restore a Keypair](/developers/cookbook/wallets/restore-keypair)
      * [How to Verify a Keypair](/developers/cookbook/wallets/verify-keypair)
      * [How to Validate a Public Key](/developers/cookbook/wallets/check-publickey)
      * [How to Generate Mnemonics for Keypairs](/developers/cookbook/wallets/generate-mnemonic)
      * [How to Restore a Keypair from a Mnemonic](/developers/cookbook/wallets/restore-from-mnemonic)
      * [How to Generate a Vanity Address](/developers/cookbook/wallets/generate-vanity-address)
      * [How to Sign and Verify a Message](/developers/cookbook/wallets/sign-message)
      * [How to Connect a Wallet with React](/developers/cookbook/wallets/connect-wallet-react)
    * Transactions
      * [How to Send SOL](/developers/cookbook/transactions/send-sol)
      * [How to Send Tokens](/developers/cookbook/transactions/send-tokens)
      * [How to Calculate Transaction Cost](/developers/cookbook/transactions/calculate-cost)
      * [How to Add a Memo to a Transaction](/developers/cookbook/transactions/add-memo)
      * [How to Add Priority Fees to a Transaction](/developers/cookbook/transactions/add-priority-fees)
      * [How to Optimize Compute Requested](/developers/cookbook/transactions/optimize-compute)
    * Accounts
      * [How to Create an Account](/developers/cookbook/accounts/create-account)
      * [How to Calculate Account Creation Cost](/developers/cookbook/accounts/calculate-rent)
      * [How to Create a PDA's Account](/developers/cookbook/accounts/create-pda-account)
      * [How to Sign with a PDA's Account](/developers/cookbook/accounts/sign-with-pda)
      * [How to Close an Account](/developers/cookbook/accounts/close-account)
      * [How to Get Account Balance](/developers/cookbook/accounts/get-account-balance)

Managed by

[](/)

[](/youtube)[](/twitter)[](/discord)[](/reddit)[](/github)[](/telegram)

© 2024 Solana Foundation. All rights reserved.

Solana

  * [Grants](https://solana.org/grants)
  * [Break Solana](https://break.solana.com/)
  * [Media Kit](/branding)
  * [Careers](https://jobs.solana.com/)
  * [Disclaimer](/tos)
  * [Privacy Policy](/privacy-policy)

Get Connected

  * [Ecosystem](/ecosystem)
  * [Blog](/news)
  * [Newsletter](/newsletter)

en

© 2024 Solana Foundation. All rights reserved.

