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

# The Smart Contract Wallet Infrastructure for Solana and SVM

Mar 10, 2023

![Squads Protocol Solana Smart Contract Wallet Infrastructure SVM Account
Abstraction Solana
PDA](https://framerusercontent.com/images/XHhURNnA2l0xC2b4i3Kp5LAFPE.png)

Squads Protocol is the smart contract wallet infrastructure powering
[Squads](https://squads.so/blog/what-is-squads) \- the platform for teams on
Solana and SVM seeking to securely manage their on-chain assets with multi-
signature logic.

This article covers what Squads Protocol is, highlighting its potential
applications for developers and various security measures we have implemented
to offer a safe and reliable smart contract wallet layer for the Solana and
SVM ecosystems.

## What is Squads Protocol

Squads Protocol is a collection of programs (smart contracts) that together
form the smart wallet infrastructure layer for Solana and SVM. It enables
developers to deploy and program smart contract wallets - a next generation of
self-custody solutions.

Smart (contract) wallets can have more complex rules and conditions for
sending transactions than traditional hot and cold wallets like Ledger or
Phantom. In the case of smart wallets user accounts are no longer single
private keys, but instead programmable accounts managed by several keys.
Traditional wallets make the account (which holds the assets) and the signer
(which invokes transactions in respect of the assets) identical, whereas
Squads Protocolâs programs âabstractâ the signer from the account. The
concept of such decoupling, allows for greater security and programmability,
and is commonly referred to as Account Abstraction (AA).

**Multisigs are perhaps the most well-known use case of AA,** which are smart
contract wallets managed by multiple owners requiring multiple signatures to
confirm transactions. However, beyond multi-signature wallets AA allows for a
plethora of features including social recovery, 2FA, daily withdrawal limits
and alternative signing schemes. Developers have virtually limitless
possibilities when it comes to what they can build around self-custody tools
on Account Abstraction rails.

As of now, the Squads platform has already implemented several features that
are enabled by Squads Protocol including multisig and batched transactions.

## Built with Composability and Security in Mind

Squads Protocol is designed to simplify development for projects seeking to
build on top of it. It makes it easy to leverage AA capabilities of Squads
Protocol while using lightning fast and low fees of the Solana blockchain.
Teams looking to build on top of Squads Protocol have access to the:

  * **SDK,** made to simplify interaction with Squads Protocol: <https://www.npmjs.com/package/@sqds/sdk>

  * **Anchor** **IDLs** : <https://github.com/Squads-Protocol/squads-mpl/blob/main/idl/squads_mpl.ts>

  * **comprehensive documentation,** drafted to guide them through the development process: [https://docs.squads.so/squads-v3-docs/](https://docs.squads.so/squads-v3-docs/*)

  * **open-source codebase,** available for review: <https://github.com/Squads-Protocol/squads-mpl>

Composability of Squads Protocol is supported by a multitude of security
measures undertaken by Squads Labs, to ensure that the protocol is a secure
and reliable foundation for developers.

![squads-protocol-open-source-solana-immutable-protocol-formally-verified-
audited-by-neodyme-ottersec-audit-firm-solana-smart-contract-wallet-account-
abtstraction-infrastructure-solana-squads-svm-pda-
solana](https://framerusercontent.com/images/HAWk5AgecBs8CJBNmjbCgMe4UU.png)

Measures implemented to ensure security of Squads V3 include:

  * **Audits** : Squads V3 has undergone several audits from reputable firms such as Neodyme and OtterSec;

  * **Anchor** : the entire code has been written using [Anchor](https://www.anchor-lang.com/), a framework for building secure Solana programs;

  * **Formally Verified** : Squads Protocol is the first Solana protocol to be formally verified. [Formal verification](https://osec.io/blog/2023-01-26-formally-verifying-solana-programs) (FV) is the process of using a formal specification to verify the correctness of a system. The goal of FV is to ensure that a program is free of bugs and working as intended;

  * **Immutability** : since February 2023, the upgrade authority for v3 (SMPLecH534NA9acpos4G6x7uf3LWbCAwZQE9e8ZekMu) has been burned, making the program immutable. In essence it means that nobody controls the upgrade authority, even Squads Labs, the program lives autonomously on the Solana blockchain.

Moreover, countless key players in the ecosystem support and rely on Squads
Protocol. Protocols like [Mesha](https://www.mesha.club/),
[Streamflow](https://streamflow.finance/) and others have built their products
leveraging the protocol and relying on its capabilities, adding multisig
support to their platforms.

Squads Protocol enables developers to create innovative self-custody solutions
on Solana, leveraging the speed, low transaction fees and account abstraction
capabilities of the Solana blockchain. Its numerous use cases, coupled with
robust security measures, as well as adoption by multiple protocols, establish
Squads Protocol as the leading smart contract wallet infrastructure for the
Solana and SVM ecosystems.

For any teams looking for additional support on their journey of building on
top of Squads Protocol or to have their questions answered, we are available
to assist [here](https://discord.com/invite/YPXz64TrKs).

  

### Start Building on top of Squads Protocol

 _Code:  _[_https://github.com/Squads-Protocol/squads-
mpl_](https://github.com/Squads-Protocol/squads-mpl) _  
SDK:
_[_https://www.npmjs.com/package/@sqds/sdk_](https://www.npmjs.com/package/@sqds/sdk)
_  
IDLs:  _[_https://github.com/Squads-Protocol/squads-
mpl/blob/main/idl/squads_mpl.ts_](https://github.com/Squads-Protocol/squads-
mpl/blob/main/idl/squads_mpl.ts) _  
Documentation:
_[_https://docs.squads.so/squads-v3-docs/_](https://docs.squads.so/squads-v3-docs/)

  

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

