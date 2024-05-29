Skip to main content

[](/en/)

  * Learn
  * Use
  * Build
  * Participate
  * Research

Search```K`

Languages EN

# How to use Slither to find smart contract bugs

soliditysmart contractssecuritytestingstatic analysis

Advanced

![✍️](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/270d.svg)Trailofbits

![📚](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4da.svg)[Building
secure contracts(opens in a new tab)](https://github.com/crytic/building-
secure-contracts/tree/master/program-analysis/slither)

![📆](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4c6.svg)
June 9, 2020

![⏱️](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/23f1.svg)7
minute read minute read

On this page

  * How to use Slither
  * Installation
    * Running a script
    * Command line
  * Static analysis
    * Code representation
    * Abstract Syntax Trees (AST)
    * Control Flow Graph (CFG)
    * Analysis
    * Syntax analysis
    * Semantic analysis
    * Intermediate representation
  * API Basics
    * Exploring contracts and functions

## How to use Slither

The aim of this tutorial is to show how to use Slither to automatically find
bugs in smart contracts.

  * Installation
  * Command line usage
  * Introduction to static analysis: Brief introduction to static analysis
  * API: Python API description

## Installation

Slither requires Python >= 3.6. It can be installed through pip or using
docker.

Slither through pip:

    
    
    pip3 install --user slither-analyzer

Slither through docker:

    
    
    docker pull trailofbits/eth-security-toolbox
    
    docker run -it -v "$PWD":/home/trufflecon trailofbits/eth-security-toolbox

 _The last command runs eth-security-toolbox in a docker that has access to
your current directory. You can change the files from your host, and run the
tools on the files from the docker_

Inside docker, run:

    
    
    solc-select 0.5.11
    
    cd /home/trufflecon/

### Running a script

To run a python script with python 3:

    
    
    python3 script.py

### Command line

**Command line versus user-defined scripts.** Slither comes with a set of
predefined detectors that find many common bugs. Calling Slither from the
command line will run all the detectors, no detailed knowledge of static
analysis needed:

    
    
    slither project_paths

In addition to detectors, Slither has code review capabilities through its
[printers(opens in a new tab)](https://github.com/crytic/slither#printers) and
[tools(opens in a new tab)](https://github.com/crytic/slither#tools).

Use [crytic.io(opens in a new tab)](https://github.com/crytic) to get access
to private detectors and GitHub integration.

## Static analysis

The capabilities and design of the Slither static analysis framework has been
described in blog posts ([1(opens in a new
tab)](https://blog.trailofbits.com/2018/10/19/slither-a-solidity-static-
analysis-framework/), [2(opens in a new
tab)](https://blog.trailofbits.com/2019/05/27/slither-the-leading-static-
analyzer-for-smart-contracts/)) and an [academic paper(opens in a new
tab)](https://github.com/trailofbits/publications/blob/master/papers/wetseb19.pdf).

Static analysis exists in different flavors. You most likely realize that
compilers like [clang(opens in a new tab)](https://clang-analyzer.llvm.org/)
and [gcc(opens in a new tab)](https://lwn.net/Articles/806099/) depend on
these research techniques, but it also underpins ([Infer(opens in a new
tab)](https://fbinfer.com/), [CodeClimate(opens in a new
tab)](https://codeclimate.com/), [FindBugs(opens in a new
tab)](http://findbugs.sourceforge.net/) and tools based on formal methods like
[Frama-C(opens in a new tab)](https://frama-c.com/) and [Polyspace(opens in a
new tab)](https://www.mathworks.com/products/polyspace.html).

We won't be exhaustively reviewing static analysis techniques and researcher
here. Instead, we'll focus on what is needed to understand how Slither works
so you can more effectively use it to find bugs and understand code.

  * Code representation
  * Code analysis
  * Intermediate representation

### Code representation

In contrast to a dynamic analysis, which reasons about a single execution
path, static analysis reasons about all the paths at once. To do so, it relies
on a different code representation. The two most common ones are the abstract
syntax tree (AST) and the control flow graph (CFG).

### Abstract Syntax Trees (AST)

AST are used every time the compiler parses code. It is probably the most
basic structure upon which static analysis can be performed.

In a nutshell, an AST is a structured tree where, usually, each leaf contains
a variable or a constant and internal nodes are operands or control flow
operations. Consider the following code:

    
    
    1function safeAdd(uint a, uint b) pure internal returns(uint){
    
    2    if(a + b <= a){
    
    3        revert();
    
    4    }
    
    5    return a + b;
    
    6}
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

The corresponding AST is shown in:

[![AST](/_next/image/?url=%2Fcontent%2Fdevelopers%2Ftutorials%2Fhow-to-use-
slither-to-find-smart-contract-
bugs%2Fast.png&w=1080&q=75)](/content/developers/tutorials/how-to-use-slither-
to-find-smart-contract-bugs/ast.png)

Slither uses the AST exported by solc.

While simple to build, the AST is a nested structure. At times, this is not
the most straightforward to analyze. For example, to identify the operations
used by the expression `a + b <= a`, you must first analyze `<=` and then `+`.
A common approach is to use the so-called visitor pattern, which navigates
through the tree recursively. Slither contains a generic visitor in
[`ExpressionVisitor`(opens in a new
tab)](https://github.com/crytic/slither/blob/master/slither/visitors/expression/expression.py).

The following code uses `ExpressionVisitor` to detect if the expression
contains an addition:

    
    
    1from slither.visitors.expression.expression import ExpressionVisitor
    
    2from slither.core.expressions.binary_operation import BinaryOperationType
    
    3
    
    4class HasAddition(ExpressionVisitor):
    
    5
    
    6    def result(self):
    
    7        return self._result
    
    8
    
    9    def _post_binary_operation(self, expression):
    
    10        if expression.type == BinaryOperationType.ADDITION:
    
    11            self._result = True
    
    12
    
    13visitor = HasAddition(expression) # expression is the expression to be tested
    
    14print(f'The expression {expression} has a addition: {visitor.result()}')
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

### Control Flow Graph (CFG)

The second most common code representation is the control flow graph (CFG). As
its name suggests, it is a graph-based representation which exposes all the
execution paths. Each node contains one or multiple instructions. Edges in the
graph represent the control flow operations (if/then/else, loop, etc). The CFG
of our previous example is:

[![CFG](/_next/image/?url=%2Fcontent%2Fdevelopers%2Ftutorials%2Fhow-to-use-
slither-to-find-smart-contract-
bugs%2Fcfg.png&w=640&q=75)](/content/developers/tutorials/how-to-use-slither-
to-find-smart-contract-bugs/cfg.png)

The CFG is the representation on top of which most of the analyses are built.

Many other code representations exist. Each representation has advantages and
drawbacks according to the analysis you want to perform.

### Analysis

The simplest type of analyses you can perform with Slither are syntactic
analyses.

### Syntax analysis

Slither can navigate through the different components of the code and their
representation to find inconsistencies and flaws using a pattern matching-like
approach.

For example the following detectors look for syntax-related issues:

  * [State variable shadowing(opens in a new tab)](https://github.com/crytic/slither/wiki/Detector-Documentation#state-variable-shadowing): iterates over all the state variables and check if any shadow a variable from an inherited contract ([state.py#L51-L62(opens in a new tab)](https://github.com/crytic/slither/blob/0441338e055ab7151b30ca69258561a5a793f8ba/slither/detectors/shadowing/state.py#L51-L62))

  * [Incorrect ERC20 interface(opens in a new tab)](https://github.com/crytic/slither/wiki/Detector-Documentation#incorrect-erc20-interface): look for incorrect ERC20 function signatures ([incorrect_erc20_interface.py#L34-L55(opens in a new tab)](https://github.com/crytic/slither/blob/0441338e055ab7151b30ca69258561a5a793f8ba/slither/detectors/erc/incorrect_erc20_interface.py#L34-L55))

### Semantic analysis

In contrast to syntax analysis, a semantic analysis will go deeper and analyze
the “meaning” of the code. This family includes some broad types of analyses.
They lead to more powerful and useful results, but are also more complex to
write.

Semantic analyses are used for the most advanced vulnerability detections.

#### Data dependency analysis

A variable `variable_a` is said to be data-dependent of `variable_b` if there
is a path for which the value of `variable_a` is influenced by `variable_b`.

In the following code, `variable_a` is dependent of `variable_b`:

    
    
    1// ...
    
    2variable_a = variable_b + 1;
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Slither comes with built-in [data dependency(opens in a new
tab)](https://github.com/crytic/slither/wiki/data-dependency) capabilities,
thanks to its intermediate representation (discussed in a later section).

An example of data dependency usage can be found in the [dangerous strict
equality detector(opens in a new
tab)](https://github.com/crytic/slither/wiki/Detector-Documentation#dangerous-
strict-equalities). Here Slither will look for strict equality comparison to a
dangerous value ([incorrect_strict_equality.py#L86-L87(opens in a new
tab)](https://github.com/crytic/slither/blob/6d86220a53603476f9567c3358524ea4db07fb25/slither/detectors/statements/incorrect_strict_equality.py#L86-L87)),
and will inform the user that it should use `>=` or `<=` rather than `==`, to
prevent an attacker to trap the contract. Among other, the detector will
consider as dangerous the return value of a call to `balanceOf(address)`
([incorrect_strict_equality.py#L63-L64(opens in a new
tab)](https://github.com/crytic/slither/blob/6d86220a53603476f9567c3358524ea4db07fb25/slither/detectors/statements/incorrect_strict_equality.py#L63-L64)),
and will use the data dependency engine to track its usage.

#### Fixed-point computation

If your analysis navigates through the CFG and follows the edges, you are
likely to see already visited nodes. For example, if a loop is presented as
shown below:

    
    
    1for(uint i; i < range; ++){
    
    2    variable_a += 1
    
    3}
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Your analysis will need to know when to stop. There are two main strategies
here: (1) iterate on each node a finite number of times, (2) compute a so-
called _fixpoint_. A fixpoint basically means that analyzing this node does
not provide any meaningful information.

An example of fixpoint used can be found in the reentrancy detectors: Slither
explores the nodes, and look for externals calls, write and read to storage.
Once it has reached a fixpoint ([reentrancy.py#L125-L131(opens in a new
tab)](https://github.com/crytic/slither/blob/master/slither/detectors/reentrancy/reentrancy.py#L125-L131)),
it stops the exploration, and analyze the results to see if a reentrancy is
present, through different reentrancy patterns ([reentrancy_benign.py(opens in
a new
tab)](https://github.com/crytic/slither/blob/b275bcc824b1b932310cf03b6bfb1a1fef0ebae1/slither/detectors/reentrancy/reentrancy_benign.py),
[reentrancy_read_before_write.py(opens in a new
tab)](https://github.com/crytic/slither/blob/b275bcc824b1b932310cf03b6bfb1a1fef0ebae1/slither/detectors/reentrancy/reentrancy_read_before_write.py),
[reentrancy_eth.py(opens in a new
tab)](https://github.com/crytic/slither/blob/b275bcc824b1b932310cf03b6bfb1a1fef0ebae1/slither/detectors/reentrancy/reentrancy_eth.py)).

Writing analyses using efficient fixed point computation requires a good
understanding of how the analysis propagates its information.

### Intermediate representation

An intermediate representation (IR) is a language meant to be more amenable to
static analysis than the original one. Slither translates Solidity to its own
IR: [SlithIR(opens in a new
tab)](https://github.com/crytic/slither/wiki/SlithIR).

Understanding SlithIR is not necessary if you only want to write basic checks.
However, it will come in handy if you plan to write advanced semantic
analyses. The [SlithIR(opens in a new
tab)](https://github.com/crytic/slither/wiki/Printer-documentation#slithir)
and [SSA(opens in a new tab)](https://github.com/crytic/slither/wiki/Printer-
documentation#slithir-ssa) printers will help you to understand how the code
is translated.

## API Basics

Slither has an API that lets you explore basic attributes of the contract and
its functions.

To load a codebase:

    
    
    1from slither import Slither
    
    2slither = Slither('/path/to/project')
    
    3
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

### Exploring contracts and functions

A `Slither` object has:

  * `contracts (list(Contract)`: list of contracts
  * `contracts_derived (list(Contract)`: list of contracts that are not inherited by another contract (subset of contracts)
  * `get_contract_from_name (str)`: Return a contract from its name

A `Contract` object has:

  * `name (str)`: Name of the contract
  * `functions (list(Function))`: List of functions
  * `modifiers (list(Modifier))`: List of functions
  * `all_functions_called (list(Function/Modifier))`: List of all the internal functions reachable by the contract
  * `inheritance (list(Contract))`: List of inherited contracts
  * `get_function_from_signature (str)`: Return a Function from its signature
  * `get_modifier_from_signature (str)`: Return a Modifier from its signature
  * `get_state_variable_from_name (str)`: Return a StateVariable from its name

A `Function` or a `Modifier` object has:

  * `name (str)`: Name of the function
  * `contract (contract)`: the contract where the function is declared
  * `nodes (list(Node))`: List of the nodes composing the CFG of the function/modifier
  * `entry_point (Node)`: Entry point of the CFG
  * `variables_read (list(Variable))`: List of variables read
  * `variables_written (list(Variable))`: List of variables written
  * `state_variables_read (list(StateVariable))`: List of state variables read (subset of variables`read)
  * `state_variables_written (list(StateVariable))`: List of state variables written (subset of variables`written)

n

Last edit: [@nhsz(opens in a new tab)](https://github.com/nhsz), August 15,
2023

See contributors

### Was this tutorial helpful?

YesNo

  * [Edit page(opens in a new tab)](https://github.com/ethereum/ethereum-org-website/tree/dev/public/content/developers/tutorials/how-to-use-slither-to-find-smart-contract-bugs/index.md)
  * On this page

    * How to use Slither
    * Installation
      * Running a script
      * Command line
    * Static analysis
      * Code representation
      * Abstract Syntax Trees (AST)
      * Control Flow Graph (CFG)
      * Analysis
      * Syntax analysis
      * Semantic analysis
      * Intermediate representation
    * API Basics
      * Exploring contracts and functions

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

