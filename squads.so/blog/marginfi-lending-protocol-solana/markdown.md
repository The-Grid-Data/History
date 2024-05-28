s m a r t

w a l l e t s

a t

l i g h t s p e e d

[Squads](../)

[Protocol](../protocol)

[Extension](../extension)

[Use Cases](../use-cases)

[About](https://www.sqds.io/)

[Blog](../blog)

[](../)

Get started

# Project Spotlight: marginfi - A New Borrow/Lend Protocol

Aug 22, 2023

![marginfi-solana-lending-protocol-borrow-lend-mrgnlend-solana-interest-rate-
apy-lending-sol-jitosol-
msol](https://framerusercontent.com/images/Mpc9bwmMGA7OcH76Is4QDFyyQg.png)

Over the last few months, the activity around Solana DeFi has significantly
increased, and marginfi has been one of the major catalysts behind this surge.
With risk management as its primary focus, not many know that behinds the
scenes Squads is also an important factor in protecting the marginfi
protocolâs assets.

This article dives into what marginfi is and how it implemented Squads to
secure the core assets of the protocol, such as its programs, serving as a
guide for other projects to follow the same security practices.

## What is marginfi

While marginfi was initially focusing on margin trading across Solana
perpetual exchanges, it launched earlier this year âmrgnlendâ, a new
decentralized and overcollateralized lending protocol for the Solana
ecosystem. It gained major traction right after the launch of its incentive
program:
[points](https://twitter.com/marginfi/status/1675863618666270722?s=20).

Alongside AMMs, borrowing/lending was one of the first major use cases of DeFi
in the crypto space. It emerged with protocols like Compound and AAVE, which
are now the biggest protocols on Ethereum and EVM chains. On Solana, a gap
appeared after the collapse of FTX, leading marginfi to build its own
borrow/lend protocol to fill this void.

The concept of lending protocols like marginfi is simple. Users looking to
earn interest on their crypto deposit their tokens on the platform. This
capital is then lent to borrowers who are willing to pay an interest because:

  * Lenders take a risk in giving up their capital and potentially suffering an opportunity cost;

  * Borrowers pay this rate to access capital to perform various strategies such as leveraging, shorting, or hedging.  
  

![how-does-marginfi-work-solana-lending-protocol-explained-borrow-lend-sol-
crypto-jitosol-msol-interest-rate-solana-lst-
lsd](https://framerusercontent.com/images/sjphUoNiCiLlwbfbHpar7mihU0.png)

To facilitate liquidity for borrowers, the assets lent by users are pooled
together. The lending and borrowing rates vary based on the demand from each
side - if borrowers are aggressive, the lending rates will increase.
Conversely, if the lending side is much larger than borrowing, the lending
rate will be low as there is more than enough liquidity for borrowers.

Since DeFi users are not tied to a real identity, lending assets without
security safeguards could be dangerous, as borrowers could leave without
paying back their loans. To prevent such situations, overcollateralized
borrow/lend protocols like marginfi require every borrower to deposit
collateral in exchange for borrowing assets deposited on the platform. This
means if a marginfi user wants to borrow BONK, they must first deposit an
accepted asset as collateral, such as JitoSOL or mSOL.

In cases where the user's debt (e.g. BONK in this example) significantly
increases compared to their collateral, or if the collateral's price drops too
much relative to the debt, liquidators can automatically seize their
collateral and sell it on the market to cover the debt and make a profit.
Without liquidators, lenders' positions would be at risk, as the collateral
provided by borrowers could become lower than the debt, preventing lenders
from closing their loan and getting back their assets.

In the past, many crypto borrow/lend protocols have encountered bad debt due
to accepting collateral that couldn't be liquidated for a profit by
liquidators due to low on-chain liquidity and high slippage. This situation
led to bad debt for the protocol and lenders unable to withdraw their initial
deposits.

This is where marginfi stands out. To prevent bad dept to occurring on the
protocol, marginfi core contributors implemented several risk management
mechanisms, such as risk tiers and a risk engine. [The mrgnlend risk
engine](https://docs.marginfi.com/concepts/mechanism-design/risk-management)
evaluates three main factors to determine acceptable risk parameters:

  * **Liquidator Execution Capacity:** The speed at which liquidators can execute liquidations.

  * **Market Depth:** The extent of liquidity available on-chain for liquidators to maintain profitability.

  * **Market Depth Recovery Time:** The duration required for liquidity depth imbalance to recover after large market orders.  
  

![marginfi-risk-management-mechanisms-risk-engine-parameters-mrgnlend-
marginfi-lending-protocol-borrow-lend-sol-solana-jitosol-msol-
liquidations](https://framerusercontent.com/images/Xlv8rXqp5gVPCWHndq2peGIbeM.png)

Additionally, to prevent the main lending pool from being affected by assets
with low liquidity that could potentially cause bad debt, marginfi has an
isolated pool for risky SPL assets that can only be borrowed but not used as
collateral. Low-liquid assets have a high chance of experiencing significant
slippage if the market drops heavily, thus not covering the debt for
liquidators. Simply put, the isolated pool makes sure liquidators only have to
liquidate assets with good on-chain liquidity, minimizing the risks of bad
debt for the protocol and users.

marginfi has also been a pioneer among DeFi protocols with its Points program
that incentivizes usage of the protocol. Users who lend, borrow, and refer
earn points that will provide perks and rewards in the future. Moreover,
marginfi is working on its stableswap AMM and overcollateralized stablecoin,
mUSD, to create a virtuous circle for DeFi strategies within the marginfi
âecosystemâ.

## Why marginfi Implemented Squads into its Operations

![marginfi-risk-management-squads-multisig-program-upgrades-management-best-
practices-mrgnlend-programs-liquidity-incentice-rewards-solana-
multisig](https://framerusercontent.com/images/rUsMAgrBwsBOfL74W3FNcqMcc.png)

As one of the leading lending protocols on Solana, marginfi needs to uphold
the highest security standards. This means implementing strong risk management
mechanisms as we've seen, but also taking program management seriously.

Every protocol on Solana has an authority key that controls changes to its
program(s). Similar to a regular SPL asset, this key can be held by a private
key like a CLI wallet or a hot/cold wallet. However, managing this program
authority key with just one simple wallet is highly risky and inconvenient for
teams due to several reasons:

  * It gives ownership of the program to one person, thus collective decisions are not possible. If this person wants to trigger a malicious upgrade, the rest of the team has no power to prevent it;

  * The security of the whole program relies solely on one key. If it gets compromised, thereâs no extra layer of security - it's too late. 

Hence, marginfi decided to use Squads to delegate the authority of their
mrgnlend programs to a multisig. A Squads multisig allows them to add all the
core contributors and set a threshold for the number of approvals needed to
execute a program upgrade. Control over the program is distributed among the
team members, preventing any malicious upgrades. Plus, even if one member's
key gets compromised, it wonât be enough to push an upgrade of the mrgnlend
program since it requires the approval of multiple members to go through.  
  

![](https://framerusercontent.com/images/zLCpuQPdRzDPqH1Czur3ezPLY.png)

Beyond securing their programs, marginfi also benefits from using a multisig
for managing their treasury. Liquidity incentive rewards are a major component
of DeFi protocols as they help attract liquidity by rewarding users who
deposit into the protocol. With Squads, marginfi core contributors can
securely hold the token rewards from their partners for a short period before
transferring them to the corresponding mrgnlend lending pool.

marginfi is not the only protocol taking security seriously: other projects
like Jupiter, Kamino, Drift, Zeta, Phoenix,
[Jito](https://squads.so/blog/jito-mev-solana-jitosol), Mayan, and many more
are using Squads to safeguard the management of their program upgrades. It has
become the leading multisig solution on Solana, with over $170 million in TVL
across the programs protected by Squads.

We are proud to assist teams like marginfi in building their projects with
peace of mind, and we will continue to provide the best product for on-chain
organization on Solana, helping them manage their on-chain assets securely.

  

### About marginfi

marginfi is a decentralized lending protocol on Solana that prioritizes risk
management to provide a safe and reliable solution for users looking to access
leverage and maximize capital efficiency.

**Learn more**

App: <https://www.marginfi.com/>  
Documentation: <https://docs.marginfi.com/>  
Analytics: <https://analytics.marginfi.com/>  
  

### About Squads

Squads is a crypto company operations platform that simplifies management of
developer and treasury assets for teams building on Solana. Open source,
formally verified, immutable, Squads enables teams to secure their on-chain
assets in a multisig and jointly manage them.

**Learn more**

What is Squads: <https://squads.so/blog/what-is-squads>  
Program management with Multisigs: <https://squads.so/blog/solana-multisig-
program-upgrades-management>  
Why use Multisigs: <https://squads.so/blog/what-are-multisig-wallets>  
How does Jito use Squads: <https://squads.so/blog/jito-mev-solana-jitosol>

  

Continue reading

[![solana-treasury-stablecoins-landscape-solutions-usdc-usdt-usdy-ybx-
diversify-stable-treasury-euroe-vchf-maple-credix-stablecoin-yield-
solana](https://framerusercontent.com/images/0bRVstnkv4oB5BpXjXmmQiSc.png)The
Current Stablecoin Landscape on Solana for Enterprise TreasuryMarch 13,
2024](./stablecoins-overview-solana)[![pyth-token-airdrop-solana-squads-
multisig-pyth-allocation-grant-team-pyth-staking-token-governance-squads-app-
squads-
protocol](https://framerusercontent.com/images/owWa2e8vUVngZkQfEWqZ8xinX0.png)Squads
Receives Allocation of $PYTH TokensFebruary 8, 2024](./pyth-airdrop-
allocation)[![solana-defi-ecosystem-state-overview-solana-defi-projects-list-
ecosystem-defi-solana-
summer](https://framerusercontent.com/images/rVTc4yu2ZCZ4qqXFy0sVEIyptc.png)An
Overview of the Solana DeFi Ecosystem (2023)July 14, 2023](./state-solana-
defi-ecosystem)

[](../)

All rights reserved

Â© Squads Protocol 2024

Product

[Squads](../)

[Protocol](../protocol)

[Extension](../extension)

[Use Cases](../use-cases)

[Why Multisig](https://squads.so/blog/what-are-multisig-wallets)

Resources

[Github](https://github.com/Squads-Protocol)

[SDK](https://www.npmjs.com/package/@sqds/multisig)

[Documentation](https://docs.squads.so/main/basics/welcome-to-squads)

[Blog](../blog)

[Multisig vs MPC](https://squads.so/blog/mpc-wallets-risks-vs-multisig)

Company

[About](../about)

[Brand assets](../brand-assets)

[Twitter](https://twitter.com/squadsprotocol)

[Discord](https://discord.com/invite/YPXz64TrKs)

[Farcaster](https://warpcast.com/squads)

Legal

[Terms of Service](../legal/terms-of-service)

[Privacy Policy](../legal/privacy-policy)

[Contact us](https://discord.com/invite/YPXz64TrKs)

