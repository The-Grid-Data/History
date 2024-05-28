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

# Multisig vs MPC

Jul 31, 2023

![mpc-wallet-multi-party-computation-fireblocks-institutional-wallet-coinbase-
copper-fordefi-mpc-technology-solana-mpc-
multisig](https://framerusercontent.com/images/L6llWmB3jCRHqkDk74lbrYhhlQ.png)

Multisigs have been part of the crypto landscape for some time, but they
seemed to have been overshadowed by the emergence of MPC (Multi-Party
Computation) wallets in recent years. MPC wallets gained popularity and
adoption largely because there were limited alternatives available when they
emerged, and that Multisigs were considered less advanced and not fully
developed. However, this is no longer true, as Multisigs and Smart Wallets are
now quickly improving, offering the same features and user experience.

While we've previously covered the topic of
[Multisig](https://squads.so/blog/what-are-multisig-wallets) extensively, this
article will dive into MPC and explain why we believe that it served as a
temporary solution until more secure options, like Multisigs, could be refined
and optimized.

MPC and Multisig are the two solutions most often recommended for
institutional investors or high-net-worth individuals looking to trade crypto
assets. Although these options seem to offer similar features at first glance,
the aim of this article is also to present the hidden trade-offs of MPC
wallets, which introduce additional risks for users. In contrast, Multisigs
and Smart Wallets are surfacing as more secure and reliable alternatives.

## What Are MPCs Wallets and How Did They Emerge

The term âMPCâ stands for Multi-Party Computation. Generally, MPC allows
two (or more) parties to jointly generate a result (like a transaction
signature), without exposing their private information to each other.

In the context of crypto, the concept of MPC was first implemented to enhance
the security of wallets. Traditional crypto wallets have a single private key,
which, if stolen, could allow unauthorized individuals to access and transfer
the funds in the wallet. To mitigate this risk, the MPC technology splits the
private key into multiple parts, referred to as shares/shards, which are
distributed among multiple parties. No single party has the complete key, and
a transaction can only be authorized if a predefined minimum number of these
parties come together to recreate the key.  
  

![how-mpc-wallets-work-vs-multisig-traditional-wallet-mpc-key-shares-
fireblocks-coinbase-fordefi-mpc-technology-multi-party-computation-vs-
multisig-
technology](https://framerusercontent.com/images/ywTVA404ROCJ75IUN8cUAVN3dM.png)

The emergence of MPC wallets can be traced back to the growth of the crypto
industry around 2018 and the increasing need for secure crypto wallets,
particularly for institutional and high-net-worth investors. The first
companies to adopt MPC technology did so with the intent to offer custody
solutions that were more secure than single key wallets, while also retaining
the convenience of being able to execute transactions on any blockchain like
Bitcoin and Ethereum.

One of the earliest companies to propose and implement Multi-Party Computation
(MPC) in wallet technology was Curv, back in 2018 (later acquired by PayPal in
2021). At that time, Ethereum was merely beginning to emerge as a potentially
âviableâ blockchain alongside Bitcoin, but it wasn't quite ready to
accommodate Smart Wallets or developed Multisigs, and [account
abstraction](https://squads.so/blog/what-is-account-abstraction-ethereum-vs-
solana) wasn't on top of everyoneâs mind as it is today. Safe (formerly
Gnosis Safe), which is now the leading multisig on Ethereum, launched later
the same year. However, it was brand new and wasn't equipped to meet the needs
of institutions that required something more advanced at the time.

Curvâs emergence attracted many institutional investors to crypto such as
[Franklin Templeton](https://decrypt.co/11930/global-fund-franklin-templeton-
enlists-crypto-wallet-service-to-secure-digital-shares). This led to the
development of other MPC providers like ZenGo and Fireblocks, who launched
their solutions around the same time. Multisigs, on the other hand, were not
ready for widespread adoption due to technical limitations (Smart Wallets
weren't even a concept at that time) - institutions and organizations had no
choice but to use MPC wallets for their operations if they wanted a secure
method to trade and interact with crypto assets.

Today, the market is dominated by Fireblocks, Copper, BitGo, Coinbase Prime,
and Ceffu (Binance), all of which employ MPC technology in their wallets. Each
provider has built their own unique solution with specific features since
there isn't a standardized framework for this technology. Most of these MPC
providers use the Threshold Signature Scheme (TSS), an off-chain protocol
that, when combined with MPC, determines how many key shares need to be used
to sign a transaction. This allows the user/service provider to customize
their configuration when setting up their MPC wallet.  
  

![types-of-mpc-wallets-multi-party-computation-centralized-hybrid-fireblocks-
coinbase-mpc-copper-fordefi-institutional-wallet-
tap](https://framerusercontent.com/images/LWsF5XmoapFQqFkCVzOxFCu4nvA.png)

Usually, MPC wallets are classified into two types:

  1. **Centralized MPC:** Here, a single organization retains control of all the key parts in a secure, isolated cloud environment. Institutions such as centralized exchanges or custodial service providers commonly use this model. Despite its operational effectiveness, it potentially exposes assets to internal breaches and single failure points.

  2. **Hybrid MPC:** In this setup, the responsibility of the key shares is divided among the user, the service provider, and an additional third party. This dispersion of control aims to limit the necessity to fully trust a single centralized entity with all the key pieces. Even though it can offer increased security, it still requires a centralized party to safely distribute, oversee, and invalidate key fragments.

While in the early stages of crypto adoption for institutional and high-net-
worth investors all viable solutions leaned towards MPC, times have definitely
changed. Yes, Multisig technology was initially lacking in terms of
products/features and blockchain compatibility, but that's history. Ethereum
has matured beyond its initial potential as a âviableâ blockchain, and its
community and ecosystem actors, like Safe, have worked hard on improving self-
custody solutions. Multiple initiatives around account abstraction have also
made contract/programmable accounts more usable and easier for Multisigs to
operate. Other blockchains, such as Solana, have also gone live, featuring
better compatibility for Smart Wallets and even bypassing some technical
hurdles that Multisig and advanced wallets were facing on EVM.

Overall, it's worth noting that popularity does not necessarily equate to
superiority. While MPC served a need in the past and functioned as a decent
short-term solution, better alternatives have matured. If flexibility is what
you're after, MPC is an appealing choice. However, when it comes to security,
there are numerous reasons why Multisig and Smart Wallets outshines MPC and
offer a superior solution, particularly for institutions where security is
paramount.

## Multisigs and Smart Contract Wallets Have Matured

In contrast to MPC where a single key is divided into several parts, each
managed by a different party, in a Multisig setup each participant has their
own private key. For a transaction to be authorized, it requires approval from
a minimum number of participants, as per the predetermined threshold.

For a long time, multisigs were not widely used due to their complexity and
technical limitations. They were not fully supported by the Ethereum Virtual
Machine and faced challenges when attempting to interact with the network.
Multisigs could not initiate transactions themselves, and Multisig solutions
had to find workarounds for them to work. But much has changed since 2018, and
the implementation of new standards like ERC-4337 has allowed Multisig and
innovative crypto wallets (Smart Wallets) to fully integrate with Ethereum and
EVM chains. On Solana, the landscape of Multisigs and Smart Wallets was
different, given its status as a completely new blockchain with a novel
virtual machine (VM) and programming model. This environment required
developers to take time to deeply understand how to build such solutions. As
the ecosystem matured Solana multisig solutions quickly developed with Squads
being the leading actor.

Smart (contract) wallets are emerging as a next generation of crypto wallets
that, instead of being built on simple user accounts, are built on top of
smart contracts/programs, offering better security features for users than
traditional wallets. Multisig is likely the most known example of Smart
Wallet. Due to being programmable accounts, they can let users do many things
off-chain solutions like MPC cannot do without relying on centralized
entities. [Fuse](https://fuse.squads.so/), built by Squads Labs, will be the
first institutional-grade smart wallet on Solana featuring those unique
features.  
  

![](https://framerusercontent.com/images/FnGd1Bu3ZUEWffNC8M4fui81E8.png)

Compared to the MPC architecture, the design of Smart Wallets is entirely on-
chain at the protocol layer, eliminating the need to rely on any centralized
entity for managing and securing assets. While there are challenges, such as
cross-chain compatibility or full compatibility with dApps, we believe these
are not insurmountable in the long term. It's worth being patient, rather than
rushing to adopt temporary solutions like MPC. Moreover, Smart Wallets are
close to reaching features and UX parity with MPC wallets, while already
surpassing them in security and decentralization.

Additionally, being fully on-chain and built on a smart contract/program adds
many advantages that MPC cannot match. Smart Wallets can easily perform
mutable actions to change their operational setup, allowing flexibility in
management. Each user or organization has control over their wallet's rules
and functionalities. Conversely, MPC wallets typically come with a predefined
set of functionalities and do not offer the same level of customization.  
  

![smart-wallet-multisig-vs-mpc-wallets-which-are-better-pros-and-cons-mpc-vs-
smart-contract-wallet-solana-mpc-
multisig](https://framerusercontent.com/images/mXsrBUKM8x8oTlxN5z0bNMTtmw.png)

Overall, after several years of developing Multisig technology, we believe
Smart Wallets built on top of multi-signature functionality are much safer
than MPC solutions for several reasons:

**Transparency** : Everything happens on-chain, which eliminates any ambiguity
during the transaction process. This is in direct contrast to MPC, where at
many steps of executing a transaction the user has no way to know what's
happening (since everything is done off-chain), which parts of the key signed
the transaction, ultimately leading to [accountability
issues](https://blog.bitgo.com/multi-sig-vs-mpc-which-is-more-
secure-699ecefc8430#:~:text=Signature%20Accountability);

**No dependence on a centralized party** : From creation to adding members,
setting a threshold, and executing a transaction, Smart Wallets do not require
trust in a centralized entity for managing and securing assets. This is very
different from MPC setups who inherently require a trusted centralized party
to secure one or more key shares. This reliance on key shares necessitates
complex and trusted cloud infrastructure, and it opens the possibility for
risks such as insider threats. These vulnerabilities can potentially lead to
the exposure of key shares and, worst, full control over your assets by an
attacker;

**Secure key revocation/rotation** : And that's the biggest risk of MPC
solutions - when setting up the threshold signature scheme (TSS), this part is
immutable and cannot be changed in the future. This means that if someone
within the organization needs to be removed from the setup, you either need to
trust them to return their share and not use it in the future, or your
organization would have to switch to a new MPC wallet to eliminate any risk.
In contrast, Smart Wallets allow for true revocation of any member from the
Multisig program;

**Programmable** : Since MPC is off-chain and has many non-mutable features
like thresholds or key revocation, it is limited in the features it can offer
compared to Smart Wallets. Smart Wallets can implement any feature that can be
coded in a smart contract/program;

**Security logic battle-tested** : Multisig technology has been battle-tested
for years, with Safe being the most significant example on Ethereum with
$40bln+ in assets stored, and Squads, which is used by the largest teams on
Solana. This is very different from MPC solutions, which involve complex
algorithms with no standardized implementation. Most current MPC
implementations are proprietary, with limited public scrutiny. This lack of
transparency makes it hard to verify the security and effectiveness of these
solutions.

And regarding privacy, Solana is about to enable developers to anonymize parts
of their code at the protocol level thanks to Zero-Knowledge (ZK) layer
solutions like [Light Protocol](https://lightprotocol.com/), or
[Elusiv](https://elusiv.io/) for private transfers. This design is superior
since users would be able to set up their own private Multisig/Smart Wallet
and know which parts are anonymized. In contrast, with MPC solutions these
aspects are obscured by default for everyone.

## Moving Beyond MPC Wallets

![vitalik-buterin-mpc-vs-multisig-smart-contract-wallet-are-the-only-option-
vitalik-quote-tweet-mpc-wallet-are-bad-multisig-safe-
squads](https://framerusercontent.com/images/MFmTTTJOmL94mhtWkm4ROJhiv8.png)

While Multisig protocols like Safe and Squads are completely on-chain, open-
source, and formally verified, MPC solutions are the complete opposite and
innately opaque. The algorithms behind MPC are mathematically complex and can
be challenging to implement correctly. They often require expertise in both
cryptography and software engineering. Even slight mistakes in implementation
can lead to significant security vulnerabilities, like for example the private
key information leakage found with GG18 and GG20, which were used by major MPC
providers like [Fireblocks](https://www.fireblocks.com/blog/vulnerabilities-
discovered-and-patched-in-legacy-mpc-algorithm-fireblocks-urges-move-to-mpc-
cmp/) between 2019-2021.

More recently, the [Multichain
incident](https://twitter.com/MultichainOrg/status/1679768407628185600) also
highlighted the operational risks of implementing MPC technology. All the MPC
nodes for Multichain were actually run under the personal cloud server account
of the company's CEO. When the CEO was arrested, all access keys to the
operational account were revoked, meaning no one from the team could access
the funds held within the platform.

Even though MPC technology offers some advantages when it comes to
flexibility, and some underlying solutions such as wallet as a service
providers are great for onboarding mass users at scale (where security is less
at stake compared to solutions made for managing large amounts of crypto
assets), as of today, MPC solutions are not fully suitable to be the
definitive infrastructure for securing large amounts of capital. They hold a
mix of trade-offs to allow for convenience. Moreover, unlike Multisig
technology, which has been widely standardized, the implementations of MPC
vary significantly between providers. This lack of standardization makes it
harder to thoroughly vet and audit MPC solutions, thereby increasing the risk
of undiscovered vulnerabilities.

Looking ahead, we anticipate that MPC providers will begin to incorporate
elements of Multisig technology into their solutions to mitigate these risks.
By combining the strengths of both technologies, it will be possible to create
safer and more robust digital asset custody solutions. However, until this
evolution is complete, teams and institutions must be aware of the risks
involved with pure MPC solutions and carefully consider whether these risks
are acceptable given their specific use case. On the other hand, Smart Wallets
are rapidly improving and closing the gap with MPC offerings, all while
retaining the highest security measures for holding crypto assets.

This article is the first part of our introduction to Smart Wallets. Our
second piece will present our vision for Smart Wallets, and how this new
generation of crypto wallets will improve crypto custody across the entire
industry.

  

### About Squads

Squads is a crypto company operations platform that simplifies management of
developer, creator, and treasury assets for teams building on Solana and SVM.
Open source, formally verified, immutable, Squads enables teams to secure
their on-chain assets in a multisig and jointly manage them.

**Learn more**

What is Squads: <https://squads.so/blog/what-is-squads>  
Squads Protocol: <https://squads.so/blog/solana-svm-smart-contract-wallet-
infrastructure>  
Code: <https://github.com/Squads-Protocol/squads-mpl>  
Why use Multisigs: <https://squads.so/blog/what-are-multisig-wallets>

  

Continue reading

[![Smart Account
Basics](https://framerusercontent.com/images/HXRhLfdkpXz0YDKXQQ8LnjSJI.png)Smart
Account Basics: Why Smart Accounts Will Power the Onchain EconomyMay 22,
2024](./smart-account-basics-why-smart-accounts-will-power-the-onchain-
economy)[![account-abstraction-use-cases-smart-contract-wallet-solana-
ethereum-account-abstraction-eip-erc-4337-applications-use-cases-solana-
pda](https://framerusercontent.com/images/O8JVEriGowPcPDjADPC3ErE7W00.png)Exploring
Account Abstraction Use CasesApril 5, 2023](./account-abstraction-use-
cases)[![account-abstraction-ethereum-vs-solana-pda-program-derived-addresses-
ethereum-aa-eip-erc-4337-smart-contract-wallets-
solana](https://framerusercontent.com/images/P3OOJ94NoGqBPK1lFEHoi8GCMM.png)An
Introduction to Account AbstractionMarch 21, 2023](./what-is-account-
abstraction-ethereum-vs-solana)

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

