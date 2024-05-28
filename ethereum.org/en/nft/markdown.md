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
website/tree/dev/public/content/nft/index.md)

![🖼️](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f5bc.svg)

# Non-fungible tokens (NFT)

  * A way to represent anything unique as an Ethereum-based asset.
  * NFTs are giving more power to content creators than ever before.
  * Powered by smart contracts on the Ethereum blockchain.

On this page

  * What are NFTs?
  * The internet of assets
    * A comparison
  * What are NFTs used for?
  * How do NFTs work?
    * NFT security
  * Further reading

![An Eth logo being displayed via
hologram.](/_next/image/?url=%2Finfrastructure_transparent.png&w=1920&q=75)

Ethereum use cases

[Decentralized finance (DeFi)](/en/defi/)[Non-fungible tokens
(NFTs)](/en/nft/)[Decentralized autonomous organisations
(DAOs)](/en/dao/)[Decentralized social networks](/en/social-
networks/)[Decentralized identity](/en/decentralized-identity/)[Decentralized
science (DeSci)](/en/desci/)[Regenerative finance (ReFi)](/en/refi/)

## On this page

  * What are NFTs?
  * The internet of assets
  * What are NFTs used for?
  * How do NFTs work?
  * Further reading

## What are NFTs?

NFTs are tokens that are **individually unique**. Each NFT has different
properties (non-fungible) and is provably scarce. This is different from
tokens such as _ETH_ or other Ethereum based tokens like USDC where every
token is identical and has the same properties ('fungible'). You don't care
which specific dollar bill (or ETH) you have in your wallet, because they are
all identical and worth the same. However, you _do_ care which specific NFT
you own, because they all have individual properties that distinguish them
from others ('non-fungible').

The uniqueness of each NFT enables tokenization of things like art,
collectibles, or even real estate, where one specific unique NFT represents
some specific unique real world or digital item. Ownership of an asset is
publicly verifiable on Ethereum _blockchain_.

## The internet of assets

NFTs and Ethereum solve some of the problems that exist on the internet today.
As everything becomes more digital, there's a need to replicate the properties
of physical items like scarcity, uniqueness, and proof of ownership in a way
that isn't controlled by a central organization. For example, with NFTs, you
can own a music mp3 file across all Ethereum based apps and not be bound to
one company's specific music app like Spotify or Apple Music. You can own a
social media handle that you can sell or swap, but **can't be arbitrarily
taken away from you** by a platform provider.

Here's how an internet of NFTs compared to the internet most of us use today
looks...

### A comparison

An NFT internet| The internet today  
---|---  
**You own your assets!** Only you can sell or swap them.| **You rent an
asset** from some organization and it can be taken away from you.  
NFTs are **digitally unique** , no two NFTs are the same.| **A copy often
cannot be distinguished** from the original.  
Ownership of an NFT is stored on the blockchain for anyone to **verify
publicly**.| The access to ownership records of digital items is **controlled
by institutions** – you must take their word for it.  
NFTs are _smart contracts_ on Ethereum. This means they **can easily be used
in other smart contracts** and apps on Ethereum!| Companies with digital items
usually **require their own "walled garden" infrastructure**.  
Content **creators can sell their work anywhere** and can access a global
market.| Creators rely on the infrastructure and distribution of the platforms
they use. These are often subject to terms of use and **geographical
restrictions**.  
NFT creators **can retain ownership rights** over their own work, and program
royalties directly into the NFT contract.| Platforms, such as music
**streaming services, retain the majority of profits from sales**.  
  
## What are NFTs used for?

NFTs are used for many things, including:

  * proving that you attended an event
  * certify that you completed a course
  * ownable items for games
  * digital art
  * tokenizing real-world assets
  * proving your online identity
  * gating access to content
  * ticketing
  * decentralized internet domain names
  * collateral in _decentralized finance_

Maybe you are an artist that wants to share their work using NFTs, without
losing control and sacrificing your profits to intermediaries. You can create
a new contract and specify the number of NFTs, their properties and a link to
some specific artwork. As the artist, **you can program into the smart
contract the royalties** you should be paid (e.g. transfer 5% of the sale
price to the contract owner each time an NFT is transferred). You can also
always prove that you created the NFTs because you own the _wallet_ that
deployed the contract. Your buyers can easily prove that they own an
**authentic NFT** from your collection because their wallet _address_ is
associated with a token in your smart contract. They can use it across the
Ethereum ecosystem, confident in its authenticity.

![👀](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f440.svg)

Explore, buy or create your own NFT art/collectibles...

[Explore NFT art](/en/dapps/?category=collectibles#explore)

Or consider a ticket to a sporting event. Just as an **organizer of an event
can choose how many tickets to sell** , the creator of an NFT can decide how
many replicas exist. Sometimes these are exact replicas, such as 5000 General
Admission tickets. Sometimes several are minted that are very similar, but
each slightly different, such as a ticket with an assigned seat. These can be
bought and sold peer-to-peer without paying ticket handlers and the buyer
always with assurance of the ticket authenticity by checking the contract
address.

On ethereum.org, **NFTs are used to demonstrate that people have meaningfully
contributed** to our Github repository (programmed the website, written or
modified an article...), translated our content, or attended our community
calls, and we've even got our own NFT domain name. If you contribute to
ethereum.org, you can claim a _POAP_ NFT. Some crypto meetups have used POAPs
as tickets. [More on contributing](/en/contributing/#poap).

[![ethereum.org
POAP](/_next/image/?url=%2Fcontent%2Fnft%2Fpoap.png&w=1920&q=75)](/content/nft/poap.png)

This website also has an alternative domain name powered by NFTs,
**ethereum.eth**. Our `.org` address is centrally managed by a domain name
system (DNS) provider, whereas ethereum`.eth` is registered on Ethereum via
the Ethereum Name Service (ENS). And it's owned and managed by us. [Check our
ENS record(opens in a new tab)](https://app.ens.domains/name/ethereum.eth)

[More on ENS(opens in a new tab)](https://app.ens.domains)

## How do NFTs work?

NFTs, like any digital items on the Ethereum blockchain, are created through a
special Ethereum based computer program called a "smart contract." These
contracts follow certain rules, like the _ERC-721_ or _ERC-1155_ standards,
which determine what the contract can do.

The NFT smart contract can do a few key things:

  * **Create NFTs:** It can make new NFTs.
  * **Assign Ownership:** It keeps track of who owns which NFTs by linking them to specific Ethereum addresses.
  * **Give Each NFT an ID:** Each NFT has a number that makes it unique. Additionally, there's usually some information (metadata) attached to it, describing what the NFT represents.

When someone "creates" or "mints" an NFT, they're basically telling the smart
contract to give them ownership of a particular NFT. This information is
securely and publicly stored in the blockchain.

Furthermore, the creator of the contract can add extra rules. They might limit
how many of a certain NFT can be made or decide that they should get a small
royalty fee whenever the NFT changes hands.

### NFT security

Ethereum's security comes from _proof-of-stake_. The system is designed to
economically disincentivize malicious actions, making Ethereum tamper-proof.
This is what makes NFTs possible. Once the _block_ containing your NFT
transaction becomes _finalized_ it would cost an attacker millions of ETH to
change it. Anyone running Ethereum software would immediately be able to
detect dishonest tampering with an NFT, and the bad actor would be
economically penalized and ejected.

Security issues relating to NFTs are most often related to phishing scams,
smart contract vulnerabilities or user errors (such as inadvertently exposing
private keys), making good wallet security critical for NFT owners.

[More on security](/en/security/)

## Further reading

  * [A beginner's guide to NFTs(opens in a new tab)](https://linda.mirror.xyz/df649d61efb92c910464a4e74ae213c4cab150b9cbcc4b7fb6090fc77881a95d) – _Linda Xie, January 2020_
  * [EtherscanNFT tracker(opens in a new tab)](https://etherscan.io/nft-top-contracts)
  * [ERC-721 token standard](/en/developers/docs/standards/tokens/erc-721/)
  * [ERC-1155 token standard](/en/developers/docs/standards/tokens/erc-1155/)
  * [Popular NFT Apps and Tools(opens in a new tab)](https://www.ethereum-ecosystem.com/blockchains/ethereum/nfts)

## Test your Ethereum knowledge

NFTs - Non-fungible tokens

Question number 1:Two NFTs representing the same artwork are the same thing.

A

True

B

False

Check answer

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

### Ether

The native cryptocurrency of Ethereum, commonly referred to as “ETH”. It is
used to cover transaction fees when using Ethereum ecosystem and applications.
[More on ether](/en/eth/).

### Blockchain

A blockchain is a database of transactions, duplicated and shared on all
computers in the network, ensuring data cannot be altered retroactively.

### Smart contract

A smart contract is a program that automatically executes agreements on a
blockchain, like a self-enforcing digital contract. [Introduction to smart
contracts](/en/smart-contracts/).

### DeFi

A broad category of Ethereum apps aiming to provide financial services backed
by the blockchain, without any intermediaries. [More on decentralized finance
(DeFi)](/en/defi/)

### Wallet

A wallet is a digital tool to store, send, and receive digital currency, like
a virtual purse for your online money. [More on Ethereum
wallets](/en/wallets/).

### Address

An Ethereum address is a unique identifier used for receiving tokens,
functions similar to a bank account number for cryptocurrencies. Its used to
identify your Ethereum account.

### POAP

Proof of Attendance Protocol is used to create a digital collectible (NFT)
that proves you attended a specific event or activity.

### ERC-721

A standard set of rules used to create NFTs (non fungible tokens).

### ERC-1155

A type of Ethereum token standard similar to NFT (like unique collectible
items) that also allows to create interchangeable items (like currency) within
a single smart contract.

### Proof-of-stake (PoS)

A method by which a cryptocurrency blockchain protocol aims to achieve
distributed [consensus](/en/glossary/#consensus). PoS asks users to prove
ownership of a certain amount of cryptocurrency (their "stake" in the network)
in order to be able to participate in the validation of transactions. [More on
proof-of-stake](/en/developers/docs/consensus-mechanisms/pos/).

### Block

A block is where transactions or digital actions are stored. Once a block is
full, it gets linked to the previous one, creating a chain of blocks or a
"blockchain". [More on blocks](/en/developers/docs/blocks/).

### Finality

Finality is the guarantee that a set of transactions cannot be changed without
a huge amount of ETH being lost.

