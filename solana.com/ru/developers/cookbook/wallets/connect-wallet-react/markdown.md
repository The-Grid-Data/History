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
content/tree/main/content/cookbook/wallets/connect-wallet-react.md)

# [How to Connect a Wallet with
React](/ru/developers/cookbook/wallets/connect-wallet-react)

Solana's [wallet-adapter](https://github.com/anza-xyz/wallet-adapter) library
make it easy to manage wallet connections client-side. For a full length
guide, check out [how to add wallet-adapter to
nextjs](/ru/developers/guides/wallets/add-solana-wallet-adapter-to-nextjs).

## How to Connect to a Wallet with React #

For quick setup with React use:

    
    
    npx create-solana-dapp <app-name>

For manual setup, run the following command to install the required
dependencies:

    
    
    npm install --save \
        @solana/wallet-adapter-base \
        @solana/wallet-adapter-react \
        @solana/wallet-adapter-react-ui \
        @solana/wallet-adapter-wallets \
        @solana/web3.js \
        react

The `WalletProvider` can than be setup to connect to a user's wallet and later
send transactions.

    
    
    import React, { FC, useMemo } from 'react';
    import { ConnectionProvider, WalletProvider } from '@solana/wallet-adapter-react';
    import { WalletAdapterNetwork } from '@solana/wallet-adapter-base';
    import { UnsafeBurnerWalletAdapter } from '@solana/wallet-adapter-wallets';
    import {
        WalletModalProvider,
        WalletDisconnectButton,
        WalletMultiButton
    } from '@solana/wallet-adapter-react-ui';
    import { clusterApiUrl } from '@solana/web3.js';
     
    // Default styles that can be overridden by your app
    require('@solana/wallet-adapter-react-ui/styles.css');
     
    export const Wallet: FC = () => {
        // The network can be set to 'devnet', 'testnet', or 'mainnet-beta'.
        const network = WalletAdapterNetwork.Devnet;
     
        // You can also provide a custom RPC endpoint.
        const endpoint = useMemo(() => clusterApiUrl(network), [network]);
     
        const wallets = useMemo(
            () => [
                /**
                 * Wallets that implement either of these standards will be available automatically.
                 *
                 *   - Solana Mobile Stack Mobile Wallet Adapter Protocol
                 *     (https://github.com/solana-mobile/mobile-wallet-adapter)
                 *   - Solana Wallet Standard
                 *     (https://github.com/anza-xyz/wallet-standard)
                 *
                 * If you wish to support a wallet that supports neither of those standards,
                 * instantiate its legacy wallet adapter here. Common legacy adapters can be found
                 * in the npm package `@solana/wallet-adapter-wallets`.
                 */
                new UnsafeBurnerWalletAdapter(),
            ],
            // eslint-disable-next-line react-hooks/exhaustive-deps
            [network]
        );
     
        return (
            <ConnectionProvider endpoint={endpoint}>
                <WalletProvider wallets={wallets} autoConnect>
                    <WalletModalProvider>
                        <WalletMultiButton />
                        <WalletDisconnectButton />
                        { /* Your app's components go here, nested within the context providers. */ }
                    </WalletModalProvider>
                </WalletProvider>
            </ConnectionProvider>
        );
    };

[Previous« How to Sign and Verify a
Message](/ru/developers/cookbook/wallets/sign-message)[NextHow to Send SOL
»](/ru/developers/cookbook/transactions/send-sol)

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

