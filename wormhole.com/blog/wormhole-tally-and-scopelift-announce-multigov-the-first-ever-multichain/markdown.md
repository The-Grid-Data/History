[![wormhole
logo](https://images.ctfassets.net/n8aw1cra6v98/2057wAXk6apiGi4vfTeC2u/9e200f5dfebaf6bb113c879243cf4508/wormwhole.svg?w=384&q=100)](/)

Products

Ecosystem

Developers

Platform

Community

[Start Building](https://docs.wormhole.com/)

news

### Wormhole, Tally, and ScopeLift Announce ‘MultiGov,’ the First-Ever
Multichain Governance System

Apr 08, 2024

·

4 min read

![https://images.ctfassets.net/n8aw1cra6v98/2i7q9lBUmBf6StcuA0jftx/e1240f3ba3572f84eb39bd0090231225/Wormhole-
x-Tally-x-Scopelift-
MultiGov.png](https://images.ctfassets.net/n8aw1cra6v98/2i7q9lBUmBf6StcuA0jftx/e1240f3ba3572f84eb39bd0090231225/Wormhole-
x-Tally-x-Scopelift-MultiGov.png?w=1080&q=75)

Wormhole, [Tally](https://www.tally.xyz/?ref=wormhole.ghost.io), and
[ScopeLift](https://scopelift.co/?ref=wormhole.ghost.io) are teaming up to
build MultiGov: an industry-first multichain governance system soon available
to DAOs on Solana, Ethereum mainnet, and EVM L2s. The Wormhole DAO will be the
first to adopt MultiGov, enabling W holders to create, vote on, and execute
governance proposals on any supported chain. Integrating this innovative
governance model marks a significant shift towards a truly decentralized and
inclusive decision-making process that operates at a level above the multiple
underlying chains.

##### What is Multichain Governance?

Your DAO operated by users on any chain. Multichain governance lets DAOs meet
token holders where they are. DAO members can raise proposals, delegate, vote,
and generally participate in governance for an onchain DAO from whichever
chain they hold tokens on. MultiGov will support multichain DAOs across
Solana, Ethereum mainnet, and EVM-compatible L2s. As more projects expand to
multiple chains, MultiGov will lower barriers to DAO participation and
increase user reach in nearly all major ecosystems. Tally, Wormhole, and
Scopelift are combining their expertise in state-of-the-art governance,
delegation, and multichain infrastructure to build MultiGov.

##### Single-chain vs Multichain

Until now, DAOs have operated their governance on a single chain. Many of the
oldest and largest DAOs keep their token, governance, and treasury all on
Ethereum mainnet. However, rising L1 gas costs make managing and participating
in governance increasingly expensive. In addition, with the growth of robust
multichain infrastructure, DAO token holders are increasingly distributed
across many chains. To maintain active, accessible, and decentralized
governance, many existing DAOs are exploring options to expand their
governance systems. Newer protocol DAOs often plan out their multichain
strategy from day 1, launching on one network and then strategically expanding
to other chains to grow their users and liquidity.

![CleanShot-2024-04-08-at-12.21.34@2x](//images.ctfassets.net/n8aw1cra6v98/3yUnzeaH2NGOjXxccHMlF6/95880018386f754acec92151ae9d80ef/CleanShot-2024-04-08-at-12.21.34_2x.png?w=1080&q=75)

##### MultiGov aims to keep DAO governance:

  * Active, by meeting community members where they are.
  * Accessible to all token holders, by lowering gas costs.
  * Decentralized, by enabling token holders to vote on any chain
  * Flexible, by allowing DAOs to easily expand to new networks along with their protocol

##### Implementation: MultiGov’s hub-and-spoke model

MultiGov implements a hub-and-spoke governance model. This model combines
well-understood building blocks – governor, timelock, cross-chain token
transfers, and cross-chain messaging.

![CleanShot-2024-04-08-at-12.22.07@2x](//images.ctfassets.net/n8aw1cra6v98/3OdHFk5TfAUVxbtpOmX4bl/b4ef9200acf85c65a8ffb3a8ca01b4ac/CleanShot-2024-04-08-at-12.22.07_2x.png?w=1080&q=75)

On the "hub" chain, a DAO using MultiGov has a standard [ERC20Votes
token](https://github.com/OpenZeppelin/openzeppelin-
contracts/blob/master/contracts/token/ERC20/extensions/ERC20Votes.sol?ref=wormhole.ghost.io)
and [OpenZeppelin Governor](https://github.com/OpenZeppelin/openzeppelin-
contracts/tree/master/contracts/governance?ref=wormhole.ghost.io) with the
[Flexible Voting
extension](https://flexiblevoting.com/?ref=wormhole.ghost.io). The hub can be
any supported EVM chain. Token holders can choose to natively transfer their
hub governance tokens to spoke chains.

On each "spoke," there is a native governance token and a spoke Governor
contract. The native governance token keeps track of voting power on that
chain. When there is a proposal, token holders on that spoke chain submit
votes to the spoke Governor. Votes on each spoke Governor can be aggregated
and sent back to the hub chain via a cross-chain message. Users who are on the
hub chain can submit votes directly to the hub chain Governor.

When the voting period is over, the hub chain will tally the votes it has
collected from all the spoke chains and from users who submitted directly on
the hub. If the proposal passes, it is executed on the hub chain, and sent to
each of the spokes for execution via a cross-chain message. Creating new
proposals to vote on follows a similar design, where proposals are created on
the hub chain and then broadcast to each spoke chain.

To learn more about how DAOs can go multichain, watch Tally CTO Raf Solari’s
ETH Denver 2024 talk on Multichain DAOs
[here](https://twitter.com/tallyxyz/status/1762609578863198698?ref=wormhole.ghost.io).

##### The Wormhole DAO

The Wormhole DAO, governed by W holders, will be the first to use MultiGov’s
pioneering multichain governance system. Wormhole's DAO will enable W token
holders on any supported chain to participate in governance for the Wormhole
protocol. This approach will provide users with a familiar interface for
participating in Wormhole governance, whether they are on Ethereum, an EVM L2,
or Solana. The Wormhole contributors hope that this will help maintain a
vibrant and active Wormhole community while keeping governance completely
decentralized and accessible to all.

DAOs interested in implementing MultiGov can reach out to contributors at
Wormhole, Tally, and ScopeLift by submitting this
[form](https://forms.clickup.com/45049775/f/1aytxf-10244/JKYWRUQ70AUI99F32Q?ref=wormhole.ghost.io).

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

