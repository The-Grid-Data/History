Skip to main content

[](/en/)

  * Learn
  * Use
  * Build
  * Participate
  * Research

Search```K`

Languages EN

# How to use Manticore to find bugs in smart contracts

soliditysmart contractssecuritytestingformal verification

Advanced

![✍️](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/270d.svg)Trailofbits

![📚](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4da.svg)[Building
secure contracts(opens in a new tab)](https://github.com/crytic/building-
secure-contracts/tree/master/program-analysis/manticore)

![📆](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4c6.svg)
January 13, 2020

![⏱️](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/23f1.svg)11
minute read minute read

On this page

  * Installation
    * Manticore through docker
    * Manticore through pip
    * Running a script
  * Introduction to dynamic symbolic execution
    * Dynamic Symbolic Execution in a Nutshell
    * Path Predicate Example
    * Verifying properties
  * Running under Manticore
    * Run a standalone exploration
    * Manipulate a smart contract through the API
    * Creating Accounts
    * Executing transactions
    * Workspace
    * Terminate the Exploration
    * Summary: Running under Manticore
  * Getting throwing paths
    * Using state information
    * How to generate testcase
    * Summary
    * Summary: Getting Throwing Path
  * Adding constraints
    * Operators
    * Constraints
    * Checking Constraint
    * Summary: Adding Constraints

The aim of this tutorial is to show how to use Manticore to automatically find
bugs in smart contracts.

## Installation

Manticore requires >= python 3.6. It can be installed through pip or using
docker.

### Manticore through docker

    
    
    docker pull trailofbits/eth-security-toolbox
    
    docker run -it -v "$PWD":/home/training trailofbits/eth-security-toolbox

 _The last command runs eth-security-toolbox in a docker that has access to
your current directory. You can change the files from your host, and run the
tools on the files from the docker_

Inside docker, run:

    
    
    solc-select 0.5.11
    
    cd /home/trufflecon/

### Manticore through pip

    
    
    pip3 install --user manticore

solc 0.5.11 is recommended.

### Running a script

To run a python script with python 3:

    
    
    python3 script.py

## Introduction to dynamic symbolic execution

### Dynamic Symbolic Execution in a Nutshell

Dynamic symbolic execution (DSE) is a program analysis technique that explores
a state space with a high degree of semantic awareness. This technique is
based on the discovery of "program paths", represented as mathematical
formulas called `path predicates`. Conceptually, this technique operates on
path predicates in two steps:

  1. They are constructed using constraints on the program's input.
  2. They are used to generate program inputs that will cause the associated paths to execute.

This approach produces no false positives in the sense that all identified
program states can be triggered during concrete execution. For example, if the
analysis finds an integer overflow, it is guaranteed to be reproducible.

### Path Predicate Example

To get an insight of how DSE works, consider the following example:

    
    
    1function f(uint a){
    
    2
    
    3  if (a == 65) {
    
    4      // A bug is present
    
    5  }
    
    6
    
    7}
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

As `f()` contains two paths, a DSE will construct two different path
predicates:

  * Path 1: `a == 65`
  * Path 2: `Not (a == 65)`

Each path predicate is a mathematical formula that can be given to a so-called
[SMT solver(opens in a new
tab)](https://wikipedia.org/wiki/Satisfiability_modulo_theories), which will
try to solve the equation. For `Path 1`, the solver will say that the path can
be explored with `a = 65`. For `Path 2`, the solver can give `a` any value
other than 65, for example `a = 0`.

### Verifying properties

Manticore allows a full control over all the execution of each path. As a
result, it allows you to add arbitrary constraints to almost anything. This
control allows for the creation of properties on the contract.

Consider the following example:

    
    
    1function unsafe_add(uint a, uint b) returns(uint c){
    
    2  c = a + b; // no overflow protection
    
    3  return c;
    
    4}
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Here there is only one path to explore in the function:

  * Path 1: `c = a + b`

Using Manticore, you can check for overflow, and add constraints to the path
predicate:

  * `c = a + b AND (c < a OR c < b)`

If it is possible to find a valuation of `a` and `b` for which the path
predicate above is feasible, it means that you have found an overflow. For
example the solver can generate the input `a = 10 , b = MAXUINT256`.

If you consider a fixed version:

    
    
    1function safe_add(uint a, uint b) returns(uint c){
    
    2  c = a + b;
    
    3  require(c>=a);
    
    4  require(c>=b);
    
    5  return c;
    
    6}
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

The associated formula with overflow check would be:

  * `c = a + b AND (c >= a) AND (c=>b) AND (c < a OR c < b)`

This formula cannot be solved; in other world this is a **proof** that in
`safe_add`, `c` will always increase.

DSE is thereby a powerful tool, that can verify arbitrary constraints on your
code.

## Running under Manticore

We will see how to explore a smart contract with the Manticore API. The target
is the following smart contract [`example.sol`(opens in a new
tab)](https://github.com/crytic/building-secure-contracts/blob/master/program-
analysis/manticore/examples/example.sol):

    
    
    1pragma solidity >=0.4.24 <0.6.0;
    
    2
    
    3contract Simple {
    
    4    function f(uint a) payable public{
    
    5        if (a == 65) {
    
    6            revert();
    
    7        }
    
    8    }
    
    9}
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

### Run a standalone exploration

You can run Manticore directly on the smart contract by the following command
(`project` can be a Solidity File, or a project directory):

    
    
    $ manticore project

You will get the output of testcases like this one (the order may change):

    
    
    1...
    
    2... m.c.manticore:INFO: Generated testcase No. 0 - STOP
    
    3... m.c.manticore:INFO: Generated testcase No. 1 - REVERT
    
    4... m.c.manticore:INFO: Generated testcase No. 2 - RETURN
    
    5... m.c.manticore:INFO: Generated testcase No. 3 - REVERT
    
    6... m.c.manticore:INFO: Generated testcase No. 4 - STOP
    
    7... m.c.manticore:INFO: Generated testcase No. 5 - REVERT
    
    8... m.c.manticore:INFO: Generated testcase No. 6 - REVERT
    
    9... m.c.manticore:INFO: Results in /home/ethsec/workshops/Automated Smart Contracts Audit - TruffleCon 2018/manticore/examples/mcore_t6vi6ij3
    
    10...
    
    Show all

Without additional information, Manticore will explore the contract with new
symbolic transactions until it does not explore new paths on the contract.
Manticore does not run new transactions after a failing one (e.g: after a
revert).

Manticore will output the information in a `mcore_*` directory. Among other,
you will find in this directory:

  * `global.summary`: coverage and compiler warnings
  * `test_XXXXX.summary`: coverage, last instruction, account balances per test case
  * `test_XXXXX.tx`: detailed list of transactions per test case

Here Manticore founds 7 test cases, which correspond to (the filename order
may change):

| Transaction 0| Transaction 1| Transaction 2| Result  
---|---|---|---|---  
**test_00000000.tx**|  Contract creation| f(!=65)| f(!=65)| STOP  
**test_00000001.tx**|  Contract creation| fallback function| | REVERT  
**test_00000002.tx**|  Contract creation| | | RETURN  
**test_00000003.tx**|  Contract creation| f(65)| | REVERT  
**test_00000004.tx**|  Contract creation| f(!=65)| | STOP  
**test_00000005.tx**|  Contract creation| f(!=65)| f(65)| REVERT  
**test_00000006.tx**|  Contract creation| f(!=65)| fallback function| REVERT  
  
 _Exploration summary f(!=65) denotes f called with any value different than
65._

As you can notice, Manticore generates an unique test case for every
successful or reverted transaction.

Use the `--quick-mode` flag if you want fast code exploration (it disable bug
detectors, gas computation, ...)

### Manipulate a smart contract through the API

This section describes details how to manipulate a smart contract through the
Manticore Python API. You can create new file with python extension `*.py` and
write the necessary code by adding the API commands (basics of which will be
described below) into this file and then run it with the command `$ python3
*.py`. Also you can execute the commands below directly into the python
console, to run the console use the command `$ python3`.

### Creating Accounts

The first thing you should do is to initiate a new blockchain with the
following commands:

    
    
    1from manticore.ethereum import ManticoreEVM
    
    2
    
    3m = ManticoreEVM()
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

A non-contract account is created using [m.create_account(opens in a new
tab)](https://manticore.readthedocs.io/en/latest/evm.html?highlight=create_account#manticore.ethereum.ManticoreEVM.create_account):

    
    
    1user_account = m.create_account(balance=1000)
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

A Solidity contract can be deployed using [m.solidity_create_contract(opens in
a new
tab)](https://manticore.readthedocs.io/en/latest/evm.html?highlight=solidity_create#manticore.ethereum.ManticoreEVM.create_contract):

    
    
    1source_code = '''
    
    2pragma solidity >=0.4.24 <0.6.0;
    
    3contract Simple {
    
    4    function f(uint a) payable public{
    
    5        if (a == 65) {
    
    6            revert();
    
    7        }
    
    8    }
    
    9}
    
    10'''
    
    11# Initiate the contract
    
    12contract_account = m.solidity_create_contract(source_code, owner=user_account)
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

#### Summary

  * You can create user and contract accounts with [m.create_account(opens in a new tab)](https://manticore.readthedocs.io/en/latest/evm.html?highlight=create_account#manticore.ethereum.ManticoreEVM.create_account) and [m.solidity_create_contract(opens in a new tab)](https://manticore.readthedocs.io/en/latest/evm.html?highlight=solidity_create#manticore.ethereum.ManticoreEVM.create_contract).

### Executing transactions

Manticore supports two types of transaction:

  * Raw transaction: all the functions are explored
  * Named transaction: only one function is explored

#### Raw transaction

A raw transaction is executed using [m.transaction(opens in a new
tab)](https://manticore.readthedocs.io/en/latest/evm.html?highlight=transaction#manticore.ethereum.ManticoreEVM.transaction):

    
    
    1m.transaction(caller=user_account,
    
    2              address=contract_account,
    
    3              data=data,
    
    4              value=value)
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

The caller, the address, the data, or the value of the transaction can be
either concrete or symbolic:

  * [m.make_symbolic_value(opens in a new tab)](https://manticore.readthedocs.io/en/latest/evm.html?highlight=make_symbolic_value#manticore.ethereum.ManticoreEVM.make_symbolic_value) creates a symbolic value.
  * [m.make_symbolic_buffer(size)(opens in a new tab)](https://manticore.readthedocs.io/en/latest/evm.html?highlight=make_symbolic_buffer#manticore.ethereum.ManticoreEVM.make_symbolic_buffer) creates a symbolic byte array.

For example:

    
    
    1symbolic_value = m.make_symbolic_value()
    
    2symbolic_data = m.make_symbolic_buffer(320)
    
    3m.transaction(caller=user_account,
    
    4              address=contract_address,
    
    5              data=symbolic_data,
    
    6              value=symbolic_value)
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

If the data is symbolic, Manticore will explore all the functions of the
contract during the transaction execution. It will be helpful to see the
Fallback Function explanation in the [Hands on the Ethernaut CTF(opens in a
new tab)](https://blog.trailofbits.com/2017/11/06/hands-on-the-ethernaut-ctf/)
article for understanding how the function selection works.

#### Named transaction

Functions can be executed through their name. To execute `f(uint var)` with a
symbolic value, from user_account, and with 0 ether, use:

    
    
    1symbolic_var = m.make_symbolic_value()
    
    2contract_account.f(symbolic_var, caller=user_account, value=0)
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

If `value` of the transaction is not specified, it is 0 by default.

#### Summary

  * Arguments of a transaction can be concrete or symbolic
  * A raw transaction will explore all the functions
  * Function can be called by their name

### Workspace

`m.workspace` is the directory used as output directory for all the files
generated:

    
    
    1print("Results are in {}".format(m.workspace))
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

### Terminate the Exploration

To stop the exploration use [m.finalize()(opens in a new
tab)](https://manticore.readthedocs.io/en/latest/evm.html?highlight=finalize#manticore.ethereum.ManticoreEVM.finalize).
No further transactions should be sent once this method is called and
Manticore generates test cases for each of the path explored.

### Summary: Running under Manticore

Putting all the previous steps together, we obtain:

    
    
    1from manticore.ethereum import ManticoreEVM
    
    2
    
    3m = ManticoreEVM()
    
    4
    
    5with open('example.sol') as f:
    
    6    source_code = f.read()
    
    7
    
    8user_account = m.create_account(balance=1000)
    
    9contract_account = m.solidity_create_contract(source_code, owner=user_account)
    
    10
    
    11symbolic_var = m.make_symbolic_value()
    
    12contract_account.f(symbolic_var)
    
    13
    
    14print("Results are in {}".format(m.workspace))
    
    15m.finalize() # stop the exploration
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

All the code above you can find in the [`example_run.py`(opens in a new
tab)](https://github.com/crytic/building-secure-contracts/blob/master/program-
analysis/manticore/examples/example_run.py)

## Getting throwing paths

We will now generate specific inputs for the paths raising an exception in
`f()`. The target is still the following smart contract [`example.sol`(opens
in a new tab)](https://github.com/crytic/building-secure-
contracts/blob/master/program-analysis/manticore/examples/example.sol):

    
    
    1pragma solidity >=0.4.24 <0.6.0;
    
    2contract Simple {
    
    3    function f(uint a) payable public{
    
    4        if (a == 65) {
    
    5            revert();
    
    6        }
    
    7    }
    
    8}
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

### Using state information

Each path executed has its state of the blockchain. A state is either ready or
it is killed, meaning that it reaches a THROW or REVERT instruction:

  * [m.ready_states(opens in a new tab)](https://manticore.readthedocs.io/en/latest/states.html#accessing): the list of states that are ready (they did not execute a REVERT/INVALID)
  * [m.killed_states(opens in a new tab)](https://manticore.readthedocs.io/en/latest/states.html#accessings): the list of states that are killed
  * [m.all_states(opens in a new tab)](https://manticore.readthedocs.io/en/latest/states.html#accessings): all the states

    
    
    1for state in m.all_states:
    
    2    # do something with state
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

You can access state information. For example:

  * `state.platform.get_balance(account.address)`: the balance of the account
  * `state.platform.transactions`: the list of transactions
  * `state.platform.transactions[-1].return_data`: the data returned by the last transaction

The data returned by the last transaction is an array, which can be converted
to a value with ABI.deserialize, for example:

    
    
    1data = state.platform.transactions[0].return_data
    
    2data = ABI.deserialize("uint", data)
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

### How to generate testcase

Use [m.generate_testcase(state, name)(opens in a new
tab)](https://manticore.readthedocs.io/en/latest/evm.html?highlight=generate_testcase#manticore.ethereum.ManticoreEVM.generate_testcase)
to generate testcase:

    
    
    1m.generate_testcase(state, 'BugFound')
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

### Summary

  * You can iterate over the state with m.all_states
  * `state.platform.get_balance(account.address)` returns the account’s balance
  * `state.platform.transactions` returns the list of transactions
  * `transaction.return_data` is the data returned
  * `m.generate_testcase(state, name)` generate inputs for the state

### Summary: Getting Throwing Path

    
    
    1from manticore.ethereum import ManticoreEVM
    
    2
    
    3m = ManticoreEVM()
    
    4
    
    5with open('example.sol') as f:
    
    6    source_code = f.read()
    
    7
    
    8user_account = m.create_account(balance=1000)
    
    9contract_account = m.solidity_create_contract(source_code, owner=user_account)
    
    10
    
    11symbolic_var = m.make_symbolic_value()
    
    12contract_account.f(symbolic_var)
    
    13
    
    14## Check if an execution ends with a REVERT or INVALID
    
    15for state in m.terminated_states:
    
    16    last_tx = state.platform.transactions[-1]
    
    17    if last_tx.result in ['REVERT', 'INVALID']:
    
    18        print('Throw found {}'.format(m.workspace))
    
    19        m.generate_testcase(state, 'ThrowFound')
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

All the code above you can find into the [`example_run.py`(opens in a new
tab)](https://github.com/crytic/building-secure-contracts/blob/master/program-
analysis/manticore/examples/example_run.py)

_Note we could have generated a much simpler script, as all the states
returned by terminated_state have REVERT or INVALID in their result: this
example was only meant to demonstrate how to manipulate the API._

## Adding constraints

We will see how to constrain the exploration. We will make the assumption that
the documentation of `f()` states that the function is never called with `a ==
65`, so any bug with `a == 65` is not a real bug. The target is still the
following smart contract [`example.sol`(opens in a new
tab)](https://github.com/crytic/building-secure-contracts/blob/master/program-
analysis/manticore/examples/example.sol):

    
    
    1pragma solidity >=0.4.24 <0.6.0;
    
    2contract Simple {
    
    3    function f(uint a) payable public{
    
    4        if (a == 65) {
    
    5            revert();
    
    6        }
    
    7    }
    
    8}
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

### Operators

The [Operators(opens in a new
tab)](https://github.com/trailofbits/manticore/blob/master/manticore/core/smtlib/operators.py)
module facilitates the manipulation of constraints, among other it provides:

  * Operators.AND,
  * Operators.OR,
  * Operators.UGT (unsigned greater than),
  * Operators.UGE (unsigned greater than or equal to),
  * Operators.ULT (unsigned lower than),
  * Operators.ULE (unsigned lower than or equal to).

To import the module use the following:

    
    
    1from manticore.core.smtlib import Operators
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

`Operators.CONCAT` is used to concatenate an array to a value. For example,
the return_data of a transaction needs to be changed to a value to be checked
against another value:

    
    
    1last_return = Operators.CONCAT(256, *last_return)
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

### Constraints

You can use constraints globally or for a specific state.

#### Global constraint

Use `m.constrain(constraint)` to add a global constraint. For example, you can
call a contract from a symbolic address, and restraint this address to be
specific values:

    
    
    1symbolic_address = m.make_symbolic_value()
    
    2m.constraint(Operators.OR(symbolic == 0x41, symbolic_address == 0x42))
    
    3m.transaction(caller=user_account,
    
    4              address=contract_account,
    
    5              data=m.make_symbolic_buffer(320),
    
    6              value=0)
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

#### State constraint

Use [state.constrain(constraint)(opens in a new
tab)](https://manticore.readthedocs.io/en/latest/states.html?highlight=StateBase#manticore.core.state.StateBase.constrain)
to add a constraint to a specific state. It can be used to constrain the state
after its exploration to check some property on it.

### Checking Constraint

Use `solver.check(state.constraints)` to know if a constraint is still
feasible. For example, the following will constraint symbolic_value to be
different from 65 and check if the state is still feasible:

    
    
    1state.constrain(symbolic_var != 65)
    
    2if solver.check(state.constraints):
    
    3    # state is feasible
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

### Summary: Adding Constraints

Adding constraint to the previous code, we obtain:

    
    
    1from manticore.ethereum import ManticoreEVM
    
    2from manticore.core.smtlib.solver import Z3Solver
    
    3
    
    4solver = Z3Solver.instance()
    
    5
    
    6m = ManticoreEVM()
    
    7
    
    8with open("example.sol") as f:
    
    9    source_code = f.read()
    
    10
    
    11user_account = m.create_account(balance=1000)
    
    12contract_account = m.solidity_create_contract(source_code, owner=user_account)
    
    13
    
    14symbolic_var = m.make_symbolic_value()
    
    15contract_account.f(symbolic_var)
    
    16
    
    17no_bug_found = True
    
    18
    
    19## Check if an execution ends with a REVERT or INVALID
    
    20for state in m.terminated_states:
    
    21    last_tx = state.platform.transactions[-1]
    
    22    if last_tx.result in ['REVERT', 'INVALID']:
    
    23        # we do not consider the path were a == 65
    
    24        condition = symbolic_var != 65
    
    25        if m.generate_testcase(state, name="BugFound", only_if=condition):
    
    26            print(f'Bug found, results are in {m.workspace}')
    
    27            no_bug_found = False
    
    28
    
    29if no_bug_found:
    
    30    print(f'No bug found')
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

All the code above you can find into the [`example_run.py`(opens in a new
tab)](https://github.com/crytic/building-secure-contracts/blob/master/program-
analysis/manticore/examples/example_run.py)

l

Last edit: [@lukassim(opens in a new tab)](https://github.com/lukassim), April
26, 2024

See contributors

### Was this tutorial helpful?

YesNo

  * [Edit page(opens in a new tab)](https://github.com/ethereum/ethereum-org-website/tree/dev/public/content/developers/tutorials/how-to-use-manticore-to-find-smart-contract-bugs/index.md)
  * On this page

    * Installation
      * Manticore through docker
      * Manticore through pip
      * Running a script
    * Introduction to dynamic symbolic execution
      * Dynamic Symbolic Execution in a Nutshell
      * Path Predicate Example
      * Verifying properties
    * Running under Manticore
      * Run a standalone exploration
      * Manipulate a smart contract through the API
      * Creating Accounts
      * Executing transactions
      * Workspace
      * Terminate the Exploration
      * Summary: Running under Manticore
    * Getting throwing paths
      * Using state information
      * How to generate testcase
      * Summary
      * Summary: Getting Throwing Path
    * Adding constraints
      * Operators
      * Constraints
      * Checking Constraint
      * Summary: Adding Constraints

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

