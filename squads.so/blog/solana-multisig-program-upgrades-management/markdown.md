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

# Why Manage Program Upgrades with a Multisig

Mar 8, 2023

![Solana Multisig to Manage Program Upgrades Management Upgrade Authority Key
Solana Protocol Security Squads Multisig
Platform](https://framerusercontent.com/images/do2lcH5MjdrHgwwH3T0UCgFaSFk.png)

Securely managing a protocol on Solana involves multiple aspects, but there
are limited resources available to assist teams and developers in learning the
best practices to be applied. One component that is not talked about
frequently enough, and which almost severely damaged the Solana DeFi ecosystem
during the FTX collapse, is the management of program upgrade authorities.

The security of Solana protocols and their user funds is directly impacted by
how teams manage their programs. Most protocols on Solana are upgradeable, and
program upgrade authority allows developers to effect any kind of changes to
the protocol. That makes it a very valuable asset for any project, and
mismanagement at this level can significantly affect both the protocol and its
users.

This article will cover what to avoid when it comes to managing and keeping
program upgrade authorities safe, as well as diving into the solution we built
at Squads to make the process of upgrading Solana programs secure, robust and
intuitive.

## The Process of Upgrading Solana Programs and Its Risks

On Solana, most programs (smart contracts) are upgradeable, allowing protocols
to easily push updates without requiring users to transfer funds to a new
program. While this comes with advantages, it also presents tradeoffs that
must be considered when developing on Solana.

In order to upgrade a program, developers must redeploy it. To do so, each
program account on Solana contains an upgrade key that enables modifications
to be made to the program. Typically, the authority key is the Solana
account/address that originally deployed the program (though it can be changed
to another key). Every time a transaction is created to update a Solana
program, it needs to be signed by this authority key.

This is where a lack of education regarding program upgrade security becomes
apparent: according to
[Neodyme](https://blog.neodyme.io/posts/solana_upgrade_authority/), most
Solana protocols use a simple cold wallet to manage their authority key, which
poses significant risks if the account/address holding the authority key is
stolen or compromised. Furthermore, a single wallet essentially gives
âownershipâ over the program to one entity, thus establishing a single
point of failure.

Fortunately, beyond cold/hot wallets there are other solutions for managing
program upgrades of a Solana protocol. One way is to move the upgrade
authority to a DAO, where token holders can vote to make changes to the code.
However, this approach is not considered the most optimal for projects that
are not yet ready to give up control over the program to the community and
transition to a DAO structure. From an operational standpoint it can also be
difficult for the protocol to quickly fix bugs or issues without alerting the
entire community, including potential malicious actors who could take
advantage of the situation (particularly relevant at the early stages of
protocol development).

A second solution, which is starting to take hold, is to move the upgrade
authority to a multisig. A multisig (short for multi-signature) is a consensus
mechanism that requires multiple parties to sign off on a transaction before
it can be executed. It thus eliminates the risk of holding the upgrade
authority with a single key, and enables team members to fix bugs or any issue
safely and in a timely manner while maintaining a level of decentralization
amongst the team.

Although many factors point to a multisig being the most secure and flexible
solution, its use and adoption levels for managing upgrade authorities could
be a lot higher in the Solana ecosystem. Many were alerted to that reality
when the Serum case has unfolded during the FTX collapse.

_Note that while burning the authority keys to make the code immutable is
another option to consider, it could create additional risks if issues are
identified post immutability. This approach works well for some protocols
early on and should be the end goal for most, however the realities of
shipping code and building in such a fast paced environment as crypto require
teams to stay agile and be able to upgrade their codebase on a regular basis.
For newer protocols, it is important for the codebase to stand the test of
time in terms of security and resiliency before thinking of taking this step._

## The Serum Upgrade Authority Case

In November 2022, shortly after the FTX incident, the Solana DeFi ecosystem
narrowly avoided a potential disaster. The panic was sparked by Serum, which
was a foundational protocol for the Solanaâs DeFi ecosystem at the time,
powering countless major projects including Jupiter, Raydium, and Mango
Markets.

Several days after FTX suspended withdrawals, a security breach occurred on
the exchange. While this could have been an isolated event, it turned out that
the Serum program upgrade key was not under the control of Serum DAO, but
rather was managed by a private key held by FTX. As a result, the exchange
attacker(s) could also have been in position to potentially compromise the
Serum code, as nobody at that time knew where and who was holding its
authority key.

Since the identity of the individual holding the Serum authority key was still
unknown during this time, and could potentially have fallen into the hands of
the hacker(s), the Serum code could have been upgraded without notifying
anyone. This would have included the ability to lock funds from the Serum
order book or transfer them to a new wallet address, resulting in significant
losses for users and the ecosystem. To prevent this, a fork of Serum was made
with its upgrade authority managed by a DAO of contributors from the Solana
ecosystem.

Despite the successful handling of the situation by the [Solana
community](https://twitter.com/m_schneider/status/1591636068650352640) through
the creation of OpenBook (Serum fork), it does not seem that the message has
been widely spread. The ecosystem still heavily relies on using cold/hot
wallets to manage authority keys, instead of splitting the ownership across
several owners to decentralize the security of protocol programs amongst the
team members/core developers.

In fact, many Solana projects continue to use insecure and centralized methods
to manage their programs even after the Serum fork event.

## Most Solana Protocols Are Still Using a Traditional Wallet to Manage their
Authority Key

Despite the significant impact of the Serum incident, it appears that the
importance of using a multisig to manage program upgrades has not been fully
realized by the ecosystem.

As previously mentioned, the practice of using traditional wallets to manage
program upgrades poses a significant danger to both the protocol and the
users' funds, adding unnecessary risks. With over $250mln locked in various
Solana protocols, this could have devastating effects on the ecosystem,
endangering the benefits of composability, where one protocol being
compromised can impact several others and their users.

Fortunately, there is a straightforward solution to this problem for projects
- transferring the upgrade authority to a multisig, instead of relying on a
cold/hot wallet. This approach offers numerous benefits for teams looking to
manage their program upgrade authorities:

  * it greatly reduces the likelihood of the upgrade authority being compromised and thus prevents the loss of funds, as ownership is distributed among multiple addresses with thresholds to approve an upgrade;

  * all team members involved in managing program upgrades can be held accountable for their actions, ensuring that decisions are made in the best interests of the project;

  * the entire team, including non-technical founders, can view all changes to the code in a single interface, such as the one offered by Squads. This includes every update, the protocol's upgrade history, and notifications when an upgrade is being pushed through;

  * it prevents any single individual from exerting singular control over the protocol, as changes require approval from all team members added in the multisig.

The process is also straightforward, as solutions like Squads make it easy to
change the upgrade authority through an intuitive interface. Additionally,
users who prefer a safer way to perform the authority transfer can make a
[Safe Authority Transfer](https://docs.squads.so/squads-v3-docs/navigating-
your-squad/developers/programs#add-programs) (SAT).

For a long time, Solana teams had no viable options to manage their programs
with a secure and reliable multisig solution, which significantly contributed
to the culture of using cold/hot wallets to manage upgrade authority instead
of leveraging more robust self-custody tools. With Squads, that is no longer
the case.

## Squads: The Most Advanced Multisig Solution to Manage Program Upgrades on
Solana

![squads-program-upgrades-tool-platform-programs-management-upgrade-authority-
key-solana-security-
protocol](https://framerusercontent.com/images/WRGt00fvG2XAD44iMXnmi24xVwA.png)

Enter Squads, a platform that streamlines the management of developer assets
on Solana and SVM, allowing teams to easily manage program upgrades through a
sleek interface. Squads is built on top of [Squads
Protocol](https://squads.so/blog/solana-svm-smart-contract-wallet-
infrastructure), an **immutable** and [**formally
verified**](https://osec.io/blog/2023-01-26-formally-verifying-solana-
programs) (the first on Solana) multisig infrastructure. **Open-source** and
multiple time **audited** by top-tier firms like OtterSec and Neodyme, every
Squad is a multisig at its core, which ensures that any transaction or action
taken within the platform requires the approval of multiple members of the
team.

By using Squads, teams can transfer the upgrade authority of their Solana
programs to a multisig wallet, eliminating the reliance on a single key for
control. The process for program upgrades then occurs through the Squads
platform, requiring multi-signature approval before deployment. Adding Solana
programs to Squads is a straightforward process for teams and comes with an
easy-to-use UX.

Several Solana protocols such as Raydium, Marginfi, Kamino, Jupiter, Francium
are using Squads to decentralize their workflows and program management
amongst the team, pushing the Solana ecosystem towards a more protocol
security oriented culture. Over 85 programs have been delegated to a Squads
multisig to date, proving its usefulness for teams.

![squads-trusted-by-jito-kamino-clockword-raydium-jupiter-marginfi-francium-
frakt-squads-multisig-
partners](https://framerusercontent.com/images/HRCCz3egyLGWGTjBsEW5LP1fUfs.png)

While many Solana protocols were unaware of better solutions to manage their
programs in the past, it is now clear that change is necessary. Solana
programsâ upgradeability should not pose a security risk to users, as this
could cause a loss of trust and potentially drive users to other immutable
solutions like those offered by Ethereum protocols. Fortunately, platforms
like Squads offer teams the ability to secure their most valuable assets in
one place, from treasury to programs, and eliminate the risks associated with
relying solely on cold/hot wallets to manage authority keys.

  

### Get Started

 _Create a Squad:_[_https://v3.squads.so_](https://v3.squads.so/) _  
Start Securing your Programs with a
Multisig:_[_https://docs.squads.so/squads-v3-docs/navigating-your-
squad/developers/programs_](https://docs.squads.so/squads-v3-docs/navigating-
your-squad/developers/programs) _  
Review the Code:  _[_https://github.com/Squads-Protocol/squads-
mpl_](https://github.com/Squads-Protocol/squads-mpl) _  
Get your Questions
Answered:_[_https://discord.com/invite/YPXz64TrKs_](https://discord.com/invite/YPXz64TrKs)

  

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

