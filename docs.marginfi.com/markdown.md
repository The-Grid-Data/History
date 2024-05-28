[![Logo](https://docs.marginfi.com/~gitbook/image?url=https%3A%2F%2F3821122071-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-
x-
prod.appspot.com%2Fo%2Fspaces%252F8hWN5YwVh2AYTRXK1REu%252Flogo%252FscAo1R3HKu23kMNzP4a6%252Fmarginfi-
logomark-
slate.png%3Falt%3Dmedia%26token%3D1289736f-78d3-458b-bd7e-35a0e079c9a3&width=192&dpr=4&quality=100&sign=8d73883f309e28bd60bb788caf9cfb2c14ec2f9cbe3ab371d2b764464d30e78c)![Logo](https://docs.marginfi.com/~gitbook/image?url=https%3A%2F%2F3821122071-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-
x-
prod.appspot.com%2Fo%2Fspaces%252F8hWN5YwVh2AYTRXK1REu%252Flogo%252FscAo1R3HKu23kMNzP4a6%252Fmarginfi-
logomark-
slate.png%3Falt%3Dmedia%26token%3D1289736f-78d3-458b-bd7e-35a0e079c9a3&width=192&dpr=4&quality=100&sign=8d73883f309e28bd60bb788caf9cfb2c14ec2f9cbe3ab371d2b764464d30e78c)](/)

[ Launch App](https://app.marginfi.com)

SearchCtrl \+ K

  * [What is mrgn?](/)

  * [The marginfi Protocol](/marginfi-protocol)

  * Community

    * [Twitter](https://twitter.com/marginfi)
    * [Discord](https://discord.com/invite/wbKERVhQcs)
    * [Medium](https://medium.com/marginfi)
    * [Substack](https://mrgn.substack.com/)
    * [Spotify](https://open.spotify.com/show/0sgdNFaGijvlT5y9BeQ97l)
    * [Media Pack](https://www.dropbox.com/sh/5ljf5fniaoync7k/AACH_wTQQRdcy7Ipcy7ODmt1a?e=2&dl=0)
  * Concepts

    * [The Basics](/concepts/the-basics)

      * [Lending + Borrowing](/concepts/the-basics/lending-+-borrowing)

      * [Fees + Yield](/concepts/the-basics/fees-+-yield)

      * [Account Health](/concepts/the-basics/account-health)

    * [Mechanism Design](/concepts/mechanism-design)

      * [Oracle usage](/concepts/mechanism-design/oracle-usage)

      * [Interest rate mechanism](/concepts/mechanism-design/interest-rate-mechanism)

      * [Risk management](/concepts/mechanism-design/risk-management)

        * [Risk Tiers](/concepts/mechanism-design/risk-management/risk-tiers)

        * [Risk Engine](/concepts/mechanism-design/risk-management/risk-engine)

          * [Liquidator execution capacity](/concepts/mechanism-design/risk-management/risk-engine/liquidator-execution-capacity)

          * [Market depth](/concepts/mechanism-design/risk-management/risk-engine/market-depth)

          * [Market depth recovery time](/concepts/mechanism-design/risk-management/risk-engine/market-depth-recovery-time)

          * [Configuring protocol constraints](/concepts/mechanism-design/risk-management/risk-engine/configuring-protocol-constraints)

    * [Liquid Staking Token (LST) User Guide](/concepts/liquid-staking-token-lst-user-guide)

    * [mrgnlend User Guide](/concepts/mrgnlend-user-guide)

    * [Listing Criteria](/concepts/listing-criteria)

  * Contracts

    * [marginfi v2: mrgnlend](/contracts/marginfi-v2-mrgnlend)

    * [Liquidity Incentive Program (LIP)](/contracts/liquidity-incentive-program-lip)

    * [$YBX](/contracts/usdybx)

  * Liquidators

    * [Example marginfi v2 liquidator](https://github.com/mrgnlabs/mrgn-ts/tree/main/apps/alpha-liquidator)
  * Security

    * [Audits](/security/audits)

    * [Fuzz tests](/security/fuzz-tests)

  * SDKs

    * [Typescript](/sdks/typescript)

    * [Rust](/sdks/rust)

  * Analytics

    * [Realtime 24h analytics](/analytics/realtime-24h-analytics)

  * Contributing

    * [Developers](/contributing/developers)

      * [Github](https://github.com/mrgnlabs)

    * [Technical Writers](/contributing/technical-writers)

[Powered by
GitBook](https://www.gitbook.com/?utm_source=content&utm_medium=trademark&utm_campaign=8hWN5YwVh2AYTRXK1REu)

# What is mrgn?

Protocol, Interface, Company

To begin, it's important to make a clear distinction between different areas
of "mrgn", a growing ecosystem of entities and projects that may confuse new
users.

  * **MRGN, Inc:** The company which initially developed the marginfi protocol, along with some associated web interfaces, software development kits (SDKs), data analytics, and risk management systems.

  * **The marginfi Protocol** :**** Intentionally branded in _all lowercase_ , marginfi is a suite of persistent smart contracts that together create a composable defi-native prime brokerage, a protocol that facilitates peer-to-peer lending and portfolio management of trader positions across blockchains.

  * **mrgnlend:** mrgnlend is an overcollateralized borrow/lend protocol embedded within marginfi. It's the only product live in the marginfi ecosystem today. mrgnlend allows you to borrow, and it allows you to lend.

  * **The marginfi Interface:** A web interface that allows for easy interaction with the marginfi protocol. The interface is only one of many ways one may interact with the marginfi protocol.

[NextThe marginfi Protocol](/marginfi-protocol)

Last updated 6 days ago

On this page

Was this helpful?

![Logo](https://docs.marginfi.com/~gitbook/image?url=https%3A%2F%2F3821122071-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-
x-
prod.appspot.com%2Fo%2Fspaces%252F8hWN5YwVh2AYTRXK1REu%252Flogo%252FzWcZEf1mVa77pGYEgR4R%252Flogo.png%3Falt%3Dmedia%26token%3D950eaa8a-8202-4ca5-9820-bf941318ee48&width=320&dpr=4&quality=100&sign=13e5855381bf47ee907e36ff740776ea10836e4bd45405b4193eba230e829d3f)![Logo](https://docs.marginfi.com/~gitbook/image?url=https%3A%2F%2F3821122071-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-
x-
prod.appspot.com%2Fo%2Fspaces%252F8hWN5YwVh2AYTRXK1REu%252Flogo%252FzWcZEf1mVa77pGYEgR4R%252Flogo.png%3Falt%3Dmedia%26token%3D950eaa8a-8202-4ca5-9820-bf941318ee48&width=320&dpr=4&quality=100&sign=13e5855381bf47ee907e36ff740776ea10836e4bd45405b4193eba230e829d3f)

Developers

[Feedback](https://marginfi.canny.io/mrgnlend)

Github

[Organization](https://github.com/mrgnlabs)[mrgn-
ts](https://github.com/mrgnlabs/mrgn-ts)

Ecosystem

[Home](https://www.marginfi.com)[App](https://app.marginfi.com)[Analytics
(TBA)](https://analytics.marginfi.com)[Brand Assets
(TBA)](https://brand.marginfi.com)

Community

[Twitter](https://twitter.com/marginfi)[Discord](https://discord.gg/wbKERVhQcs)

