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

# How to Improve Treasury Operations with Spending Limits

Nov 29, 2023

![squads-solana-leading-multisig-spending-limits-treasury-management-solana-
multisig-wallet-squads-protocol-audited-formal-
verification](https://framerusercontent.com/images/2tyh01MPlECImwUoS4lpntdjCM.png)

Crypto organizations often need to move funds to recurring recipients. While
multisigs offer the best environment for such companies to secure and manage
their treasuries, this layer of security can be a burden for regular
transactions. With our new v4 program, we have overcome this issue and
released Spending Limits, ensuring Squads users can move their funds more
seamlessly without impacting the security of the multisig.

This article uncovers how Spending Limits work as well as how to set them up
for your Squads multisig.

## How Do Spending Limits Work

At its core, a spending limit acts as a pre-approved allowance granted to a
member of a Squads multisig. It gives the member the ability to move specific
assets from the treasury without the need for multiple approvals that are
usually required to meet the multisig threshold. Think of it as granting a
trusted team member a company credit card with a fixed spending capacity.  
  

![squads-how-spending-limits-work-squads-
protocol-v4-features](https://framerusercontent.com/images/4itkVSPDZ4qgOfRbrLCxACexE.png)

In brief, Squads Spending Limits offer flexibility for the operations of a
Squad:

  * No more waiting for multiple members to approve minor or routine transactions.

  * Members can act promptly, especially in time-sensitive situations.

Such a feature is pretty common in traditional finance apps where business
users need to add flexibility on top of their secure banking setup to not slow
down their processes. Now, crypto organizations can replicate the same for
their on-chain treasury operations.

Letâs take a scenario where a project uses Squads for storing USDC collected
on-chain from users. They off-ramp this to their Circle business account every
day for fast settlement. Waiting for multisig approvals for each transaction
was time-consuming and could often delay operations. Implementing spending
limits now allows the project to execute these off-ramp transactions quickly
without waiting for multiple members to approve, leading to better service for
their users and improved operational flow.

In another scenario, a business collecting revenue on-chain requires regular
payments to vendors and service providers. Multiple approvals over regular
payments were causing delays and operational inefficiencies. By setting
spending limits for specific team members, the company can ensure timely
settlements with their business partners.

Additionally, combined with other Squads features, spending limits can be a
powerful mechanism to streamline treasury operations. This includes our
integration with Coinflow, which offers immediate USDC off-ramping to US bank
accounts and plans to extend the same service for EUROe to EU bank accounts
soon. With Squads Spending Limits, teams and businesses can easily off-ramp to
their bank account without having to go through multiple approvals, which can
be a huge time saver. Since the bank account used for off-ramping is the
business account of the company, it is managed by multiple people and can
safely receive funds from the multisig.

Developers can also leverage the v4 program's spending limits for their
products. They can implement features such as withdrawal limits to protect
users, prevent unauthorized transfers of their funds and match the security
features offered by web2 companies like neobanks while offering the benefits
of blockchain technology such as self-custody.

However, granting a spending limit should be reserved for trusted members
only, where there's confidence they wonât engage in malicious actions.
Ideally, apply spending limits to recipient addresses under collective control
or oversight of multiple members. A prime example of this is using a Circle
Business Account SPL address for such transactions.

## Setting Up a Spending Limit

The way setting up a spending limit works effectively enables teams and
organizations to prevent undesirable scenarios in fund withdrawals.

![](https://framerusercontent.com/images/moiYLdtFHz6Ho2bjMMNtYDBVeqU.png)

For example, selecting USDC as the token for a spending limit ensures that no
other token type can be withdrawn by a member. If SOL tokens are available and
a member, potentially with malicious intent, wishes to use them, they must
first seek approval from the members of the multisig. This involves not only
requesting approval to convert SOL into USDC but also providing a clear
rationale for this exchange to the rest of the Squads multisig members.

When a member initiates a spending limit, they'll have to set several crucial
parameters:

  * **Member:** This refers to the specific member address from which funds can be withdrawn.

  * **Token and Maximum Amount:** The member must choose the particular token type and decide the maximum amount that can be withdrawn. It's essential to note that only one token type can be set for each spending limit.

  * **Time Frame:** This establishes the window during which the spending limit is valid. For example, if a monthly time frame is chosen, the allowed spending amount will reset at the beginning of the subsequent month. If "None" is selected, the spending limit remains active until the entire specified token amount is exhausted.

  * **Destination:** These are the destination addresses where the member can send funds without extra approvals. Multiple addresses can be added.

Once a spending limit is active, it's not set in stone. Spending limits can be
adjusted and monitored. By simply clicking on a member's card, one can view
their designated spending limit. For more detailed insights and to make edits,
members can navigate to the "Settings" tab. Here, they can modify the
parameters or even revoke spending limits if necessary.

Lastly, it is recommended to regularly review and adjust spending limits to
align with changing organizational needs. This ensures that the limits remain
relevant and effective. Also, prepare for situations where a memberâs key
gets compromised or the member is no longer part of the organization.

Spending Limits are one of the many features we've rolled out with our new v4
program. [Check out our latest article on Squads
Permissions](https://squads.so/blog/permissions-roles-in-multisig) to discover
how to enable granular control over the members of your multisig through
roles.

  

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

[![why-use-squads-why-multisig-solana-multisig-wallet-squads-leading-multi-
signature-solution-mpc-alternative-solana-secure-sol-for-company-squads-
protocol-
audited](https://framerusercontent.com/images/6S99P6ebVfLr6xzbo831NVDrCM.png)Why
Do Enterprises Use Squads For Their On-chain OperationsMarch 6, 2024](./why-
use-squads)[![how-to-create-mint-solana-spl-token-burn-mint-authority-solana-
multisig-squads-spl-token-
management](https://framerusercontent.com/images/YeQMBSozonTrL7s0M1gHdvMHtCw.png)Create
and Manage Solana (SPL) Tokens with SquadsDecember 13, 2023](./create-manage-
solana-spl-token)[![maple-us-treasury-bills-solana-product-cash-management-
pool-solana-multisig-squads-squadsx-extension-solana-wallet-solana-tbill-
yield-solana-multisig-
wallet](https://framerusercontent.com/images/phcIaPOZX2To9oDZzBAIxW2a40.png)Access
U.S. Treasury Bills Yield on Solana through Maple with SquadsXOctober 23,
2023](./maple-squadsx-on-chain-treasury-bills-solana)

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

