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
content/tree/main/content/cookbook/wallets/connect-wallet-react.md)

# [How to Connect a Wallet with
React](/vi/developers/cookbook/wallets/connect-wallet-react)

Solana's [wallet-adapter](https://github.com/anza-xyz/wallet-adapter) library
make it easy to manage wallet connections client-side. For a full length
guide, check out [how to add wallet-adapter to
nextjs](/vi/developers/guides/wallets/add-solana-wallet-adapter-to-nextjs).

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
Message](/vi/developers/cookbook/wallets/sign-message)[NextHow to Send SOL
»](/vi/developers/cookbook/transactions/send-sol)

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

