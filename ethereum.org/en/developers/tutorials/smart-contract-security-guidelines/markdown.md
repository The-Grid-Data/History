Skip to main content

[](/en/)

  * Learn
  * Use
  * Build
  * Participate
  * Research

Search```K`

Languages EN

# Smart contract security guidelines

soliditysmart contractssecurity

Intermediate

![✍️](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/270d.svg)Trailofbits

![📚](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4da.svg)[Building
secure contracts(opens in a new tab)](https://github.com/crytic/building-
secure-contracts/blob/master/development-guidelines/guidelines.md)

![📆](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4c6.svg)
September 6, 2020

![⏱️](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/23f1.svg)4
minute read minute read

On this page

  * Design guidelines
    * Documentation and specifications
    * On-chain vs off-chain computation
    * Upgradeability
  * Implementation guidelines
    * Function composition
    * Inheritance
    * Events
    * Avoid known pitfalls
    * Dependencies
    * Testing and verification
    * Solidity
  * Deployment guidelines

Follow these high-level recommendations to build more secure smart contracts.

## Design guidelines

The design of the contract should be discussed ahead of time, prior to writing
any line of code.

### Documentation and specifications

Documentation can be written at different levels, and should be updated while
implementing the contracts:

  * **A plain English description of the system** , describing what the contracts do and any assumptions on the codebase.
  * **Schema and architectural diagrams** , including the contract interactions and the state machine of the system. [Slither printers(opens in a new tab)](https://github.com/crytic/slither/wiki/Printer-documentation) can help to generate these schemas.
  * **Thorough code documentation** , the [Natspec format(opens in a new tab)](https://solidity.readthedocs.io/en/develop/natspec-format.html) can be used for Solidity.

### On-chain vs off-chain computation

  * **Keep as much code as you can off-chain.** Keep the on-chain layer small. Pre-process data with code off-chain in such a way that verification on-chain is simple. Do you need an ordered list? Sort the list offchain, then only check its order onchain.

### Upgradeability

We discussed the different upgradeability solutions in [our blogpost(opens in
a new tab)](https://blog.trailofbits.com/2018/09/05/contract-upgrade-anti-
patterns/). Make a deliberate choice to support upgradeability or not prior to
writing any code. The decision will influence how you structure your code. In
general, we recommend:

  * **Favoring[contract migration(opens in a new tab)](https://blog.trailofbits.com/2018/10/29/how-contract-migration-works/) over upgradeability.** Migration systems have many of the same advantages as upgradeable ones, without their drawbacks.
  * **Using the data separation pattern over the delegatecallproxy one.** If your project has a clear abstraction separation, upgradeability using data separation will necessitate only a few adjustments. The delegatecallproxy requires EVM expertise and is highly error-prone.
  * **Document the migration/upgrade procedure before the deployment.** If you have to react under stress without any guidelines, you will make mistakes. Write the procedure to follow ahead of time. It should include:
    * The calls that initiate the new contracts
    * Where are stored the keys and how to access them
    * How to check the deployment! Develop and test a post-deployment script.

## Implementation guidelines

**Strive for simplicity.** Always use the simplest solution that fits your
purpose. Any member of your team should be able to understand your solution.

### Function composition

The architecture of your codebase should make your code easy to review. Avoid
architectural choices that decrease the ability to reason about its
correctness.

  * **Split the logic of your system** , either through multiple contracts or by grouping similar functions together (for example, authentication, arithmetic, ...).
  * **Write small functions, with a clear purpose.** This will facilitate easier review and allow the testing of individual components.

### Inheritance

  * **Keep the inheritance manageable.** Inheritance should be used to divide the logic, however, your project should aim to minimize the depth and width of the inheritance tree.
  * **Use Slither’s[inheritance printer(opens in a new tab)](https://github.com/crytic/slither/wiki/Printer-documentation#inheritance-graph) to check the contracts’ hierarchy.** The inheritance printer will help you review the size of the hierarchy.

### Events

  * **Log all crucial operations.** Events will help to debug the contract during the development, and monitor it after deployment.

### Avoid known pitfalls

  * **Be aware of the most common security issues.** There are many online resources to learn about common issues, such as [Ethernaut CTF(opens in a new tab)](https://ethernaut.openzeppelin.com/), [Capture the Ether(opens in a new tab)](https://capturetheether.com/), or [Not so smart contracts(opens in a new tab)](https://github.com/crytic/not-so-smart-contracts/).
  * **Be aware of the warnings sections in the[Solidity documentation(opens in a new tab)](https://solidity.readthedocs.io/en/latest/).** The warnings sections will inform you about non-obvious behavior of the language.

### Dependencies

  * **Use well-tested libraries.** Importing code from well-tested libraries will reduce the likelihood that you write buggy code. If you want to write an ERC20 contract, use [OpenZeppelin(opens in a new tab)](https://github.com/OpenZeppelin/openzeppelin-contracts/tree/master/contracts/token/ERC20).
  * **Use a dependency manager; avoid copy-pasting code.** If you rely on an external source, then you must keep it up-to-date with the original source.

### Testing and verification

  * **Write thorough unit-tests.** An extensive test suite is crucial to build high-quality software.
  * **Write[Slither(opens in a new tab)](https://github.com/crytic/slither), [Echidna(opens in a new tab)](https://github.com/crytic/echidna) and [Manticore(opens in a new tab)](https://github.com/trailofbits/manticore) custom checks and properties.** Automated tools will help ensure your contract is secure. Review the rest of this guide to learn how to write efficient checks and properties.
  * **Use[crytic.io(opens in a new tab)](https://crytic.io/).** Crytic integrates with GitHub, provides access to private Slither detectors, and runs custom property checks from Echidna.

### Solidity

  * **Favor Solidity 0.5 over 0.4 and 0.6.** In our opinion, Solidity 0.5 is more secure and has better built-in practices than 0.4. Solidity 0.6 has proven too unstable for production and needs time to mature.
  * **Use a stable release to compile; use the latest release to check for warnings.** Check that your code has no reported issues with the latest compiler version. However, Solidity has a fast release cycle and has a history of compiler bugs, so we do not recommend the latest version for deployment (see Slither’s [solc version recommendation(opens in a new tab)](https://github.com/crytic/slither/wiki/Detector-Documentation#recommendation-33)).
  * **Do not use inline assembly.** Assembly requires EVM expertise. Do not write EVM code if you have not _mastered_ the yellow paper.

## Deployment guidelines

Once the contract has been developed and deployed:

  * **Monitor your contracts.** Watch the logs, and be ready to react in case of contract or wallet compromise.
  * **Add your contact info to[blockchain-security-contacts(opens in a new tab)](https://github.com/crytic/blockchain-security-contacts).** This list helps third-parties contact you if a security flaw is discovered.
  * **Secure the wallets of privileged users.** Follow our [best practices(opens in a new tab)](https://blog.trailofbits.com/2018/11/27/10-rules-for-the-secure-use-of-cryptocurrency-hardware-wallets/) if you store keys in hardware wallets.
  * **Have a response to incident plan.** Consider that your smart contracts can be compromised. Even if your contracts are free of bugs, an attacker may take control of the contract owner's keys.

p

Last edit: [@pettinarip(opens in a new tab)](https://github.com/pettinarip),
December 8, 2023

See contributors

### Was this tutorial helpful?

YesNo

  * [Edit page(opens in a new tab)](https://github.com/ethereum/ethereum-org-website/tree/dev/public/content/developers/tutorials/smart-contract-security-guidelines/index.md)
  * On this page

    * Design guidelines
      * Documentation and specifications
      * On-chain vs off-chain computation
      * Upgradeability
    * Implementation guidelines
      * Function composition
      * Inheritance
      * Events
      * Avoid known pitfalls
      * Dependencies
      * Testing and verification
      * Solidity
    * Deployment guidelines

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

