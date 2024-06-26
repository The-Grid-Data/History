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

[Home](/de)>[Developers](/de/developers)>[Guides](/de/developers/guides)

# [How to auto approve transactions](/de/developers/guides/advanced/auto-
approve)

updated 25\. April 2024

[beginner](/de/developers/guides?difficulty=beginner)[games](/de/developers/guides?tags=games)[wallets](/de/developers/guides?tags=wallets)[transactions](/de/developers/guides?tags=transactions)[unity](/de/developers/guides?tags=unity)

[![How to auto approve
transactions](https://solana.com/_next/image?url=%2Fopengraph%2Fdevelopers%2Fguides%2Fadvanced%2Fauto-
approve&w=3840&q=75)](/de/developers/guides/advanced/auto-approve)

Auto approving transactions means that the user does not have to manually
confirm every transaction. This is especially useful for on-chain games where
you want to have fluid game play. Here are some options on how this can be
achieved.

## Wallet Auto Approve #

A few popular Solana wallet applications have transaction "auto approve"
functionality directly with in them. Some accomplish this with burner wallets.
This is a very convenient solution, but it may limit your players to using one
of these wallets. Players may also be resistant to activate the feature since
it may be seen as a security risk.

  * [Solflare auto approve](https://twitter.com/solflare_wallet/status/1625950688709644324)
  * [Phantom auto approve](https://phantom.app/learn/blog/auto-confirm)

## Local Keypair #

Another way to add transaction auto approval is to create a keypair in your
game/dApp and let the player transfer some SOL to that wallet and then use it
to pay for transaction fees. The only problem with this is that you need to
handle the security for this wallet and the keys can get lost if the users
clear their browser cache.

Here, you can find some example source code on how to implement transaction
auto approval using local keypairs:

  * [Example Source Code](https://github.com/solana-developers/solana-game-examples/blob/main/seven-seas/unity/Assets/SolPlay/Scripts/Services/WalletHolderService.cs)
  * [Example Game Seven seas](https://solplay.de/sevenseas/)

## Server Backend #

Using a server backend for your game or dApp, you can configure a system that
will allow your backend to handle paying the [Solana fees](/de/docs/core/fees)
yourself. This backend would allow you to create and sign transactions for the
user, marking your secure backend keypair the `fee payer`, and enabling your
application to interact with it via an API endpoint.

To accomplish this, your client application (i.e. game or dApp) would send
parameters to your backend server. The backend server would then authenticate
that request and the build a transaction with the required data from the user.
The backend would then sign and send this transaction to the Solana
blockchain, confirm the transaction was successful, and send a confirmation
message to the client.

This server backend method is an easy and convenient solution, but you need to
handle the user's authentication and security. So that could add complexity to
your application's infrastructure and architecture.

## Session Keys #

Session Keys are ephemeral (short lived) keypairs with fine-grained
program/instruction scoping for tiered access in your Solana programs. They
allow users to interact with apps by signing transactions locally using a
temporary keypair. The temporary keypair acts a bit like an oauth token from
web 2, allowing access for a certain amount of time.

Session keys make for a really great user experience, but they do need some
extra work to implement in the on-chain program. You can use the `session-
keys` crate maintained by [Magic Block](https://www.magicblock.gg/) using
their [official
documentation](https://docs.magicblock.gg/Onboarding/Session%20Keys/integrating-
sessions-in-your-program).

## Shadow Signer #

Shadow signer is a feature within the [Honeycomb
Protocol](https://twitter.com/honeycomb_prtcl) that allows you to sign
transactions.

  * [How Shadow Signer works](https://twitter.com/honeycomb_prtcl/status/1777807635795919038)
  * [Docs](https://docs.honeycombprotocol.com/services/)

[NextHow to Optimize Compute Usage on Solana
»](/de/developers/guides/advanced/how-to-optimize-compute)

##### Table of Contents

  * [Wallet Auto Approve](/de/developers/guides/advanced/auto-approve#wallet-auto-approve)
  * [Local Keypair](/de/developers/guides/advanced/auto-approve#local-keypair)
  * [Server Backend](/de/developers/guides/advanced/auto-approve#server-backend)
  * [Session Keys](/de/developers/guides/advanced/auto-approve#session-keys)
  * [Shadow Signer](/de/developers/guides/advanced/auto-approve#shadow-signer)

[Scroll to Top](/de/developers/guides/advanced/auto-approve#)

[Edit Page](https://github.com/solana-foundation/developer-
content/tree/main/content/guides/advanced/auto-approve.md)

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

