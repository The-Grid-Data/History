Skip to main content

[](/en/)

  * Learn
  * Use
  * Build
  * Participate
  * Research

Search```K`

Languages EN

# Token integration checklist

soliditysmart contractssecuritytokens

Intermediate

![✍️](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/270d.svg)Trailofbits

![📚](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4da.svg)[Building
secure contracts(opens in a new tab)](https://github.com/crytic/building-
secure-contracts/blob/master/development-guidelines/token_integration.md)

![📆](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4c6.svg)
August 13, 2020

![⏱️](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/23f1.svg)4
minute read minute read

On this page

  * General considerations
  * ERC conformity
  * Contract composition
  * Owner privileges
  * Token scarcity

Follow this checklist when interacting with arbitrary tokens. Make sure you
understand the risks associated with each item, and justify any exceptions to
these rules.

For convenience, all Slither [utilities(opens in a new
tab)](https://github.com/crytic/slither#tools) can be run directly on a token
address, such as:

[Using Slither tutorial](/en/developers/tutorials/how-to-use-slither-to-find-
smart-contract-bugs/)

    
    
    slither-check-erc 0xdac17f958d2ee523a2206206994597c13d831ec7 TetherToken

To follow this checklist, you'll want to have this output from Slither for the
token:

    
    
    - slither-check-erc [target] [contractName] [optional: --erc ERC_NUMBER]
    
    - slither [target] --print human-summary
    
    - slither [target] --print contract-summary
    
    - slither-prop . --contract ContractName # requires configuration, and use of Echidna and Manticore

## General considerations

  * **The contract has a security review.** Avoid interacting with contracts that lack a security review. Check the length of the assessment (aka “level of effort”), the reputation of the security firm, and the number and severity of the findings.
  * **You have contacted the developers.** You may need to alert their team to an incident. Look for appropriate contacts on [blockchain-security-contacts(opens in a new tab)](https://github.com/crytic/blockchain-security-contacts).
  * **They have a security mailing list for critical announcements.** Their team should advise users (like you!) when critical issues are found or when upgrades occur.

## ERC conformity

Slither includes a utility, [slither-check-erc(opens in a new
tab)](https://github.com/crytic/slither/wiki/ERC-Conformance), that reviews
the conformance of a token to many related ERC standards. Use slither-check-
erc to review that:

  * **Transfer and transferFrom return a boolean.** Several tokens do not return a boolean on these functions. As a result, their calls in the contract might fail.
  * **The name, decimals, and symbol functions are present if used.** These functions are optional in the ERC20 standard and might not be present.
  * **Decimals returns a uint8.** Several tokens incorrectly return a uint256. If this is the case, ensure the value returned is below 255.
  * **The token mitigates the known[ERC20 race condition(opens in a new tab)](https://github.com/ethereum/EIPs/issues/20#issuecomment-263524729).** The ERC20 standard has a known ERC20 race condition that must be mitigated to prevent attackers from stealing tokens.
  * **The token is not an ERC777 token and has no external function call in transfer and transferFrom.** External calls in the transfer functions can lead to reentrancies.

Slither includes a utility, [slither-prop(opens in a new
tab)](https://github.com/crytic/slither/wiki/Property-generation), that
generates unit tests and security properties that can discover many common ERC
flaws. Use slither-prop to review that:

  * **The contract passes all unit tests and security properties from slither-prop.** Run the generated unit tests, then check the properties with [Echidna(opens in a new tab)](https://github.com/crytic/echidna) and [Manticore(opens in a new tab)](https://manticore.readthedocs.io/en/latest/verifier.html).

Finally, there are certain characteristics that are difficult to identify
automatically. Review for these conditions by hand:

  * **Transfer and transferFrom should not take a fee.** Deflationary tokens can lead to unexpected behavior.
  * **Potential interest earned from the token is taken into account.** Some tokens distribute interest to token holders. This interest might be trapped in the contract if not taken into account.

## Contract composition

  * **The contract avoids unneeded complexity.** The token should be a simple contract; a token with complex code requires a higher standard of review. Use Slither’s [human-summary printer(opens in a new tab)](https://github.com/crytic/slither/wiki/Printer-documentation#human-summary) to identify complex code.
  * **The contract uses SafeMath.** Contracts that do not use SafeMath require a higher standard of review. Inspect the contract by hand for SafeMath usage.
  * **The contract has only a few non–token-related functions.** Non–token-related functions increase the likelihood of an issue in the contract. Use Slither’s [contract-summary printer(opens in a new tab)](https://github.com/crytic/slither/wiki/Printer-documentation#contract-summary) to broadly review the code used in the contract.
  * **The token only has one address.** Tokens with multiple entry points for balance updates can break internal bookkeeping based on the address (e.g. `balances[token_address][msg.sender]` might not reflect the actual balance).

## Owner privileges

  * **The token is not upgradeable.** Upgradeable contracts might change their rules over time. Use Slither’s [human-summary printer(opens in a new tab)](https://github.com/crytic/slither/wiki/Printer-documentation#contract-summary) to determine if the contract is upgradeable.
  * **The owner has limited minting capabilities.** Malicious or compromised owners can abuse minting capabilities. Use Slither’s [human-summary printer(opens in a new tab)](https://github.com/crytic/slither/wiki/Printer-documentation#contract-summary) to review minting capabilities, and consider manually reviewing the code.
  * **The token is not pausable.** Malicious or compromised owners can trap contracts relying on pausable tokens. Identify pauseable code by hand.
  * **The owner cannot blacklist the contract.** Malicious or compromised owners can trap contracts relying on tokens with a blacklist. Identify blacklisting features by hand.
  * **The team behind the token is known and can be held responsible for abuse.** Contracts with anonymous development teams, or that reside in legal shelters should require a higher standard of review.

## Token scarcity

Reviews for issues of token scarcity requires manual review. Check for these
conditions:

  * **No user owns most of the supply.** If a few users own most of the tokens, they can influence operations based on the token's repartition.
  * **The total supply is sufficient.** Tokens with a low total supply can be easily manipulated.
  * **The tokens are located in more than a few exchanges.** If all the tokens are in one exchange, a compromise of the exchange can compromise the contract relying on the token.
  * **Users understand the associated risks of large funds or flash loans.** Contracts relying on the token balance must carefully take in consideration attackers with large funds or attacks through flash loans.
  * **The token does not allow flash minting**. Flash minting can lead to substantial swings in the balance and the total supply, which neccessitate strict and comprehensive overflow checks in the operation of the token.

n

Last edit: [@nhsz(opens in a new tab)](https://github.com/nhsz), August 15,
2023

See contributors

### Was this tutorial helpful?

YesNo

  * [Edit page(opens in a new tab)](https://github.com/ethereum/ethereum-org-website/tree/dev/public/content/developers/tutorials/token-integration-checklist/index.md)
  * On this page

    * General considerations
    * ERC conformity
    * Contract composition
    * Owner privileges
    * Token scarcity

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

