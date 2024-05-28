Skip to main content

[](/en/)

  * Learn
  * Use
  * Build
  * Participate
  * Research

Search```K`

Languages EN

![📝](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4dd.svg)

Uses of Ethereum are always developing and evolving. Add any info you think
will make things clearer or more up to date. [Edit page(opens in a new
tab)](https://github.com/ethereum/ethereum-org-
website/tree/dev/public/content/decentralized-identity/index.md)

![🆔](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f194.svg)

# Decentralized identity

  * Traditional identity systems have centralized the issuance, maintenance and control of your identifiers.
  * Decentralized identity removes reliance on centralized third parties.
  * Thanks to crypto, users now have the tools to issue, hold and control their own identifiers and attestations once again.

On this page

  * What is identity?
  * What are identifiers?
  * Benefits of decentralized identity
  * Decentralized identity use-cases
    * 1\. Universal logins
    * 2\. KYC authentication
    * 3\. Voting and online communities
    * 4\. Anti-Sybil protection
  * What are attestations?
    * What are decentralized identifiers?
  * What makes decentralized identifiers possible?
    * 1\. Public Key Cryptography
    * 2\. Decentralized datastores
  * How do decentralized identifiers and attestations enable decentralized identity?
  * Types of attestations in decentralized identity
    * Off-chain attestations
    * Off-chain attestations with persistent access
    * On-chain attestations
    * Soulbound tokens and identity
  * Use decentralized identity
  * Further reading
    * Articles
    * Videos
    * Communities

![](/_next/image/?url=%2Feth-gif-cat.png&w=1920&q=75)

Ethereum use cases

[Decentralized finance (DeFi)](/en/defi/)[Non-fungible tokens
(NFTs)](/en/nft/)[Decentralized autonomous organisations
(DAOs)](/en/dao/)[Decentralized social networks](/en/social-
networks/)[Decentralized identity](/en/decentralized-identity/)[Decentralized
science (DeSci)](/en/desci/)[Regenerative finance (ReFi)](/en/refi/)

## On this page

  * What is identity?
  * What are identifiers?
  * Benefits of decentralized identity
  * Decentralized identity use-cases
  * What are attestations?
  * What makes decentralized identifiers possible?
  * How do decentralized identifiers and attestations enable decentralized identity?
  * Types of attestations in decentralized identity
  * Use decentralized identity
  * Further reading

Identity underpins virtually every aspect of your life today. Using online
services, opening a bank account, voting in elections, buying property,
securing employment—all of these things require proving your identity.

However, traditional identity management systems have long relied on
centralized intermediaries who issue, hold, and control your identifiers and
_attestations_. This means you cannot control your identity-related
information or decide who has access to personally identifiable information
(PII) and how much access these parties have.

To solve these problems, we have decentralized identity systems built on
public blockchains like Ethereum. Decentralized identity allows individuals to
manage their identity-related information. With decentralized identity
solutions, _you_ can create identifiers and claim and hold your attestations
without relying on central authorities, like service providers or governments.

## What is identity?

Identity means an individual's sense of self, defined by unique
characteristics. Identity refers to being an _individual_ , i.e., a distinct
human entity. Identity could also refer to other non-human entities, such as
an organization or authority.

## What are identifiers?

An identifier is a piece of information that acts as a pointer to a particular
identity or identities. Common identifiers include:

  * Name
  * Social security number/tax ID number
  * Mobile number
  * Date and place of birth
  * Digital identification credentials, e.g., email addresses, usernames, avatars

These traditional examples of identifiers are issued, held and controlled by
central entities. You need permission from your government to change your name
or from a social media platform to change your handle.

## Benefits of decentralized identity

  1. Decentralized identity increases individual control of identifying information. Decentralized identifiers and attestations can be verified without relying on centralized authorities and third-party services.

  2. Decentralized identity solutions facilitates a trustless, seamless, and privacy-protecting method for verifying and managing user identity.

  3. Decentralized identity harnesses blockchain technology, which creates trust between different parties and provides cryptographic guarantees to prove the validity of attestations.

  4. Decentralized identity makes identity data portable. Users store attestations and identifiers in a mobile wallet and can share with any party of their choice. Decentralized identifiers and attestations are not locked into the database of the issuing organization.

  5. Decentralized identity should work well with emerging _zero-knowledge_ technologies that will enable individuals to prove they own or have done something without revealing what that thing is. This could become a powerful way to combine trust and privacy for applications such as voting.

  6. Decentralized identity enables _anti-Sybil_ mechanisms to identify when one individual human is pretending to be multiple humans to game or spam some system.

## Decentralized identity use-cases

Decentralized identity has many potential use-cases:

### 1\. Universal logins

Decentralized identity can help replace password-based logins with
decentralized authentication. Service providers can issue attestations to
users, which can be stored in an Ethereum wallet. An example attestation would
be an _NFT_ granting the holder access to an online community.

A [Sign-In with Ethereum(opens in a new tab)](https://login.xyz/) function
would then enable servers to confirm the user's Ethereum account and fetch the
required attestation from their account address. This means users can access
platforms and websites without having to memorize long passwords and improves
the online experience for users.

### 2\. KYC authentication

Using many online services requires individuals to provide attestations and
credentials, such as a driving license or national passport. But this approach
is problematic because private user information can be compromised and service
providers cannot verify the authenticity of the attestation.

Decentralized identity allows companies to skip on conventional [Know-Your-
Customer (KYC)(opens in a new
tab)](https://en.wikipedia.org/wiki/Know_your_customer) processes and
authenticate user identities via Verifiable Credentials. This reduces the cost
of identity management and prevents the use of fake documentation.

### 3\. Voting and online communities

Online voting and social media are two novel applications for decentralized
identity. Online voting schemes are susceptible to manipulation, especially if
malicious actors create false identities to vote. Asking individuals to
present on-chain attestations can improve the integrity of online voting
processes.

Decentralized identity can help create online communities that are free of
fake accounts. For example, each user might have to authenticate their
identity using an on-chain identity system, like the Ethereum Name Service,
reducing the possibility of bots.

### 4\. Anti-Sybil protection

Sybil attacks refer to individual humans tricking a system into thinking they
are multiple people to increase their influence. Grant-giving applications
that use _quadratic voting_ are vulnerable to these Sybil attacks because the
value of a grant is increased when more individuals vote for it, incentivizing
users to split their contributions across many identities. Decentralized
identities help to prevent this by raising the burden on each participant to
prove that they are really human, although often without having to reveal
specific private information.

## What are attestations?

An attestation is a claim made by one entity about another entity. If you live
in the United States, the driver's license issued to you by the Department of
Motor Vehicles (one entity) attests that you (another entity) are legally
allowed to drive a car.

Attestations are different from identifiers. An attestation _contains_
identifiers to reference a particular identity, and makes a claim about an
attribute related to this identity. So, your driver's license has identifiers
(name, date of birth, address) but is also the attestation about your legal
right to drive.

### What are decentralized identifiers?

Traditional identifiers like your legal name or email address rely on third
parties—governments and email providers. Decentralized identifiers (DIDs) are
different—they aren't issued, managed, or controlled by any central entity.

Decentralized identifiers are issued, held, and controlled by individuals. An
_Ethereum account_ is an example of a decentralized identifier. You can create
as many accounts as you want without permission from anyone and without the
need to store them in a central registry.

Decentralized identifiers are stored on distributed ledgers (_blockchains_) or
_peer-to-peer networks_. This makes DIDs [globally unique, resolvable with
high availability, and cryptographically verifiable(opens in a new
tab)](https://w3c-ccg.github.io/did-primer/). A decentralized identifier can
be associated with different entities, including people, organizations, or
government institutions.

## What makes decentralized identifiers possible?

### 1\. Public Key Cryptography

Public-key cryptography is an information security measure that generates a
_public key_ and _private key_ for an entity. Public-key _cryptography_ is
used in blockchain networks to authenticate user identities and prove
ownership of digital assets.

Some decentralized identifiers, such as an Ethereum account, have public and
private keys. The public key identifies the account's controller, while the
private keys can sign and decrypt messages for this account. Public key
cryptography provides proofs needed to authenticate entities and prevent
impersonation and use of fake identities, using [cryptographic
signatures(opens in a new
tab)](https://andersbrownworth.com/blockchain/public-private-keys/) to verify
all claims.

### 2\. Decentralized datastores

A blockchain serves as a verifiable data registry: an open, trustless, and
decentralized repository of information. The existence of public blockchains
eliminates the need to store identifiers in centralized registries.

If anyone needs to confirm the validity of a decentralized identifier, they
can look up the associated public key on the blockchain. This is different
from traditional identifiers that require third parties to authenticate.

## How do decentralized identifiers and attestations enable decentralized
identity?

Decentralized identity is the idea that identity-related information should be
self-controlled, private, and portable, with decentralized identifiers and
attestations being the primary building blocks.

In the context of decentralized identity, attestations (also known as
[Verifiable Credentials(opens in a new tab)](https://www.w3.org/TR/vc-data-
model/)) are tamper-proof, cryptographically verifiable claims made by the
issuer. Every attestation or Verifiable Credential an entity (e.g., an
organization) issues is associated with their DID.

Because DIDs are stored on the blockchain, anyone can verify the validity of
an attestation by cross-checking the issuer's DID on Ethereum. Essentially,
the Ethereum blockchain acts like a global directory that enables the
verification of DIDs associated with certain entities.

Decentralized identifiers are the reason attestations are self-controlled and
verifiable. Even if the issuer doesn't exist anymore, the holder always has
proof of the attestation's provenance and validity.

Decentralized identifiers are also crucial to protecting the privacy of
personal information through decentralized identity. For instance, if an
individual submits proof of an attestation (a driver's license), the verifying
party doesn't need to check the validity of information in the proof. Instead,
the verifier only needs cryptographic guarantees of the attestation's
authenticity and the identity of the issuing organization to determine if the
proof is valid.

## Types of attestations in decentralized identity

How attestation information is stored and retrieved in an Ethereum-based
identity ecosystem is different from traditional identity management. Here is
an overview of the various approaches to issuing, storing, and verifying
attestations in decentralized identity systems:

### Off-chain attestations

One concern with storing attestations on-chain is that they might contain
information individuals want to keep private. The public nature of the
Ethereum blockchain makes it unattractive to store such attestations.

The solution is to issue attestations, held by users off-chain in digital
wallets, but signed with the issuer's DID stored on-chain. These attestations
are encoded as [JSON Web Tokens(opens in a new
tab)](https://en.wikipedia.org/wiki/JSON_Web_Token) and contain the issuer's
digital signature—which allows for easy verification of off-chain claims.

Here's an hypothetical scenario to explain off-chain attestations:

  1. A university (the issuer) generates an attestation (a digital academic certificate), signs with its keys, and issues it to Bob (the identity owner).

  2. Bob applies for a job and wants to prove his academic qualifications to an employer, so he shares the attestation from his mobile wallet. The company (the verifier) can then confirm the validity of the attestation by checking the issuer's DID (i.e., its public key on Ethereum).

### Off-chain attestations with persistent access

Under this arrangement attestations are transformed into JSON files and stored
off-chain (ideally on a [decentralized cloud
storage](/en/developers/docs/storage/) platform, such as IPFS or Swarm).
However, a _hash_ of the JSON file is stored on-chain and linked to a DID via
an on-chain registry. The associated DID could either be that of the issuer of
the attestation or the recipient.

This approach enables attestations to gain blockchain-based persistence, while
keeping claims information encrypted and verifiable. It also allows for
selective disclosure since the holder of the private key can decrypt the
information.

### On-chain attestations

On-chain attestations are held in _smart contracts_ on the Ethereum
blockchain. The smart contract (acting as a registry) will map an attestation
to a corresponding on-chain decentralized identifier (a public key).

Here's an example to show how on-chain attestations might work in practice:

  1. A company (XYZ Corp) plans to sell ownership shares using a smart contract but only wants buyers that have completed a background check.

  2. XYZ Corp can have the company performing background checks to issue on-chain attestations on Ethereum. This attestation certifies that an individual has passed the background check without exposing any personal information.

  3. The smart contract selling shares can check the registry contract for the identities of screened buyers, making it possible for the smart contract to determine who is permitted to buy shares or not.

### Soulbound tokens and identity

[Soulbound tokens(opens in a new
tab)](https://vitalik.eth.limo/general/2022/01/26/soulbound.html) (_non-
transferable NFTs_) could be used to collect information unique to a specific
wallet. This effectively creates a unique on-chain identity bound to a
particular Ethereum address that could include tokens representing
achievements (e.g. finishing some specific online course or passing a
threshold score in a game) or community participation.

## Use decentralized identity

There are many ambitious projects using Ethereum as a foundation for
decentralized identity solutions:

  * **[Ethereum Name Service (ENS)(opens in a new tab)](https://ens.domains/)** \- _A decentralized naming system for on-chain, machine-readable identifiers, like, Ethereum wallet addresses, content hashes, and metadata._
  * **[SpruceID(opens in a new tab)](https://www.spruceid.com/)** \- _A decentralized identity project which allows users to control digital identity with Ethereum accounts and ENS profiles instead of relying on third-party services._
  * **[Ethereum Attestation Service (EAS)(opens in a new tab)](https://attest.sh/)** \- _A decentralized ledger/protocol for making on-chain or off-chain attestations about anything._
  * **[Proof of Humanity(opens in a new tab)](https://www.proofofhumanity.id)** \- _Proof of Humanity (or PoH) is a social identity verification system built on Ethereum._
  * **[BrightID(opens in a new tab)](https://www.brightid.org/)** \- _A decentralized, open-source social identity network seeking to reform identity verification through the creation and analysis of a social graph._
  * **[walt.id(opens in a new tab)](https://walt.id)** — _Open source decentralized identity and wallet infrastructure that enables developers and organizations to leverage self-sovereign identity and NFTs/SBTs._
  * **[Masca(opens in a new tab)](https://masca.io/)** — _Open source decentralized identity wallet implemented as MetaMask Snap that enables users and developers to leverage DIDs and VCs._

## Further reading

### Articles

  * [Blockchain Use Cases: Blockchain in Digital Identity(opens in a new tab)](https://consensys.net/blockchain-use-cases/digital-identity/) — _ConsenSys_
  * [What is Ethereum ERC725? Self-Sovereign Identity Management on the Blockchain(opens in a new tab)](https://cryptoslate.com/what-is-erc725-self-sovereign-identity-management-on-the-blockchain/) — _Sam Town_
  * [How Blockchain Could Solve the Problem of Digital Identity(opens in a new tab)](https://time.com/6142810/proof-of-humanity/) — _Andrew R. Chow_
  * [What Is Decentralized Identity And Why Should You Care?(opens in a new tab)](https://web3.hashnode.com/what-is-decentralized-identity) — _Emmanuel Awosika_
  * [Introduction to Decentralized Identity(opens in a new tab)](https://walt.id/white-paper/digital-identity) — _Dominik Beron_

### Videos

  * [Decentralized Identity (Bonus Livestream Session)(opens in a new tab)](https://www.youtube.com/watch?v=ySHNB1za_SE&t=539s) — _A great explainer video on decentralized identity by Andreas Antonopolous_
  * [Sign In with Ethereum and Decentralized Identity with Ceramic, IDX, React, and 3ID Connect(opens in a new tab)](https://www.youtube.com/watch?v=t9gWZYJxk7c) — _YouTube tutorial on building out an identity management system for creating, reading, and updating a user's profile using their Ethereum wallet by Nader Dabit_
  * [BrightID - Decentralized Identity on Ethereum(opens in a new tab)](https://www.youtube.com/watch?v=D3DbMFYGRoM) — _Bankless podcast episode discussing BrightID, a decentralized identity solution for Ethereum_
  * [The Off Chain Internet: Decentralized Identity & Verifiable Credentials(opens in a new tab)](https://www.youtube.com/watch?v=EZ_Bb6j87mg) — EthDenver 2022 presentation by Evin McMullen
  * [Verifiable Credentials Explained(opens in a new tab)](https://www.youtube.com/watch?v=ce1IdSr-Kig) \- YouTube explainer video with demo by Tamino Baumann

### Communities

  * [ERC-725 Alliance on GitHub(opens in a new tab)](https://github.com/erc725alliance) — _Supporters of the ERC725 standard for managing identity on the Ethereum blockchain_
  * [SpruceID Discord server(opens in a new tab)](https://discord.com/invite/Sf9tSFzrnt) — _Community for enthusiasts and developers working on Sign-in with Ethereum_
  * [Veramo Labs(opens in a new tab)](https://discord.gg/sYBUXpACh4) — _A community of developers contributing to building a framework for verifiable data for applications_
  * [walt.id(opens in a new tab)](https://discord.com/invite/AW8AgqJthZ) — _A community of developers and builders working on decentralized identity use cases across various industries_

### Was this page helpful?

YesNo

Ethereum use cases

[Decentralized finance (DeFi)](/en/defi/)[Non-fungible tokens
(NFTs)](/en/nft/)[Decentralized autonomous organisations
(DAOs)](/en/dao/)[Decentralized social networks](/en/social-
networks/)[Decentralized identity](/en/decentralized-identity/)[Decentralized
science (DeSci)](/en/desci/)[Regenerative finance (ReFi)](/en/refi/)

Website last updated: May 22, 2024

[(opens in a new tab)](https://github.com/ethereum/ethereum-org-
website)[(opens in a new tab)](https://twitter.com/ethdotorg)[(opens in a new
tab)](https://discord.gg/ethereum-org)

### Learn

  * [Learn Hub](/en/learn/)
  * [What is Ethereum?](/en/what-is-ethereum/)
  * [What is ether (ETH)?](/en/eth/)
  * [Ethereum wallets](/en/wallets/)
  * [What is Web3?](/en/web3/)
  * [Smart contracts](/en/smart-contracts/)
  * [Gas fees](/en/gas/)
  * [Run a node](/en/run-a-node/)
  * [Ethereum security and scam prevention](/en/security/)
  * [Quiz Hub](/en/quizzes/)
  * [Ethereum glossary](/en/glossary/)

### Use

  * [Guides](/en/guides/)
  * [Choose your wallet](/en/wallets/find-wallet/)
  * [Get ETH](/en/get-eth/)
  * [Dapps - Decentralized applications](/en/dapps/)
  * [Stablecoins](/en/stablecoins/)
  * [NFTs - Non-fungible tokens](/en/nft/)
  * [DeFi - Decentralized finance](/en/defi/)
  * [DAOs - Decentralized autonomous organizations](/en/dao/)
  * [Decentralized identity](/en/decentralized-identity/)
  * [Stake ETH](/en/staking/)
  * [Layer 2](/en/layer-2/)

### Build

  * [Builder's home](/en/developers/)
  * [Tutorials](/en/developers/tutorials/)
  * [Documentation](/en/developers/docs/)
  * [Learn by coding](/en/developers/learning-tools/)
  * [Set up local environment](/en/developers/local-environment/)
  * [Grants](/en/community/grants/)
  * [Foundational topics](/en/developers/docs/intro-to-ethereum/)
  * [UX/UI design fundamentals](/en/developers/docs/design-and-ux/)
  * [Enterprise - Mainnet Ethereum](/en/enterprise/)
  * [Enterprise - Private Ethereum](/en/enterprise/private-ethereum/)

### Participate

  * [Community hub](/en/community/)
  * [Online communities](/en/community/online/)
  * [Ethereum events](/en/community/events/)
  * [Contributing to ethereum.org](/en/contributing/)
  * [Translation Program](/en/contributing/translation-program/)
  * [Ethereum bug bounty program](/en/bug-bounty/)
  * [Ethereum Foundation](/en/foundation/)
  * [Ethereum Foundation Blog(opens in a new tab)](https://blog.ethereum.org/)
  * [Ecosystem Support Program(opens in a new tab)](https://esp.ethereum.foundation)
  * [Devcon(opens in a new tab)](https://devcon.org/)

### Research

  * [Ethereum Whitepaper](/en/whitepaper/)
  * [Ethereum roadmap](/en/roadmap/)
  * [Improved security](/en/roadmap/security/)
  * [Technical history of Ethereum](/en/history/)
  * [Open research](/en/community/research/)
  * [Ethereum Improvement Proposals](/en/eips/)
  * [Ethereum governance](/en/governance/)

  * [About us](/en/about/)
  * [Ethereum brand assets](/en/assets/)
  * [Code of conduct](/en/community/code-of-conduct/)
  * [Jobs](/en/about/#open-jobs)
  * [Privacy policy](/en/privacy-policy/)
  * [Terms of use](/en/terms-of-use/)
  * [Cookie policy](/en/cookie-policy/)
  * [Press Contact(opens in a new tab)](mailto:press@ethereum.org)

Is this page helpful?

### Attestation

A claim made by an entity that something is true. In context of Ethereum,
consensus validators must make a claim as to what they believe the state of
the chain to be. At designated times, each validator is responsible for
publishing different attestations that formally declare this validator's view
of the chain, including the last finalized checkpoint and the current head of
the chain. [More on attestations](/en/developers/docs/consensus-
mechanisms/pos/attestations/).

### Zero-knowledge proof

A zero-knowledge proof is a cryptographic method that allows an individual to
prove that a statement is true without conveying any additional information.
[More on zero-knowledge rollups](/en/developers/docs/scaling/zk-rollups/).

### Anti-Sybil

Are ways to stop people from pretending to be many users at once on the
internet, ensuring each user is a real, separate person. This helps keep
online interactions fair and honest.

### Non-fungible token (NFT)

Non-fungible-token (NFT ) is a unique digital item you can own, like art or
collectibles, verified by blockchain technology. [More on Non-Fungible Tokens
(NFTs)](/en/nft/).

### Quadratic voting

Is a voting method where voters express how strongly they feel about issues.
It allows voters to show not just preference, but also the intensity of their
preference.

### Account

An Ethereum account is a digital identity on the Ethereum blockchain, allowing
users to send, receive Ether or other digital assets, and interact with smart
contracts.

### Blockchain

A blockchain is a database of transactions, duplicated and shared on all
computers in the network, ensuring data cannot be altered retroactively.

### Peer-to-peer network

A network of computers (peers) that are collectively able to perform
functionalities without the need for centralized, server-based services.

### Public key

A public key is a set of characters that lets others send you digital currency
securely, like an email address for money.

### Private key

A private key is a secret code that proves you own your digital money and lets
you spend it, like a PIN for your account. **DO NOT SHARE IT**.

### Cryptography

It is the practice of making communication private and secure so that only
those for whom the information is intended can read it.

### Hash

A fixed-length fingerprint of variable-size input, produced by a hash
function. (See [keccak-256](/en/glossary/#keccak-256)).

### Smart contract

A smart contract is a program that automatically executes agreements on a
blockchain, like a self-enforcing digital contract. [Introduction to smart
contracts](/en/smart-contracts/).

### Non-fungible token (NFT)

Non-fungible-token (NFT ) is a unique digital item you can own, like art or
collectibles, verified by blockchain technology. [More on Non-Fungible Tokens
(NFTs)](/en/nft/).

