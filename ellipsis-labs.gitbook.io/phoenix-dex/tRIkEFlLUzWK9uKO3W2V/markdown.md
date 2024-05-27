[![Logo](https://ellipsis-
labs.gitbook.io/~gitbook/image?url=https%3A%2F%2F2958162351-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-
x-
prod.appspot.com%2Fo%2Fspaces%252FO6I6v4yXZJFfKmgjJZGu%252Ficon%252FGgaNnbxzJ7b0rxCbpYAm%252FScreen%2520Shot%25202022-12-31%2520at%25201.33.50%2520AM.png%3Falt%3Dmedia%26token%3D90c507ec-0326-448d-b8b6-966b58563833&width=32&dpr=4&quality=100&sign=00a45f162fd37ce26e56732752cfc1d7250bf30293e715833504c66318068acb)![Logo](https://ellipsis-
labs.gitbook.io/~gitbook/image?url=https%3A%2F%2F2958162351-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-
x-
prod.appspot.com%2Fo%2Fspaces%252FO6I6v4yXZJFfKmgjJZGu%252Ficon%252FGgaNnbxzJ7b0rxCbpYAm%252FScreen%2520Shot%25202022-12-31%2520at%25201.33.50%2520AM.png%3Falt%3Dmedia%26token%3D90c507ec-0326-448d-b8b6-966b58563833&width=32&dpr=4&quality=100&sign=00a45f162fd37ce26e56732752cfc1d7250bf30293e715833504c66318068acb)Phoenix
DEX](/phoenix-dex/tRIkEFlLUzWK9uKO3W2V)

SearchCtrl \+ K

  * Getting Started

    * [Phoenix Overview](/phoenix-dex/tRIkEFlLUzWK9uKO3W2V)

    * [Technical Overview](/phoenix-dex/tRIkEFlLUzWK9uKO3W2V/getting-started/technical-overview)

      * [Key Structures](/phoenix-dex/tRIkEFlLUzWK9uKO3W2V/getting-started/technical-overview/key-structures)

      * [Events](/phoenix-dex/tRIkEFlLUzWK9uKO3W2V/getting-started/technical-overview/events)

      * [Instructions](/phoenix-dex/tRIkEFlLUzWK9uKO3W2V/getting-started/technical-overview/instructions)

      * [Technical Glossary](/phoenix-dex/tRIkEFlLUzWK9uKO3W2V/getting-started/technical-overview/technical-glossary)

      * [Seats](/phoenix-dex/tRIkEFlLUzWK9uKO3W2V/getting-started/technical-overview/seats)

        * [Phoenix Seat Manager Program](/phoenix-dex/tRIkEFlLUzWK9uKO3W2V/getting-started/technical-overview/seats/phoenix-seat-manager-program)

      * [Units](/phoenix-dex/tRIkEFlLUzWK9uKO3W2V/getting-started/technical-overview/units)

      * [Market Addresses](/phoenix-dex/tRIkEFlLUzWK9uKO3W2V/getting-started/technical-overview/market-addresses)

    * [Market Maker Overview](/phoenix-dex/tRIkEFlLUzWK9uKO3W2V/getting-started/market-maker-overview)

    * [Developer Overview](/phoenix-dex/tRIkEFlLUzWK9uKO3W2V/getting-started/developer-overview)

      * [Rust SDK](/phoenix-dex/tRIkEFlLUzWK9uKO3W2V/getting-started/developer-overview/rust-sdk)

[Powered by
GitBook](https://www.gitbook.com/?utm_source=content&utm_medium=trademark&utm_campaign=O6I6v4yXZJFfKmgjJZGu)

# Phoenix Overview

[Phoenix](https://www.phoenix.trade/) is a decentralized limit order book on
Solana, supporting markets for spot assets.

###

Why

**A composable liquidity hub is a public good for all of DeFi.** Developers
can build other on-chain applications that either post liquidity to or draw
liquidity from the canonical liquidity source.

AMMs either rely on unsustainable liquidity incentives, or require retail LPs
to consistently lose money. Because Solana has high throughput, fast blocks,
and low fees, Solana DEXs can support active liquidity provisioning. This
enables professional market makers to provide tighter and deeper liquidity
while still being profitable and sustainable.

###

Technical Features

  * Phoenix has instant settlement. Unlike existing order books on Solana, Phoenix doesn't require an asynchronous crank to settle trades.

  * Phoenix is maximally composable. Phoenix's sensible interfaces and small number of accounts required mean that traders can fit more instructions into a single transaction.

  * Phoenix cleanly exposes data. All market events (limit order placed, limit order cancelled, fills, etc.) are written on-chain, so it's easy for traders to query the full live and historical state of all Phoenix markets.

###

Decentralization

The Phoenix program source will be made public before mainnet launch, and the
deployed version will be a verified build.

Market listings are permissionless and no admin controls will exist on the
Phoenix program. The Ellipsis Labs team will control the initial program
upgrade authority via multisig, with plans to renounce the upgrade authority
once the program has been battle-tested.

[NextTechnical Overview](/phoenix-dex/tRIkEFlLUzWK9uKO3W2V/getting-
started/technical-overview)

Last updated 9 months ago

On this page

  * Why
  * Technical Features
  * Decentralization

