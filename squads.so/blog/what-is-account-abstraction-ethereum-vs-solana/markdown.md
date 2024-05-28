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

# An Introduction to Account Abstraction

Mar 21, 2023

![account-abstraction-ethereum-vs-solana-pda-program-derived-addresses-
ethereum-aa-eip-erc-4337-smart-contract-wallets-
solana](https://framerusercontent.com/images/P3OOJ94NoGqBPK1lFEHoi8GCMM.png)

For a long time, crypto wallets were reserved exclusively for advanced users,
offering limited capabilities and hindering the onboarding of newcomers.
Recent advancements in account abstraction are finally facilitating the
creation of new self-custody solutions that could potentially attract the next
generation of users into crypto. While it has been implemented natively in
newer blockchain networks such as Solana, account abstraction has recently
gained significant interest across the Ethereum community, primarily due to
the long-awaited ERC-4337 upgrade.

This article aims to introduce the general concept of account abstraction (AA)
in crypto while navigating the AA capabilities of both Ethereum and Solana
networks and understanding their differences. Lastly, we will explore the
smart contract wallet standard that we built at Squads to facilitate
developing account abstraction on Solana.

_Note: The terms âaccountâ or âuser accountâ will often be mentioned
in this article. An account is not a wallet. In crypto, a wallet is only an
interface or application that lets users interact with blockchain accounts._

## What is Account Abstraction

Account abstraction is a concept that has been around in crypto since
[2015](https://hackmd.io/@matt/r1neQ_B38), with Vitalik being a prominent
advocate for it. While AA is a broad term, it roughly refers to the process of
abstracting away the rigidity and built-in structures of user accounts within
a blockchain, making them more flexible and adaptable while still allowing
them to interact with the network. This abstraction enables developers to
create user-friendly on-chain accounts with custom logic, where they can set
their own conditions for storing assets and executing transactions, instead of
relying on the built-in rules of standard blockchain accounts that are not
suited for everyday use.

Beyond traditional blockchains, where account structures are bound to a single
owner and a specific keypair (private and public keys), AA makes it possible
for developers to create smart contracts that can act as user accounts. These
smart contracts can interact with multiple accounts, perform cross-program
communications, and integrate a wide range of customized logic.

![what-is-account-abstraction-smart-contract-wallet-solana-multisig-smart-
wallet-fuse-aa-use-cases-account-abstraction-
solana](https://framerusercontent.com/images/DkhUvs5MkkoCFKa0goUxsFgs8.png)

Although the term âaccount abstractionâ can be used both in Ethereum and
Solana, it is important to understand that its implementation and features
differ between the two blockchains. Generally speaking, account abstraction in
crypto involves the customization of:

  * **account structures** : developers can define their own account structures for specific purposes and how the data is stored;

  * **validation and execution schemes** : enabling implementation of custom transaction validation and execution logic;

  * **interaction between accounts** : facilitating composability between different user accounts/smart contracts in how they can work together.

With AA, the idea is thus to allow and simplify the process for developers to
create user accounts for any need, that are no longer blocked by a set
structure, and are natively supported by the network. In the words of
[Argent](https://www.argent.xyz/blog/wtf-is-account-abstraction/), _âaccount
abstraction moves crypto from the current approach of one-account-fits-all,
where someone can lose everything with a small mistake, to a future where an
account can be tailored to someone's needs. Where you can build a safety net
for self-custody. And give them much slicker UX too.â_

The ultimate goal of AA is to make the underlying technology (blockchain) of
the user account imperceptible to users.

## Account Abstraction on Ethereum and ERC-4337 Explained

In Ethereum, account abstraction has always been an ongoing area of research
and development due to the rigidity and structure of Ethereum accounts. Until
ERC-4337, there was no standardized approach for developers to create and
implement custom user accounts, which has led to a poor user experience to
store and manage assets on-chain.

Due to the late implementation of a standard for account abstraction, most
Ethereum wallets today such as Metamask only allow users to create and manage
EOA wallets. These are a type of Ethereum account with limited customization
and flexibility. Externally Owned Accounts (EOAs) are controlled by private
keys and can only be used to store data (ETH, ERC-20, or ERC-721 tokens) and
interact with smart contracts by signing transactions. Because they have a
built-in structure, these accounts offer limited functionality and cannot have
custom logic implemented, which restricts the range of actions for managing
assets and interacting with smart contracts. For a long time, EOAs were the
only way to sign and interact with Ethereum smart contracts.

Smart (contract) wallets emerged as a solution to address EOAs limitations by
offering wallets based on [Contract
Accounts](https://ethereum.org/en/developers/docs/accounts/#types-of-account)
\- a type of account that brings account abstraction to Ethereum and unlocks
new possibilities in the way user accounts function. A Contract Account is a
smart contract that stores data, and code. Thus, its behavior is determined by
the code within the smart contract and is not controlled by a private key.
This design enables Ethereum Contract Accounts to have programmable logic and
literally create any type of customized account for users. Smart wallets
leverage the capabilities of contract accounts, which makes them a more
advanced and user-friendly alternative to traditional Externally Owned
Accounts (EOAs) as they can offer a plethora of use cases: social recovery,
paying fees in any token (e.g. USDC), recurring payments, session keys, and
more.

Contract accounts have never really been widely used to create and manage user
wallets due to their complexity and cost of use. They were not fully supported
by the Ethereum Virtual Machine (EVM) and posed challenges when attempting to
interact with the network as they couldnât initiate transactions themselves.
While solutions like Argent and
[Safe](https://safe.mirror.xyz/9KmZjEbFkmI79s28d9xar6JWYrE50F5AHpa5CR12YGI)
have found workarounds to implement account abstraction on Ethereum for
creating smart wallets, there was no clear standard for developers to build
custom user accounts in a truly decentralized and secure manner - until
EIP-4337 was implemented and became the ERC-4337 standard.

### The Role of ERC-4337

[ERC-4337](https://eips.ethereum.org/EIPS/eip-4337) is a new smart contract
wallet standard that allows to have highly programmable user accounts natively
on Ethereum without making changes to the protocol. Rather than altering the
consensus layer to support smart contract wallets, a new system has been
integrated alongside the standard transaction process of EVM. This advanced
system bundles Contract Accounts actions and their associated signatures and
then sends them to a specific âmempoolâ where validators can gather them
to create a âbundle transactionâ. They are then included in Ethereum
blocks just like regular transactions.

Additionally, ERC-4337 changes the way Contract Accounts function by
outsourcing complex safety features to a universal wallet contract known as
the "entry point." This contract manages operations like fee payments and EVM
code execution, enabling developers to build composable accounts without
security concerns around centralization.

ERC-4337 is the first step towards implementing native account abstraction and
making contract accounts, particularly smart contract wallets, more efficient
and flexible on EVM. It is already in the process of being supported by
prominent smart wallets on Ethereum, such as
[Safe](https://safe.mirror.xyz/9KmZjEbFkmI79s28d9xar6JWYrE50F5AHpa5CR12YGI).

## Account Abstraction on Solana - Always Has Been

Compared to Ethereum, Solana has always been a blockchain that natively
enables account abstraction since its architecture is fundamentally different
from EVM. Accounts on Solana are by default more flexible, simplifying the
development of complex interactions between them and smart contracts. In fact,
everything in Solana is considered as an account. [Solanaâs account
model](https://www.alchemy.com/overviews/solana-account-model) treats all
accounts as âstorage bucketsâ, meaning they can store data, tokens, as
well as any information associated with a specific program/smart contract
(smart contracts on Solana are named programs).  
  

![solana-account-model-account-types-executable-non-executable-account-solana-
program-accounts-data-accounts-pda-ethereum-vs-solana-account-model-
types](https://framerusercontent.com/images/vDrvxgtTmYXgEi56PXdanKYiAIE.png)

There are 2 main account types on Solana:

  * **executable** (program accounts) - these are smart contracts that store code and are more often referred to as âprogramsâ;

  * and **non-executable** (data accounts) - they can receive tokens or data, but cannot execute code.

Typically, traditional Solana wallets allow users to create data accounts/non-
executable accounts. These are regular accounts used for storing data, tokens
information and signing transactions. Data accounts on Solana share some
similarities with Ethereum's External Owned Accounts (EOAs) in the sense that
both types of accounts are primarily used by users to hold and manage their
tokens, as well as interacting with decentralized applications (dApps) and
smart contracts. Even though they offer additional features than Ethereumâs
EOAs, they still remain unfriendly to use for neophytes as they only offer a
single method to sign transactions: the use of a private key.

What makes Solana special is that its account model natively enables programs
to create and manage specific accounts, offering developers the ability to
define custom rules and logic for managing them. This feature, that further
extends account abstraction capabilities on Solana, is called [Program Derived
Addresses](https://www.alchemy.com/overviews/program-derived-address) (PDAs).
Solana programs, conversely to data accounts, are executable accounts. They
contain code that can be executed. With PDAs, developers can set up a set of
rules and mechanisms to sign transactions. It allows programs to authorize
different on-chain operations on behalf of a controlled account (PDA) in a way
that is recognized and accepted by the Solana network without needing a
private key.

PDAs are a key feature of account abstraction on Solana, since they can be
used to enable actions without requiring private keys, reducing the burden on
end-users to manage them. They can also allow implementation of custom rules
and logic in how to access, store, and manage SPL assets. Smart wallets on
Solana like [Squads](https://squads.so/) leverage PDAs functionality to enable
complex customization of account management such as multi-signature (multisig)
or batched transactions. Moreover, PDAs serve as the foundation for [Cross-
Program Invocation](https://docs.solana.com/developing/programming-
model/calling-between-programs) (CPI), which allows Solana accounts to
interact and compose with one another.

While both Solana and Ethereum aim to provide a flexible environment for
building custom account structures, we can see that their approaches to AA
differ significantly. Ethereum features a more rigid account structure with
distinct account types, whereas Solana employs a more flexible account model,
simplifying development and enabling complex account interactions. While EVM
developers must rely on workarounds or wait for protocol layer updates, SVM
developers can create self-custody products leveraging native AA without any
constraints.

But even if the customization of user accounts is more advanced and
decentralized on Solana since it is already enabled at the protocol level,
there are still many challenges standing in the way of ubiquitous adoption of
account abstraction-powered solutions like smart wallets. One of them is poor
support for workflows involving smart wallets in the ecosystem, as well as
protocols that are trying to artificially limit their composability by
preventing other programs from calling into them and/or keeping their code
private and not providing IDL (interface) for it.

## Squads Protocol - The Smart Contract Wallet Standard That Unlocks
Solanaâs AA Capabilities

ERC-4337 has established a standard on Ethereum for building self-custody
solutions like smart contract wallets that implement AA. Until recently,
Solana was lacking simplification for building self-custody and treasury
management products on top of its PDA functionality, although it natively
enables a high level of account abstraction.

Squads Multisig Program Library (or SMPL) is a set of open-source programs on
Solana that anyone can leverage to build self custody products on top of -
making it the ultimate smart contract wallet infrastructure for SVM.
Solanaâs account model has supported account abstraction since inception,
and Squads Protocol makes it easier for developers to work with it.

Squads Protocol stack allows Solana developers to create customizable self-
custody solutions tailored to specific use cases and user needs. SMPL has been
built to support effortless implementation of AA on Solana, and facilitates
developers in how they can build smart wallets. With it, they can build
advanced features like social recovery, granular controls/permissions on funds
held, or even remove the need to save a 12/24 word seed phrase to access and
manage SPL assets.

By unlocking the full potential of account abstraction, Squads Protocol paves
the way for a more seamless and user-friendly experience for onboarding the
next generation of crypto users on Solana. Ultimately, the importance of AA
lies not only in its implementation by the network but also in the features
that developers can create using it as a foundation. Whether users are on
Ethereum or Solana, implementing account abstraction enables the creation of
self-custody solutions that make them forget they are using a blockchain and
bridge the gap with web2 financial products.

In our next article, we'll explore some account abstraction use cases that
Solana builders can consider developing.

  

### About Squads

Squads is a crypto company operations platform that simplifies management of
developer and treasury assets for teams building on Solana and SVM. Open
source, formally verified, immutable, audited by Neodyme and OtterSec, Squads
enables teams to secure their treasuries, programs, validators, tokens in a
multisig and jointly manage them.

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
use-cases-smart-contract-wallet-solana-ethereum-account-abstraction-eip-
erc-4337-applications-use-cases-solana-
pda](https://framerusercontent.com/images/O8JVEriGowPcPDjADPC3ErE7W00.png)Exploring
Account Abstraction Use CasesApril 5, 2023](./account-abstraction-use-cases)

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

