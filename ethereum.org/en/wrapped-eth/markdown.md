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
  2. [wrapped-eth](/en/wrapped-eth/)

Page last updated: April 2, 2024

On this page

  * Why do we need to wrap ETH as an ERC-20?
  * Wrapped ether (WETH) vs ether (ETH): What is the difference?
  * Frequently asked questions
  * Further reading

# Wrapped ether (WETH)

Ether (ETH) is the main currency of Ethereum. It's used for several purposes
like staking, as a currency, and paying for gas fees for computation. **WETH
is effectively an upgraded form of ETH with some additional functionality
required by many applications and _ERC-20 tokens_** , which are other types of
digital assets on Ethereum. To work with these tokens, ETH must follow the
same rules they do, known as the ERC-20 standard.

To bridge this gap, wrapped ETH (WETH) was created. **Wrapped ETH is a smart
contract that lets you deposit any amount of ETH into the contract and receive
the same amount in minted WETH** that conforms to the ERC-20 token standard.
WETH is a representation of ETH that allows you to interact with it as an
ERC-20 token, not as the native asset ETH. You will still need native ETH to
pay for gas fees, so make sure you save some when depositing.

You are able to unwrap WETH for ETH by using the WETH smart contract. You can
redeem any amount of WETH with the WETH smart contract, and you will receive
the same amount in ETH. The WETH deposited is then burned and taken out of the
circulating supply of WETH.

**Roughly ~3% of the circulating ETH supply is locked in the WETH token
contract** making it one of the most used _smart contracts_. WETH is
especially important with users interacting with applications in decentralized
finance (DeFi).

## Why do we need to wrap ETH as an ERC-20?

[ERC-20](/en/developers/docs/standards/tokens/erc-20/) defines a standard
interface for transferable tokens, so anyone can create tokens that interact
seamlessly with applications and tokens that use this standard in Ethereum's
ecosystem. Since **ETH predates the ERC-20 standard** , ETH doesn't conform to
this specification. This means **you can't easily** exchange ETH for other
ERC-20 tokens or **use ETH in apps using the ERC-20 standard**. Wrapping ETH
gives you the opportunity to do the following:

  * **Exchange ETH for ERC-20 tokens** : You cannot exchange ETH directly for other ERC-20 tokens. WETH is a representation of ether that complies with the ERC-20 fungible token standard and can be exchanged with other ERC-20 tokens. 

  * **Use ETH in dapps** : Because ETH isn’t ERC20-compatible, developers would need to create separate interfaces (one for ETH and another for ERC-20 tokens) in dapps. Wrapping ETH removes this obstacle and enables developers to handle ETH and other tokens within the same dapp. Many decentralized finance applications use this standard, and create markets for exchanging these tokens.

## Wrapped ether (WETH) vs ether (ETH): What is the difference?

| **Ether (ETH)**| **Wrapped Ether (WETH)**  
---|---|---  
Supply| The supply of ETH is managed by the Ethereum protocol. The
[issuance](/en/roadmap/merge/issuance/) of ETH is handled by Ethereum
validators when processing transactions and creating blocks.| WETH is an
ERC-20 token whose supply is managed by a smart contract. New units of WETH
are issued by the contract after it receives ETH deposits from users, or units
of WETH are burned when a user wishes to redeem WETH for ETH.  
Ownership| Ownership is managed by the Ethereum protocol through your account
balance.| Ownership of WETH is managed by the WETH token smart contract,
secured by the Ethereum protocol.  
Gas| Ether (ETH) is the accepted unit of payment for computation on the
Ethereum network. Gas fees are denominated in gwei (a unit of ether).| Paying
gas with WETH tokens is not natively supported.  
  
## Frequently asked questions

###

Do you pay to wrap/unwrap ETH?

More

You pay gas fees to wrap or unwrap ETH using the WETH contract.

###

Is WETH safe?

More

WETH is generally considered secure because it is based on a simple, battle-
tested smart contract. The WETH contract has also been formally verified,
which is the highest security standard for smart contracts on Ethereum.

###

Why am I seeing different WETH tokens?

More

Besides the [canonical implementation of WETH(opens in a new
tab)](https://etherscan.io/token/0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2)
described on this page, there are other variants in the wild. These may be
custom tokens created by app developers or versions issued on other
blockchains, and may behave differently or have different security properties.
**Always double-check the token information to know which WETH implementation
you're interacting with.**

###

What are the WETH contracts on other networks?

More

  * [Ethereum Mainnet(opens in a new tab)](https://etherscan.io/token/0xC02aaA39b223FE8D0A0e5C4F27eAD9083C756Cc2)
  * [Arbitrum(opens in a new tab)](https://arbiscan.io/token/0x82af49447d8a07e3bd95bd0d56f35241523fbab1)
  * [Optimism(opens in a new tab)](https://optimistic.etherscan.io/token/0x4200000000000000000000000000000000000006)

## Further reading

  * [WTF is WETH?(opens in a new tab)](https://weth.tkn.eth.limo/)
  * [WETH token information on Etherscan(opens in a new tab)](https://etherscan.io/token/0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2)
  * [Formal Verification of WETH(opens in a new tab)](https://zellic.io/blog/formal-verification-weth)

### Was this article helpful?

YesNo

  * [Edit page(opens in a new tab)](https://github.com/ethereum/ethereum-org-website/tree/dev/public/content/wrapped-eth/index.md)
  * On this page

    * Why do we need to wrap ETH as an ERC-20?
    * Wrapped ether (WETH) vs ether (ETH): What is the difference?
    * Frequently asked questions
    * Further reading

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

### ERC-20

Is the standard set of rules that most tokens on Ethereum network are created
with.

### Smart contract

A smart contract is a program that automatically executes agreements on a
blockchain, like a self-enforcing digital contract. [Introduction to smart
contracts](/en/smart-contracts/).

