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

# Project Spotlight: Jito - Efficient MEV for Solana

Jun 19, 2023

![jito-labs-solana-mev-jito-token-jitosol-jito-foundation-validator-client-
squads-
multisig](https://framerusercontent.com/images/39PJX7pFFgz3PUq32AoIuPYBaRA.png)

Many teams on Solana are using Squads for their operations, whether it's for
treasury management, programs, validators, and more. This article introduces
our new Project Spotlight series, where we explore some of the projects using
Squads, how they operate, and how they secure their operations and protocol
with the leading multisig solution on Solana. On top of discovering new
projects, these articles will be helpful for teams looking to understand how
they can benefit from using a multisig for their company.

This first article covers Jito, a major player on Solana that is behind Jito
Labs and Jito Foundation (JitoSOL). Weâll dive into the MEV infrastructure
and products they built to make the Solana network more efficient while
increasing rewards for validators and stakers. The second part of this article
will unpack how Jito manages its treasury and programs with Squads for better
security.

## What is Jito - MEV Infrastructure on Solana

In order to understand what Jito does and its role on Solana, with first need
to unravel what MEV is and the problems it caused on the network before Jito's
solution entered the picture.

MEV, short for Maximal Extractable Value, represents the profit opportunities
that can be extracted by validators and participants of a blockchain network
by ordering transactions. In [Solana's model](https://medium.com/chorus-
one/analyzing-mev-instances-on-solana-c30d06953ed8), validators take turns in
a set pattern to create blocks (batches of processed transactions). The
validator that's in charge at the moment decides the order of transactions in
that block. Knowing which validator will be the leader at a given time is
public information. MEV traders can exploit this by focusing on the leader
validator and either attempt to work with him or forward as many transactions
as possible to make sure they are placed in a favorable order in the block,
helping them make a profit.

For example, imagine there is a large order on a decentralized exchange (DEX)
that is expected to decrease the price of an asset, causing a price imbalance
between two exchanges. Due to the large order's execution on DEX A, the pool
price has decreased to $19.70, while on DEX B the price hasn't changed and is
still at $20. MEV searchers will detect this price imbalance and race to
capture this arbitrage opportunity by buying low on DEX A and then selling
high on DEX B. While arbitrage is a common type of MEV, it comes in [many
other forms](https://ethereum.org/en/developers/docs/mev/#mev-examples) such
as: NFT mints, liquidations, sandwiches, JIT liquidity, and more.  
  

![what-is-mev-jito-labs-mev-example-arbitrage-mev-search-jitosol-bundles-jito-
solana-squads-mev-transaction-maximum-extractable-
value](https://framerusercontent.com/images/DcxRyEI04JI7O8wUfQQrh0s2PSc.png)

MEV was for a long time a significant problem on Solana. Rather than working
with validators, MEV searchers would spam the network with transactions to
increase their chances of having them processed first. This was because the
potential profits were much larger compared to the low fees of the chain, but
also because there wasn't an easy way for MEV traders to collaborate with
validators. Consequently, Solana validators were burdened with processing
these MEV transactions, leading to network congestion and reducing usability
for users. But that was until Jito.

Jito developed a solution to those MEV issues on Solana with their [Jito-
Solana validator client](https://medium.com/@Jito-Foundation/jito-solana-is-
now-open-source-e1028c53fae1), a fork of the main Solana Labs client. This
software package is what allows anyone to run a validator on the Solana
blockchain to process transactions. With this second client, Jito provides an
efficient way to deal with spamming from MEV searchers compared to the main
validator client, thanks to three main features:

  * **Bundles** : MEV searchers can send a list of transactions that are executed sequentially, atomically, and all-or-nothing. Bundles streamline the submission of transactions by grouping them together, which helps in reducing network congestion and improving transaction processing efficiency;

  * **Block Engine** : It connects MEV searchers and validators via an off-chain blockspace auction. The Jito Block Engine simulates every transaction combination and forwards the highest paying batch of Bundles to validators;

  * **Relayer** : Essentially, it helps in filtering and verifying transactions on a separate server, thereby offloading some of the responsibilities that would otherwise fall on the validators. It then submits verified transactions to the Block Engine and validators.  
  

![jito-mev-client-solana-jito-labs-validator-client-firedancer-jito-bundles-
relayer-jito-foundation-block-engine-
squads](https://framerusercontent.com/images/QyqxL74Lcutaap027dR5VJmEGU.png)

In practice, this is what it looks like for validators and traders to use the
Jito client:

  * MEV traders submit bids for sequences of transactions (bundles) they believe are profitable;

  * Jitoâs Block engine runs simulations to determine the combination of transactions that offers the highest value;

  * The filtered bids are then sent to Jito-Solana validators to process those bundled transactions.

Validators thus receive higher rewards than they usually would with the Solana
Labs validator client. Not only this increases profit for validators, this
also reduces spamming and consequently network congestion. MEV searchers can
now send transactions with tips to encourage validators to process their
transactions first, which is more efficient than spamming the network and
hoping their transactions get processed. In the end, it makes spam bots
ineffective since transactions are prioritized by the highest payer.

The particularly unique feature about Jito is that a part of the fees from
these tradersâ bids is distributed to [JitoSOL](https://www.jito.network/),
Jitoâs liquid staking solution. This enables Jito stakers to earn MEV
rewards in addition to SOL staking rewards. It also means that anyone who
stakes SOL with the Jito [stake pool](https://solana.org/stake-pools) can
access a portion of those MEV opportunities, without its risks.  
  

![jitosol-solana-mev-liquid-staking-token-solana-jito-foundation-mev-rewards-
staking-rewards-jito-solana-validator-client-mev-
searchers](https://framerusercontent.com/images/WOaDAsfNXSu9VvfGOL8CQflVLpI.png)

Liquid staking allows users to stake tokens on a Proof-of-Stake blockchain,
securing the network, while retaining liquidity. Instead of locking up tokens,
users receive liquid staking tokens (LSTs) in return, which represent
ownership of the staked assets and rewards. These LSTs can be traded,
transferred, or used in DeFi applications. In our case, users can delegate
their SOL tokens to the Jito stake pool and receive a "proof" of their deposit
in the form of JitoSOL tokens. All those SOL tokens delegated accrue in value
by accumulating MEV and staking rewards and can be redeemed for JitoSOL tokens
at any time.

The Jito stake pool delegates the SOL tokens to the top validators running the
Jito-Solana validator client, in order to receive MEV rewards (in addition to
staking emissions/rewards).

## How Jito Secures its Operations with Squads

Jito uses the Squads multisig platform for various aspects of their company.
As a quick reminder, Squads allows teams to create a
[multisig](https://squads.so/blog/what-are-multisig-wallets) on Solana to
secure their on-chain assets. A multisig, short for multi-signature, is
governed by multiple owners/private keys and requires multiple signatures for
moving or accessing the assets held within it. With a solution like Squads,
teams can for instance secure their treasury, as well as manage their program
upgrades.  
  

![what-is-multisig-multisignature-wallet-solana-multisig-
explained](https://framerusercontent.com/images/lmaTdhVmvrkUn4wgyvAh5E8sERo.png)

Jito's first use of Squads is to secure the stake pool manager of JitoSOL.
Every stake pool on Solana has an authority key that manages critical
parameters, such as the fee structure of the stake pool. Since it is crucial
for overall control and configuration of JitoSOL, this key needs rigorous
security measures - a multisig was the most appropriate solution to fulfill
these security requirements.

Along with holding the Jito stake pool manager key within a multisig, Jito
also uses Squads to manage upgrades to their programs. This means that any
change that would require to update one of their programs held within their
multisig, such as the Jito MEV tip program, needs multiple signatures from the
stakeholders for the transaction upgrade to through.

Additionally, all revenue generated from the Jito stake pool is deposited in a
Squads multisig for enhanced security and transparency. Treasury management is
a great use case of multisigs, since in addition to collective management they
bring on-chain transparency, which is not possible with traditional custodians
or centralized exchanges. A treasury covers a wide range of assets such as
native tokens, grants, funds raised, liquidity mining rewards, or in the case
of Jito, revenue streams.

In short, using a solution like Squads is beneficial for Jito as it enables
its contributors to:

  * Secure the stake pool manager in a safe place - even if one of the multisig key owners is compromised, it doesnât affect the stake pool manager;

  * Monitor all upgrades happening on their programs and prevent unauthorized actions;

  * Have transparency and collective control over the revenue generated by the Jito stake pool.  
  

![jito-labs-multisig-jitosol-stake-pool-manager-jito-foundation-treasury-
programs-squads-multisig-solana-jito-mev-
bundles](https://framerusercontent.com/images/EmVRoItYgHnMsCWmgavGbKGwWg.png)

Since the Squads multisig program is
[immutable](https://twitter.com/SquadsProtocol/status/1628776620243963904)/non-
upgradeable, it ensures that only the owners of a multisig can access or move
their assets. Moreover, Squads is open-source, allowing anyone to check how
the code works.

Multisig is by far the most advanced way for crypto companies to manage their
on-chain assets, as traditional solutions donât offer enough customization
or arenât adapted to the needs of teams. For instance, managing program
upgrades with a cold wallet means relying on one person/key for the entire
security of the protocol, and it completely removes the possibility of any
collective management. This approach does not work for teams, who need robust
safeguards against unauthorized actions on their programs. The same applies to
treasury management and any on-chain assets managed by a crypto business.

By using Squads, Jito is among the teams on Solana that implements the highest
measures possible to manage their projectâs assets with multisig security.
Not only does this protect them from malicious attacks, it also adds a layer
of confidence for the JitoSOL users and the ecosystem more broadly. As more
crypto projects take the right measures to protect their protocols and its on-
chain assets to the greatest extent possible, it will help create a safer
ecosystem and foster more trust for both current users and newcomers.

  

### About Jito

Jito Labs is a leading MEV infrastructure company building high-performance
systems to scale Solana and maximize validator rewards. Jito's software
enables Solana to run more efficiently and earn MEV rewards. Jitoâs liquid
staking token, JitoSOL, is the first MEV-boosted LST on Solana. JitoSOL
delivers high rewards through MEV with a decentralized validator set.

**Learn more**

Jito Labs: <https://www.jito.wtf/>  
Jito-Solana Client: <https://jito-foundation.gitbook.io/mev/jito-solana/>  
JitoSOL: <https://www.jito.network/>  
Documentation: <https://jito-foundation.gitbook.io/>  
  

### About Squads

Squads is a crypto company operations platform that simplifies management of
developer, creator, and treasury assets for teams building on Solana and SVM.
Open source, formally verified, immutable, Squads enables teams to secure
their on-chain assets in a multisig and jointly manage them.

**Learn more**

What is Squads: <https://squads.so/blog/what-is-squads>  
Why use Multisigs: <https://squads.so/blog/what-are-multisig-wallets>  
Stake SOL into the Jito stake pool on Squads:
<https://docs.squads.so/squads-v3-docs/integrations/staking/jitosol>

  

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
allocation)[![marginfi-solana-lending-protocol-borrow-lend-mrgnlend-solana-
interest-rate-apy-lending-sol-jitosol-
msol](https://framerusercontent.com/images/Mpc9bwmMGA7OcH76Is4QDFyyQg.png)Project
Spotlight: marginfi - A New Borrow/Lend ProtocolAugust 22, 2023](./marginfi-
lending-protocol-solana)

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

