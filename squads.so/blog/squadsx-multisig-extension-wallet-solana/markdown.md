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

# SquadsX - Access the Solana Ecosystem with Multisig Security

Oct 9, 2023

![squadsx-solana-multisig-extension-wallet-squads-solana-multisig-multi-
signature-squads-pro-connect-multisig-to-dapps-squads-protocol-v4-multisig-
transactions-solana-
walletconnect](https://framerusercontent.com/images/BSiI7vGsYKdP4zpXCHRRrAICuE.png)

[Multisigs](https://squads.so/blog/what-are-multisig-wallets) are well-known
for the security they provide to users who want to manage on-chain assets.
Although robust and secure, for a long time it was challenging for teams and
organizations to use their funds held in a multisig as seamlessly as they
would with traditional self custody solutions such as hot wallets, without
sacrificing the benefits of multi-signature security.

Over the last year, we have spent time building a new way to allow Squads
multisigs to interact with Solana dApps with the familar UX of regular
wallets. This not only "unlocks" the value managed in Squads multisigs for the
ecosystem for the first time, it also enables enterprises and teams to operate
on-chain with the operational security of their multisig setup. Let's dive
into SquadsX and why this represents a significant advancement for Solana.

## A Secure Way to Interact with Solana dApps

![squads-solana-multisig-security-squadsx-extension-wallet-multisig-
transactions-solana-leading-multisig-infra-squads-
protocol-v4](https://framerusercontent.com/images/lFqeAJvduhJWduDPO7FnkxTOkI.png)

Traditional wallet solutions don't allow for shared management of assets. If
teams and organizations want to start operating on-chain, they have to either
rely on one single key or person for the security of the assets used. This can
lead to unwanted situations where not only could the person holding the funds
steal them, they could also simply have their key compromised, impacting the
projectâs assets.

On-chain organizations often have to interact with dApps for their business
operations, whether it's providing liquidity for their native token or hedging
their exposure to SOL. This is more emphasized for funds/institutions looking
to perform complex strategies on-chain, such as opening a delta-neutral
position on a DEX, arbitraging rates between lending protocols, but require a
reliable setup to do so.

That is why we developed a companion tool to our multisig app: SquadsX.
Multisigs offer all the operational efficiency and security that teams and
organizations need. They can add key stakeholders, store their liquid assets
like SOL, staked SOL, ecosystem tokens and ensure every transaction needs to
be approved by several members until the multisig threshold set is reached.
But while the Squads app supports essential actions like swapping and staking,
it quickly became challenging to enable users to perform granular actions on
dApps from their multisig. Here comes SquadsX.  
  

![squadsx-use-cases-multisig-wallet-extension-solana-squads-
protocol-v4-audited-formally-
verified](https://framerusercontent.com/images/Uu1mTiCkQK4eRbb9MZS71uZeKgA.png)

SquadsX has been built with enterprise-level security in mind, powered by
multisig technology. Rather than being a wallet, SquadsX acts as an extension
to the Squads app, enabling users to connect their multisig to any dapp as
they usually would with a regular wallet. Teams can now explore the vast
ecosystem of dApps on Solana and connect the funds held in their multisig to
it. This enables teams and institutions to tap into the Solana ecosystem with
their security requirements and undertake various on-chain activities like
liquidity provisioning, lending/borrowing, on-chain futures and more.

However, while the "Connect to dApps" experience mirrors that of conventional
wallets, executing transactions with SquadsX diverges both in the process and
the enhanced security it offers.

## How Does SquadsX Work

![squadsx-solana-wallet-most-secure-multisig-transactions-squads-
protocol-v4-leading-solana-
multisig](https://framerusercontent.com/images/Zq2DqUouSu8Kp9L2gZQSej8E.png)

The main purpose of SquadsX is to simplify the creation of multisig
transactions. Unlike regular wallets where all transactions are done through
the wallet itself, SquadsX only connects to dApps to send transactions to the
multisig, moving the funds from it to those dApps. See it as a way to link a
multisig to a dApp and trigger transactions for it.

For instance, a team could use SquadsX to provide liquidity for their token on
Raydium. One of the members can use SquadsX to connect the teamâs multisig
to Raydium and trigger a multisig transaction to deposit funds into a Raydium
liquidity pool from the multisig. This transaction will appear on the
Transactions page of the Squad and will be processed once all the members have
approved and executed it.

When setting up SquadsX, a new key is created and added as a member to the
Squads multisig. This member/key is used to create those multisig transactions
through SquadsX for the multisig, and hence it only needs the [âProposerâ
role](https://docs.squads.so/main/squads-pro/permissions). By leveraging
multisig, SquadsX significantly reduces the success of harmful transactions,
making it unlikely for an on-chain organization to lose funds or experience
theft from a member. Even if the key used for SquadsX is compromised, it
wouldnât be able to move any funds out of the multisig. This is very
different from regular wallets where interacting with a malicious program
could immediately compromise the assets held within.  
  

![solana-multisig-wallet-extension-squadsx-squads-solana-leading-multisig-
connect-to-dapps-multisig-transaction-squads-
protocol-v4](https://framerusercontent.com/images/olYlc0KyX63KhQItAjq8jtPKoA.png)

SquadsX is built on [Squads Protocol
v4](https://docs.squads.so/main/v/development/introduction/what-is-squads-
protocol), a program that has been audited three times by: Trail of Bits,
OtterSec, and Neodyme. It is currently undergoing two formal verifications by
Certora and OtterSec. Squads Protocol is as of today the most trusted multisig
infrastructure on Solana and it is used by the largest Solana-based
organizations, securing over $600 million in value.

While WalletConnect is a well-known solution in the EVM ecosystem for dApp
connections, it wasn't as established or tailored for Solana when we started
developing SquadsX. Building our own extension gave us the flexibility we
needed to perfect the experience of connecting multisigs to Solana dApps. Most
crucially, WalletConnect lacked a specific feature required for SquadsX. The
main goal of SquadsX is to take a transaction from a dApp, convert it into a
multisig transaction proposal, to then sign it and send it back. Though we
considered WalletConnect, we found that its current design only allowed for
returning a signature, not a fully signed transaction.

Building SquadsX is a huge achievement for the ecosystem and the next
generation of Solana wallets, albeit accompanied by its unique set of
challenges.

## Paving the Path for a New Era of Wallets and Their Challenges

As SquadsX represents a novel approach to interacting with Solana programs,
launching it presented challenges such as compatibility issues with dApps.
Right off the bat, SquadsX might already be perfectly integrated with your
favorite dApps, assuming it supports the latest Solana Wallet Standard and
embodies certain characteristics that we will cover below.

SquadsX can be considered as part of the new generation of wallets on Solana.
Built on multisig technology, transactions done with SquadsX deviate from
standard wallet transactions since they require multiple approvals before
execution. This creation and execution of a transaction become an asynchronous
multi-step process. This can cause some UI issues for dApps that don't
recognize âdelayedâ transactions, either displaying a âconfirmed
transactionâ or âerrorâ pop-up when trying to execute a multisig
transaction. In both cases, this most often doesn't impact the success of the
transaction but provides a less than optimal experience for users.

Wrapping a standard transaction into a multisig transaction proposal is also a
complex process, which can fail if the size of a transaction becomes too
large. The best solution to overcome this problem is by implementing:

  * [Address Lookup Tables](https://docs.solana.com/developing/lookup-tables) (ALTs) - it reduces the size of a transaction by storing public keys in a lookup table and then referencing them by their index;

  * and [Versioned Transactions](https://docs.solana.com/developing/versioned-transactions) \- it ensures that even if the transaction format or the smart contract's logic changes in the future, older versions can still be processed correctly.

Thankfully, most newer dApps already implement both concepts, allowing SquadsX
to already work smoothly with them.

Additionally, dApp developers should avoid using Ephemeral Signers (ES) in
transactions as they are keys that sign and are immediately discarded. This
mechanism is problematic with wallets like SquadsX that don't instantly
execute transactions, as the ephemeral keypair won't be available later to
sign the "execute" transaction. Instead:

  1. Prefer `SystemProgram.createAccountWithSeed` over `SystemProgram.createAccount`: The former doesn't require the new account's signature since the new account is controlled by a known base public key, often the primary signer.

  2. Use SquadsX's `getEphemeralSigners` API: If you need a secondary signer, [SquadsX provides an API ](https://docs.squads.so/main/v/squadsx-beta-development/guides/overcoming-integration-obstacles/ephemeral-signers)to request ephemeral signers directly from the wallet.

Lastly, Squads multisigs are PDAs, and while powerful, they inherently cannot
sign messages. Thus, we strongly advise developers against making Sign-In
mandatory for using their dApp.

By implementing these changes, developers will more likely make their dApps
compatible from day one with this new generation of wallets, allowing users
from those solutions to engage with their projects.

## Get Started with SquadsX

![squadsx-squads-extension-multisig-wallet-
partners](https://framerusercontent.com/images/AVH3vzknTbnsD8JDIr4p7JeQOw.png)

SquadsX is now available to all Pro subscribers through the [Squads
app](https://app.squads.so/squads) and is already compatible with many Solana
dApps. In the coming weeks, we will be working with the last major Solana
dApps that are not yet fully compatible with SquadsX to allow them to
seamlessly work with it. For dApp developers looking to integrate SquadsX,
check out the [SquadsX development
documentation](https://docs.squads.so/main/v/squadsx-beta-development/).

Weâre excited to finally roll out the first multisig extension wallet for
Solana and look forward to seeing how it will help the ecosystem in onboarding
more advanced and institutional players in need for a reliable and secure
setup to operate on Solana.

  

**About Squads Labs**

Squads Labs is a core contributor to Squads Protocol, the leading multisig
infrastructure on Solana. In addition to helping maintain the protocol, Squads
Labs makes the Squads platform, an institutional-grade multisig platform for
Solana-based teams. The Squads platform helps web3-native teams manage and
secure digital assets on-chain. To learn more about Squads Labs, visit
<https://www.sqds.io/>.

**About Squads Protocol**

Squads is a multisig protocol that helps web3-native teams manage and secure
digital assets on-chain. Squads Protocol v3 is the first formally verified
program on Solana. Squads Protocol v4 introduces time locks, spending limits,
roles, sub-accounts, fee relayers, multiple-party payments, support for
SquadsX and more. Squads v4 has already been audited by Neodyme, OtterSec. To
learn more about Squads Protocol, visit <https://squads.so/protocol>

  

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

