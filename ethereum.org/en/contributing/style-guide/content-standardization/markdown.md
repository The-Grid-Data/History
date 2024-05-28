Skip to main content

[](/en/)

  * Learn
  * Use
  * Build
  * Participate
  * Research

Search```K`

Languages EN

  1. [Home](/en/)/
  2. [Contributing](/en/contributing/)/
  3. [Style guide](/en/contributing/style-guide/)/
  4. [Content standardization](/en/contributing/style-guide/content-standardization/)

Page last updated: February 21, 2024

On this page

  * Use American English
  * Terminology
    * Ethereum
    * Ether
    * Mainnet
    * Proof-of-work / Proof-of-stake
    * Smart contract
    * The Merge
    * Zero-knowledge
    * ZK-proof
    * ZK-rollup
    * Use active voice
    * Date Format
    * Linking to internal pages
    * Linking to images
    * Using emojis
    * Header casing
    * Article authors

# Content standardization

This style guide aims to standardize certain aspects of writing content to
make the contribution process smoother.

## Use American English

For words that have multiple spellings, use American English over British
English.

**For example:**

  * "decentralized" over "decentralised"
  * "color" over "colour"
  * "analyze" over "analyse"

## Terminology

### Ethereum

Ethereum is a proper noun and should always be capitalized.

  * "Ethereum" not "ethereum"

### Ether

Ether is a common noun and should not be capitalized unless at the beginning
of a sentence. ETH, on the other hand, is a currency abbreviation (and ticker
symbol) and should always be capitalized.

  * "ether" not "Ether"
  * "ETH" not "eth or Eth"

### Mainnet

When referring to the Ethereum Mainnet (i.e. not referring to a testnet) use
the proper noun. Proper nouns help avoid confusion and build greater
understanding.

**Correct usage:**

  * Mainnet
  * Ethereum Mainnet

**Incorrect usage:**

  * main net
  * mainnet
  * Main net
  * Ethereum mainnet

### Proof-of-work / Proof-of-stake

Proof-of-work should be capitalized only when at the beginning of a sentence.
In any other instance, all letters should be lower case. In either case,
proof-of-work should be hyphenated between each word.

**Correct usage:**

  * Proof-of-work
  * proof-of-work

**Incorrect usage:**

  * Proof-of-Work
  * Proof of work
  * proof of work

The same rules we apply to proof-of-work are applicable to proof-of-stake,
proof-of-authority, proof-of-humanity, proof-of-individuality, etc.

### Smart contract

Smart contract is a common noun and should only be capitalized at the
beginning of a sentence. In any other instance, all letters should be
lowercase.

**Correct usage:**

  * Smart contract
  * smart contract

**Incorrect usage:**

  * Smart Contract

### The Merge

When referring to The Merge, treat it as a proper noun. Always capitalize the
first letter in each word.

**Correct usage:**

  * The Merge

**Incorrect usage:**

  * The merge
  * the Merge

### Zero-knowledge

Zero-knowledge is a common noun and should only be capitalized at the
beginning of a sentence. In any other instance, all letters should be
lowercase. In either case, zero-knowledge should be hyphenated between each
word.

**Correct usage:**

  * Zero-knowledge
  * zero-knowledge

**Incorrect usage:**

  * Zero-Knowledge
  * Zero knowledge
  * zero knowledge

### ZK-proof

When using the abbreviated form of zero-knowledge proof you should shorten
zero-knowledge to ZK, and hyphenate the abbreviation.

**Correct usage:**

  * ZK-proof

**Incorrect usage:**

  * Zk-proof
  * zK-proof
  * zk-proof
  * Zk proof
  * zK proof
  * zk proof

### ZK-rollup

When using the abbreviated form of zero-knowledge rollup you should shorten
zero-knowledge to ZK, and hyphenate the abbreviation.

**Correct usage:**

  * ZK-rollup

**Incorrect usage:**

  * Zk-rollup
  * zK-rollup
  * zk-rollup
  * Zk rollup
  * zK rollup
  * zk rollup

### Use active voice

Sentences using active voice are more concise and efficient, making your
writing more engaging and easier to comprehend.

**Active voice sentence:** an actor acts on a target

>  _"The man bought a car."_

**Passive voice sentence:** a target acts on an actor

>  _"The car was bought by a man."_

[Read more on active voice(opens in a new
tab)](https://www.grammarly.com/blog/active-vs-passive-voice/)

_This isn't an easy one, especially for non-native English speakers. If you
aren't sure, don't worry. We'll help with any of these._

### Date Format

When including dates in markdown content across Ethereum documentation, it is
essential to maintain a consistent and clear presentation. In order to achieve
this, we recommend the following guidelines:

**Format:**

Use the "D-Mon-YYYY" format for dates. This format eliminates ambiguity
between the month and day, providing a standardized and easily understandable
representation.

**Examples:**

  * Preferred: 2-Nov-2023, 11-Feb-2023
  * Avoid: Nov-2-2023, 2/11/2023, 11/2/2023

By adhering to these guidelines, we create a unified approach to presenting
dates, fostering clarity and comprehension throughout Ethereum documentation.

### Linking to internal pages

When linking to another page on Ethereum.org, use the relative path over the
absolute path. Do not hard-code the language path (i.e. `/en/`) in any links.
This maintains consistent functionality across different language versions of
the site.

    
    
    <!-- Good -->
    
    Read more about [smart contracts](/docs/developers/smart-contracts/)
    
    <!-- Bad -->
    
    Read more about [smart contracts](/en/docs/developers/smart-contracts)
    Read more about [smart contracts](https://ethereum.org/en/docs/developers/smart-contracts)
    

Please also add a trailing slash to all links. This keeps links consistent and
avoids redirects, which hurts site performance.

    
    
    <!-- Good -->
    
    Read more about [smart contracts](/docs/developers/smart-contracts/)
    
    <!-- Bad -->
    
    Read more about [smart contracts](/docs/developers/smart-contracts)
    

### Linking to images

When adding an image to a page, the image should be downloaded and placed in
the same folder as the markdown file. You can reference the image like this:

`![alt text for image](./image.png)`

    
    
    <!-- Good -->
    
    ![How to mint your NFT](./mintYourNFT.gif)
    
    <!-- Bad -->
    
    ![How to mint your NFT](https://cdn-images-1.medium.com/max/2000/0342fj_fsdfs.gif)
    

This helps us ensure the image will be available.

### Using emojis

Everyone loves emojis
![🥰](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f970.svg) To
standardize the appearance of all Emojis across browsers, ethereum.org uses an
`<Emoji />` React component.

    
    
    <--- Good --->
    
    The London Upgrade is live <Emoji text=":tada:" size={1} />
    
    The London Upgrade is live <Emoji text="🎉" size={1} />
    
    <--- Bad --->
    
    The London Upgrade is live 🎉
    

### Header casing

This site uses **sentence casing** for header names as a convention. Only the
first word and proper nouns are capitalized. This applies to all markdown
files on lines that begin with hashes (#).

    
    
    <!-- Good -->
    
    ## Minting your NFT
    
    ### Setting up your wallet
    
    ### Get enough ether
    
    <!-- Bad -->
    
    ## Minting Your NFT
    
    ### Setting Up Your Wallet
    
    ### Getting Enough Ether
    

### Article authors

When citing articles from a specific author or organization, use the article's
name as a link, followed by a dash, then the author's name italicized.

    
    
    <--- Good --->
    
    - [A rollup-centric ethereum roadmap](https://ethereum-magicians.org/t/a-rollup-centric-ethereum-roadmap/4698) — _Vitalik Buterin_
    - [The History of Ethereum Testnets](https://consensys.net/blog/news/the-history-of-ethereum-testnets/) – _ConsenSys_
    
    <--- Bad--->
    
    - [A rollup-centric ethereum roadmap by Vitalik Buterin](https://ethereum-magicians.org/t/a-rollup-centric-ethereum-roadmap/4698)
    - [ConsenSys on The History of Ethereum Testnets](https://consensys.net/blog/news/the-history-of-ethereum-testnets/) – _ConsenSys_
    

### Was this article helpful?

YesNo

  * [Edit page(opens in a new tab)](https://github.com/ethereum/ethereum-org-website/tree/dev/public/content/contributing/style-guide/content-standardization/index.md)
  * On this page

    * Use American English
    * Terminology
      * Ethereum
      * Ether
      * Mainnet
      * Proof-of-work / Proof-of-stake
      * Smart contract
      * The Merge
      * Zero-knowledge
      * ZK-proof
      * ZK-rollup
      * Use active voice
      * Date Format
      * Linking to internal pages
      * Linking to images
      * Using emojis
      * Header casing
      * Article authors

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

