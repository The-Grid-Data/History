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

# Security Audit Report of v4 by Trail of Bits

Nov 17, 2023

![squads-protocol-v4-audit-trail-of-bits-solana-multisig-audited-secure-
formally-verified-open-source-immutable-squads-leading-solana-multi-signature-
wallet-svm](https://framerusercontent.com/images/fRNSNWYxKXpCpSD97BHGK7bY.png)

We are pleased to announce the completion of a security audit report on Squads
Protocol v4 conducted by Trail of Bits. This comprehensive audit included a
detailed examination of our new program, with the auditors having full
knowledge of the target system, including access to our source code and
documentation.

[Trail of Bits](https://www.trailofbits.com/), recognized as a Tier-1 security
auditor, has a center of excellence with regard to blockchain security. Their
notable projects include audits of Chainlink, Compound, Ethereum 2.0,
MakerDAO, Matic and Uniswap. They have also worked with renowned clients
outside of the crypto industry like Google, Stripe and Microsoft.

A team of two consultants carried out the review from September 11 to
September 22, 2023, dedicating a total of four engineer-weeks of effort.
Employing both static and dynamic testing of the codebase, they used automated
and manual processes.

The audit aimed to provide a security assessment of the v4 program, focusing
on various critical security questions:

  * Proper approval requirements for instruction execution;

  * Restrictions on fund withdrawals from vaults;

  * Possibility of "bricking" a multisig;

  * Interactions between multisig instances;

  * Adherence to spending limits and permissions;

  * Vulnerabilities to front-running.

The analysis methods included a documentation review, static analysis using
tools like cargo-audit and Clippy, test coverage review, and manual review of
program code. Particular attention was paid to areas like proposal handling,
member management, permissions checking, spending limit use, config
authorities and transaction execution.

After the initial audit findings, Squads Labs reviewed and implemented fixes
and mitigations for the issues described in the report. On September 27, 2023,
Trail of Bits examined these fixes to ensure their effectiveness in resolving
the associated issues. A full listing of unresolved or partially resolved
findings is available on page 43 of the Trail of Bits audit report.

Quality smart contract assurance is key to identifying potential issues and
ensuring protocol security. While there are no guarantees of security after an
audit, a thorough smart contract auditor can still perform comprehensive
reviews to uncover potential issues, potentially preventing catastrophic
vulnerabilities after launch. We at Squads Labs prioritize security as a
critical aspect of our multisig infrastructure, and that is why we run regular
security audits for maintaining user safety.

View the full Trail of Bits report [here](https://github.com/Squads-
Protocol/v4/blob/main/trail_of_bits_security_audit%20_squads_v4.pdf).

  

**About Trail of Bits**

Since 2012, Trail of Bits has helped secure the worldâs most targeted
organizations and products. They combine high-end security research with a
real-world attacker mentality to reduce risk and fortify code. To learn more
about Trail of Bits, please visit <https://www.trailofbits.com/>.

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

