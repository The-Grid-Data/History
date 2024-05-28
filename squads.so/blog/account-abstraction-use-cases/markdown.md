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

# Exploring Account Abstraction Use Cases

Apr 5, 2023

![account-abstraction-use-cases-smart-contract-wallet-solana-ethereum-account-
abstraction-eip-erc-4337-applications-use-cases-solana-
pda](https://framerusercontent.com/images/O8JVEriGowPcPDjADPC3ErE7W00.png)

In our [previous article](https://squads.so/blog/what-is-account-abstraction-
ethereum-vs-solana), we discussed how account abstraction (AA) in crypto is a
broad concept that can take on many forms. To recap, AA roughly refers to the
process of abstracting away the rigidity and built-in structures of user
accounts within a blockchain, making them more flexible and adaptable while
still allowing them to interact with the network.

As a broad and emerging concept, it can be challenging for developers to
identify ideas or examples of what can be built with account abstraction. This
article aims to highlight the promising potential applications of AA for
Solana developers and projects, as well as showcase some emerging use cases.
For those interested in exploring the full spectrum of ideas around account
abstraction, a comprehensive list will be included at the end of the article.

## Potential Opportunities for Solana Developers and Projects

By incorporating account abstraction, developers can create solutions that
overcome the complexities and barriers often associated with traditional
blockchain interactions. This can help projects attract a wider audience
including those who are new to the world of crypto and more broadly DeFi.
Given the extensive range of possibilities, we decided to focus on the most
promising use cases that address the gaps in onboarding newcomers to Solana,
making the process more accessible and user-friendly. The first application
that in our view stands out in this regard is âSession Keysâ.

### Session Keys

Session Keys can significantly change the way users interact with dApps
(decentralized applications). The idea is to let users create a session key
that pre-approves transactions within a dApp for a specific time, up to a
certain limit and with particular rules. This means users can use their
favorite project without having to repeatedly confirm transactions through
their wallet.

Since users predefine the allowed actions, they can interact with a protocol
while ensuring their assets remain secure. Currently, most dApps require users
to sign transactions repeatedly, which is inconvenient for users who perform
many transactions. The Session Keys approach strikes a balance between user-
friendliness and minimized risk. Session keys can be customized in various
ways, such as setting a time limit, maximum gas limit, maximum transaction
volume for a specific token, or allowing only certain functions on a specific
program. This flexibility allows protocols to offer tailored âkeysâ for
different purposes and users.

For instance, Session Keys could significantly enhance the user experience for
derivative exchanges on Solana like Drift, Zeta, or Cypher. A trader could
create a session key valid for one hour, allowing them to trade up to $50,000
without needing to confirm each transaction with their wallet. This would
create an experience similar to what users enjoy on centralized exchanges like
Binance, without the cons of centralization.

### Gasless Transactions

Another use case that could bridge the gap between DeFi and CeFi is "Gasless
Transactions," which is a concept also referred to as "Sponsored
Transactions.â The idea is to allow users to perform transactions without
having to pay gas fees. This is achieved by using a smart contract/program to
cover the gas fees on behalf of the user, simplifying the user experience and
allowing to perform transactions without requiring $SOL for gas fees.

To put it into context, consider the following example:

  1. The user interacts with a dApp that supports Gasless Transactions;

  2. When the user initiates a transaction, the protocol calls a specific program that is designed to handle Gasless Transactions;

  3. The program, known as the âsponsorâ, pays the gas fees on behalf of the user. The gas sponsor may either cover the cost as an âacquisition costâ or could ask the user to pay in a different token for instance;

  4. The program executes the user's requested transaction, while covering the gas fees.

NFT marketplaces like Magic Eden or Tensor are great examples of how this
implementation could work, since they are prone to attract users who may not
be familiar with gas fees. With Gasless Transactions, a user could have only
USDC in his wallet and still purchase NFTs and pay royalties, without having
to be concerned with gas fees for the transaction execution. On the other
hand, Tensor could introduce its own token and integrate it into the platform,
requiring users to purchase $TENSOR to perform transactions. An entire
gamification experience could be created, where users who utilize the Tensor
token for transaction fees can earn points, rewards, and additional benefits.

### Transaction Guards

Wallets also hold the potential to revolutionize the self-custody experience
for their users by implementing an account abstraction concept known as
âTransaction Guardsâ. It refers to a mechanism that allows users to define
specific conditions and rules that must be met before a transaction is
executed. This adds another layer of security and control, ensuring that
transactions follow predefined rules set by the user account.

This use case can involve features such as withdrawal limits, daily spending
limits, or whitelisted addresses. Wallets on Solana such as Backpack or
Ultimate could adopt those safeguards to help users protect their funds in
case their private key gets compromised. By generating a keypair with a wallet
like Backpack, users could configure specific triggers to manage their funds
more securely.

Protocols could also incorporate Transaction Guards that examine a user's
historical behavior and automatically halt the transaction if a potential risk
is detected (e.g., a user usually withdraws amounts ranging from $500 to $1000
but in this case the transaction amount is 20 times larger). In such cases, a
2FA confirmation might be required to ensure that it's the actual user
initiating the action, rather than a malicious actor.

### The End of Seed Phrases - Enhanced Account Authentication and Signing
Methods

Beyond enhanced security features, one of the applications that could
potentially facilitate the onboarding of newcomers to DeFi is the elimination
of seed phrases. Social recovery, login with email, and 2FA are all well-
established features in web2 that can now be implemented in crypto with
account abstraction.

For social recovery, the recovery process can involve executing a program with
a predefined set of conditions, such as obtaining signatures from a majority
of trusted associates. Users could designate friends, family members or third-
party solutions who can help recover their account if they lose access to
their private key, which will enable them to regenerate a new one.

The adaptability of smart contract wallets also allows them to work with MPC,
enabling users to log in using a social account (like Google) or an email and
password combination. The signing process can be enhanced as well by
integrating new solutions to sign transactions like 2FA, which requires users
to confirm their identity using an additional factor, such as a one-time
password or a hardware token, before executing a transaction.

While those concepts may appear promising on paper, their true value is when
implemented in real projects. Fortunately, Solana is a blockchain that already
has a variety of impressive applications, showcasing the potential of these
ideas and offering tangible examples of how crypto and DeFi can, in fact, also
be for non-crypto experts.

## Examples of Account Abstraction Applications on Solana

[Squads](https://squads.so/) is a well-known example of account abstraction in
action on Solana. It leverages Squads Protocol to provide multi-signature
functionality, allowing teams to securely manage their treasury, developer,
and creator assets. In this setup, every action taken within Squads requires
the approval of all the owners before the transaction can be executed.

More recently, Solana Grizzlython has given birth to many new projects that
are implementing some forms of account abstraction:

  * Bunkr: It aims to introduce TOTP (Time-based OneTime Password) 2FA to Solana, allowing users to secure their assets with an authenticator app of their choice;

  * RayAuth: The project wants to offer plenty of account abstraction use cases such as social logins, gasless transactions, or even session keys;

  * Cordelia: They plan to add a social recovery feature for their treasury management solution;

  * Stache (Kaizen Corps): Stache is building a smart wallet with account abstraction features like account recovery, optional seed phrases, automations.

Several existing Solana protocols have also already implemented various forms
of account abstraction. For example, [Kamino](https://app.kamino.finance/)
batches multiple transactions into one, enabling users to simply deposit one
token into a vault, with the swap and complete deposit process managed by the
protocol on their behalf. [Drift](https://app.drift.trade/), on the other
hand, recently utilized PDAs (Program Derived Addresses) to enable users to
create referral accounts, showcasing yet another application of account
abstraction on Solana.

[Drip](https://www.dcaf.so/) by Dcaf enables on-chain dollar-cost averaging
(DCA) for SPL tokens, leveraging AA to process payments automatically
according to a predetermined schedule, eliminating the need for users to
manually approve each transaction. Similarly, Gum recently introduced
[Sparkled Sessions](https://twitter.com/shek_dev/status/1642901317969645568),
which is essentially the "Session Keys" concept we've seen above. This
establishes a secure, ephemeral session between the user's wallet and the
dApp, eliminating manual approvals for every transaction.

There are countless use cases of what is possible on Solana, and the
relatively limited knowledge about account abstraction and the role of PDAs
may explain why we have only recently started to see AA implementations on
Solana. As awareness and adoption of these concepts expand, we can expect to
see more innovative use cases emerge in the ecosystem.

## AA Use Cases Are Only Limited by Your Mind

The examples shown here are just a brief overview of the many opportunities
that account abstraction offers. By moving away from the restrictions of
typical user accounts, developers can now mix the best parts of web2 and web3,
while still keeping users in control of their assets. This freedom allows
builders to come up with fresh and unique user experiences that were once
thought impossible. Below, weâve gathered all the use cases we could think
of for account abstraction:

![account-abstraction-ethereum-solana-use-cases-applications-aa-account-
abstraction-eip-4337-erc-4337-solana-pda-solana-program-derived-addresses-spl-
smart-contract-
wallet](https://framerusercontent.com/images/81k95coy1X81viAHSFluizy40.png)

As the concept of account abstraction expands further, we can't wait to see
the innovative ideas and solutions that will come from the minds of Solana
builders.

  

### About Squads

Squads is a crypto company operations platform that simplifies management of
developer, creator, and treasury assets for teams building on Solana and SVM.
Open source, formally verified, immutable, audited by Neodyme and OtterSec,
Squads enables teams to secure their treasuries, programs, validators, tokens
in a multisig and jointly manage them.

**Learn more**

 _Squads:_[_https://squads.so/blog/what-is-
squads_](https://squads.so/blog/what-is-squads) _  
Squads Protocol:_[_https://squads.so/blog/solana-svm-smart-contract-wallet-
infrastructure_](https://squads.so/blog/solana-svm-smart-contract-wallet-
infrastructure) _  
Code:_[_https://github.com/Squads-Protocol/squads-
mpl_](https://github.com/Squads-Protocol/squads-mpl)

  

Continue reading

[![Smart Account
Basics](https://framerusercontent.com/images/HXRhLfdkpXz0YDKXQQ8LnjSJI.png)Smart
Account Basics: Why Smart Accounts Will Power the Onchain EconomyMay 22,
2024](./smart-account-basics-why-smart-accounts-will-power-the-onchain-
economy)[![mpc-wallet-multi-party-computation-fireblocks-institutional-wallet-
coinbase-copper-fordefi-mpc-technology-solana-mpc-
multisig](https://framerusercontent.com/images/L6llWmB3jCRHqkDk74lbrYhhlQ.png)Multisig
vs MPCJuly 31, 2023](./mpc-wallets-risks-vs-multisig)[![account-abstraction-
ethereum-vs-solana-pda-program-derived-addresses-ethereum-aa-eip-
erc-4337-smart-contract-wallets-
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

