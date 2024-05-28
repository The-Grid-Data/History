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

# Releasing the Squads Backup Kit

Feb 8, 2024

![squads-multisig-frontend-alternative-ui-open-source-cli-tool-command-line-
interace-squads-protocol-solana-multisig-sdk-backup-
kit](https://framerusercontent.com/images/uAfAsDKP5JsZAuoDiRStU955nQ.png)

Today we are releasing the [Squads Backup Kit](https://backup.squads.so/):
open-source UI, CLI, SDK - a suite of tools providing multiple options for
Squads users to access their assets in any situation.

While we contribute to and maintain the main Squads app, in the unlikely event
it becomes inaccessible for a long period it can become a single point of
failure for users. Users relying on a multisig program like Squads to secure
their assets should always have multiple ways to interact the program rather
that just one. We believe the permissionless and self-custody aspects of
securing assets are paramount for on-chain organizations and superior to
centralized solutions, which can at any point of time block access to their
usersâ assets.

Our philosophy has always been about offering a transparent, open multisig
product to teams and organizations on Solana. This Backup Kit takes it even
further, providing full reassurance to users securing their assets with Squads
that they are always in full control.

Squads users now have four different ways to access their assets on Squads:

  * Squads official app (maintained by Squads Labs);

  * Squads minimal interface;

  * CLI;

  * v4 SDK.

## Squads Minimal Interface

The Squads minimal interface is a simple, open-source frontend that anyone can
use in the unlikely event that the main [app.squads.so](http://app.squads.so/)
frontend is not available. It features quick actions like withdrawing funds,
managing authorities and approving transactions. It should not be used as your
main app as it does not feature all the functionalities available on the
official Squads app - this is an emergency simple interface only.

![squads-minimal-interface-open-source-ui-frontend-fork-squads-
multisig](https://framerusercontent.com/images/GSh9w0sTr4Y0s3GJ7bOCzGdA.png)

We have built it so it can easily be used by any Squads users as backup in
case the Squads official app is not accessible. This minimal interface
provides assurance that your on-chain operations can continue uninterrupted,
regardless of the status of the Squads app.

To use this minimal UI, simply go to <https://github.com/Squads-
Protocol/squads-v4-public-ui> and clone the repository to a folder on your
device. You can then host it locally and use your web browser to access your
Squads account(s) and connect your wallet (like you would on
[app.squads.so](http://app.squads.so/)). You can find a simple guide to using
this app in the repositories README.md file.

Once connected, you can select the actions you want to perform. Note that this
UI mostly focuses on emergency actions (e.g. withdrawing funds or programs).
We do not encourage using it as your main app as it is not optimised and far
from the experience you get on [app.squads.so](http://app.squads.so/).

## CLI Tool

The second tool at Squads users' disposal to access their assets is the Squads
Command-Line Interface (CLI). This allows anyone to quickly interact with the
Squads program from their computer terminal and access their assets stored on
Squads.

The Squads CLI offers a range of commands for interacting with the Squads
program on Solana, and supports the same wallets as the Solana CLI, including
file system and Ledger hardware wallets. It facilitates the core operations
offered by the Squads app like creating multisigs, voting on proposals and
performing transactions. It also allows for detailed actions such as adding or
removing members, changing signature thresholds, setting time locks, and
managing spending limits.

To use the Squads CLI, installation of Rust is required. You can find the
installation steps [here](https://www.rust-lang.org/tools/install). Then, open
the terminal on your computer and use the command `cargo install squads-
multisig-cli` to install it. Start it by using the command `squads-cli`.
Running the command will start the tool and prompt a few setup questions for
the wallet and the network cluster.

For a walkthrough on how to use the Squads CLI commands, follow this guide:
<https://docs.squads.so/main/v/development/squads-cli/commands>

## v4 SDK

Probably the most complex, as mainly built for integration and thus
developers, another way to access your assets is through the Squads SDK. Note
that interacting with an SDK requires developer knowledge and is best suited
for technical users. If you have limited technical skills or need quick access
to your assets, we recommend using the Squads minimal UI or the CLI tool.

The Squads SDK provides a powerful toolkit to integrate Squads V4
functionalities directly into their applications, enabling management of your
Squads multisigs. Through the SDK, developers can programmatically create
Squads multisigs, propose and vote on transactions and interact with the
Squads program's advanced features like spending limits and time locks. This
allows for the creation of custom front-end as well as automation of your
multisig operations. The SDK supports a wide range of operations, from basic
multisig setup to complex configurations for threshold adjustments and member
permissions.

For more detailed information and to get started with the SDK, check out
<https://docs.squads.so/main/v/development/development/overview>.

As a reminder, the codebase powering the Squads app is available on GitHub. It
has recently undergone three additional audits, bringing its total number of
audits to 7. We frequently collaborate with OtterSec, Neodyme and Certora to
ensure the security of the v4 program. They are leading audit firms, and their
expertise helps reinforce the security of Squads by catching bugs and errors
with might have missed.

![squads-protocol-audits-solana-
multisig](https://framerusercontent.com/images/OwizjmkhyeVJTdzczymMumGOE.png)

Lastly, we have also recently deployed our v4 program with a verifiable build
to allow our users to verify on the [Solana.FM](http://solana.fm/) explorer
that they are interacting with the right audited and secure Squads program
published on our GitHub.

The security of our users is our top priority. While we have multiple measures
to ensure the operationality of the official Squads app, the Squads Backup Kit
guarantees that our users can always access their assets. Our next priority is
to make the v4 program immutable, which we aim to achieve by the end of Q1.

Find the Squads Backup Kit [here](https://backup.squads.so/).

  

**About Squads Labs**

Squads Labs is a core contributor to Squads Protocol, the leading multisig
infrastructure on Solana. In addition to helping maintain the protocol, Squads
Labs makes the Squads platform, an institutional-grade multisig platform for
Solana-based teams. The Squads platform helps web3-native teams manage and
secure digital assets on-chain. To learn more about Squads Labs, please visit
<https://www.sqds.io/>.

**About Squads Protocol**

Squads is a multisig protocol that helps web3-native teams manage and secure
digital assets on-chain. Squads Protocol v3 is the first formally verified
program on Solana. Squads Protocol v4 introduces time locks, spending limits,
roles, sub-accounts, fee relayers, multiple-party payments, support for
SquadsX and more. Squads v4 has already been audited by Neodyme, OtterSec, and
Trail of Bits. It is currently undergoing two formal verifications, one by
OtterSec and the other by Certora. To learn more about Squads Protocol, please
visit <https://squads.so/protocol>

  

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

