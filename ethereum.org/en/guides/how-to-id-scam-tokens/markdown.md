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
  2. [Guides](/en/guides/)/
  3. [how-to-id-scam-tokens](/en/guides/how-to-id-scam-tokens/)

Page last updated: August 15, 2023

On this page

  * How do scam tokens work?
  * Appearing legitimate
  * Scammy websites
  * How can you protect yourself?
  * Conclusion

# How to identify scam tokens

One of the most common uses for Ethereum is for a group to create a tradable
token, in a sense their own currency. These tokens typically follow a
standard, [ERC-20](/en/developers/docs/standards/tokens/erc-20/). However,
anywhere there are legitimate use cases that bring value, there are also
criminals who try to steal that value for themselves.

There are two ways in which they are likely to deceive you:

  * **Selling you a scam token** , which may look like the legitimate token you want to purchase, but are issued by the scammers and worth nothing.
  * **Tricking you into signing bad transactions** , usually by directing you into their own user interface. They might try to get you into giving their contracts an allowance on your ERC-20 tokens, exposing sensitive information that gives them access to your assets, etc. These user interfaces might be near-perfect clones of honest sites, but with hidden tricks.

To illustrate what scam tokens are, and how to identify them, we are going to
look at an example of one: [`wARB`(opens in a new
tab)](https://etherscan.io/token/0xb047c8032b99841713b8e3872f06cf32beb27b82).
This token attempts to look like the legitimate [`ARB`(opens in a new
tab)](https://etherscan.io/address/0xb50721bcf8d664c30412cfbc6cf7a15145234ad1)
token.

###

What is ARB?

More

Arbitrum is an organization that develops and manages [optimistic
rollups](/en/developers/docs/scaling/optimistic-rollups/). Initially, Arbitrum
was organized as a for-profit company, but then took steps to decentralize. As
part of that process, they issued a tradeable [governance
token](/en/dao/#token-based-membership).

###

Why is the scam token called wARB?

More

There is a convention in Ethereum that when an asset is not ERC-20 compliant
we create a "wrapped" version of it with the name starting with "w". So, for
example, we have wBTC for bitcoin and [wETH for ether(opens in a new
tab)](https://cointelegraph.com/news/what-is-wrapped-ethereum-weth-and-how-
does-it-work).

It does not make sense to create a wrapped version of an ERC-20 token that is
already on Ethereum, but scammers rely on the appearance of legitimacy rather
than the underlying reality.

## How do scam tokens work?

The whole point of Ethereum is decentralization. This means that there is no
central authority that can confiscate your assets or prevent you from
deploying a smart contract. But it also means that scammers can deploy any
smart contract they wish.

###

What are smart contracts?

More

[Smart contracts](/en/developers/docs/smart-contracts/) are the programs that
run on top of the Ethereum blockchain. Every ERC-20 token, for example, is
implemented as a smart contract.

Specifically, Arbitrum deployed a contract that uses the symbol `ARB`. But
that doesn't stop other people from also deploying a contract that uses the
exact same symbol, or a similar one. Whoever writes the contract gets to set
what the contract will do.

## Appearing legitimate

There are several tricks that scam token creators do to appear legitimate.

  * **Legitimate name and symbol**. As mentioned before, ERC-20 contracts can have the same symbol and name as other ERC-20 contracts. You cannot count on those fields for security.

  * **Legitimate owners**. Scam tokens often airdrop significant balances to addresses that can be expected to be legitimate holders of the real token.

For example, let's look at `wARB` again. [About 16% of the tokens(opens in a
new
tab)](https://etherscan.io/token/0xb047c8032b99841713b8e3872f06cf32beb27b82?a=0x1c8db745abe3c8162119b9ef2c13864cd1fdd72f)
are held by an address whose public tag is [Arbitrum Foundation:
Deployer(opens in a new
tab)](https://etherscan.io/address/0x1c8db745abe3c8162119b9ef2c13864cd1fdd72f).
This is _not_ a fake address, it really is the address that [deployed the real
ARB contract on Ethereum mainnet(opens in a new
tab)](https://etherscan.io/tx/0x242b50ab4fe9896cb0439cfe6e2321d23feede7eeceb31aa2dbb46fc06ed2670).

Because the ERC-20 balance of an address is part of the ERC-20 contract's
storage, it can be specified by the contract to be whatever the contract
developer wishes. It is also possible for a contract to forbid transfers so
the legitimate users won't be able to get rid of those scam tokens.

  * **Legitimate transfers**. _Legitimate owners wouldn't pay to transfer a scam token to others, so if there are transfers it must be legitimate, right?_ **Wrong**. `Transfer` events are produced by the ERC-20 contract. A scammer can easily write the contract in such a way it will produce those actions.

## Scammy websites

Scammers can also produce very convincing websites, sometimes even precise
clones of authentic sites with identical UIs, but with subtle tricks. Examples
might be external links that seem legitimate actually sending the user to an
external scam site, or incorrect instructions that guide the user to exposing
their keys or sending funds to an attacker's address.

The best practice for avoiding this is to carefully check the URL for the
sites you visit, and save addresses for known authentic sites in your
bookmarks. Then, you can access the real site through your bookmarks without
accidentally making spelling errors or relying on external links.

## How can you protect yourself?

  1. **Check the contract address**. Legitimate tokens come from legitimate organizations, and you can see the contract addresses on the organization's website. For example, [for `ARB` you can see the legitimate addresses here(opens in a new tab)](https://docs.arbitrum.foundation/deployment-addresses#token).

  2. **Real tokens have liquidity**. Another option is to look at liquidity pool size on [Uniswap(opens in a new tab)](https://uniswap.org/), one of the most common token swapping protocols. This protocol works using liquidity pools, into which investors deposit their tokens in hope of a return from trading fees.

Scam tokens typically have tiny liquidity pools, if any, because the scammers
don't want to risk real assets. For example, the `ARB`/`ETH` Uniswap pool
holds about a million dollars ([see here for the up to date value(opens in a
new
tab)](https://info.uniswap.org/#/pools/0x755e5a186f0469583bd2e80d1216e02ab88ec6ca))
and buying or selling a small amount is not going to change the price:

[![Buying a legitimate token](/_next/image/?url=%2Fcontent%2Fguides%2Fhow-to-
id-scam-tokens%2Funiswap-real.png&w=828&q=75)](/content/guides/how-to-id-scam-
tokens/uniswap-real.png)

But when you try to buy the scam token `wARB`, even a tiny purchase would
change the price by over 90%:

[![Buying a scam token](/_next/image/?url=%2Fcontent%2Fguides%2Fhow-to-id-
scam-tokens%2Funiswap-scam.png&w=828&q=75)](/content/guides/how-to-id-scam-
tokens/uniswap-scam.png)

This is another piece of evidence that shows us `wARB` is not likely to be a
legitimate token.

  3. **Look in Etherscan**. A lot of scam tokens have already been identified and reported by the community. Such tokens are [marked in Etherscan(opens in a new tab)](https://info.etherscan.com/etherscan-token-reputation/). While Etherscan is not an authoritative source of truth (it is the nature of decentralized networks that there can't be an authoritative source for legitimacy), tokens that are identified by Etherscan as scams are likely to be scams.

[![Scam token in Etherscan](/_next/image/?url=%2Fcontent%2Fguides%2Fhow-to-id-
scam-tokens%2Fetherscan-scam.png&w=1920&q=75)](/content/guides/how-to-id-scam-
tokens/etherscan-scam.png)

## Conclusion

As long as there is value in the world, there are going to be scammers who
attempt to steal it for themselves, and in a decentralized world there is
nobody to protect you except for yourself. Hopefully, you remember these
points to help tell the legitimate tokens from the scams:

  * Scam tokens impersonate legitimate tokens, they can use the same name, symbol, etc.
  * Scam tokens _cannot_ use the same contract address.
  * The best source for the address of the legitimate token is the organization whose token it is.
  * Failing that, you can use popular, trusted applications such as [Uniswap(opens in a new tab)](https://app.uniswap.org/#/swap) and [Etherscan(opens in a new tab)](https://etherscan.io/).

### Was this article helpful?

YesNo

  * [Edit page(opens in a new tab)](https://github.com/ethereum/ethereum-org-website/tree/dev/public/content/guides/how-to-id-scam-tokens/index.md)
  * On this page

    * How do scam tokens work?
    * Appearing legitimate
    * Scammy websites
    * How can you protect yourself?
    * Conclusion

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

