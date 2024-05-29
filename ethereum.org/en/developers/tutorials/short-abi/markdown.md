Skip to main content

[](/en/)

  * Learn
  * Use
  * Build
  * Participate
  * Research

Search```K`

Languages EN

# Short ABIs for Calldata Optimization

layer 2

Intermediate

![✍️](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/270d.svg)Ori
Pomerantz

![📆](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4c6.svg)
April 1, 2022

![⏱️](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/23f1.svg)15
minute read minute read

On this page

  * Introduction
    * Full disclosure
    * Terminology
  * How can we further reduce the cost of L2 transactions?
    * Cost of L2 transactions
    * The ABI
  * Reducing costs when you don't control the destination
    * Token.sol
    * CalldataInterpreter.sol
    * test.js
    * Example
  * Reducing the cost when you do control the destination contract
    * Token.sol
    * CalldataInterpreter.sol
    * Test.js
    * Example
  * Conclusion

## Introduction

In this article, you learn about [optimistic
rollups](/en/developers/docs/scaling/optimistic-rollups/), the cost of
transactions on them, and how that different cost structure requires us to
optimize for different things than on the Ethereum Mainnet. You also learn how
to implement this optimization.

### Full disclosure

I'm a full time [Optimism(opens in a new tab)](https://www.optimism.io/)
employee, so examples in this article will run on Optimism. However, the
technique explained here should work just as well for other rollups.

### Terminology

When discussing rollups, the term 'layer 1' (L1) is used for Mainnet, the
production Ethereum network. The term 'layer 2' (L2) is used for the rollup or
any other system that relies on L1 for security but does most of its
processing off-chain.

## How can we further reduce the cost of L2 transactions?

[Optimistic rollups](/en/developers/docs/scaling/optimistic-rollups/) have to
preserve a record of every historical transaction so that anybody will be able
to go through them and verify that the current state is correct. The cheapest
way to get data into the Ethereum Mainnet is to write it as calldata. This
solution was chosen by both [Optimism(opens in a new
tab)](https://help.optimism.io/hc/en-us/articles/4413163242779-What-is-a-
rollup-) and [Arbitrum(opens in a new
tab)](https://developer.offchainlabs.com/docs/rollup_basics#intro-to-rollups).

### Cost of L2 transactions

The cost of L2 transactions is composed of two components:

  1. L2 processing, which is usually extremely cheap
  2. L1 storage, which is tied to Mainnet gas costs

As I'm writing this, on Optimism the cost of L2 gas is 0.001
[Gwei](/en/developers/docs/gas/#pre-london). The cost of L1 gas, on the other
hand, is approximately 40 gwei. [You can see the current prices here(opens in
a new tab)](https://public-grafana.optimism.io/d/9hkhMxn7z/public-
dashboard?orgId=1&refresh=5m).

A byte of calldata costs either 4 gas (if it is zero) or 16 gas (if it is any
other value). One of the most expensive operations on the EVM is writing to
storage. The maximum cost of writing a 32-byte word to storage on L2 is 22100
gas. Currently, this is 22.1 gwei. So if we can save a single zero byte of
calldata, we'll be able to write about 200 bytes to storage and still come out
ahead.

### The ABI

The vast majority of transactions access a contract from an externally-owned
account. Most contracts are written in Solidity and interpret their data field
per [the application binary interface (ABI)(opens in a new
tab)](https://docs.soliditylang.org/en/latest/abi-spec.html#formal-
specification-of-the-encoding).

However, the ABI was designed for L1, where a byte of calldata costs
approximately the same as four arithmetic operations, not L2 where a byte of
calldata costs more than a thousand arithmetic operations. For example, [here
is an ERC-20 transfer transaction(opens in a new tab)](https://kovan-
optimistic.etherscan.io/tx/0x7ce4c144ebfce157b4de99d8ad53a352ae91b57b3fa06d8a1c79439df6bfa998).
The calldata is divided like this:

Section| Length| Bytes| Wasted bytes| Wasted gas| Necessary bytes| Necessary
gas  
---|---|---|---|---|---|---  
Function selector| 4| 0-3| 3| 48| 1| 16  
Zeroes| 12| 4-15| 12| 48| 0| 0  
Destination address| 20| 16-35| 0| 0| 20| 320  
Amount| 32| 36-67| 17| 64| 15| 240  
Total| 68| | | 160| | 576  
  
Explanation:

  * **Function selector** : The contract has less than 256 functions, so we can distinguish them with a single byte. These bytes are typically non-zero and therefore [cost sixteen gas(opens in a new tab)](https://eips.ethereum.org/EIPS/eip-2028).
  * **Zeroes** : These bytes are always zero because a twenty-byte address does not require a thirty-two-byte word to hold it. Bytes that hold zero cost four gas ([see the yellow paper(opens in a new tab)](https://ethereum.github.io/yellowpaper/paper.pdf), Appendix G, p. 27, the value for `G``txdatazero`).
  * **Amount** : If we assume that in this contract `decimals` is eighteen (the normal value) and the maximum amount of tokens we transfer will be 1018, we get a maximum amount of 1036. 25615 > 1036, so fifteen bytes are enough.

A waste of 160 gas on L1 is normally negligible. A transaction costs at least
[21,000 gas(opens in a new tab)](https://yakkomajuri.medium.com/blockchain-
definition-of-the-week-ethereum-gas-2f976af774ed), so an extra 0.8% doesn't
matter. However, on L2, things are different. Almost the entire cost of the
transaction is writing it to L1. In addition to the transaction calldata,
there are 109 bytes of transaction header (destination address, signature,
etc.). The total cost is therefore `109*16+576+160=2480`, and we are wasting
about 6.5% of that.

## Reducing costs when you don't control the destination

Assuming that you do not have control over the destination contract, you can
still use a solution similar to [this one(opens in a new
tab)](https://github.com/qbzzt/ethereum.org-20220330-shortABI). Let's go over
the relevant files.

### Token.sol

[This is the destination contract(opens in a new
tab)](https://github.com/qbzzt/ethereum.org-20220330-shortABI/blob/master/contracts/Token.sol).
It is a standard ERC-20 contract, with one additional feature. This `faucet`
function lets any user get some token to use. It would make a production
ERC-20 contract useless, but it makes life easier when an ERC-20 exists only
to facilitate testing.

    
    
    1    /**
    
    2     * @dev Gives the caller 1000 tokens to play with
    
    3     */
    
    4    function faucet() external {
    
    5        _mint(msg.sender, 1000);
    
    6    }   // function faucet
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

[You can see an example of this contract being deployed here(opens in a new
tab)](https://kovan-
optimistic.etherscan.io/address/0x950c753c0edbde44a74d3793db738a318e9c8ce8).

### CalldataInterpreter.sol

[This is the contract that transactions are supposed to call with shorter
calldata(opens in a new
tab)](https://github.com/qbzzt/ethereum.org-20220330-shortABI/blob/master/contracts/CalldataInterpreter.sol).
Let's go over it line by line.

    
    
    1//SPDX-License-Identifier: Unlicense
    
    2pragma solidity ^0.8.0;
    
    3
    
    4
    
    5import { OrisUselessToken } from "./Token.sol";
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

We need the token function to know how to call it.

    
    
    1contract CalldataInterpreter {
    
    2
    
    3    OrisUselessToken public immutable token;
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

The address of the token for which we are a proxy.

    
    
    1
    
    2    /**
    
    3     * @dev Specify the token address
    
    4     * @param tokenAddr_ ERC-20 contract address
    
    5     */
    
    6    constructor(
    
    7        address tokenAddr_
    
    8    )  {
    
    9        token = OrisUselessToken(tokenAddr_);
    
    10    }   // constructor
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

The token address is the only parameter we need to specify.

    
    
    1    function calldataVal(uint startByte, uint length)
    
    2        private pure returns (uint) {
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Read a value from the calldata.

    
    
    1        uint _retVal;
    
    2
    
    3        require(length < 0x21,
    
    4            "calldataVal length limit is 32 bytes");
    
    5
    
    6        require(length + startByte <= msg.data.length,
    
    7            "calldataVal trying to read beyond calldatasize");
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

We are going to load a single 32-byte (256-bit) word to memory and remove the
bytes that aren't part of the field we want. This algorithm doesn't work for
values longer than 32 bytes, and of course we can't read past the end of the
calldata. On L1 it might be necessary to skip these tests to save on gas, but
on L2 gas is extremely cheap, which enables whatever sanity checks we can
think of.

    
    
    1        assembly {
    
    2            _retVal := calldataload(startByte)
    
    3        }
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

We could have copied the data from the call to `fallback()` (see below), but
it is easier to use [Yul(opens in a new
tab)](https://docs.soliditylang.org/en/v0.8.12/yul.html), the assembly
language of the EVM.

Here we use [the CALLDATALOAD opcode(opens in a new
tab)](https://www.evm.codes/#35) to read bytes `startByte` to `startByte+31`
into the stack. In general, the syntax of an opcode in Yul is `<opcode
name>(<first stack value, if any>,<second stack value, if any>...)`.

    
    
    1
    
    2        _retVal = _retVal >> (256-length*8);
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Only the most significant `length` bytes are part of the field, so we [right-
shift(opens in a new tab)](https://en.wikipedia.org/wiki/Logical_shift) to get
rid of the other values. This has the added advantage of moving the value to
the right of the field, so it is the value itself rather than the value times
256something.

    
    
    1
    
    2        return _retVal;
    
    3    }
    
    4
    
    5
    
    6    fallback() external {
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

When a call to a Solidity contract does not match any of the function
signatures, it calls [the `fallback()` function(opens in a new
tab)](https://docs.soliditylang.org/en/v0.8.12/contracts.html#fallback-
function) (assuming there is one). In the case of `CalldataInterpreter`, _any_
call gets here because there are no other `external` or `public` functions.

    
    
    1        uint _func;
    
    2
    
    3        _func = calldataVal(0, 1);
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Read the first byte of the calldata, which tells us the function. There are
two reasons why a function would not be available here:

  1. Functions that are `pure` or `view` don't change the state and don't cost gas (when called off-chain). It makes no sense to try to reduce their gas cost.
  2. Functions that rely on [`msg.sender`(opens in a new tab)](https://docs.soliditylang.org/en/v0.8.12/units-and-global-variables.html#block-and-transaction-properties). The value of `msg.sender` is going to be `CalldataInterpreter`'s address, not the caller.

Unfortunately, [looking at the ERC-20 specifications(opens in a new
tab)](https://eips.ethereum.org/EIPS/eip-20), this leaves only one function,
`transfer`. This leaves us with only two functions: `transfer` (because we can
call `transferFrom`) and `faucet` (because we can transfer the tokens back to
whoever called us).

    
    
    1
    
    2        // Call the state changing methods of token using
    
    3        // information from the calldata
    
    4
    
    5        // faucet
    
    6        if (_func == 1) {
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

A call to `faucet()`, which doesn't have parameters.

    
    
    1            token.faucet();
    
    2            token.transfer(msg.sender,
    
    3                token.balanceOf(address(this)));
    
    4        }
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

After we call `token.faucet()` we get tokens. However, as the proxy contract,
we do not **need** tokens. The EOA (externally owned account) or contract that
called us does. So we transfer all of our tokens to whoever called us.

    
    
    1        // transfer (assume we have an allowance for it)
    
    2        if (_func == 2) {
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Transferring tokens requires two parameters: the destination address and the
amount.

    
    
    1            token.transferFrom(
    
    2                msg.sender,
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

We only allow callers to transfer tokens they own

    
    
    1                address(uint160(calldataVal(1, 20))),
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

The destination address starts at byte #1 (byte #0 is the function). As an
address, it is 20-bytes long.

    
    
    1                calldataVal(21, 2)
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

For this particular contract we assume that the maximum number of tokens
anybody would want to transfer fits in two bytes (less than 65536).

    
    
    1            );
    
    2        }
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Overall, a transfer takes 35 bytes of calldata:

Section| Length| Bytes  
---|---|---  
Function selector| 1| 0  
Destination address| 32| 1-32  
Amount| 2| 33-34  
      
    
    1    }   // fallback
    
    2
    
    3}       // contract CalldataInterpreter
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

### test.js

[This JavaScript unit test(opens in a new
tab)](https://github.com/qbzzt/ethereum.org-20220330-shortABI/blob/master/test/test.js)
shows us how to use this mechanism (and how to verify it works correctly). I
am going to assume you understand [chai(opens in a new
tab)](https://www.chaijs.com/) and [ethers(opens in a new
tab)](https://docs.ethers.io/v5/) and only explain the parts that specifically
apply to the contract.

    
    
    1const { expect } = require("chai");
    
    2
    
    3describe("CalldataInterpreter", function () {
    
    4  it("Should let us use tokens", async function () {
    
    5    const Token = await ethers.getContractFactory("OrisUselessToken")
    
    6    const token = await Token.deploy()
    
    7    await token.deployed()
    
    8    console.log("Token addr:", token.address)
    
    9
    
    10    const Cdi = await ethers.getContractFactory("CalldataInterpreter")
    
    11    const cdi = await Cdi.deploy(token.address)
    
    12    await cdi.deployed()
    
    13    console.log("CalldataInterpreter addr:", cdi.address)
    
    14
    
    15    const signer = await ethers.getSigner()
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

We start by deploying both contracts.

    
    
    1    // Get tokens to play with
    
    2    const faucetTx = {

We can't use the high-level functions we'd normally use (such as
`token.faucet()`) to create transactions, because we do not follow the ABI.
Instead, we have to build the transaction ourselves and then send it.

    
    
    1      to: cdi.address,
    
    2      data: "0x01"

There are two parameters we need to provide for the transaction:

  1. `to`, the destination address. This is the calldata interpreter contract.
  2. `data`, the calldata to send. In the case of a faucet call, the data is a single byte, `0x01`.

    
    
    1
    
    2    }
    
    3    await (await signer.sendTransaction(faucetTx)).wait()

We call [the signer's `sendTransaction` method(opens in a new
tab)](https://docs.ethers.io/v5/api/signer/#Signer-sendTransaction) because we
already specified the destination (`faucetTx.to`) and we need the transaction
to be signed.

    
    
    1// Check the faucet provides the tokens correctly
    
    2expect(await token.balanceOf(signer.address)).to.equal(1000)

Here we verify the balance. There is no need to save gas on `view` functions,
so we just run them normally.

    
    
    1// Give the CDI an allowance (approvals cannot be proxied)
    
    2const approveTX = await token.approve(cdi.address, 10000)
    
    3await approveTX.wait()
    
    4expect(await token.allowance(signer.address, cdi.address)).to.equal(10000)

Give the calldata interpreter an allowance to be able to do transfers.

    
    
    1// Transfer tokens
    
    2const destAddr = "0xf5a6ead936fb47f342bb63e676479bddf26ebe1d"
    
    3const transferTx = {
    
    4  to: cdi.address,
    
    5  data: "0x02" + destAddr.slice(2, 42) + "0100",
    
    6}

Create a transfer transaction. The first byte is "0x02", followed by the
destination address, and finally the amount (0x0100, which is 256 in decimal).

    
    
    1    await (await signer.sendTransaction(transferTx)).wait()
    
    2
    
    3    // Check that we have 256 tokens less
    
    4    expect (await token.balanceOf(signer.address)).to.equal(1000-256)
    
    5
    
    6    // And that our destination got them
    
    7    expect (await token.balanceOf(destAddr)).to.equal(256)
    
    8  })    // it
    
    9})      // describe
    
    Show all

### Example

If you want to see these files in action without running them yourself, follow
these links:

  1. [Deployment of `OrisUselessToken`(opens in a new tab)](https://kovan-optimistic.etherscan.io/tx/1410744) to [address `0x950c753c0edbde44a74d3793db738a318e9c8ce8`(opens in a new tab)](https://kovan-optimistic.etherscan.io/address/0x950c753c0edbde44a74d3793db738a318e9c8ce8).
  2. [Deployment of `CalldataInterpreter`(opens in a new tab)](https://kovan-optimistic.etherscan.io/tx/1410745) to [address `0x16617fea670aefe3b9051096c0eb4aeb4b3a5f55`(opens in a new tab)](https://kovan-optimistic.etherscan.io/address/0x16617fea670aefe3b9051096c0eb4aeb4b3a5f55).
  3. [Call to `faucet()`(opens in a new tab)](https://kovan-optimistic.etherscan.io/tx/1410746).
  4. [Call to `OrisUselessToken.approve()`(opens in a new tab)](https://kovan-optimistic.etherscan.io/tx/1410747). This call has to go directly to the token contract because the processing relies on `msg.sender`.
  5. [Call to `transfer()`(opens in a new tab)](https://kovan-optimistic.etherscan.io/tx/1410748).

## Reducing the cost when you do control the destination contract

If you do have control over the destination contract you can create functions
that bypass the `msg.sender` checks because they trust the calldata
interpreter. [You can see an example of how this works here, in the `control-
contract` branch(opens in a new
tab)](https://github.com/qbzzt/ethereum.org-20220330-shortABI/tree/control-
contract).

If the contract were responding only to external transactions, we could get by
with having just one contract. However, that would break
[composability](/en/developers/docs/smart-contracts/composability/). It is
much better to have a contract that responds to normal ERC-20 calls, and
another contract that responds to transactions with short call data.

### Token.sol

In this example we can modify `Token.sol`. This lets us have a number of
functions that only the proxy may call. Here are the new parts:

    
    
    1    // The only address allowed to specify the CalldataInterpreter address
    
    2    address owner;
    
    3
    
    4    // The CalldataInterpreter address
    
    5    address proxy = address(0);
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

The ERC-20 contract needs to know the identity of the authorized proxy.
However, we cannot set this variable in the constructor, because we don't know
the value yet. This contract is instantiated first because the proxy expects
the token's address in its constructor.

    
    
    1    /**
    
    2     * @dev Calls the ERC20 constructor.
    
    3     */
    
    4    constructor(
    
    5    ) ERC20("Oris useless token-2", "OUT-2") {
    
    6        owner = msg.sender;
    
    7    }
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

The address of the creator (called `owner`) is stored here because that is the
only address allowed to set the proxy.

    
    
    1    /**
    
    2     * @dev set the address for the proxy (the CalldataInterpreter).
    
    3     * Can only be called once by the owner
    
    4     */
    
    5    function setProxy(address _proxy) external {
    
    6        require(msg.sender == owner, "Can only be called by owner");
    
    7        require(proxy == address(0), "Proxy is already set");
    
    8
    
    9        proxy = _proxy;
    
    10    }    // function setProxy
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

The proxy has privileged access, because it can bypass security checks. To
make sure we can trust the proxy we only let `owner` call this function, and
only once. Once `proxy` has a real value (not zero), that value cannot change,
so even if the owner decides to become rogue, or the mnemonic for it is
revealed, we are still safe.

    
    
    1    /**
    
    2     * @dev Some functions may only be called by the proxy.
    
    3     */
    
    4    modifier onlyProxy {
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

This is a [`modifier` function(opens in a new
tab)](https://www.tutorialspoint.com/solidity/solidity_function_modifiers.htm),
it modifies the way other functions work.

    
    
    1      require(msg.sender == proxy);
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

First, verify we got called by the proxy and nobody else. If not, `revert`.

    
    
    1      _;
    
    2    }
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

If so, run the function which we modify.

    
    
    1   /* Functions that allow the proxy to actually proxy for accounts */
    
    2
    
    3    function transferProxy(address from, address to, uint256 amount)
    
    4        public virtual onlyProxy() returns (bool)
    
    5    {
    
    6        _transfer(from, to, amount);
    
    7        return true;
    
    8    }
    
    9
    
    10    function approveProxy(address from, address spender, uint256 amount)
    
    11        public virtual onlyProxy() returns (bool)
    
    12    {
    
    13        _approve(from, spender, amount);
    
    14        return true;
    
    15    }
    
    16
    
    17    function transferFromProxy(
    
    18        address spender,
    
    19        address from,
    
    20        address to,
    
    21        uint256 amount
    
    22    ) public virtual onlyProxy() returns (bool)
    
    23    {
    
    24        _spendAllowance(from, spender, amount);
    
    25        _transfer(from, to, amount);
    
    26        return true;
    
    27    }
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

These are three operations that normally require the message to come directly
from the entity transferring tokens or approving an allowance. Here we have a
proxy version these operations which:

  1. Is modified by `onlyProxy()` so nobody else is allowed to control them.
  2. Gets the address that would normally be `msg.sender` as an extra parameter.

### CalldataInterpreter.sol

The calldata interpreter is nearly identical to the one above, except that the
proxied functions receive a `msg.sender` parameter and there is no need for an
allowance for `transfer`.

    
    
    1        // transfer (no need for allowance)
    
    2        if (_func == 2) {
    
    3            token.transferProxy(
    
    4                msg.sender,
    
    5                address(uint160(calldataVal(1, 20))),
    
    6                calldataVal(21, 2)
    
    7            );
    
    8        }
    
    9
    
    10        // approve
    
    11        if (_func == 3) {
    
    12            token.approveProxy(
    
    13                msg.sender,
    
    14                address(uint160(calldataVal(1, 20))),
    
    15                calldataVal(21, 2)
    
    16            );
    
    17        }
    
    18
    
    19        // transferFrom
    
    20        if (_func == 4) {
    
    21            token.transferFromProxy(
    
    22                msg.sender,
    
    23                address(uint160(calldataVal( 1, 20))),
    
    24                address(uint160(calldataVal(21, 20))),
    
    25                calldataVal(41, 2)
    
    26            );
    
    27        }
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

### Test.js

There are a few changes between the previous testing code and this one.

    
    
    1const Cdi = await ethers.getContractFactory("CalldataInterpreter")
    
    2const cdi = await Cdi.deploy(token.address)
    
    3await cdi.deployed()
    
    4await token.setProxy(cdi.address)
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

We need to tell the ERC-20 contract which proxy to trust

    
    
    1console.log("CalldataInterpreter addr:", cdi.address)
    
    2
    
    3// Need two signers to verify allowances
    
    4const signers = await ethers.getSigners()
    
    5const signer = signers[0]
    
    6const poorSigner = signers[1]
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

To check `approve()` and `transferFrom()` we need a second signer. We call it
`poorSigner` because it does not get any of our tokens (it does need to have
ETH, of course).

    
    
    1// Transfer tokens
    
    2const destAddr = "0xf5a6ead936fb47f342bb63e676479bddf26ebe1d"
    
    3const transferTx = {
    
    4  to: cdi.address,
    
    5  data: "0x02" + destAddr.slice(2, 42) + "0100",
    
    6}
    
    7await (await signer.sendTransaction(transferTx)).wait()
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Because the ERC-20 contract trusts the proxy (`cdi`), we don't need an
allowance to relay transfers.

    
    
    1// approval and transferFrom
    
    2const approveTx = {
    
    3  to: cdi.address,
    
    4  data: "0x03" + poorSigner.address.slice(2, 42) + "00FF",
    
    5}
    
    6await (await signer.sendTransaction(approveTx)).wait()
    
    7
    
    8const destAddr2 = "0xE1165C689C0c3e9642cA7606F5287e708d846206"
    
    9
    
    10const transferFromTx = {
    
    11  to: cdi.address,
    
    12  data: "0x04" + signer.address.slice(2, 42) + destAddr2.slice(2, 42) + "00FF",
    
    13}
    
    14await (await poorSigner.sendTransaction(transferFromTx)).wait()
    
    15
    
    16// Check the approve / transferFrom combo was done correctly
    
    17expect(await token.balanceOf(destAddr2)).to.equal(255)
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Test the two new functions. Note that `transferFromTx` requires two address
parameters: the giver of the allowance and the receiver.

### Example

If you want to see these files in action without running them yourself, follow
these links:

  1. [Deployment of `OrisUselessToken-2`(opens in a new tab)](https://kovan-optimistic.etherscan.io/tx/1475397) at address [`0xb47c1f550d8af70b339970c673bbdb2594011696`(opens in a new tab)](https://kovan-optimistic.etherscan.io/address/0xb47c1f550d8af70b339970c673bbdb2594011696).
  2. [Deployment of `CalldataInterpreter`(opens in a new tab)](https://kovan-optimistic.etherscan.io/tx/1475400) at address [`0x0dccfd03e3aaba2f8c4ea4008487fd0380815892`(opens in a new tab)](https://kovan-optimistic.etherscan.io/address/0x0dccfd03e3aaba2f8c4ea4008487fd0380815892).
  3. [Call to `setProxy()`(opens in a new tab)](https://kovan-optimistic.etherscan.io/tx/1475402).
  4. [Call to `faucet()`(opens in a new tab)](https://kovan-optimistic.etherscan.io/tx/1475409).
  5. [Call to `transferProxy()`(opens in a new tab)](https://kovan-optimistic.etherscan.io/tx/1475416).
  6. [Call to `approveProxy()`(opens in a new tab)](https://kovan-optimistic.etherscan.io/tx/1475419).
  7. [Call to `transferFromProxy()`(opens in a new tab)](https://kovan-optimistic.etherscan.io/tx/1475421). Note that this call comes from a different address than the other ones, `poorSigner` instead of `signer`.

## Conclusion

Both [Optimism(opens in a new tab)](https://medium.com/ethereum-optimism/the-
road-to-sub-dollar-transactions-part-2-compression-edition-6bb2890e3e92) and
[Arbitrum(opens in a new
tab)](https://developer.offchainlabs.com/docs/special_features) are looking
for ways to reduce the size of the calldata written to L1 and therefore the
cost of transactions. However, as infrastructure providers looking for generic
solutions, our abilities are limited. As the dapp developer, you have
application-specific knowledge, which lets you optimize your calldata much
better than we could in a generic solution. Hopefully, this article helps you
find the ideal solution for your needs.

n

Last edit: [@nhsz(opens in a new tab)](https://github.com/nhsz), August 15,
2023

See contributors

### Was this tutorial helpful?

YesNo

  * [Edit page(opens in a new tab)](https://github.com/ethereum/ethereum-org-website/tree/dev/public/content/developers/tutorials/short-abi/index.md)
  * On this page

    * Introduction
      * Full disclosure
      * Terminology
    * How can we further reduce the cost of L2 transactions?
      * Cost of L2 transactions
      * The ABI
    * Reducing costs when you don't control the destination
      * Token.sol
      * CalldataInterpreter.sol
      * test.js
      * Example
    * Reducing the cost when you do control the destination contract
      * Token.sol
      * CalldataInterpreter.sol
      * Test.js
      * Example
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

