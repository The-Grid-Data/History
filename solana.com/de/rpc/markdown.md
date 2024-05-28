This website uses cookies to offer you a better browsing experience. Find out
more on how we use cookies.

Opt-out[Details](/de/privacy-policy#collection-of-information)

Accept

[![Solana](/_next/static/media/logotype.e4df684f.svg)](/de)

  * Learn
  * Developers
  * Solutions
  * Network
  * Community

Search```K`

# RPC Infrastructure

**Overview:**  RPC requests are an application’s gateway to the Solana
cluster. The requests are serviced by aptly named RPC Nodes, which are
typically dedicated to the task rather than participating in consensus.
Nevertheless, from an application user’s perspective, poor RPC performance is
no different from poor cluster performance. To give your users a great
experience and show off Solana’s speed and low-latency, it is important to
have RPC infrastructure that is up to the task.

**Development:**  Developers are encouraged to use a local cluster during
development, especially in the early stages and for testing. Local clusters
are more flexible than the public offerings, granting the freedom to run
unoptimized early iterations. The easiest way to run a local cluster is with
the [solana-test-validator](https://docs.solana.com/developing/test-validator)
binary, included in the Solana CLI Tools suite. Once the application reaches a
stable state, deploying on a public cluster becomes more appropriate.

Like all code optimization tasks, when it comes to RPC requests, less is more.
Avoid making frequent, repetitive calls for the same data. Avoid building
clients that make RPC requests directly. “Backend-less dApps” are a myth; you
are just pummelling someone else’s infrastructure. Cache expensive calls
(especially getProgramAccount, getSignaturesForAddress2, and
getConfirmedBlock) in an app-optimized way and serve your users from the
cache. Taking the time to optimize your code before going live can save you a
lot of headaches from poor user experience reports, and can significantly
reduce your infrastructure spend.

## Free Services

Several providers offer free RPC access to the public Solana clusters. These
services are good for real-world testing, early demos, and small, private beta
programs. Keep in mind that you get exactly what you are paying for. Free
services typically do not autoscale, are rate-limited, offer no SLA, and are
not afraid to ban abusers. When an application is ready to be opened to the
public, it is time to invest in private RPC access.

**Some free RPC providers:**

**Testnet**

  * [https://api.testnet.solana.com](https://api.testnet.solana.com/)

**Devnet**

  * [https://api.devnet.solana.com](https://api.devnet.solana.com/)
  * <https://rpc.ankr.com/solana_devnet>
  * [Helius](https://helius.xyz/)
  * [QuickNode](https://www.quicknode.com/chains/sol)

**Mainnet-beta**

  * [https://api.mainnet-beta.solana.com](https://api.mainnet-beta.solana.com/)
  * [Syndica](https://syndica.io/)
  * [Blockdaemon](https://www.blockdaemon.com/protocols/solana)
  * <https://rpc.ankr.com/solana>
  * [GetBlock](https://getblock.io/nodes/sol/)
  * [Helius](https://helius.xyz/)
  * [QuickNode](https://www.quicknode.com/chains/sol)

## **﻿Private Services**

Due to the variability in RPC requirements between applications, generalized
public RPC infrastructure rarely fits the bill. To ensure users get a good
experience, public facing applications need to secure their own private RPC
access. This will allow you to autoscale based on user demand, relax rate
limits according to your application, and have peace of mind that other
applications’ users won’t crowd yours out. Several organizations offer high-
availability, on-demand RPC services; see below. If none of the providers are
a good fit and you’re up to the task of running your own RPC service, please
reach out to the Solana Foundation for guidance.

  * [QuickNode](https://www.quicknode.com/chains/sol) (shared)
  * [Triton/RPC Pool](https://triton.one/) (shared and dedicated)
  * [Chainflow](https://chainflow.io/contact/) (dedicated)
  * [Chainstack](https://chainstack.com/build-better-with-solana/) (shared and dedicated)
  * [GenesysGo](https://genesysgo.com/) (dedicated)
  * [Figment](https://datahub.figment.io/sign_up?service=solana) (shared)
  * [Foundation Server Program](https://solana.org/delegation-program) \- bare metal at a discount to run-your-own
  * [Syndica](https://syndica.io/)
  * [Alchemy](https://www.alchemy.com/solana) (shared)
  * [Blockdaemon](https://blockdaemon.com/marketplace/solana/)
  * [Ankr](https://www.ankr.com/)
  * [GetBlock](https://getblock.io/nodes/sol/)
  * [Helius](https://helius.xyz/)
  * [NOWNodes](https://nownodes.io/nodes/solana-sol) (shared and dedicated)

![](https://cdn.builder.io/api/v1/pixel?apiKey=ce0c7323a97a4d91bd0baa7490ec9139)![](https://cdn.builder.io/api/v1/pixel?apiKey=ce0c7323a97a4d91bd0baa7490ec9139)![](https://cdn.builder.io/api/v1/pixel?apiKey=ce0c7323a97a4d91bd0baa7490ec9139)![](https://cdn.builder.io/api/v1/pixel?apiKey=ce0c7323a97a4d91bd0baa7490ec9139)![](https://cdn.builder.io/api/v1/pixel?apiKey=ce0c7323a97a4d91bd0baa7490ec9139)![](https://cdn.builder.io/api/v1/pixel?apiKey=ce0c7323a97a4d91bd0baa7490ec9139)![](https://cdn.builder.io/api/v1/pixel?apiKey=ce0c7323a97a4d91bd0baa7490ec9139)![](https://cdn.builder.io/api/v1/pixel?apiKey=ce0c7323a97a4d91bd0baa7490ec9139)![](https://cdn.builder.io/api/v1/pixel?apiKey=ce0c7323a97a4d91bd0baa7490ec9139)![](https://cdn.builder.io/api/v1/pixel?apiKey=ce0c7323a97a4d91bd0baa7490ec9139)![](https://cdn.builder.io/api/v1/pixel?apiKey=ce0c7323a97a4d91bd0baa7490ec9139)![](https://cdn.builder.io/api/v1/pixel?apiKey=ce0c7323a97a4d91bd0baa7490ec9139)![](https://cdn.builder.io/api/v1/pixel?apiKey=ce0c7323a97a4d91bd0baa7490ec9139)![](https://cdn.builder.io/api/v1/pixel?apiKey=ce0c7323a97a4d91bd0baa7490ec9139)![](https://cdn.builder.io/api/v1/pixel?apiKey=ce0c7323a97a4d91bd0baa7490ec9139)![](https://cdn.builder.io/api/v1/pixel?apiKey=ce0c7323a97a4d91bd0baa7490ec9139)![](https://cdn.builder.io/api/v1/pixel?apiKey=ce0c7323a97a4d91bd0baa7490ec9139)

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

