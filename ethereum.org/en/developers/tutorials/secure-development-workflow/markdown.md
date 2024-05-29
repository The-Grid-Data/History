Skip to main content

[](/en/)

  * Learn
  * Use
  * Build
  * Participate
  * Research

Search```K`

Languages EN

# Smart contract security checklist

smart contractssecuritysolidity

Intermediate

![✍️](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/270d.svg)Trailofbits

![📚](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4da.svg)[Building
secure contracts(opens in a new tab)](https://github.com/crytic/building-
secure-contracts/blob/master/development-guidelines/workflow.md)

![📆](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4c6.svg)
September 7, 2020

![⏱️](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/23f1.svg)2
minute read minute read

On this page

  * Smart contract development checklist
  * Ask for help

## Smart contract development checklist

Here's a high-level process we recommend following while you write your smart
contracts.

Check for known security issues:

  * Review your contracts with [Slither(opens in a new tab)](https://github.com/crytic/slither). It has more than 40 built-in detectors for common vulnerabilities. Run it on every check-in with new code and ensure it gets a clean report (or use triage mode to silence certain issues).
  * Review your contracts with [Crytic(opens in a new tab)](https://crytic.io/). It checks for 50 issues that Slither does not. Crytic can help your team stay on top of each other too, by easily surfacing security issues in Pull Requests on GitHub.

Consider special features of your contract:

  * Are your contracts upgradeable? Review your upgradeability code for flaws with [`slither-check-upgradeability`(opens in a new tab)](https://github.com/crytic/slither/wiki/Upgradeability-Checks) or [Crytic(opens in a new tab)](https://blog.trailofbits.com/2020/06/12/upgradeable-contracts-made-safer-with-crytic/). We've documented 17 ways upgrades can go sideways.
  * Do your contracts purport to conform to ERCs? Check them with [`slither-check-erc`(opens in a new tab)](https://github.com/crytic/slither/wiki/ERC-Conformance). This tool instantly identifies deviations from six common specs.
  * Do you have unit tests in Truffle? Enrich them with [`slither-prop`(opens in a new tab)](https://github.com/crytic/slither/wiki/Property-generation). It automatically generates a robust suite of security properties for features of ERC20 based on your specific code.
  * Do you integrate with 3rd party tokens? Review our [token integration checklist](/en/developers/tutorials/token-integration-checklist/) before relying on external contracts.

Visually inspect critical security features of your code:

  * Review Slither's [inheritance-graph(opens in a new tab)](https://github.com/trailofbits/slither/wiki/Printer-documentation#inheritance-graph) printer. Avoid inadvertent shadowing and C3 linearization issues.
  * Review Slither's [function-summary(opens in a new tab)](https://github.com/trailofbits/slither/wiki/Printer-documentation#function-summary) printer. It reports function visibility and access controls.
  * Review Slither's [vars-and-auth(opens in a new tab)](https://github.com/trailofbits/slither/wiki/Printer-documentation#variables-written-and-authorization) printer. It reports access controls on state variables.

Document critical security properties and use automated test generators to
evaluate them:

  * Learn to [document security properties for your code](/en/developers/tutorials/guide-to-smart-contract-security-tools/). It's tough as first, but it's the single most important activity for achieving a good outcome. It's also a prerequisite for using any of the advanced techniques in this tutorial.
  * Define security properties in Solidity, for use with [Echidna(opens in a new tab)](https://github.com/crytic/echidna) and [Manticore(opens in a new tab)](https://manticore.readthedocs.io/en/latest/verifier.html). Focus on your state machine, access controls, arithmetic operations, external interactions, and standards conformance.
  * Define security properties with [Slither's Python API](/en/developers/tutorials/how-to-use-slither-to-find-smart-contract-bugs/). Focus on inheritance, variable dependencies, access controls, and other structural issues.
  * Run your property tests on every commit with [Crytic(opens in a new tab)](https://crytic.io). Crytic can consume and evaluate security property tests so everyone on your team can easily see that they pass on GitHub. Failing tests can block commits.

Finally, be mindful of issues that automated tools cannot easily find:

  * Lack of privacy: everyone else can see your transactions while they're queued in the pool
  * Front running transactions
  * Cryptographic operations
  * Risky interactions with external DeFi components

## Ask for help

[Ethereum office hours(opens in a new tab)](https://calendly.com/dan-
trailofbits/ethereum-office-hours) run every Tuesday afternoon. These 1-hour,
1-on-1 sessions are an opportunity to ask us any questions you have about
security, troubleshoot using our tools, and get feedback from experts about
your current approach. We will help you work through this guide.

Join our Slack: [Empire Hacking(opens in a new
tab)](https://join.slack.com/t/empirehacking/shared_invite/zt-h97bbrj8-1jwuiU33nnzg67JcvIciUw).
We're always available in the #crytic and #ethereum channels if you have any
questions.

n

Last edit: [@nhsz(opens in a new tab)](https://github.com/nhsz), August 15,
2023

See contributors

### Was this tutorial helpful?

YesNo

  * [Edit page(opens in a new tab)](https://github.com/ethereum/ethereum-org-website/tree/dev/public/content/developers/tutorials/secure-development-workflow/index.md)
  * On this page

    * Smart contract development checklist
    * Ask for help

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

