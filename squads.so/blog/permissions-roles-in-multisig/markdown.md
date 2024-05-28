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

# How Permissions Improve the Management of Assets in Multisig

Oct 20, 2023

![squads-permissions-crypto-multisig-roles-solana-multi-signature-squads-pro-
squads-app-multisig-customizations-best-
multisig](https://framerusercontent.com/images/2BnnlodfT2WBqV61GeJDVwxUdo.png)

Our new v4 program, which powers the Squads app, has introduced novel features
making multisigs more powerful than ever on Solana. One of these new features
is Permissions, a new approach for enabling granular control over the members
of a multisig through roles.

This article is the first in our series highlighting the new features powered
by Squads Protocol v4 and what use cases they enable for teams and
organizations operating on Solana.

## Enhancing Multisig Setups with Permissions

Multisigs are a powerful solution for managing on-chain assets collectively
and securely. To execute a transaction in a multisig, it requires several
signatures until a threshold is reached, eliminating single points of failure
and reducing the risk of asset compromise.

In traditional multisig setups like Squads v3, all the members added have the
same level of power, offering no room for customization at the organization
level. This can lead to undesired situations where a member needed in the
multisig for certain functions holds more power than necessary. Thus, this
restricts the customization an organization might require to manage its
assets, such as treasuries and programs, hindering it from fully operating on-
chain.

This limitation is now gone with Squads Permissions, which enable for the
first time teams and organizations to clearly define the role of each
key/member in a Solana multisig and how transactions are approved.  
  

![squads-permissions-v4-squads-protocol-multisig-transactions-crypto-multisig-
roles-solana-multi-signature-squads-pro-squads-app-multisig-
customizations](https://framerusercontent.com/images/ITTC9KEeH2hUMJcjbmRXoJ4ONKI.png)

Using Permissions, teams can now assign roles to each key/member of their
multisig, enhancing the ways in which on-chain assets can be managed
collectively. Squads Permissions includes three roles:

  * **Proposer** \- can only create transactions for the multisig;

  * **Voter** \- can only vote on proposed transactions for the multisig;

  * **Executor** \- can only execute transactions that have reached the threshold.

One of the use cases of Permissions is to reflect organizational hierarchy. It
allows for mirroring the specific rights and authorizations team members
require for asset management, all while on-chain and governed by multisig
consensus. Through roles, it ensures members can't execute or vote on
transactions unless explicitly granted that authority.

Take for example a crypto project that requires to make financial decisions on
the funds they recently raised from their Series A. With Squads Permissions,
the co-founders can hold all three pivotal roles: Proposer, Voter, and
Executor. The CFO, responsible for initiating expenditure requests, can be
assigned the Proposer role. To provide their approval on these requests, they
can also have the Voter role. On the other hand, team members like Marketing
managers who need to be kept informed but may not play a pivotal role in fund
allocations can be given the Proposer role.  
  

![squads-permissions-organization-v4-crypto-multisig-roles-solana-multi-
signature-squads-pro-squads-app-multisig-
customizations](https://framerusercontent.com/images/pLfJeVU78YanCYhim1T6FvgFwQU.png)

Crypto venture and liquid funds also require a transparent and efficient way
to allocate and release funds. Using Permissions, individual fund managers can
have the Proposer role, enabling them to create transactions to send funds to
portfolio companies. The fund's investment committee, responsible for
evaluating and endorsing investment decisions, can be assigned the Voter role.
Meanwhile the fund's managing partner who oversees major decisions and has the
final authority can hold the Executor role, ensuring that capital is allocated
in alignment with the fund's strategy.

Community-driven groups like DAOs also need to manage their assets
collectively. Here too, Permissions acts as a powerful solution. Active
community members can use the Proposer role to suggest actions while elected
members, who ensure proposals align with the goals of the group, can have
Voter and Executor rights for final actions.

Permissions pave the way for entirely new setups for on-chain organizations.
This not only benefits the Squads app but also dApps and protocols leveraging
the v4 program for their offerings.  
  

![squads-permissions-multisig-infrastruture-smart-contract-wallet-solana-
squads-protocol-v4-audited-crypto-multisig-roles-solana-multi-signature-
squads-pro-squads-app-multisig-
customizations](https://framerusercontent.com/images/Fp2jVr2kao8YnwbDXx8vGVdUZ0.png)

This is beneficial for protocols that for instance need a key to create
transactions for team approval but wish to limit the power of that key in the
event it gets compromised. Permissions can be viewed as a method to customize
each multisig key's capabilities based on their designated roles or use cases.
If you have an account dedicated solely to voting, you can use permissions to
ensure it only participates in that specific action.

For example, [SquadsX](https://squads.so/blog/squadsx-multisig-extension-
wallet-solana) was designed to facilitate dApp transactions for a multisig.
Therefore, it shouldn't hold more authority than required: wrapping dApp
transactions into multisig transactions. That's the reason we prompt users in
SquadsX to assign the proposer role to their SquadsX key. If it interacts with
a malicious program and becomes compromised, it doesn't have the power to
execute or block transactions in the multisig (which a voter could, for
example). This significantly reduces the risk of potential attacks for the
multisig.

## Setting Up Permissions for a Multisig and Key Considerations

![squads-permissions-v4-roles-functions-explained-squads-protocol-crypto-
multisig-roles-solana-multi-signature-squads-pro-squads-app-multisig-
customizations](https://framerusercontent.com/images/UWJpOOZ0mVv9gBsmP75DwKXiGhQ.png)

As we've seen, setting up permissions for a multisig lies in defining the role
members will play. Individuals holding significant authority within the
organization would likely necessitate having all roles, namely Proposer, Voter
and Executor, within the multisig setup. This approach allows them to be
involved in every aspect of the multisig - from creating transaction proposals
to having decisive power over them, especially in scenarios of disagreement.

Conversely, there are members whose primary function is to remain informed
about the daily operational activities of a project's assets, or simply create
transaction proposals for higher ends. While their awareness is important,
granting them the ability to execute or, in certain circumstances, vote on
ongoing transactions could inadvertently affect operations. For such
individuals, the Proposer role emerges as the optimal choice. It offers them
the freedom to put forward transaction propositions without the added
capabilities that could potentially affect the assets held within the
multisig. This role is perfect for operators.

However, Permissions introduce new security considerations for a multisig
setup. Removing major roles could prevent members from conducting and
executing transactions, affecting the assets stored within. For instance, for
a 2-3 multisig always ensure that at least two keys have voting and execution
capabilities, with the remainder having voting rights, especially if one of
the keys becomes compromised and needs replacement. It is alway essential to
maintain an adequate number of members with "Voter" and "Executor" permissions
to meet the confirmation threshold established for your Squad and to execute
proposed transactions.

Lastly, roles and permissions within the multisig are mutable. Members can
easily reassign them whenever needed through the Squads interface (or SDK for
developers) without removing the key/member.  
  

![](https://framerusercontent.com/images/b8TyBw8CEEXmgAgZiYQ9VBq75E.png)

On the security front, Permissions are enabled by our new program, v4. Squads
Protocol v4 has been audited three times by OtterSec, Neodyme and Trail of
Bits. It is currently completing two formal verifications by Certora and
OtterSec. Any project leveraging permissions through v4 directly benefits from
the security measures that have been implemented, reducing both the cost and
time required to build their product.

We have built Squads Protocol v4 to enable powerful multisig use cases.
Permissions are only the tip of the iceberg of what it allows for. In our
upcoming articles, we will dive into the plethora of features it offers,
including spending limits and fee relayer.

You can learn more about the new Squads platform and v4 in our recent
[announcement article](https://squads.so/blog/v4-and-new-squads-app).

  

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
solana-spl-token)[![squads-solana-leading-multisig-spending-limits-treasury-
management-solana-multisig-wallet-squads-protocol-audited-formal-
verification](https://framerusercontent.com/images/2tyh01MPlECImwUoS4lpntdjCM.png)How
to Improve Treasury Operations with Spending LimitsNovember 29,
2023](./spending-limits)

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

