Skip to main content

[](/en/)

  * Learn
  * Use
  * Build
  * Participate
  * Research

Search```K`

Languages EN

# How to use Echidna to test smart contracts

soliditysmart contractssecuritytestingfuzzing

Advanced

![✍️](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/270d.svg)Trailofbits

![📚](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4da.svg)[Building
secure contracts(opens in a new tab)](https://github.com/crytic/building-
secure-contracts/tree/master/program-analysis/echidna)

![📆](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4c6.svg)
April 10, 2020

![⏱️](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/23f1.svg)13
minute read minute read

On this page

  * Installation
    * Echidna through docker
    * Binary
  * Introduction to property-based fuzzing
    * Fuzzing
    * Property-based fuzzing
    * Testing a property with Echidna
    * Write a property
    * Initiate a contract
    * Run Echidna
    * Summary: Testing a property
  * Filtering functions to call during a fuzzing campaign
    * Filtering functions
    * Run Echidna
    * Summary: Filtering functions
  * How to test Solidity's assert with Echidna
    * Write an assertion
    * Run Echidna
    * When and how use assertions
    * Summary: Assertion Checking
  * Collecting and modifying an Echidna corpus
    * Collecting a corpus
    * Seeding a corpus
  * Finding transactions with high gas consumption
    * Measuring Gas Consumption
    * Run Echidna
    * Filtering Out Gas-Reducing Calls
    * Summary: Finding transactions with high gas consumption

## Installation

Echidna can be installed through docker or using the pre-compiled binary.

### Echidna through docker

    
    
    docker pull trailofbits/eth-security-toolbox
    
    docker run -it -v "$PWD":/home/training trailofbits/eth-security-toolbox

 _The last command runs eth-security-toolbox in a docker that has access to
your current directory. You can change the files from your host, and run the
tools on the files from the docker_

Inside docker, run :

    
    
    solc-select 0.5.11
    
    cd /home/training

### Binary

<https://github.com/crytic/echidna/releases/tag/v1.4.0.0>[(opens in a new
tab)](https://github.com/crytic/echidna/releases/tag/v1.4.0.0)

## Introduction to property-based fuzzing

Echidna is a property-based fuzzer, we described in our previous blogposts
([1(opens in a new tab)](https://blog.trailofbits.com/2018/03/09/echidna-a-
smart-fuzzer-for-ethereum/), [2(opens in a new
tab)](https://blog.trailofbits.com/2018/05/03/state-machine-testing-with-
echidna/), [3(opens in a new tab)](https://blog.trailofbits.com/2020/03/30/an-
echidna-for-all-seasons/)).

### Fuzzing

[Fuzzing(opens in a new tab)](https://wikipedia.org/wiki/Fuzzing) is a well-
known technique in the security community. It consists of generating inputs
that are more or less random to find bugs in the program. Fuzzers for
traditional software (such as [AFL(opens in a new
tab)](http://lcamtuf.coredump.cx/afl/) or [LibFuzzer(opens in a new
tab)](https://llvm.org/docs/LibFuzzer.html)) are known to be efficient tools
to find bugs.

Beyond the purely random generation of inputs, there are many techniques and
strategies to generate good inputs, including:

  * Obtain feedback from each execution and guide generation using it. For example, if a newly generated input leads to the discovery of a new path, it can make sense to generate new inputs closes to it.
  * Generating the input respecting a structural constraint. For example, if your input contains a header with a checksum, it will make sense to let the fuzzer generates input validating the checksum.
  * Using known inputs to generate new inputs: if you have access to a large dataset of valid input, your fuzzer can generate new inputs from them, rather than starting from scratch its generation. These are usually called _seeds_.

### Property-based fuzzing

Echidna belongs to a specific family of fuzzer: property-based fuzzing heavily
inspired by [QuickCheck(opens in a new
tab)](https://wikipedia.org/wiki/QuickCheck). In contrast to classic fuzzer
that will try to find crashes, Echidna will try to break user-defined
invariants.

In smart contracts, invariants are Solidity functions, that can represent any
incorrect or invalid state that the contract can reach, including:

  * Incorrect access control: the attacker became the owner of the contract.
  * Incorrect state machine: the tokens can be transferred while the contract is paused.
  * Incorrect arithmetic: the user can underflow its balance and get unlimited free tokens.

### Testing a property with Echidna

We will see how to test a smart contract with Echidna. The target is the
following smart contract [`token.sol`(opens in a new
tab)](https://github.com/crytic/building-secure-contracts/blob/master/program-
analysis/echidna/example/token.sol):

    
    
    1contract Token{
    
    2  mapping(address => uint) public balances;
    
    3  function airdrop() public{
    
    4      balances[msg.sender] = 1000;
    
    5  }
    
    6  function consume() public{
    
    7      require(balances[msg.sender]>0);
    
    8      balances[msg.sender] -= 1;
    
    9  }
    
    10  function backdoor() public{
    
    11      balances[msg.sender] += 1;
    
    12  }
    
    13}
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

We will make the assumption that this token must have the following
properties:

  * Anyone can have at maximum 1000 tokens
  * The token cannot be transferred (it is not an ERC20 token)

### Write a property

Echidna properties are Solidity functions. A property must:

  * Have no argument
  * Return `true` if it is successful
  * Have its name starting with `echidna`

Echidna will:

  * Automatically generate arbitrary transactions to test the property.
  * Report any transactions leading a property to return `false` or throw an error.
  * Discard side-effect when calling a property (i.e. if the property changes a state variable, it is discarded after the test)

The following property checks that the caller has no more than 1000 tokens:

    
    
    1function echidna_balance_under_1000() public view returns(bool){
    
    2      return balances[msg.sender] <= 1000;
    
    3}
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Use inheritance to separate your contract from your properties:

    
    
    1contract TestToken is Token{
    
    2      function echidna_balance_under_1000() public view returns(bool){
    
    3            return balances[msg.sender] <= 1000;
    
    4      }
    
    5  }
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

[`token.sol`(opens in a new tab)](https://github.com/crytic/building-secure-
contracts/blob/master/program-analysis/echidna/example/token.sol) implements
the property and inherits from the token.

### Initiate a contract

Echidna needs a [constructor](/en/developers/docs/smart-
contracts/anatomy/#constructor-functions) without argument. If your contract
needs a specific initialization, you need to do it in the constructor.

There are some specific addresses in Echidna:

  * `0x00a329c0648769A73afAc7F9381E08FB43dBEA72` which calls the constructor.
  * `0x10000`, `0x20000`, and `0x00a329C0648769a73afAC7F9381e08fb43DBEA70` which randomly calls the other functions.

We do not need any particular initialization in our current example, as a
result our constructor is empty.

### Run Echidna

Echidna is launched with:

    
    
    echidna-test contract.sol

If contract.sol contains multiple contracts, you can specify the target:

    
    
    echidna-test contract.sol --contract MyContract

### Summary: Testing a property

The following summarizes the run of echidna on our example:

    
    
    1contract TestToken is Token{
    
    2    constructor() public {}
    
    3        function echidna_balance_under_1000() public view returns(bool){
    
    4          return balances[msg.sender] <= 1000;
    
    5        }
    
    6  }
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy
    
    
    echidna-test testtoken.sol --contract TestToken
    
    ...
    
    echidna_balance_under_1000: failed!💥
    
      Call sequence, shrinking (1205/5000):
    
        airdrop()
    
        backdoor()
    
    ...
    
    Show all

Echidna found that the property is violated if `backdoor` is called.

## Filtering functions to call during a fuzzing campaign

We will see how to filter the functions to be fuzzed. The target is the
following smart contract:

    
    
    1contract C {
    
    2  bool state1 = false;
    
    3  bool state2 = false;
    
    4  bool state3 = false;
    
    5  bool state4 = false;
    
    6
    
    7  function f(uint x) public {
    
    8    require(x == 12);
    
    9    state1 = true;
    
    10  }
    
    11
    
    12  function g(uint x) public {
    
    13    require(state1);
    
    14    require(x == 8);
    
    15    state2 = true;
    
    16  }
    
    17
    
    18  function h(uint x) public {
    
    19    require(state2);
    
    20    require(x == 42);
    
    21    state3 = true;
    
    22  }
    
    23
    
    24 function i() public {
    
    25    require(state3);
    
    26    state4 = true;
    
    27  }
    
    28
    
    29  function reset1() public {
    
    30    state1 = false;
    
    31    state2 = false;
    
    32    state3 = false;
    
    33    return;
    
    34  }
    
    35
    
    36  function reset2() public {
    
    37    state1 = false;
    
    38    state2 = false;
    
    39    state3 = false;
    
    40    return;
    
    41  }
    
    42
    
    43  function echidna_state4() public returns (bool) {
    
    44    return (!state4);
    
    45  }
    
    46}
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

This small example forces Echidna to find a certain sequence of transactions
to change a state variable. This is hard for a fuzzer (it is recommended to
use a symbolic execution tool like [Manticore(opens in a new
tab)](https://github.com/trailofbits/manticore)). We can run Echidna to verify
this:

    
    
    echidna-test multi.sol
    
    ...
    
    echidna_state4: passed! 🎉
    
    Seed: -3684648582249875403

### Filtering functions

Echidna has trouble finding the correct sequence to test this contract because
the two reset functions (`reset1` and `reset2`) will set all the state
variables to `false`. However, we can use a special Echidna feature to either
blacklist the reset function or to whitelist only the `f`, `g`, `h` and `i`
functions.

To blacklist functions, we can use this configuration file:

    
    
    1filterBlacklist: true
    
    2filterFunctions: ["reset1", "reset2"]

Another approach to filter functions is to list the whitelisted functions. To
do that, we can use this configuration file:

    
    
    1filterBlacklist: false
    
    2filterFunctions: ["f", "g", "h", "i"]

  * `filterBlacklist` is `true` by default.
  * Filtering will be performed by name only (without parameters). If you have `f()` and `f(uint256)`, the filter `"f"` will match both functions.

### Run Echidna

To run Echidna with a configuration file `blacklist.yaml`:

    
    
    echidna-test multi.sol --config blacklist.yaml
    
    ...
    
    echidna_state4: failed!💥
    
      Call sequence:
    
        f(12)
    
        g(8)
    
        h(42)
    
        i()

Echidna will find the sequence of transactions to falsify the property almost
immediately.

### Summary: Filtering functions

Echidna can either blacklist or whitelist functions to call during a fuzzing
campaign using:

    
    
    1filterBlacklist: true
    
    2filterFunctions: ["f1", "f2", "f3"]
    
    
    echidna-test contract.sol --config config.yaml
    
    ...

Echidna starts a fuzzing campaign either blacklisting `f1`, `f2` and `f3` or
only calling these, according to the value of the `filterBlacklist` boolean.

## How to test Solidity's assert with Echidna

In this short tutorial, we are going to show how to use Echidna to test
assertion checking in contracts. Let's suppose we have a contract like this
one:

    
    
    1contract Incrementor {
    
    2  uint private counter = 2**200;
    
    3
    
    4  function inc(uint val) public returns (uint){
    
    5    uint tmp = counter;
    
    6    counter += val;
    
    7    // tmp <= counter
    
    8    return (counter - tmp);
    
    9  }
    
    10}
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

### Write an assertion

We want to make sure that `tmp` is less or equal than `counter` after
returning its difference. We could write an Echidna property, but we will need
to store the `tmp` value somewhere. Instead, we could use an assertion like
this one:

    
    
    1contract Incrementor {
    
    2  uint private counter = 2**200;
    
    3
    
    4  function inc(uint val) public returns (uint){
    
    5    uint tmp = counter;
    
    6    counter += val;
    
    7    assert (tmp <= counter);
    
    8    return (counter - tmp);
    
    9  }
    
    10}
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

### Run Echidna

To enable the assertion failure testing, create an [Echidna configuration
file(opens in a new tab)](https://github.com/crytic/echidna/wiki/Config)
`config.yaml`:

    
    
    1checkAsserts: true

When we run this contract in Echidna, we obtain the expected results:

    
    
    echidna-test assert.sol --config config.yaml
    
    Analyzing contract: assert.sol:Incrementor
    
    assertion in inc: failed!💥
    
      Call sequence, shrinking (2596/5000):
    
        inc(21711016731996786641919559689128982722488122124807605757398297001483711807488)
    
        inc(7237005577332262213973186563042994240829374041602535252466099000494570602496)
    
        inc(86844066927987146567678238756515930889952488499230423029593188005934847229952)
    
    Seed: 1806480648350826486
    
    Show all

As you can see, Echidna reports some assertion failure in the `inc` function.
Adding more than one assertion per function is possible, but Echidna cannot
tell which assertion failed.

### When and how use assertions

Assertions can be used as alternatives to explicit properties, specially if
the conditions to check are directly related with the correct use of some
operation `f`. Adding assertions after some code will enforce that the check
will happen immediately after it was executed:

    
    
    1function f(..) public {
    
    2    // some complex code
    
    3    ...
    
    4    assert (condition);
    
    5    ...
    
    6}
    
    7
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

On the contrary, using an explicit echidna property will randomly execution
transactions and there is no easy way to enforce exactly when it will be
checked. It is still possible to do this workaround:

    
    
    1function echidna_assert_after_f() public returns (bool) {
    
    2    f(..);
    
    3    return(condition);
    
    4}
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

However, there are some issues:

  * It fails if `f` is declared as `internal` or `external`.
  * It is unclear which arguments should be used to call `f`.
  * If `f` reverts, the property will fail.

In general, we recommend following [John Regehr's recommendation(opens in a
new tab)](https://blog.regehr.org/archives/1091) on how to use assertions:

  * Do not force any side effect during the assertion checking. For instance: `assert(ChangeStateAndReturn() == 1)`
  * Do not assert obvious statements. For instance `assert(var >= 0)` where `var` is declared as `uint`.

Finally, please **do not use** `require` instead of `assert`, since Echidna
will not be able to detect it (but the contract will revert anyway).

### Summary: Assertion Checking

The following summarizes the run of echidna on our example:

    
    
    1contract Incrementor {
    
    2  uint private counter = 2**200;
    
    3
    
    4  function inc(uint val) public returns (uint){
    
    5    uint tmp = counter;
    
    6    counter += val;
    
    7    assert (tmp <= counter);
    
    8    return (counter - tmp);
    
    9  }
    
    10}
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy
    
    
    echidna-test assert.sol --config config.yaml
    
    Analyzing contract: assert.sol:Incrementor
    
    assertion in inc: failed!💥
    
      Call sequence, shrinking (2596/5000):
    
        inc(21711016731996786641919559689128982722488122124807605757398297001483711807488)
    
        inc(7237005577332262213973186563042994240829374041602535252466099000494570602496)
    
        inc(86844066927987146567678238756515930889952488499230423029593188005934847229952)
    
    Seed: 1806480648350826486
    
    Show all

Echidna found that the assertion in `inc` can fail if this function is called
multiple times with large arguments.

## Collecting and modifying an Echidna corpus

We will see how to collect and use a corpus of transactions with Echidna. The
target is the following smart contract [`magic.sol`(opens in a new
tab)](https://github.com/crytic/building-secure-contracts/blob/master/program-
analysis/echidna/example/magic.sol):

    
    
    1contract C {
    
    2  bool value_found = false;
    
    3  function magic(uint magic_1, uint magic_2, uint magic_3, uint magic_4) public {
    
    4    require(magic_1 == 42);
    
    5    require(magic_2 == 129);
    
    6    require(magic_3 == magic_4+333);
    
    7    value_found = true;
    
    8    return;
    
    9  }
    
    10
    
    11  function echidna_magic_values() public returns (bool) {
    
    12    return !value_found;
    
    13  }
    
    14
    
    15}
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

This small example forces Echidna to find certain values to change a state
variable. This is hard for a fuzzer (it is recommended to use a symbolic
execution tool like [Manticore(opens in a new
tab)](https://github.com/trailofbits/manticore)). We can run Echidna to verify
this:

    
    
    echidna-test magic.sol
    
    ...
    
    echidna_magic_values: passed! 🎉
    
    Seed: 2221503356319272685

However, we can still use Echidna to collect corpus when running this fuzzing
campaign.

### Collecting a corpus

To enable the corpus collection, create a corpus directory:

    
    
    mkdir corpus-magic

And an [Echidna configuration file(opens in a new
tab)](https://github.com/crytic/echidna/wiki/Config) `config.yaml`:

    
    
    1coverage: true
    
    2corpusDir: "corpus-magic"

Now we can run our tool and check the collected corpus:

    
    
    echidna-test magic.sol --config config.yaml

Echidna still cannot find the correct magic values, but we can take look to
the corpus it collected. For instance, one of these files was:

    
    
    1[
    
    2  {
    
    3    "_gas'": "0xffffffff",
    
    4    "_delay": ["0x13647", "0xccf6"],
    
    5    "_src": "00a329c0648769a73afac7f9381e08fb43dbea70",
    
    6    "_dst": "00a329c0648769a73afac7f9381e08fb43dbea72",
    
    7    "_value": "0x0",
    
    8    "_call": {
    
    9      "tag": "SolCall",
    
    10      "contents": [
    
    11        "magic",
    
    12        [
    
    13          {
    
    14            "contents": [
    
    15              256,
    
    16              "93723985220345906694500679277863898678726808528711107336895287282192244575836"
    
    17            ],
    
    18            "tag": "AbiUInt"
    
    19          },
    
    20          {
    
    21            "contents": [256, "334"],
    
    22            "tag": "AbiUInt"
    
    23          },
    
    24          {
    
    25            "contents": [
    
    26              256,
    
    27              "68093943901352437066264791224433559271778087297543421781073458233697135179558"
    
    28            ],
    
    29            "tag": "AbiUInt"
    
    30          },
    
    31          {
    
    32            "tag": "AbiUInt",
    
    33            "contents": [256, "332"]
    
    34          }
    
    35        ]
    
    36      ]
    
    37    },
    
    38    "_gasprice'": "0xa904461f1"
    
    39  }
    
    40]
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Clearly, this input will not trigger the failure in our property. However, in
the next step, we will see how to modify it for that.

### Seeding a corpus

Echidna needs some help in order to deal with the `magic` function. We are
going to copy and modify the input to use suitable parameters for it:

    
    
    cp corpus/2712688662897926208.txt corpus/new.txt

We will modify `new.txt` to call `magic(42,129,333,0)`. Now, we can re-run
Echidna:

    
    
    echidna-test magic.sol --config config.yaml
    
    ...
    
    echidna_magic_values: failed!💥
    
      Call sequence:
    
        magic(42,129,333,0)
    
    Unique instructions: 142
    
    Unique codehashes: 1
    
    Seed: -7293830866560616537
    
    Show all

This time, it found that the property is violated immediately.

## Finding transactions with high gas consumption

We will see how to find the transactions with high gas consumption with
Echidna. The target is the following smart contract:

    
    
    1contract C {
    
    2  uint state;
    
    3
    
    4  function expensive(uint8 times) internal {
    
    5    for(uint8 i=0; i < times; i++)
    
    6      state = state + i;
    
    7  }
    
    8
    
    9  function f(uint x, uint y, uint8 times) public {
    
    10    if (x == 42 && y == 123)
    
    11      expensive(times);
    
    12    else
    
    13      state = 0;
    
    14  }
    
    15
    
    16  function echidna_test() public returns (bool) {
    
    17    return true;
    
    18  }
    
    19
    
    20}
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Here `expensive` can have a large gas consumption.

Currently, Echidna always need a property to test: here `echidna_test` always
returns `true`. We can run Echidna to verify this:

    
    
    1echidna-test gas.sol
    
    2...
    
    3echidna_test: passed! 🎉
    
    4
    
    5Seed: 2320549945714142710

### Measuring Gas Consumption

To enable the gas consumption with Echidna, create a configuration file
`config.yaml`:

    
    
    1estimateGas: true

In this example, we will also reduce the size of the transaction sequence to
make the results easier to understand:

    
    
    1seqLen: 2
    
    2estimateGas: true

### Run Echidna

Once we have the configuration file created, we can run Echidna like this:

    
    
    echidna-test gas.sol --config config.yaml
    
    ...
    
    echidna_test: passed! 🎉
    
    f used a maximum of 1333608 gas
    
      Call sequence:
    
        f(42,123,249) Gas price: 0x10d5733f0a Time delay: 0x495e5 Block delay: 0x88b2
    
    Unique instructions: 157
    
    Unique codehashes: 1
    
    Seed: -325611019680165325
    
    Show all

  * The gas shown is an estimation provided by [HEVM(opens in a new tab)](https://github.com/dapphub/dapptools/tree/master/src/hevm#hevm-).

### Filtering Out Gas-Reducing Calls

The tutorial on **filtering functions to call during a fuzzing campaign**
above shows how to remove some functions from your testing.  
This can be critical for getting an accurate gas estimate. Consider the
following example:

    
    
    1contract C {
    
    2  address [] addrs;
    
    3  function push(address a) public {
    
    4    addrs.push(a);
    
    5  }
    
    6  function pop() public {
    
    7    addrs.pop();
    
    8  }
    
    9  function clear() public{
    
    10    addrs.length = 0;
    
    11  }
    
    12  function check() public{
    
    13    for(uint256 i = 0; i < addrs.length; i++)
    
    14      for(uint256 j = i+1; j < addrs.length; j++)
    
    15        if (addrs[i] == addrs[j])
    
    16          addrs[j] = address(0x0);
    
    17  }
    
    18  function echidna_test() public returns (bool) {
    
    19      return true;
    
    20  }
    
    21}
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

If Echidna can call all the functions, it won't easily find transactions with
high gas cost:

    
    
    1echidna-test pushpop.sol --config config.yaml
    
    2...
    
    3pop used a maximum of 10746 gas
    
    4...
    
    5check used a maximum of 23730 gas
    
    6...
    
    7clear used a maximum of 35916 gas
    
    8...
    
    9push used a maximum of 40839 gas
    
    Show all

That's because the cost depends on the size of `addrs` and random calls tend
to leave the array almost empty. Blacklisting `pop` and `clear`, however,
gives us much better results:

    
    
    1filterBlacklist: true
    
    2filterFunctions: ["pop", "clear"]
    
    
    1echidna-test pushpop.sol --config config.yaml
    
    2...
    
    3push used a maximum of 40839 gas
    
    4...
    
    5check used a maximum of 1484472 gas

### Summary: Finding transactions with high gas consumption

Echidna can find transactions with high gas consumption using the
`estimateGas` configuration option:

    
    
    1estimateGas: true
    
    
    echidna-test contract.sol --config config.yaml
    
    ...

Echidna will report a sequence with the maximum gas consumption for every
function, once the fuzzing campaign is over.

p

Last edit: [@pettinarip(opens in a new tab)](https://github.com/pettinarip),
December 4, 2023

See contributors

### Was this tutorial helpful?

YesNo

  * [Edit page(opens in a new tab)](https://github.com/ethereum/ethereum-org-website/tree/dev/public/content/developers/tutorials/how-to-use-echidna-to-test-smart-contracts/index.md)
  * On this page

    * Installation
      * Echidna through docker
      * Binary
    * Introduction to property-based fuzzing
      * Fuzzing
      * Property-based fuzzing
      * Testing a property with Echidna
      * Write a property
      * Initiate a contract
      * Run Echidna
      * Summary: Testing a property
    * Filtering functions to call during a fuzzing campaign
      * Filtering functions
      * Run Echidna
      * Summary: Filtering functions
    * How to test Solidity's assert with Echidna
      * Write an assertion
      * Run Echidna
      * When and how use assertions
      * Summary: Assertion Checking
    * Collecting and modifying an Echidna corpus
      * Collecting a corpus
      * Seeding a corpus
    * Finding transactions with high gas consumption
      * Measuring Gas Consumption
      * Run Echidna
      * Filtering Out Gas-Reducing Calls
      * Summary: Finding transactions with high gas consumption

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

