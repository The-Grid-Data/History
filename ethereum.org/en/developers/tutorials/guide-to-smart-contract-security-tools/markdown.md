Skip to main content

[](/en/)

  * Learn
  * Use
  * Build
  * Participate
  * Research

Search```K`

Languages EN

# A guide to smart contract security tools

soliditysmart contractssecurity

Intermediate

![✍️](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/270d.svg)Trailofbits

![📚](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4da.svg)[Building
secure contracts(opens in a new tab)](https://github.com/crytic/building-
secure-contracts/tree/master/program-analysis)

![📆](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4c6.svg)
September 7, 2020

![⏱️](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/23f1.svg)6
minute read minute read

On this page

  * Suggested workflow
  * Determining Security Properties
    * Components
    * Tool selection cheatsheet

We are going to use three distinctive testing and program analysis techniques:

  * **Static analysis with[Slither](/en/developers/tutorials/how-to-use-slither-to-find-smart-contract-bugs/).** All the paths of the program are approximated and analyzed at the same time, through different program presentations (e.g. control-flow-graph)
  * **Fuzzing with[Echidna](/en/developers/tutorials/how-to-use-echidna-to-test-smart-contracts/).** The code is executed with a pseudo-random generation of transactions. The fuzzer will try to find a sequence of transactions to violate a given property.
  * **Symbolic execution with[Manticore](/en/developers/tutorials/how-to-use-manticore-to-find-smart-contract-bugs/).** A formal verification technique, which translates each execution path to a mathematical formula, on which on top constraints can be checked.

Each technique has advantages and pitfalls, and will be useful in specific
cases:

Technique| Tool| Usage| Speed| Bugs missed| False Alarms  
---|---|---|---|---|---  
Static Analysis| Slither| CLI & scripts| seconds| moderate| low  
Fuzzing| Echidna| Solidity properties| minutes| low| none  
Symbolic Execution| Manticore| Solidity properties & scripts| hours| none*|
none  
  
* if all the paths are explored without timeout

**Slither** analyzes contracts within seconds, however, static analysis might
lead to false alarms and will be less suitable for complex checks (e.g.
arithmetic checks). Run Slither via the API for push-button access to built-in
detectors or via the API for user-defined checks.

**Echidna** needs to run for several minutes and will only produce true
positives. Echidna checks user-provided security properties, written in
Solidity. It might miss bugs since it is based on random exploration.

**Manticore** performs the "heaviest weight" analysis. Like Echidna, Manticore
verifies user-provided properties. It will need more time to run, but it can
prove the validity of a property and will not report false alarms.

## Suggested workflow

Start with Slither's built-in detectors to ensure that no simple bugs are
present now or will be introduced later. Use Slither to check properties
related to inheritance, variable dependencies, and structural issues. As the
codebase grows, use Echidna to test more complex properties of the state
machine. Revisit Slither to develop custom checks for protections unavailable
from Solidity, like protecting against a function being overridden. Finally,
use Manticore to perform targeted verification of critical security
properties, e.g., arithmetic operations.

  * Use Slither's CLI to catch common issues
  * Use Echidna to test high-level security properties of your contract
  * Use Slither to write custom static checks
  * Use Manticore once you want in-depth assurance of critical security properties

**A note on unit tests**. Unit tests are necessary to build high-quality
software. However, these techniques are not the best suited to find security
flaws. They are typically used to test positive behaviors of code (i.e. the
code works as expected in the normal context), while security flaws tend to
reside in edge cases that the developers did not consider. In our study of
dozens of smart contract security reviews, [unit test coverage had no effect
on the number or severity of security flaws(opens in a new
tab)](https://blog.trailofbits.com/2019/08/08/246-findings-from-our-smart-
contract-audits-an-executive-summary/) we found in our client's code.

## Determining Security Properties

To effectively test and verify your code, you must identify the areas that
need attention. As your resources spent on security are limited, scoping the
weak or high-value parts of your codebase is important to optimize your
effort. Threat modeling can help. Consider reviewing:

  * [Rapid Risk Assessments(opens in a new tab)](https://infosec.mozilla.org/guidelines/risk/rapid_risk_assessment.html) (our preferred approach when time is short)
  * [Guide to Data-Centric System Threat Modeling(opens in a new tab)](https://csrc.nist.gov/publications/detail/sp/800-154/draft) (aka NIST 800-154)
  * [Shostack threat modeling(opens in a new tab)](https://www.amazon.com/Threat-Modeling-Designing-Adam-Shostack/dp/1118809998)
  * [STRIDE(opens in a new tab)](https://wikipedia.org/wiki/STRIDE_\(security\)) / [DREAD(opens in a new tab)](https://wikipedia.org/wiki/DREAD_\(risk_assessment_model\))
  * [PASTA(opens in a new tab)](https://wikipedia.org/wiki/Threat_model#P.A.S.T.A.)
  * [Use of Assertions(opens in a new tab)](https://blog.regehr.org/archives/1091)

### Components

Knowing what you want to check will also help you to select the right tool.

The broad areas that are frequently relevant for smart contracts include:

  * **State machine.** Most contracts can be represented as a state machine. Consider checking that (1) No invalid state can be reached, (2) if a state is valid that it can be reached, and (3) no state traps the contract.

    * Echidna and Manticore are the tools to favor to test state-machine specifications.
  * **Access controls.** If your system has privileged users (e.g. an owner, controllers, ...) you must ensure that (1) each user can only perform the authorized actions and (2) no user can block actions from a more privileged user.

    * Slither, Echidna and Manticore can check for correct access controls. For example, Slither can check that only whitelisted functions lack the onlyOwner modifier. Echidna and Manticore are useful for more complex access control, such as a permission given only if the contract reaches a given state.
  * **Arithmetic operations.** Checking the soundness of the arithmetic operations is critical. Using `SafeMath` everywhere is a good step to prevent overflow/underflow, however, you must still consider other arithmetic flaws, including rounding issues and flaws that trap the contract.

    * Manticore is the best choice here. Echidna can be used if the arithmetic is out-of-scope of the SMT solver.
  * **Inheritance correctness.** Solidity contracts rely heavily on multiple inheritance. Mistakes such as a shadowing function missing a `super` call and misinterpreted c3 linearization order can easily be introduced.

    * Slither is the tool to ensure detection of these issues.
  * **External interactions.** Contracts interact with each other, and some external contracts should not be trusted. For example, if your contract relies on external oracles, will it remain secure if half the available oracles are compromised?

    * Manticore and Echidna are the best choice for testing external interactions with your contracts. Manticore has an built-in mechanism to stub external contracts.
  * **Standard conformance.** Ethereum standards (e.g. ERC20) have a history of flaws in their design. Be aware of the limitations of the standard you are building on.

    * Slither, Echidna, and Manticore will help you to detect deviations from a given standard.

### Tool selection cheatsheet

Component| Tools| Examples  
---|---|---  
State machine| Echidna, Manticore|  
Access control| Slither, Echidna, Manticore| [Slither exercise 2(opens in a
new tab)](https://github.com/crytic/building-secure-
contracts/blob/master/program-analysis/slither/exercise2.md), [Echidna
exercise 2(opens in a new tab)](https://github.com/crytic/building-secure-
contracts/blob/master/program-analysis/echidna/exercises/Exercise-2.md)  
Arithmetic operations| Manticore, Echidna| [Echidna exercise 1(opens in a new
tab)](https://github.com/crytic/building-secure-contracts/blob/master/program-
analysis/echidna/exercises/Exercise-1.md), [Manticore exercises 1 - 3(opens in
a new tab)](https://github.com/crytic/building-secure-
contracts/tree/master/program-analysis/manticore/exercises)  
Inheritance correctness| Slither| [Slither exercise 1(opens in a new
tab)](https://github.com/crytic/building-secure-contracts/blob/master/program-
analysis/slither/exercise1.md)  
External interactions| Manticore, Echidna|  
Standard conformance| Slither, Echidna, Manticore| [`slither-erc`(opens in a
new tab)](https://github.com/crytic/slither/wiki/ERC-Conformance)  
  
Other areas will need to be checked depending on your goals, but these coarse-
grained areas of focus are a good start for any smart contract system.

Our public audits contain examples of verified or tested properties. Consider
reading the `Automated Testing and Verification` sections of the following
reports to review real-world security properties:

  * [0x(opens in a new tab)](https://github.com/trailofbits/publications/blob/master/reviews/0x-protocol.pdf)
  * [Balancer(opens in a new tab)](https://github.com/trailofbits/publications/blob/master/reviews/BalancerCore.pdf)

l

Last edit: [@liuye20240304(opens in a new
tab)](https://github.com/liuye20240304), May 6, 2024

See contributors

### Was this tutorial helpful?

YesNo

  * [Edit page(opens in a new tab)](https://github.com/ethereum/ethereum-org-website/tree/dev/public/content/developers/tutorials/guide-to-smart-contract-security-tools/index.md)
  * On this page

    * Suggested workflow
    * Determining Security Properties
      * Components
      * Tool selection cheatsheet

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

