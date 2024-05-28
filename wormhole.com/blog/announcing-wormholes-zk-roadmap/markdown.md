[![wormhole
logo](https://images.ctfassets.net/n8aw1cra6v98/2057wAXk6apiGi4vfTeC2u/9e200f5dfebaf6bb113c879243cf4508/wormwhole.svg?w=384&q=100)](/)

Products

Ecosystem

Developers

Platform

Community

[Start Building](https://docs.wormhole.com/)

news

### ANNOUNCING WORMHOLE’S ZK ROADMAP

Apr 01, 2024

·

3 min read

![https://images.ctfassets.net/n8aw1cra6v98/6GojDURCqaGdp2gqYxvVxx/cb17c58d3a9c8f1450da3006c30c4f06/Social-
card_Gateway-Blog-Header-Graphic---Blog---
Social.png](https://images.ctfassets.net/n8aw1cra6v98/6GojDURCqaGdp2gqYxvVxx/cb17c58d3a9c8f1450da3006c30c4f06/Social-
card_Gateway-Blog-Header-Graphic---Blog---Social.png?w=1080&q=75)

Trust lies at the very heart of every interaction, organization, or system.

One of the great innovations of crypto has been the ability to reduce reliance
on a small set of trusted actors to a wider audience of users, developers, and
stakeholders. This process of democratizing and disintermediating trust has
been challenging. But nonetheless, the Wormhole community remains committed to
upholding this ethos of trust-minimization.

Wormhole is a leading interoperability platform for facilitating multichain
communication. Since 2021, Wormhole has served as a foundational tool for
fast, reliable, and cheap multichain messaging. As new blockchains continue to
emerge, efficient and scalable mechanisms for interoperating across a wide
range of networks will continue to be a key challenge.

This post outlines a significant upgrade to Wormhole’s verification system —
the design choices, technologies in use, and the complexities of bringing
Wormhole into a trust-minimized future.

##### Introducing Wormhole ZK

Today marks a major advancement toward improving the trust assumptions of the
Wormhole protocol, with the announcement of Wormhole’s ZK Roadmap. By
integrating zero-knowledge (ZK) technology, the Wormhole protocol adds the
following improvements:

  * **Stronger Trust Guarantees:** ZK enables a new option for trustlessly verifying messages sent via Wormhole. ZK also reduces trust in the protocol, enabling stronger security guarantees to multichain apps and users.
  * **Permissionless Verification:** With ZK, anybody can quickly and easily participate in verifying Wormhole messages, enabling a larger and more diverse set of independent contributors to cooperate in securing the Wormhole protocol.
  * **Permissionless Integrations:** With ZK, new blockchain networks will be able to permissionlessly, quickly, and easily join the Wormhole ecosystem. This will enable new networks to connect to the broader Wormhole ecosystem without the explicit consent of the network of Guardians.
  * **Strong Composability:** True multichain applications require a high degree of composability. Composability enables clients, users, and applications to leverage the state and data of other networks seamlessly and at low cost. Different blockchain networks often have distinct runtime semantics, consensus models, or architectures. ZK can help define a more unified interface for access to state and data, improving consistency across applications operating across distinct blockchain networks.
  * **Flexibility:** ZK will serve as an additional option for message verification, providing users and applications with an alternative approach to verifying messages. This offers greater flexibility, allowing clients to choose the method that best suits their specific preferences and needs.

##### Wormhole Message Verification Today

Today, a Wormhole message is produced when at least 13 of the 19 (a
supermajority) Guardians agree on the state and execution of the blockchain
the message originated from, and they all observe the same message being sent.
This means that users and applications that rely on these messages (e.g.
consume them on another blockchain) must rely on the Guardians to validate
messages accurately. This constitutes the verification mechanism underlying
Wormhole — its root-of-trust.

The Guardians were recently recognized for security and decentralization by
the Uniswap Foundation’s third party Bridge Assessment Committee in a
[report](https://uniswap.notion.site/Bridge-Assessment-
Report-0c8477afadce425abac9c0bd175ca382?ref=wormhole.ghost.io) released in
2023, naming Wormhole as the only unconditionally approved interoperability
protocol for Uniswap’s multichain governance system.

Although sufficiently decentralized and highly secure, the Wormhole protocol
is becoming more secure, decentralized, and less trust-based over time; the
next step toward this objective is decentralizing Wormhole’s verification
layer and moving toward a trust-minimized model using zero-knowledge
technology.

##### The Wormhole ZK Roadmap

The Wormhole ecosystem will be launching a portfolio of software solutions to
achieve the following collective vision for ZK-enabled interoperability. The
path ahead for Wormhole ZK is marked by a few significant milestones and
strategic collaborations, all aimed at enabling extremely fast, cheap, and
trustless message verification.

Here’s a detailed look at the roadmap:

  1. **Onboarding Cryptography Expertise** – The Wormhole Foundation has given Contributor Grants to four new engineering teams specializing in zero-knowledge cryptography and will roll out these announcements over the coming weeks.
  2. **Unlocking Hardware Resources** – Wormhole contributors will be collaborating with a strategic hardware provider to accelerate a number of light client implementations, as well as to source hardware accelerators for Wormhole contributors as the number of ZK-enabled corridors and ZK-verified messages continue to scale.
  3. **Upcoming Light Client Rollouts** – Light clients allow users and applications to quickly and efficiently verify the state (e.g. current account balances, smart contract data, etc.) of a blockchain network. Running a light client directly on-chain (as a smart contract) is still infeasible on many blockchains due to the high cost of verification, but possible using succinct, verifiable computation. This allows performing the expensive light client verification off-chain, and more cheaply verifying the correctness of the light client execution on-chain. Over the coming months, ZK light-clients for blockchains, including Ethereum, Sui, Aptos, Near, and Cosmos will be deployed and integrated with Wormhole, enabling trustless, bi-directional transfers of data.

In summary, Wormhole's verification system and ZK Roadmap is focused on:

  * Adding flexibility to Wormhole by enabling the protocol to support a variety of verification mechanisms in addition to the Wormhole Guardians.
  * Advancing trust-minimization of the protocol through accelerated ZK proofs and light-client integrations, thereby enabling trustless communication between blockchains.
  * Allowing more efficient scaling to accommodate rapid, permissionless integration of new blockchains.
  * Enabling stronger multichain composability for clients so they can more easily build richer and more expressive applications across a diverse set of blockchains with distinct semantics.

* * *

###### About Wormhole

Wormhole is the leading interoperability platform that powers multichain
applications and bridges at scale. Wormhole provides developers access to
liquidity and users on over 30 of the leading blockchain networks, enabling
use cases that span DeFi, NFTs, governance, and more.

The wider Wormhole network is trusted and used by teams like Circle and
Uniswap, and to date, the platform has facilitated the transfer of over 35
billion dollars through over 1 billion cross-chain messages. To learn more
about Wormhole, visit the Wormhole
[website](https://wormhole.com/?ref=wormhole.ghost.io),
[Twitter](https://twitter.com/wormhole?ref=wormhole.ghost.io),
[Discord](https://discord.com/invite/wormholecrypto?ref=wormhole.ghost.io), or
[blog](https://wormhole.com/blog?ref=wormhole.ghost.io).

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

