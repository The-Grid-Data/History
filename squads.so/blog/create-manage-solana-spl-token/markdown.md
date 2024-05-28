s m a r t

w a l l e t s

a t

l i g h t s p e e d

[Squads](../)

[Protocol](../protocol)

[Extension](../extension)

[Use Cases](../use-cases)

[About](https://www.sqds.io/)

[Blog](../blog)

[](../)

Get started

# Create and Manage Solana (SPL) Tokens with Squads

Dec 13, 2023

![how-to-create-mint-solana-spl-token-burn-mint-authority-solana-multisig-
squads-spl-token-
management](https://framerusercontent.com/images/YeQMBSozonTrL7s0M1gHdvMHtCw.png)

This short article outlines how to create a Solana SPL token in just two steps
and manage it with Squads - the Solana platform built for teams and
organizations with multi-signature (multisig) functionality at its core.

With an easy-to-use interface and costs as low as 0.02 SOL, Squads is the most
suited solution for token management, with no developer skills required to
mint an SPL token, secure the Mint and Freeze authority keys, or manage its
supply.

## Step 1: Set up your Squad

![solana-multisig-wallet-squads-create-solana-multisig-best-wallet-spl-tokens-
multi-
signature](https://framerusercontent.com/images/uaEacUo2KhAQiwzenSGQZINk0.png)

The first step is to set up a [multisig](https://squads.so/blog/what-are-
multisig-wallets) on Squads that will be used to create and then manage the
token.

From [app.squads.so](https://app.squads.so/) connect a Solana wallet to the
platform and click "Create Squad". Enter the Squad details, such as name,
profile picture, and description. Add members to your Squad using their public
keys (wallet addresses) and set a confirmation threshold, which is the number
of approvals needed from owners for transactions to be executed. You can add
an unlimited number of initial owners, but we recommend keeping it below 20
for the optimal experience. Review your Squad's details and confirm.

The deployment cost ranges between 0.0025 - 0.0045 SOL, depending on the
number of initial owners. This fee includes the Solana rent fee and a 0.001
SOL deposit into your Squad. Once deployed, you'll be directed to your Squad
where you can start the process to mint your Solana token.

### Why Squads for Token Management

![token-management-spl-solana-tokens-multisig-dao-mint-burn-token-authority-
solana-
squads](https://framerusercontent.com/images/bGxyZ2K3S9iZt8oppXSKpEMw.png)

Squads is an ideal choice for token management due to its multisig
functionality, which enables collective management for teams and organizations
and enhances the overall security of managing a Solana token. By utilizing
multi-signature, the authority over the token is distributed among a group of
trusted individuals, ensuring that no single point of failure exists, and
minimizing the risk of lost or compromised keys. This decentralized approach
not only provides a transparent method for managing tokens but also allows for
greater confidence among the project stakeholders: every action that involves
the token, such as mint and burn of the supply, requires approval from members
of the Squad rather than from a single individual as it would be the case with
a hot/cold wallet.

Moreover, Squads is immutable. This means that the upgrade authority of the
Squads program has been burned, ensuring that no one can modify it to move or
access your funds.

## Step 2: Create a New SPL Token from your Squads Multisig

![solana-spl-token-mint-create-solana-token-generate-solana-spl-contract-
address-transfer-token-authority-multisig-
wallet](https://framerusercontent.com/images/K4fRCb9sPEqVzD88mOytutpFpI.png)

To create a token from a Squad, follow these steps:

  1. Navigate to the "Token Manager" tab and click on the "+Add Token" button. Select the "Create Token" option in the pop-up.

  2. Fill in the required information in the pop-up window, including token name, symbol, freeze authority (optional) and description (optional).

  3. Click "Next," insert a transaction description (optional) and then click the "Create" button to initiate the transaction.

  4. Once the transaction is executed, your newly created token will appear under the "Token Manager" tab.

And that's it. From this point forward, the token authorities (Mint and
Freeze) are secured within your multisig. Any interaction with the token such
as managing its supply or freezing/unfreezing accounts will require multiple
approvals from the Squad's members.

### What are SPL tokens

SPL tokens are a type of digital asset on the Solana blockchain. SPL stands
for Solana Program Library, which is a collection of programs designed to
support the creation and management of tokens on Solana. SPL tokens are
similar to ERC-20 tokens on the Ethereum blockchain, as they follow a specific
standard for creating, transferring, and managing custom tokens.

Once created, these tokens can be used within dApps, traded on DEXs, or used
for other purposes within the Solana ecosystem. Here are a few examples of SPL
tokens: JTO, PYTH, BONK, MNDE, HBB, RLB, SAMO, USDH, AURY, ORCA.

## Token Management: Mint, Burn, and Freeze

![solana-spl-token-burn-management-create-mint-solana-token-
multisig](https://framerusercontent.com/images/DBnUovX6YOM8OBVsIur018L9XFE.png)

To mint and burn token supply from a Squad, click the "Token Manager" tab,
find the token you want to mint, and click on "Actions > Mint/Burn". Specify
the amount of tokens you want to mint/burn, add a description (optional), and
launch the transaction. After the transaction has been executed, your minted
token will appear in your Squad vault.

Squads also allows projects to freeze and unfreeze accounts holding their
tokens directly through the interface. This can be useful for RWA companies
that need to comply with regulators. Additionally, both the Mint and Freeze
authorities can be transferred to another wallet or burned.

## How to Transfer an Existing SPL Token Authority to Squads

![solana-spl-token-mint-authority-secure-no-code-transfer-spl-authority-
multisig](https://framerusercontent.com/images/F76c5mgMmgZNv2kxFNV1phrP3lc.png)

Projects can transfer their token authority to a Squads multisig if they
already have an existing token at any time. To transfer the authority of an
existing token to your multisig, navigate to the "Token Manager" tab, click
the "+Add Token" button, and select the "Transfer token authority to your
Squad" option. Insert the current token authority address, copy and paste the
code into your CLI, which should be run by the current authority, and click
"Change authority". Your token authority is now securely stored in your Squad.

  

### About Squads

Squads is a crypto company operations platform that simplifies management of
developer and treasury assets for teams building on Solana and SVM. Open
source, formally verified, immutable, Squads enables teams to secure their on-
chain assets in a multisig and jointly manage them.

**Learn more**

 _Get Started:_[_https://app.squads.so_](https://app.squads.so/squads) _  
Squads:_[_https://squads.so/blog/what-is-squads_](https://squads.so/blog/what-
is-squads) _  
Squads Protocol:_[_https://squads.so/blog/solana-svm-smart-contract-wallet-
infrastructure_](https://squads.so/blog/solana-svm-smart-contract-wallet-
infrastructure) _  
Code:_[_https://github.com/Squads-Protocol/v4_](https://github.com/Squads-
Protocol/v4)

  

Continue reading

[![why-use-squads-why-multisig-solana-multisig-wallet-squads-leading-multi-
signature-solution-mpc-alternative-solana-secure-sol-for-company-squads-
protocol-
audited](https://framerusercontent.com/images/6S99P6ebVfLr6xzbo831NVDrCM.png)Why
Do Enterprises Use Squads For Their On-chain OperationsMarch 6, 2024](./why-
use-squads)[![squads-solana-leading-multisig-spending-limits-treasury-
management-solana-multisig-wallet-squads-protocol-audited-formal-
verification](https://framerusercontent.com/images/2tyh01MPlECImwUoS4lpntdjCM.png)How
to Improve Treasury Operations with Spending LimitsNovember 29,
2023](./spending-limits)[![maple-us-treasury-bills-solana-product-cash-
management-pool-solana-multisig-squads-squadsx-extension-solana-wallet-solana-
tbill-yield-solana-multisig-
wallet](https://framerusercontent.com/images/phcIaPOZX2To9oDZzBAIxW2a40.png)Access
U.S. Treasury Bills Yield on Solana through Maple with SquadsXOctober 23,
2023](./maple-squadsx-on-chain-treasury-bills-solana)

[](../)

All rights reserved

Â© Squads Protocol 2024

Product

[Squads](../)

[Protocol](../protocol)

[Extension](../extension)

[Use Cases](../use-cases)

[Why Multisig](https://squads.so/blog/what-are-multisig-wallets)

Resources

[Github](https://github.com/Squads-Protocol)

[SDK](https://www.npmjs.com/package/@sqds/multisig)

[Documentation](https://docs.squads.so/main/basics/welcome-to-squads)

[Blog](../blog)

[Multisig vs MPC](https://squads.so/blog/mpc-wallets-risks-vs-multisig)

Company

[About](../about)

[Brand assets](../brand-assets)

[Twitter](https://twitter.com/squadsprotocol)

[Discord](https://discord.com/invite/YPXz64TrKs)

[Farcaster](https://warpcast.com/squads)

Legal

[Terms of Service](../legal/terms-of-service)

[Privacy Policy](../legal/privacy-policy)

[Contact us](https://discord.com/invite/YPXz64TrKs)

