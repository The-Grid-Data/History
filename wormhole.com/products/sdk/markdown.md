[![wormhole
logo](https://images.ctfassets.net/n8aw1cra6v98/2057wAXk6apiGi4vfTeC2u/9e200f5dfebaf6bb113c879243cf4508/wormwhole.svg?w=384&q=100)](/)

Products

Ecosystem

Developers

Platform

Community

[Start Building](https://docs.wormhole.com/)

## Wormhole TypeScript SDK

A modern TypeScript SDK to take your app or wallet multichain

[Start integrating](https://github.com/wormhole-foundation/wormhole-sdk-
ts)[Get in touch](/contact)

![](https://images.ctfassets.net/n8aw1cra6v98/74s8BkcCtW5kHUFU3SRMsq/1f6e9805d09c88fda2c0b211b31fb0ae/Frame_427320693.svg?w=1200&q=75)

![](https://images.ctfassets.net/n8aw1cra6v98/47LP13JTZQhgJ8ma1CE0aW/a4339e8067bb8de826b848ce6e458a9a/gasless.svg?w=128&q=75)

Universal API

Provides a consistent interface across different chains to simplify
development, eliminating the need to set up custom logic for each chain.

![](https://images.ctfassets.net/n8aw1cra6v98/sV9vnadoEGQQdHEtsrufg/f59df52502ce553747620363a4db1f9c/bridge.svg?w=128&q=75)

Modular and organized

Tailor your development experience by including only what you need, ensuring
smaller bundles and faster startup times.

![](https://images.ctfassets.net/n8aw1cra6v98/6HDPkAlU2d8f2fFNJy3BS3/45d0743aa2691982e673c00e76d1b83b/3lines.svg?w=128&q=75)

Flexible signer interface

Allows you to employ custom gas or fee strategies, offering you more
adaptability in your projects.

![](https://images.ctfassets.net/n8aw1cra6v98/36pfFbPLlPqWDalxFi5B0b/ab1b19516f41cc15544d460b07d5cc50/user.svg?w=128&q=75)

Router plug-ins

Provide you with multiple options for choosing your route. They always find
the best route given any input, enhancing your efficiency.

### The most powerful multichain SDK

![](https://images.ctfassets.net/n8aw1cra6v98/7MziwAv40e5gCnKopY0Kfz/b0740ec716638b9f9739f2de62b643e7/worms.svg?w=1920&q=75)

### How to use Wormhole SDK

Token Transfers

Code

Copy code

`1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 ``import { Chain, Network,
TokenId, TokenTransfer, Wormhole, amount, isTokenId, wormhole, } from
"@wormhole-foundation/sdk"; // Import the platform-specific packages import
evm from "@wormhole-foundation/sdk/evm"; import solana from "@wormhole-
foundation/sdk/solana"; import { SignerStuff, getSigner, waitLog } from
"./helpers/index.js"; (async function () { // Init Wormhole object, passing
config for which network // to use (e.g. Mainnet/Testnet) and what Platforms
to support const wh = await wormhole("Testnet", [evm, solana]); // Grab chain
Contexts -- these hold a reference to a cached rpc client const sendChain =
wh.getChain("Avalanche"); const rcvChain = wh.getChain("Solana"); // Shortcut
to allow transferring native gas token const token =
Wormhole.tokenId(sendChain.chain, "native");`

Example Output

Copy code

`1 2 3 4 5 6 7 8 9 10 11 ``(async function () { // Init Wormhole object,
passing config for which network // to use (e.g. Mainnet/Testnet) and what
Platforms to support const wh = await wormhole("Testnet", [evm, solana]); //
Grab chain Contexts -- these hold a reference to a cached rpc client const
sendChain = wh.getChain("Avalanche"); const rcvChain = wh.getChain("Solana");
// Shortcut to allow transferring native gas token const token =
Wormhole.tokenId(sendChain.chain, "native"); `

Router

Code

Copy code

`1 2 3 4 5 6 7 8 9 10 11 ``(async function () { // Init Wormhole object,
passing config for which network // to use (e.g. Mainnet/Testnet) and what
Platforms to support const wh = await wormhole("Testnet", [evm, solana]); //
Grab chain Contexts -- these hold a reference to a cached rpc client const
sendChain = wh.getChain("Avalanche"); const rcvChain = wh.getChain("Solana");
// Shortcut to allow transferring native gas token const token =
Wormhole.tokenId(sendChain.chain, "native");`

Example Output

Copy code

`1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 ``import { Chain, Network,
TokenId, TokenTransfer, Wormhole, amount, isTokenId, wormhole, } from
"@wormhole-foundation/sdk"; // Import the platform-specific packages import
evm from "@wormhole-foundation/sdk/evm"; import solana from "@wormhole-
foundation/sdk/solana"; import { SignerStuff, getSigner, waitLog } from
"./helpers/index.js"; (async function () { // Init Wormhole object, passing
config for which network // to use (e.g. Mainnet/Testnet) and what Platforms
to support const wh = await wormhole("Testnet", [evm, solana]); // Grab chain
Contexts -- these hold a reference to a cached rpc client const sendChain =
wh.getChain("Avalanche"); const rcvChain = wh.getChain("Solana"); // Shortcut
to allow transferring native gas token const token =
Wormhole.tokenId(sendChain.chain, "native");`

![Backpack](https://images.ctfassets.net/n8aw1cra6v98/1GbpZWvYkTFfuRSI50AguD/6af26a7f2a78e2ca1be961dd7aa1527f/Group_427320708.png?w=1920&q=75)

Case Study

#### Backpack

Backpack is not just an average digital wallet - it’s also a regulated
centralized exchange that operates in jurisdictions across the world.

May 02, 2024

·

3 min read

[Read more](/blog/backpack-case-study)

Discover other Wormhole products

##### SDK

Build your custom multichain application.

[Learn
more](/products/sdk)![](https://images.ctfassets.net/n8aw1cra6v98/1UpskSY7IlHAT1hd8JeiJj/8926ee2806c3bfb8d8fd3247d6bff641/Queries.webp?w=1080&q=75)

##### Native Token Transfers

Make any token natively multichain.

[Learn more](/products/native-token-
transfers)![](https://images.ctfassets.net/n8aw1cra6v98/5AC4LQoh6Xvpl6MBb0spy/5a825aa9c53b41d162f23931c30c56c5/Frame_427320722.svg?w=1080&q=75)

##### Messaging

Build your custom multichain protocol.

[Learn
more](/products/messaging)![](https://images.ctfassets.net/n8aw1cra6v98/2xG6hd69OFcNCxC79vHdnO/a029107e645b4bc7169cc2304396b470/Messaging.webp?w=1080&q=75)

##### Queries

Pull any on-chain data on-demand.

[Learn
more](/products/queries)![](https://images.ctfassets.net/n8aw1cra6v98/1UpskSY7IlHAT1hd8JeiJj/8926ee2806c3bfb8d8fd3247d6bff641/Queries.webp?w=1080&q=75)

![Image](https://images.ctfassets.net/n8aw1cra6v98/2fP8M06oPDd6atrcKaUHOQ/0fcc04374046f970de7dfb7fe86574e5/worm.svg)

#### Future-proof, permissionless tooling to empower multichain builders

[Start Building](https://docs.wormhole.com/)

Subscribe for updates

Subscribe

[![x or twitter](/assets/x.svg)](https://twitter.com/wormhole)[![x or
twitter](/assets/discord.svg)](https://discord.gg/wormholecrypto)[![x or
twitter](/assets/telegram.svg)](https://t.me/wormholecrypto)[![x or
twitter](/assets/github.svg)](https://github.com/wormhole-
foundation/wormhole)[![x or
twitter](/assets/some.svg)](https://docs.wormhole.com/)[![x or
twitter](/assets/youtube.svg)](https://www.youtube.com/@wormholecrypto)

Products

[connect](/products/connect)[SDK](/products/sdk)[native token
transfers](/products/native-token-
transfers)[Queries](/products/queries)[Messaging](/products/messaging)

Ecosystem

[Multichain apps](/ecosystem/multichain-apps)[W
Token](/ecosystem/w-token)[Ecosystem Programs](/ecosystem/ecosystem-
programs)[Case Studies](/case-studies)

Developers

[Documentation](https://docs.wormhole.com/wormhole)[Github](https://github.com/wormhole-
foundation)[Bug Bounties](https://immunefi.com/bug-
bounty/wormhole/)[Wormholescan](https://wormholescan.io/)

Platform

[Blockchains](/platform/blockchains)[Security](/platform/security)[Gateway](/platform/gateway)

Community

[Hub](/community/hub)[Blog](/blog)[Brand and Press](/brand-and-press)

2024 Ⓒ Wormhole. All Rights Reserved.

[Terms of use](/pages/terms-of-use)[Privacy Policy](/pages/data-protection-
and-privacy-policy)

