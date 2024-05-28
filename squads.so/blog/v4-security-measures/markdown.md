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

# Security Measures Conducted on Squads v4 Program

Dec 19, 2023

![squads-protocol-audits-solana-multisig-audited-formally-verified-audit-
report-squads-v4-squadsx-audit-ottersec-trail-of-bits-certora-
neodyme](https://framerusercontent.com/images/v4N4xBLtGGR2gZt6Wh9BoO0ss.png)

On October 2nd of this year we released v4, our new and powerful program that
expands the capabilities of multisig security for organizations operating on
Solana, as well as Solanaâs account abstraction use cases. Drawing from our
experience with v3, we aimed to ensure that v4 follows the highest security
standards.

Security is a continuous process that requires time and effort, especially for
infrastructure projects like Squads upon which other projects rely for their
operations. Regular security assessments and updates are a key part of our
approach to ensure our codebase remains resilient against threats.
Additionally, Squads Protocol's codebase is source-available (viewable
[here](https://github.com/Squads-Protocol/v4)), and the programs have been
written in Anchor, a framework for building secure Solana programs.

This article summarizes the security measures we have conducted on Squads
Protocol v4, the codebase on which the Squads platform is built. To ensure its
security, we have taken the following actions:

  1. Multiple security audits;

  2. Several formal verifications of the program;

  3. A perpetual bug bounty program.

## Four Security Analysis Audits

Recognizing the importance of rigorous testing, we subjected our latest v4
program to a series of four security audits. Industry leaders such as
OtterSec, Neodyme, Certora and Trail of Bits were engaged to review every
aspect of the program. These audits were crucial to ensure that there were no
potential vulnerabilities and that v4 adheres to the highest standards for the
security of a Solana program. The key findings from these audits, while few in
number, have played a crucial role in shaping the robustness and security of
v4. Additionally, the straightforward nature of v4's code made its auditing
process less complex and less prone to error compared to more complex programs
that can be found in DeFi.

In an industry like crypto where threats happen every day, multiple and
thorough audits are essential for identifying and mitigating risks before they
become serious threats. These proactive measures not only protect the
integrity of platforms like Squads but also build trust with users or projects
building on top of it.

OtterSec and Neodyme are both leading audit firms on Solana, and have worked
with renowned companies like Solana Labs, Wormhole, Backpack, marginfi, among
others. While both are long-time partners of Squads, with v4 we decided to
look for additional eyes and work with top-tier firms, which are Trail of Bits
and Certora. Trail of Bits, recognized as a Tier-1 security auditor, has
worked with major crypto companies like Uniswap and Chainlink, as well as
clients outside of the crypto industry, including Google, Stripe and
Microsoft. On the other hand, Certora is the leading security audit firm for
formal verification of crypto projects.

See the reports to the security audits conducted on v4 by these audit firms:

  * [OtterSec](https://github.com/Squads-Protocol/v4/blob/main/audits/ottersec_squads_v4_audit.pdf);

  * [Neodyme](https://github.com/Squads-Protocol/v4/blob/main/audits/neodyme_squads_v4_report.pdf);

  * [Certora](https://github.com/Squads-Protocol/v4/blob/main/audits/certora_squads_v4_security_report_and_formal_verification.pdf);

  * [Trail of Bits](https://github.com/Squads-Protocol/v4/blob/main/audits/trail_of_bits_squads_v4_security_audit.pdf).

## Formal Verifications: Beyond Traditional Audits

To further strengthen the security of Squads Protocol v4, we also engaged
Certora and OtterSec for two formal verifications. Formal verification is a
process that goes beyond traditional auditing methods, employing mathematical
models to validate the correctness of a program. The goal of formal
verification is to ensure that a program is free of bugs and meets its
requirements.

As opposed to a security audit which specifically focuses on identifying
security vulnerabilities, formal verification is a mathematical approach to
evaluating that a program is working as intended. When a program is connected
to the internet, there is the new risk that bugs may introduce security holes
into a system. Even simple buffer overflows can be exploited by skilled
attackers to compromise the integrity of a program. Formal verification is one
of the most effective methods to ensure a program is free from such
vulnerabilities and we are proud to be among the few companies on Solana
formally verifying their codebase.

OtterSec developed and released the first framework for formally verifying
Solana programs in January of this year (2023) using v3 as a case study; it
was an obvious choice to work with them again for our new program. As of
Certora, it is a leading audit firm in smart contract security renowned for
its formal verification expertise. While initially focusing on EVM-based
projects, Certora has now formally verified its first program on Solana with
v4. This rigorous examination by OtterSec and Certora was pivotal in
certifying the robustness of v4 against a wide array of potential security
threats.

See the formal verification reports of v4 conducted by these firms:

  * [Certora](https://github.com/Squads-Protocol/v4/blob/main/audits/certora_squads_v4_security_report_and_formal_verification.pdf) (section âFormal Verificationâ, page 14);

  * [OtterSec](https://github.com/Squads-Protocol/v4/blob/main/audits/ottersec_squads_v4_audit_2024.pdf) (section âFormal Verificationâ).

## Perpetual Bug Bounty Program

Additionally, we have extended our perpetual bug bounty program to v4,
encouraging and rewarding independent security researchers and users for
identifying and reporting potential vulnerabilities, thus contributing to the
continuous fortification of v4.

Recognizing the value of external insights, we offer substantial bounties for
identifying critical security issues. These bounties are available for various
types of vulnerabilities, such as the ability to steal or freeze funds, replay
attacks, or unauthorized modifications of multisig or module settings.

The bug bounty program is open to participants following our outlined
processes, with fair compensations in place. Bounties are paid in locked SOL
tokens (locked for 12 months), with amounts varying based on the severity of
the discovered vulnerability:

  * Ability to steal funds - $300,000 USD in locked SOL tokens

  * Loss of availability/Ability to freeze funds - $200,000 USD in locked SOL tokens

  * Replay attacks - $25,000 USD in locked SOL tokens

  * Setting modifications - $10,000 USD in locked SOL tokens

More information on the Squads Protocol v4 bug bounty program can be found
here: <https://docs.squads.so/main/v/security/bug-bounty>

Lastly, we strongly believe in making core primitives on open, permissionless
networks immutable as soon as practical.

Immutability should be the end goal for most protocols, however the realities
of shipping code and building in such a fast-paced environment as crypto
require teams to stay agile and be able to upgrade their codebase on a regular
basis. For newer protocols, it is important for the codebase to stand the test
of time in terms of security and resiliency before thinking of taking this
step. Immutability is a significant step and should not be rushed, which is
why we are taking a cautious approach to ensure no premature decisions are
made. We plan to make Squads Protocol v4 immutable in Q1 of next year.

Our measures taken already showcase the trust of the ecosystem, as v4 recently
exceeds $500mln in assets deposited. We believe that what we have built with
Squads Protocol v4 and how we made sure it is safe will make it the definitive
infrastructure for Solana developers requiring Solanaâs account abstraction
capabilities or multisig consensus for their products.

If you are considering building on v4, please reach out, we are happy to
assist.

  

**About Squads Labs**

Squads Labs is a core contributor to Squads Protocol, the leading multisig
infrastructure on Solana. In addition to helping maintain the protocol, Squads
Labs makes the Squads platform, an institutional-grade multisig platform for
Solana-based teams. The Squads platform helps web3-native teams manage and
secure digital assets on-chain. To learn more about Squads Labs, please visit
<https://www.sqds.io/>.

  

Continue reading

[![Turn on Rent Reclaim for cost-effective
transactions](https://framerusercontent.com/images/eOILakO7M19S8jwBSRmPIXJhg.png)Rent
Reclaim: Enjoy Cost-Effective TransactionsMay 17, 2024](./update-rent-
reclaim)[![](https://framerusercontent.com/images/WOKbvF0y1nHBuYDN78pvmWH8zU.png)
Squads Validator: The Most Secure Way to Stake SOLMay 17, 2024](./update-
introducing-squads-validator)[![Use Squads Token Manager for Token Extensions
and Token Metadata
Updates](https://framerusercontent.com/images/7HnkhwbJM5yCrT3XKC9bXCdaoM.png)Squads
Token Manager: Now Supporting Token Extensions and Metadata UpdatesMay 17,
2024](./update-token-manager-token-extensions-and-metadata-updates)

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

