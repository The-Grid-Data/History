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
  3. [Adding Staking Products](/en/contributing/adding-staking-products/)

Page last updated: August 15, 2023

On this page

  * The decision framework
    * Criteria for inclusion
      * Software and smart contracts
      * Node or client tooling
      * Staking as a service
      * Staking pool
    * Other criteria: the nice-to-haves
  * How we display results
  * Add your product or service

# Adding staking products or services

We want to make sure we list the best resources possible while keeping users
safe and confident.

Anyone is free to suggest adding a staking products or service on
ethereum.org. If there's one that we have missed, **[please suggest it(opens
in a new tab)](https://github.com/ethereum/ethereum-org-
website/issues/new?assignees=&labels=feature+%3Asparkles%3A%2Ccontent+%3Afountain_pen%3A&template=suggest_staking_product.yaml)!**

We currently list staking products and services on the following pages:

  * [Solo staking](/en/staking/solo/)
  * [Staking as a service](/en/staking/saas/)
  * [Staking pools](/en/staking/pools/)

Proof-of-stake on the Beacon Chain has been live since December 1, 2020. While
staking is still relatively new, we've tried to create a fair and transparent
framework for consideration on ethereum.org but the listing criteria will
change and evolve over time, and is ultimately at the discretion of the
ethereum.org website team.

## The decision framework

The decision to list a product on ethereum.org is not dependent on any one
factor. Multiple criteria are considered together when deciding to list a
product or service. The more of these criteria are met, the more likely it is
to be listed.

**First, which category of product or service is it?**

  * Node or client tooling
  * Key management
  * Staking as a service (SaaS)
  * Staking pool

Currently, we are only listing products or services in these categories.

### Criteria for inclusion

Staking products or services submissions will be assessed by the following
criteria:

**When was the project or service launched?**

  * Is there evidence of when the product or service became available to the public?
  * This is used to determine the products "battle tested" score.

**Is the project being actively maintained?**

  * Is there an active team developing the project? Who is involved?
  * Only actively maintained products will be considered.

**Is the product or service free of trusted/human intermediaries?**

  * What steps in the users journey require trusting humans to either hold the keys to their funds, or to properly distribute rewards?
  * This is used to determine the product or services "trustless" score.

**Does the project provide accurate and reliable information?**

  * It is crucial that the product's website features up-to-date, accurate, and non-misleading information, particularly if it pertains to the Ethereum protocol or other related technologies.
  * Submissions containing misinformation, outdated details, or potentially misleading statements about Ethereum or other relevant subjects will not be listed or will be removed if already listed.

**What platforms are supported?**

  * i.e. Linux, macOS, Windows, iOS, Android

#### Software and smart contracts

For any custom software or smart contracts involved:

**Is everything open source?**

  * Open source projects should have a publicly available source code repository
  * This is used to determine the products "open source" score.

**Is the product out of _beta_ development?**

  * Where is the product at in its development cycle?
  * Products in the beta stage are not considered for inclusion on ethereum.org

**Has the software undergone an external security audit?**

  * If not, are there plans to conduct an external audit?
  * This is used to determine the products "audited" score.

**Does the project have a bug bounty program?**

  * If not, are there plans to create a security bug bounty?
  * This is used to determine the products "bug bounty" score.

#### Node or client tooling

For software products related to node or client setup, management or
migration:

**Which consensus layer clients (i.e. Lighthouse, Teku, Nimbus, Prysm) are
supported?**

  * Which clients are supported? Can the user choose?
  * This is used to determine the products "multi-client" score.

#### Staking as a service

For [staking-as-a-service listings](/en/staking/saas/) (i.e. delegated node
operation):

**What are the fees associated with using the service?**

  * What is the fee structure, e.g. is there a monthly fee for the service?
  * Any additional staking requirements?

**Are users required to sign-up for an account?**

  * Can someone use the service without permission or KYC?
  * This is used to determine the products "permissionless" score.

**Who holds the signing keys, and withdrawal keys?**

  * What keys does the user maintain access to? What keys does the service gain access to?
  * This is used to determine the products "trustless" score.

**What is the client diversity of the nodes being operated?**

  * What percent of validator keys are being run by a majority consensus layer (CL) client?
  * As of last edit, Prysm is the consensus layer client being run by a majority of node operators, which is dangerous for the network. If any CL client is currently being used by over 33% of the network, we request data related to its usage.
  * This is used to determine the products "diverse clients" score.

#### Staking pool

For [pooled staking services](/en/staking/pools/):

**What is the minimum ETH required to stake?**

  * e.g. 0.01 ETH

**What are the fees or staking requirements involved?**

  * What percentage of rewards are removed as fees?
  * Any additional staking requirements?

**Is there a liquidity token?**

  * What are the tokens involved? How do they work? What are the contract addresses?
  * This is used to determine the products "liquidity token" score.

**Can users participate as a node operator?**

  * What is required to run validator clients using the pooled funds?
  * Does this require permission from an individual, company or DAO?
  * This is used to determine the products "permissionless nodes" score.

**What is the client diversity of the pool node operators?**

  * What percent of node operators are running a majority consensus layer (CL) client?
  * As of last edit, Prysm is the consensus layer client being run by a majority of node operators, which is dangerous for the network. If any CL client is currently being used by over 33% of the network, we request data related to its usage.
  * This is used to determine the products "diverse clients" score.

### Other criteria: the nice-to-haves

**What user interfaces are supported?**

  * i.e. Browser app, desktop app, mobile app, CLI

**For node tooling, does the software provide an easy way to switch between
clients?**

  * Can the user easily and safely change clients using the tool?

**For SaaS, how many validators are currently being operated by the service?**

  * This gives us an idea of the reach of your service so far.

## How we display results

The criteria for inclusion above are used to calculate a cumulative score for
each product or service. This is used as a means of sorting and showcasing
products that meet certain objective criteria. The more criteria that evidence
is provided for, the higher a product will be sorted, with ties being
randomized on load.

The code logic and weights for these criteria are currently contained in [this
JavaScript component(opens in a new
tab)](https://github.com/ethereum/ethereum-org-
website/blob/dev/src/components/Staking/StakingProductsCardGrid.js#L350) in
our repo.

## Add your product or service

If you want to add a staking product or service to ethereum.org, create an
issue on GitHub.

[Create an issue(opens in a new tab)](https://github.com/ethereum/ethereum-
org-
website/issues/new?assignees=&labels=feature+%3Asparkles%3A%2Ccontent+%3Afountain_pen%3A&template=suggest_staking_product.yaml)

### Was this article helpful?

YesNo

  * [Edit page(opens in a new tab)](https://github.com/ethereum/ethereum-org-website/tree/dev/public/content/contributing/adding-staking-products/index.md)
  * On this page

    * The decision framework
      * Criteria for inclusion
        * Software and smart contracts
        * Node or client tooling
        * Staking as a service
        * Staking pool
      * Other criteria: the nice-to-haves
    * How we display results
    * Add your product or service

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

