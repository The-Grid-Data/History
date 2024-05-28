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

# Smart Account Basics: Why Smart Accounts Will Power the Onchain Economy

May 22, 2024

![Smart Account
Basics](https://framerusercontent.com/images/HXRhLfdkpXz0YDKXQQ8LnjSJI.png)

A growing cohort of crypto users and developers are embracing smart accounts,
a technology poised to power the vast majority of the onchain economy by
simplifying digital asset management and onchain interactions. Recognizing
this potential, Squads Labs has been building smart account technology for
Solana and the SVM since 2021. But what exactly are smart accounts? Why are
they needed? This article explores these questions and more. Letâs dive in.

## Why Smart Accounts

To understand smart accounts, we first need to start with how traditional
accounts work.

On Solana, all data is stored in accounts. These âlight accountsâ are non-
programmable and controlled by a private key. Your Phantom wallet is a gateway
for interacting with these light accounts and signing transactions using the
associated private key.

Accounts are the core primitive that store your tokens and data, meaning they
sit at the heart of onchain ownership and digital asset management. But
thereâs a problem: light accounts are fundamentally limited. They only
support basic storage and transaction capabilities, are secured by private
keys, and rely on seed phrases for recovery. The underlying issue is that
light accounts are non-programmable, and the various limitations are all
symptoms of that fact.

Are there advanced and flexible account structures that support
programmability and avoid these limitations? Yes, that's where smart accounts
come in.

## The Advent of Smart Accounts

Smart accounts revolutionize the concept of light accounts, offering a dynamic
and programmable alternative. This shift is enabled by separating the account
and its controlling object (typically the private key). Instead of relying on
a private key for transaction authorization, smart accounts use programs or
smart contracts.

Smart accounts move the industry forward from a one-size-fits-all custody
model to one based on programmability and customization. They eliminate
existing pain points like seed phrases and unlock new use cases that enable
features like:

  1. **Multi-signature:** multisig wallets are controlled by multiple private keys with assigned roles to enable secure intra and inter-company management of onchain assets.

  2. **Two-factor authentication (2FA):** add an extra layer of security to transactions with passkeys, email, or hardware wallets.

  3. **Progressive security:** start with a familiar login (email) and add stronger security (2FA, key rotation) as your needs evolve.

  4. **Sponsored transactions** : applications can cover network fees for a smoother user experience (similar to free websites that sponsor AWS fees).

  5. **Gas abstraction:** pay transaction fees in any token, not just the native network token.

  6. **Time locks:** lock your assets in a vault for a set period, keeping your assets secure from instant transfers.

  7. **Key rotation:** update your keys for enhanced security without needing to move your assets.

  8. **Spending limits:** set budgets for small transactions without needing multi-sig or 2FA approval.

  9. **Batched transactions:** group multiple blockchain actions into a single transaction for seamless app interactions.

Hereâs an analogy that might help the smart account concept stick. When
introducing the iPhone in 2007, Steve Jobs explained how the problem with
traditional phones was the bottom 40 - the keyboards. He explained that these
plastic keyboards are there whether you need them or not, the layout is fixed
for every application, and itâs impossible to update if you ever think of a
new feature. Then, he introduced the iPhoneâs touch screen. A programmable
interface that revolutionized the phone by making the screen programmable and
adaptive to the use case.  Thatâs how we think about smart accounts. Smart
accounts are programmable accounts that allow customization for every user and
use case.

![](https://framerusercontent.com/images/Jp4kOzLCZnSPyJk32xccF3AEVM.png)

Before we continue, letâs review a few definitions that will help as you
learn about smart accounts:

  1. **Light accounts** are non-programmable accounts that store onchain data and are controlled by a private key.

  2. **Smart accounts** are an upgraded version of light accounts that introduce programmability and are controlled by smart contracts that define the authentication rules.

  3. **Account abstraction** is the process of turning an account into a smart account. At a technical level, this involves decoupling the account from the object authorized to control that account (traditionally a private key).

## Smart Account Adoption

The adoption of smart accounts is gaining significant momentum, with
influential figures like [Vitalik
advocating](https://vitalik.eth.limo/general/2023/06/09/three_transitions.html)
for all wallets to transition to smart accounts.

[Safe](https://safe.global/wallet) and [Squads](https://squads.so/protocol)
are two core protocols pushing smart account adoption forward. Safe (launched
in 2018) has established itself as the EVM smart account standard - securing
over $100 billion in value across 8+ million smart accounts. The bulk of
Safeâs secured value is from protocol teams and investors, but 4+ million of
their accounts are from a partnership with Worldcoin, which creates Safe smart
accounts for users behind the scenes. Squads, which launched in 2021, is the
smart account standard on Solana and the SVM - securing $15 billion across 40+
thousand smart accounts. Squads has witnessed an explosive rise in secured
value, jumping from $2 billion to $20 billion (ATH) in just one year.

![](https://framerusercontent.com/images/UiiyKOUA8CoEE9o2Z0ZWr3SlI.jpg)

Smart accounts first found product-market fit with their multisignature
(multisig) functionality. Startups, institutions and investors use these
multisigs to securely manage various onchain assets. Multisig functionality
will continue to be a primary use case, but this is just the start of the
demand for smart accounts. Here are a few reasons why:  
  

  1. **Maturing Infrastructure.** Unlike traditional accounts, smart accounts involve smart contracts, which, like any onchain contract, can have bugs. This security risk makes creating a new standard and gaining adoption extremely difficult. However, with Safe and Squads now securing $100 billion and $15 billion, respectively, these programs have emerged as the most trusted contracts in their ecosystems (as indicated by TVL), excluding the core staking contracts. This Lindy effect, combined with multiple audits and formal verification, instills developers and teams with the confidence they need to embrace smart accounts. 

  2. **App and Ecosystem Support:** Onchain applications and protocol-level rules can present challenges for smart account interoperability and usage. However, the industry is starting to align on open-source standards as the demand for smart accounts increases. Both Ethereum and Solana teams are actively working to make smart accounts first-class citizens, and tremendous progress has been made over the last year (e.g. [EIP-4337](https://safe.global/blog/future-of-ethereum-smart-accounts) and [SquadsX](https://squads.so/blog/squadsx-multisig-extension-wallet-solana) adoption).

  3. **Consumer Crypto is Here:   **Solana and L2s have ushered in a new wave of consumers and consumer-focused apps. Previously, developers catered to crypto-native whales where frictionless onboarding was an afterthought. But now, reducing onboarding friction and improving the user experience is crucial for developers. Smart account features that enable seamless sign-in and sponsored transactions are no longer ânice-to-havesâ as developers focus on CAC (customer acquisition cost), churn and return on investment (sponsored transactions).

  4. **Smart Wallets:** For the first time, multiple teams are releasing smart wallets. [Argent](https://www.argent.xyz/), [Coinbase](https://www.coinbase.com/wallet/smart-wallet) and [Safe](https://safe.global/wallet) are building smart wallets for the EVM (focused on L2s), and [Solana's first smart wallet, Fuse](https://fusewallet.com/), is launching this summer. 

  5. **New Investors, Teams and Protocols:** The institutionalization of crypto and proliferation of onchain applications increases the demand for smart account security and multi-signature functionality to secure the industryâs growing onchain economy. 

  6. **AI Agents:** AI agents could eventually dominate onchain transaction volume. These agents will use smart accounts to manage funds and interact with apps while autonomously navigating within programmatically enforced guardrails.**  
**

## Growing The Onchain Economy

Itâs time to evolve our tools to reflect the needs of todayâs market and
tomorrowâs users. Our mission at Squads Labs is to grow the onchain economy,
and the proliferation of smart accounts is one of the best ways to do that.

We hope you took a few insights from this article and understand why we
believe smart accounts will be a massive component of cryptoâs future
success.

  
  
**About Squads Labs**

Squads Labs is a core contributor to Squads Protocol, the smart account
standard for Solana and SVM. In addition to helping maintain the protocol,
Squads Labs is building the Squads app that allows Solana-based teams and
enterprises to manage their onchain assets with smart accounts.

**About Squads Protocol**

Squads Protocol is Solana's smart account standard that secures $15+ billion
in value. Teams, individual users and developers use Squads Protocol to
leverage smart accounts to upgrade how they transact, manage and own digital
assets.

Continue reading

[![mpc-wallet-multi-party-computation-fireblocks-institutional-wallet-
coinbase-copper-fordefi-mpc-technology-solana-mpc-
multisig](https://framerusercontent.com/images/L6llWmB3jCRHqkDk74lbrYhhlQ.png)Multisig
vs MPCJuly 31, 2023](./mpc-wallets-risks-vs-multisig)[![account-abstraction-
use-cases-smart-contract-wallet-solana-ethereum-account-abstraction-eip-
erc-4337-applications-use-cases-solana-
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

