[![Logo](https://docs.solend.fi/~gitbook/image?url=https%3A%2F%2F1260822717-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-
legacy-
files%2Fo%2Fspaces%252F-MfHlKeK0wEppVzgq36Q%252Favatar-1627458873723.png%3Fgeneration%3D1627458874000935%26alt%3Dmedia&width=32&dpr=4&quality=100&sign=8efa161715cd9cb039a7268ba0982bbc639bfb85e6bcf8ab102dc6602d480ffc)![Logo](https://docs.solend.fi/~gitbook/image?url=https%3A%2F%2F1260822717-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-
legacy-
files%2Fo%2Fspaces%252F-MfHlKeK0wEppVzgq36Q%252Favatar-1627458873723.png%3Fgeneration%3D1627458874000935%26alt%3Dmedia&width=32&dpr=4&quality=100&sign=8efa161715cd9cb039a7268ba0982bbc639bfb85e6bcf8ab102dc6602d480ffc)Solend](/)

[ App](https://solend.fi)[ Twitter](https://twitter.com/solendprotocol)[
Discord](https://discord.gg/solend)

SearchCtrl \+ K

  * [Introduction to Solend](/)

  * Getting Started

    * [Start Here (Desktop)](/getting-started/start-here-desktop)

    * [Start Here (Mobile)](/getting-started/start-here-mobile)

    * [Supply & Borrow APY](/getting-started/supply-and-borrow-apy)

    * [Liquidations](/getting-started/liquidations)

    * [Risks](/getting-started/risks)

    * [FAQ](/getting-started/faq)

    * [Debugging FAQ](/getting-started/debugging-faq)

  * DAO & Token

    * [DAO](/daotoken/dao)

    * [Token](/daotoken/token)

    * [IDO](/daotoken/ido)

  * Protocol

    * [Solend Pools](/protocol/solend-pools)

    * [Parameters](/protocol/parameters)

    * [Fees](/protocol/fees)

    * [Liquidity Mining](/protocol/liquidity-mining)

    * [Limits](/protocol/limits)

    * [Media](/protocol/media)

    * [Audit](/protocol/audit)

    * [Bug Bounty](/protocol/bug-bounty)

    * [Oracles](/protocol/oracles)

  * Permissionless Pools

    * [Introduction](/permissionless-pools/introduction)

    * [Risks](/permissionless-pools/risks)

    * [Pre-Listing Checklist](/permissionless-pools/pre-listing-checklist)

    * [Listing a Pool](/permissionless-pools/listing-a-pool)

    * [Post-Listing](/permissionless-pools/post-listing)

    * [Managing a Pool](/permissionless-pools/managing-a-pool)

    * [Switchboard v2 Guide](/permissionless-pools/switchboard-v2-guide)

    * [Pool Ideas](/permissionless-pools/pool-ideas)

  * Architecture 

    * [Building Blocks](/architecture/building-blocks)

    * [Software Flowchart](/architecture/software-flowchart)

    * [Access Controls](/architecture/access-controls)

    * [User Instructions](/architecture/user-instructions)

    * [Computing Supply & Borrows](/architecture/computing-supply-and-borrows)

    * [cTokens](/architecture/ctokens)

      * [cToken Addresses](/architecture/ctokens/ctoken-addresses)

    * [Addresses](/architecture/addresses)

      * [Mainnet](/architecture/addresses/mainnet)

        * [Main Pools](/architecture/addresses/mainnet/main-pools)

        * [Isolated Pools](/architecture/addresses/mainnet/isolated-pools)

      * [Devnet](/architecture/addresses/devnet)

  * Integrations

    * [Introduction](/developers/introduction)

    * [Integration Guide](/developers/integration-guide)

    * [Solend LITE](/developers/solend-lite)

    * [Liquidators](/developers/liquidators)

    * [Flash Loans](/developers/flash-loans)

    * [Developer Referral Fee](/developers/developer-referral-fee)

    * [Resources and FAQ](/developers/resources-and-faq)

[Powered by
GitBook](https://www.gitbook.com/?utm_source=content&utm_medium=trademark&utm_campaign=-MfHlKeK0wEppVzgq36Q)

# cTokens

https://solend.fi/ctokens

cTokens are a _yield-bearing deposit receipt_. It means you can convert USDC
into cUSDC to get a tradeable token that also earns interest on Solend. You
can hold this token in your wallet to continue earning interest, or you can
send it to someone else, and they’ll earn interest.

cTokens open up a world of possibilities for developer integrations. Because
cTokens are just regular SPL tokens, they’re easily composable and compatible
with just about everything! If you’re working on something that uses Solend
cTokens, check out our [Developer Portal](https://dev.solend.fi/) and [Grants
Program](https://dev.solend.fi/docs/grants)!

Take note that cTokens currently do not have liquidity mining, such as
additional SLND or MNDE rewards. You can mint cTokens
[here](https://solend.fi/ctokens).

[![Logo](https://github.com/fluidicon.png)solana-program-library/processor.rs
at 400dd876c51862c21122f7d4378a7c82d996b0ef · solendprotocol/solana-program-
libraryGitHub](https://github.com/solendprotocol/solana-program-
library/blob/400dd876c51862c21122f7d4378a7c82d996b0ef/token-
lending/program/src/processor.rs#L439)

Normally, if you are using our Main Lend/Borrow, your cTokens will be held in
custody by our smart contracts to be used as "collateral" for borrowing
against it. This tool is mainly for developers to integrate our cTokens into
their protocols, and then direct their users here to mint their cTokens.

###

cToken Ratio Calculations:

  * cToken Ratio acts as a % ownership of the LP

  * For a pool with 99 USDC, if you deposit 1 USDC, you will own 1% of the pool

  * When the RefreshReserve occurs, the pool now has 110 USDC. Your 1% is now worth 1.1 USDC.

cToken Ratio is calculated by taking the Total USDC in the reserves / cUSDC in
Circulation.

[PreviousComputing Supply & Borrows](/architecture/computing-supply-and-
borrows)[NextcToken Addresses](/architecture/ctokens/ctoken-addresses)

Last updated 1 year ago

On this page

Was this helpful?

