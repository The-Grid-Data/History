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

##### Table of Contents

  * [Solana public RPC endpoints](/vi/docs/core/clusters#solana-public-rpc-endpoints)
  * [Using explorers with different Clusters](/vi/docs/core/clusters#using-explorers-with-different-clusters)
  * [Devnet](/vi/docs/core/clusters#devnet)
  * [Devnet endpoint](/vi/docs/core/clusters#devnet-endpoint)
  * [Devnet rate limits](/vi/docs/core/clusters#devnet-rate-limits)
  * [Testnet](/vi/docs/core/clusters#testnet)
  * [Testnet endpoint](/vi/docs/core/clusters#testnet-endpoint)
  * [Testnet rate limits](/vi/docs/core/clusters#testnet-rate-limits)
  * [Mainnet beta](/vi/docs/core/clusters#mainnet-beta)
  * [Mainnet beta endpoint](/vi/docs/core/clusters#mainnet-beta-endpoint)
  * [Mainnet beta rate limits](/vi/docs/core/clusters#mainnet-beta-rate-limits)
  * [Common HTTP Error Codes](/vi/docs/core/clusters#common-http-error-codes)

[Scroll to Top](/vi/docs/core/clusters#)

[Edit Page](https://github.com/solana-foundation/developer-
content/tree/main/docs/core/clusters.md)

[Home](/vi)>[Solana Documentation](/vi/docs)>Core Concepts

# [Clusters and Public RPC Endpoints](/vi/docs/core/clusters)

The Solana blockchain has several different groups of validators, known as
[Clusters](/vi/docs/core/clusters). Each serving different purposes within the
overall ecosystem and containing dedicated api nodes to fulfill [JSON-
RPC](/vi/docs/rpc) requests for their respective Cluster.

The individual nodes within a Cluster are owned and operated by third parties,
with a public endpoint available for each.

## Solana public RPC endpoints #

The Solana Labs organization operates a public RPC endpoint for each Cluster.
Each of these public endpoints are subject to rate limits, but are available
for users and developers to interact with the Solana blockchain.

Info

Public endpoint rate limits are subject to change. The specific rate limits
listed on this document are not guaranteed to be the most up-to-date.

### Using explorers with different Clusters #

Many of the popular Solana blockchain explorers support selecting any of the
Clusters, often allowing advanced users to add a custom/private RPC endpoint
as well.

An example of some of these Solana blockchain explorers include:

  * [http://explorer.solana.com/](https://explorer.solana.com/).
  * [http://solana.fm/](https://solana.fm/).
  * [http://solscan.io/](https://solscan.io/).
  * <http://solanabeach.io/>.
  * <http://validators.app/>.

## Devnet #

Devnet serves as a playground for anyone who wants to take Solana for a test
drive, as a user, token holder, app developer, or validator.

  * Application developers should target Devnet.
  * Potential validators should first target Devnet.
  * Key differences between Devnet and Mainnet Beta:
    * Devnet tokens are **not real**
    * Devnet includes a token faucet for airdrops for application testing
    * Devnet may be subject to ledger resets
    * Devnet typically runs the same software release branch version as Mainnet Beta, but may run a newer minor release version than Mainnet Beta.
  * Gossip entrypoint for Devnet: `entrypoint.devnet.solana.com:8001`

### Devnet endpoint #

  * `https://api.devnet.solana.com` \- single Solana Labs hosted api node; rate-limited

#### Example `solana` command-line configuration #

To connect to the `devnet` Cluster using the Solana CLI:

    
    
    solana config set --url https://api.devnet.solana.com

### Devnet rate limits #

  * Maximum number of requests per 10 seconds per IP: 100
  * Maximum number of requests per 10 seconds per IP for a single RPC: 40
  * Maximum concurrent connections per IP: 40
  * Maximum connection rate per 10 seconds per IP: 40
  * Maximum amount of data per 30 second: 100 MB

## Testnet #

Testnet is where the Solana core contributors stress test recent release
features on a live cluster, particularly focused on network performance,
stability and validator behavior.

  * Testnet tokens are **not real**
  * Testnet may be subject to ledger resets.
  * Testnet includes a token faucet for airdrops for application testing
  * Testnet typically runs a newer software release branch than both Devnet and Mainnet Beta
  * Gossip entrypoint for Testnet: `entrypoint.testnet.solana.com:8001`

### Testnet endpoint #

  * `https://api.testnet.solana.com` \- single Solana Labs api node; rate-limited

#### Example `solana` command-line configuration #

To connect to the `testnet` Cluster using the Solana CLI:

    
    
    solana config set --url https://api.testnet.solana.com

### Testnet rate limits #

  * Maximum number of requests per 10 seconds per IP: 100
  * Maximum number of requests per 10 seconds per IP for a single RPC: 40
  * Maximum concurrent connections per IP: 40
  * Maximum connection rate per 10 seconds per IP: 40
  * Maximum amount of data per 30 second: 100 MB

## Mainnet beta #

A permissionless, persistent cluster for Solana users, builders, validators
and token holders.

  * Tokens that are issued on Mainnet Beta are **real** SOL
  * Gossip entrypoint for Mainnet Beta: `entrypoint.mainnet-beta.solana.com:8001`

### Mainnet beta endpoint #

  * `https://api.mainnet-beta.solana.com` \- Solana Labs hosted api node cluster, backed by a load balancer; rate-limited

#### Example `solana` command-line configuration #

To connect to the `mainnet-beta` Cluster using the Solana CLI:

    
    
    solana config set --url https://api.mainnet-beta.solana.com

### Mainnet beta rate limits #

  * Maximum number of requests per 10 seconds per IP: 100
  * Maximum number of requests per 10 seconds per IP for a single RPC: 40
  * Maximum concurrent connections per IP: 40
  * Maximum connection rate per 10 seconds per IP: 40
  * Maximum amount of data per 30 second: 100 MB

Info

The public RPC endpoints are not intended for production applications. Please
use dedicated/private RPC servers when you launch your application, drop NFTs,
etc. The public services are subject to abuse and rate limits may change
without prior notice. Likewise, high-traffic websites may be blocked without
prior notice.

## Common HTTP Error Codes #

  * 403 -- Your IP address or website has been blocked. It is time to run your own RPC server(s) or find a private service.
  * 429 -- Your IP address is exceeding the rate limits. Slow down! Use the [Retry-After](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Retry-After) HTTP response header to determine how long to wait before making another request.

[Previous« Tokens on Solana](/vi/docs/core/tokens)[NextVersioned Transactions
»](/vi/docs/advanced/versions)

  * [Solana Documentation](/vi/docs)

    * [JSON RPC Methods](/vi/docs/rpc)
    * [Terminology](/vi/docs/terminology)
  * Introduction

    * [Overview](/vi/docs/intro/overview)
    * [Wallets](/vi/docs/intro/wallets)
    * [Intro to Development](/vi/docs/intro/dev)
  * Core Concepts

    * [Solana Account Model](/vi/docs/core/accounts)
    * [Transactions and Instructions](/vi/docs/core/transactions)
    * [Fees on Solana](/vi/docs/core/fees)
    * [Programs on Solana](/vi/docs/core/programs)
    * [Program Derived Address](/vi/docs/core/pda)
    * [Cross Program Invocation](/vi/docs/core/cpi)
    * [Tokens on Solana](/vi/docs/core/tokens)
    * [Clusters & Endpoints](/vi/docs/core/clusters)
  * Advanced Concepts

    * [Versioned Transactions](/vi/docs/advanced/versions)
    * [Address Lookup Tables](/vi/docs/advanced/lookup-tables)
    * [Confirmation & Expiration](/vi/docs/advanced/confirmation)
    * [Retrying Transactions](/vi/docs/advanced/retry)
    * [State Compression](/vi/docs/advanced/state-compression)
  * Solana Clients

    * [Rust](/vi/docs/clients/rust)
    * [JavaScript / TypeScript](/vi/docs/clients/javascript)
    * [Web3.js API Examples](/vi/docs/clients/javascript-reference)
  * [Economics](/vi/docs/economics)

    * Inflation
      * [Proposed Inflation Schedule](/vi/docs/economics/inflation/inflation-schedule)
      * [Inflation Terminology](/vi/docs/economics/inflation/terminology)
    * [Staking](/vi/docs/economics/staking)
      * [Stake Accounts](/vi/docs/economics/staking/stake-accounts)
      * [Stake Programming](/vi/docs/economics/staking/stake-programming)
  * Developing Programs

    * [Overview](/vi/docs/programs/overview)
    * [Debugging Programs](/vi/docs/programs/debugging)
    * [Deploying Programs](/vi/docs/programs/deploying)
    * [Program Examples](/vi/docs/programs/examples)
    * [FAQ](/vi/docs/programs/faq)
    * [Developing with C](/vi/docs/programs/lang-c)
    * [Developing with Rust](/vi/docs/programs/lang-rust)
    * [Limitations](/vi/docs/programs/limitations)
  * More Information

    * [Add Solana to Your Exchange](/vi/docs/more/exchange)

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

