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

[Home](/vi)>[Developers](/vi/developers)>[Guides](/vi/developers/guides)

# [Getting started with game development on
Solana](/vi/developers/guides/games/getting-started-with-game-development)

updated 25 tháng 4, 2024

[intro](/vi/developers/guides?difficulty=intro)[games](/vi/developers/guides?tags=games)[unity](/vi/developers/guides?tags=unity)[quickstart](/vi/developers/guides?tags=quickstart)

[![Getting started with game development on
Solana](https://solana.com/_next/image?url=%2Fopengraph%2Fdevelopers%2Fguides%2Fgames%2Fgetting-
started-with-game-
development&w=3840&q=75)](/vi/developers/guides/games/getting-started-with-
game-development)

The gaming space in the Solana ecosystem is expanding rapidly. Integrating
with Solana can provide numerous benefits for games, such as enabling players
to own and trade their assets (via NFTs in games), building an open and
composable in-game economy (using various DeFi protocols), creating composable
game programs, and allowing players to compete for valuable assets.

Solana is nearly purpose-built for games. With its 400ms block time and
lightning-fast confirmations: it's a real-time database that is accessible for
all. It's especially perfect for genres like strategy games, city builders,
turn-based games, and more.

With extremely cheap transaction fees, smaller integrations using NFTs that
represent game items or achievements, or that use USDC micro payments for in
game items can be done easily. There are already many tools and SDKs available
to start building these types of on-chain interactions today, using many of
the game development frameworks that you know and love.

You can build your game in [JavaScript](/vi/docs/clients/javascript) and
Canvas, [Phaser](https://github.com/Bread-Heads-NFT/phaser-solana-platformer-
template), [Turbo Rust](https://turbo.computer/), or use one of the Solana
Game SDKs for the three biggest game engines -
[UnitySDK](/vi/developers/guides/games/game-sdks#unity-sdk),
[UnrealSDK](https://github.com/staratlasmeta/FoundationKit), and
[Godot](https://github.com/Virus-Axel/godot-solana-sdk). Find a list of all
gaming SDKs here: [Game SDKs](/vi/developers/guides/games/game-sdks).

## What are the benefits of building games on Solana? #

  1. No user management: players can use their Solana wallet to authenticate themselves in the game.
  2. No server costs: Solana is a decentralized network, so you don't need to pay for additional backed servers.
  3. No running costs for your program. You can even [close the program](/vi/developers/guides/getstarted/solana-token-airdrop-and-faucets#6-reuse-devnet-sol) to get the SOL back.
  4. The ability to reward players for great achievements or let them play against each other for assets with real value outside the game.
  5. The ability to permissionlessly use all of the other programs deployed on Solana, like decentralized exchanges, NFT marketplaces, lending protocols, high score programs, loyalty/referral programs, and more.
  6. The ability to write your own onchain programs. If some game functionality you want does not already exist, you can always [write and deploy](/vi/docs/core/programs) your own custom onchain program.
  7. Platform independent payments, for all browsers, Android/iOS, and any other platform - as long as the players can sign a transaction they can buy assets.
  8. No 30% fee that Apple and Google take for in-app purchases by deploying directly to the [Saga dApp store](https://docs.solanamobile.com/dapp-publishing/intro).

## How to integrate Solana into your game? #

  1. Give players digital collectibles for in-game items or use them as characters. See [NFTs in games](/vi/developers/guides/games/nfts-in-games)
  2. Use tokens for in-app purchases or micro-payments in the game. See [Using tokens in games](/vi/developers/guides/games/interact-with-tokens)
  3. Use the player's wallet to authenticate them in the game using the [Solana Wallet Adapter](https://github.com/anza-xyz/wallet-adapter) framework
  4. Run tournaments and pay out crypto rewards to your players.
  5. Develop the game entirely on-chain to:
     * reward your players in every step they take
     * allow any game/app/device to connect with your game
     * enact governance for the game's future
     * ledger verifiable activity for anti-cheat systems

Info

See our [Solana games "Hello world"](/vi/developers/guides/games/hello-world)
for a detailed guide on how to get started with building games on Solana.

## Game SDKs #

With all these benefits, Solana is quickly becoming the go-to platform for
game developers. Get started today by first picking your favorite gaming SDK:

Platform| Language  
---|---  
[Unity SDK](/vi/developers/guides/games/game-sdks#unity-sdk)| C#  
[Godot SDK](/vi/developers/guides/games/game-sdks#godot-sdk)| GD script and
C++  
[Solana GameShift](/vi/developers/guides/games/game-sdks#solana-game-shift)|
RestAPI  
[Turbo.Computer](/vi/developers/guides/games/game-sdks#turbo-computer-rust-
game-engine)| Rust  
[Honeycomb Protocol](/vi/developers/guides/games/game-sdks#honeycomb-
protocol)| Rust and JavaScript  
[Unreal SDKs](/vi/developers/guides/games/game-sdks#unreal-sdks)| C++, C#,
Blueprints  
[Next js, React, Anchor](/vi/developers/guides/games/game-sdks#next-js-react-
anchor)| Rust/Anchor, JavaScript, C#, NextJS  
[Flutter](/vi/developers/guides/games/game-sdks#flutter)| JavaScript  
[Phaser](/vi/developers/guides/games/game-sdks#phaser)| HTML5, JavaScript  
[Python](/vi/developers/guides/games/game-sdks#python)| Python  
[Native C#](/vi/developers/guides/games/game-sdks#native-c)| C#  
  
## Game Distribution #

Distribution of your game depends highly on the platform you are using. With
Solana, there are [game SDKs](/vi/developers/guides/games/getting-started-
with-game-development#game-sdks) you can build for iOS, Android, Web and
Native Windows or Mac. Using the Unity SDK you could even connect Nintendo
Switch or XBox to Solana theoretically. Many game companies are pivoting to a
mobile first approach because there are so many people with mobile phones in
the world. Mobile comes with its own complications though, so you should pick
what fits best to your game.

Solana has a distinct edge over other blockchain platforms due to its offering
of a crypto-native mobile phone from [Solana
Mobile](https://solanamobile.com), named Saga. The Android based [Saga
phone](https://solanamobile.com/hardware) comes equipped with an innovative
dApps store that enables the distribution of crypto games without the
limitations imposed by conventional app stores, including those from Google or
Apple.

## Publishing Platforms #

Platforms where you can host and/or publish your games:

Platform| Description  
---|---  
[Fractal](https://www.fractal.is/)| A game publishing platform that supports
Solana and Ethereum. They also have their own wallet and account handling and
there is an SDK for high scores and tournaments.  
[Solana mobile dApp Store](https://github.com/solana-mobile/dapp-
publishing/blob/main/README.md)| The Solana alternative to Google Play and the
Apple App Store. A crypto first variant of a dApp store, which is open source
free for everyone to use. See([video
walkthrough](https://youtu.be/IgeE1mg1aYk?si=fZmU1WNiW-kR3qFa))  
[Apple App Store](https://www.apple.com/de/app-store/)| The Apple app store
has a high reach and is trusted by its customers. The entrance barrier for
crypto games is high though. The rules are very strict for everything that
tries to circumvent the fees that Apple takes for in app purchases. A soon as
an NFT provides benefits for the player for example Apple requires you for
example to have them purchased via their in app purchase system.  
[Google Play Store](https://play.google.com/store/games)| Google is much more
crypto friendly and games with NFTs and wallet deep links for example have had
a track record of being approved for the official Play Store.  
[xNFT Backpack](https://www.backpack.app/)| Backpack is a Solana wallet which
allows you to release apps as xNFTs. They appear in the user's wallet as soon
as they purchase them as applications. The Unity SDK has a xNFT export and any
other web app can be published as xNFT as well.  
[Elixir Games](https://elixir.games/)| Elixir Games is a platform that focuses
on blockchain-based games. They support a variety of blockchain technologies
and offer a platform for developers to publish their games.  
Self Hosting| Just host your game yourself. For example, using
[Vercel](https://vercel.com/) which can be easily setup so that a new version
get deployed as soon as you push to your repository. Other options are [GitHub
pages](https://pages.github.com/) or [Google
Firebase](https://firebase.google.com/docs/hosting) but there are many more.  
  
## Next Steps #

If you would like to learn more about developing games on Solana, take a look
at these developer resources and guides:

  * [Solana Gaming SDKs](/vi/developers/guides/games/game-sdks)
  * [Hello world on-chain game](/vi/developers/guides/games/hello-world)
  * [Learn by example](/vi/developers/guides/games/game-examples)
  * [Energy System](/vi/developers/guides/games/energy-system)
  * [NFTs in games](/vi/developers/guides/games/nfts-in-games)
  * [Dynamic metadata NFTs](/vi/developers/guides/token-extensions/dynamic-meta-data-nft)
  * [Token in games](/vi/developers/guides/games/interact-with-tokens)

[Previous« Solana Gaming SDKs](/vi/developers/guides/games/game-
sdks)[NextHello World for Solana Game Development
»](/vi/developers/guides/games/hello-world)

##### Table of Contents

  * [What are the benefits of building games on Solana](/vi/developers/guides/games/getting-started-with-game-development#what-are-the-benefits-of-building-games-on-solana)
  * [How to integrate Solana into your game](/vi/developers/guides/games/getting-started-with-game-development#how-to-integrate-solana-into-your-game)
  * [Game SDKs](/vi/developers/guides/games/getting-started-with-game-development#game-sdks)
  * [Game Distribution](/vi/developers/guides/games/getting-started-with-game-development#game-distribution)
  * [Publishing Platforms](/vi/developers/guides/games/getting-started-with-game-development#publishing-platforms)
  * [Next Steps](/vi/developers/guides/games/getting-started-with-game-development#next-steps)

[Scroll to Top](/vi/developers/guides/games/getting-started-with-game-
development#)

[Edit Page](https://github.com/solana-foundation/developer-
content/tree/main/content/guides/games/getting-started-with-game-
development.md)

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

