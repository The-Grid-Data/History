Skip to main content

[](/en/)

  * Learn
  * Use
  * Build
  * Participate
  * Research

Search```K`

Languages EN

# Uniswap-v2 Contract Walk-Through

solidity

Intermediate

![✍️](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/270d.svg)Ori
Pomerantz

![📆](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4c6.svg)
May 1, 2021

![⏱️](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/23f1.svg)60
minute read minute read

On this page

  * Introduction
    * What Does Uniswap Do?
    * Why v2? Why not v3?
    * Core Contracts vs Periphery Contracts
  * Data and Control Flows
    * Swap
    * Add Liquidity
    * Remove Liquidity
  * The Core Contracts
    * UniswapV2Pair.sol
    * UniswapV2Factory.sol
    * UniswapV2ERC20.sol
  * The Periphery Contracts
    * UniswapV2Router01.sol
    * UniswapV2Router02.sol
    * UniswapV2Migrator.sol
  * The Libraries
    * Math
    * Fixed Point Fractions (UQ112x112)
    * UniswapV2Library
    * Transfer Helper
  * Conclusion

## Introduction

[Uniswap v2(opens in a new tab)](https://uniswap.org/whitepaper.pdf) can
create an exchange market between any two ERC-20 tokens. In this article we
will go over the source code for the contracts that implement this protocol
and see why they are written this way.

### What Does Uniswap Do?

Basically, there are two types of users: liquidity providers and traders.

The _liquidity providers_ provide the pool with the two tokens that can be
exchanged (we'll call them **Token0** and **Token1**). In return, they receive
a third token that represents partial ownership of the pool called a
_liquidity token_.

_Traders_ send one type of token to the pool and receive the other (for
example, send **Token0** and receive **Token1**) out of the pool provided by
the liquidity providers. The exchange rate is determined by the relative
number of **Token0** s and **Token1** s that the pool has. In addition, the
pool takes a small percent as a reward for the liquidity pool.

When liquidity providers want their assets back they can burn the pool tokens
and receive back their tokens, including their share of the rewards.

[Click here for a fuller description(opens in a new
tab)](https://docs.uniswap.org/contracts/v2/concepts/core-concepts/swaps/).

### Why v2? Why not v3?

[Uniswap v3(opens in a new tab)](https://uniswap.org/whitepaper-v3.pdf) is an
upgrade that is much more complicated than the v2. It is easier to first learn
v2 and then go to v3.

### Core Contracts vs Periphery Contracts

Uniswap v2 is divided into two components, a core and a periphery. This
division allows the core contracts, which hold the assets and therefore _have_
to be secure, to be simpler and easier to audit. All the extra functionality
required by traders can then be provided by periphery contracts.

## Data and Control Flows

This is the flow of data and control that happens when you perform the three
main actions of Uniswap:

  1. Swap between different tokens
  2. Add liquidity to the market and get rewarded with pair exchange ERC-20 liquidity tokens
  3. Burn ERC-20 liquidity tokens and get back the ERC-20 tokens that the pair exchange allows traders to exchange

### Swap

This is most common flow, used by traders:

#### Caller

  1. Provide the periphery account with an allowance in the amount to be swapped.
  2. Call one of the periphery contract's many swap functions (which one depends on whether ETH is involved or not, whether the trader specifies the amount of tokens to deposit or the amount of tokens to get back, etc). Every swap function accepts a `path`, an array of exchanges to go through.

#### In the periphery contract (UniswapV2Router02.sol)

  3. Identify the amounts that need to be traded on each exchange along the path.
  4. Iterates over the path. For every exchange along the way it sends the input token and then calls the exchange's `swap` function. In most cases the destination address for the tokens is the next pair exchange in the path. In the final exchange it is the address provided by the trader.

#### In the core contract (UniswapV2Pair.sol)

  5. Verify that the core contract is not being cheated and can maintain sufficient liquidity after the swap.
  6. See how many extra tokens we have in addition to the known reserves. That amount is the number of input tokens we received to exchange.
  7. Send the output tokens to the destination.
  8. Call `_update` to update the reserve amounts

#### Back in the periphery contract (UniswapV2Router02.sol)

  9. Perform any necessary cleanup (for example, burn WETH tokens to get back ETH to send the trader)

### Add Liquidity

#### Caller

  1. Provide the periphery account with an allowance in the amounts to be added to the liquidity pool.
  2. Call one of the periphery contract's `addLiquidity` functions.

#### In the periphery contract (UniswapV2Router02.sol)

  3. Create a new pair exchange if necessary
  4. If there is an existing pair exchange, calculate the amount of tokens to add. This is supposed to be identical value for both tokens, so the same ratio of new tokens to existing tokens.
  5. Check if the amounts are acceptable (callers can specify a minimum amount below which they'd rather not add liquidity)
  6. Call the core contract.

#### In the core contract (UniswapV2Pair.sol)

  7. Mint liquidity tokens and send them to the caller
  8. Call `_update` to update the reserve amounts

### Remove Liquidity

#### Caller

  1. Provide the periphery account with an allowance of liquidity tokens to be burned in exchange for the underlying tokens.
  2. Call one of the periphery contract's `removeLiquidity` functions.

#### In the periphery contract (UniswapV2Router02.sol)

  3. Send the liquidity tokens to the pair exchange

#### In the core contract (UniswapV2Pair.sol)

  4. Send the destination address the underlying tokens in proportion to the burned tokens. For example if there are 1000 A tokens in the pool, 500 B tokens, and 90 liquidity tokens, and we receive 9 tokens to burn, we're burning 10% of the liquidity tokens so we send back the user 100 A tokens and 50 B tokens.
  5. Burn the liquidity tokens
  6. Call `_update` to update the reserve amounts

## The Core Contracts

These are the secure contracts which hold the liquidity.

### UniswapV2Pair.sol

[This contract(opens in a new
tab)](https://github.com/Uniswap/uniswap-v2-core/blob/master/contracts/UniswapV2Pair.sol)
implements the actual pool that exchanges tokens. It is the core Uniswap
functionality.

    
    
    1pragma solidity =0.5.16;
    
    2
    
    3import './interfaces/IUniswapV2Pair.sol';
    
    4import './UniswapV2ERC20.sol';
    
    5import './libraries/Math.sol';
    
    6import './libraries/UQ112x112.sol';
    
    7import './interfaces/IERC20.sol';
    
    8import './interfaces/IUniswapV2Factory.sol';
    
    9import './interfaces/IUniswapV2Callee.sol';
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

These are all the interfaces that the contract needs to know about, either
because the contract implements them (`IUniswapV2Pair` and `UniswapV2ERC20`)
or because it calls contracts that implement them.

    
    
    1contract UniswapV2Pair is IUniswapV2Pair, UniswapV2ERC20 {
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

This contract inherits from `UniswapV2ERC20`, which provides the ERC-20
functions for the liquidity tokens.

    
    
    1    using SafeMath  for uint;
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

The [SafeMath library(opens in a new
tab)](https://docs.openzeppelin.com/contracts/2.x/api/math) is used to avoid
overflows and underflows. This is important because otherwise we might end up
with a situation where a value should be `-1`, but is instead `2^256-1`.

    
    
    1    using UQ112x112 for uint224;
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

A lot of calculations in the pool contract require fractions. However,
fractions are not supported by the EVM. The solution that Uniswap found is to
use 224 bit values, with 112 bits for the integer part, and 112 bits for the
fraction. So `1.0` is represented as `2^112`, `1.5` is represented as `2^112 +
2^111`, etc.

More details about this library are available later in the document.

#### Variables

    
    
    1    uint public constant MINIMUM_LIQUIDITY = 10**3;
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

To avoid cases of division by zero, there is a minimum number of liquidity
tokens that always exist (but are owned by account zero). That number is
**MINIMUM_LIQUIDITY** , a thousand.

    
    
    1    bytes4 private constant SELECTOR = bytes4(keccak256(bytes('transfer(address,uint256)')));
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

This is the ABI selector for the ERC-20 transfer function. It is used to
transfer ERC-20 tokens in the two token accounts.

    
    
    1    address public factory;
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

This is the factory contract that created this pool. Every pool is an exchange
between two ERC-20 tokens, the factory is a central point that connects all of
these pools.

    
    
    1    address public token0;
    
    2    address public token1;
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

There are the addresses of the contracts for the two types of ERC-20 tokens
that can be exchanged by this pool.

    
    
    1    uint112 private reserve0;           // uses single storage slot, accessible via getReserves
    
    2    uint112 private reserve1;           // uses single storage slot, accessible via getReserves
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

The reserves the pool has for each token type. We assume that the two
represent the same amount of value, and therefore each token0 is worth
reserve1/reserve0 token1's.

    
    
    1    uint32  private blockTimestampLast; // uses single storage slot, accessible via getReserves
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

The timestamp for the last block in which an exchange occurred, used to track
exchange rates across time.

One of the biggest gas expenses of Ethereum contracts is storage, which
persists from one call of the contract to the next. Each storage cell is 256
bits long. So three variables, `reserve0`, `reserve1`, and
`blockTimestampLast`, are allocated in such a way a single storage value can
include all three of them (112+112+32=256).

    
    
    1    uint public price0CumulativeLast;
    
    2    uint public price1CumulativeLast;
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

These variables hold the cumulative costs for each token (each in term of the
other). They can be used to calculate the average exchange rate over a period
of time.

    
    
    1    uint public kLast; // reserve0 * reserve1, as of immediately after the most recent liquidity event
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

The way the pair exchange decides on the exchange rate between token0 and
token1 is to keep the multiple of the two reserves constant during trades.
`kLast` is this value. It changes when a liquidity provider deposits or
withdraws tokens, and it increases slightly because of the 0.3% market fee.

Here is a simple example. Note that for the sake of simplicity the table only
has three digits after the decimal point, and we ignore the 0.3% trading fee
so the numbers are not accurate.

Event| reserve0| reserve1| reserve0 * reserve1| Average exchange rate (token1
/ token0)  
---|---|---|---|---  
Initial setup| 1,000.000| 1,000.000| 1,000,000|  
Trader A swaps 50 token0 for 47.619 token1| 1,050.000| 952.381| 1,000,000|
0.952  
Trader B swaps 10 token0 for 8.984 token1| 1,060.000| 943.396| 1,000,000|
0.898  
Trader C swaps 40 token0 for 34.305 token1| 1,100.000| 909.090| 1,000,000|
0.858  
Trader D swaps 100 token1 for 109.01 token0| 990.990| 1,009.090| 1,000,000|
0.917  
Trader E swaps 10 token0 for 10.079 token1| 1,000.990| 999.010| 1,000,000|
1.008  
  
As traders provide more of token0, the relative value of token1 increases, and
vice versa, based on supply and demand.

#### Lock

    
    
    1    uint private unlocked = 1;
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

There is a class of security vulnerabilities that are based on [reentrancy
abuse(opens in a new tab)](https://medium.com/coinmonks/ethernaut-lvl-10-re-
entrancy-walkthrough-how-to-abuse-execution-ordering-and-reproduce-the-
dao-7ec88b912c14). Uniswap needs to transfer arbitrary ERC-20 tokens, which
means calling ERC-20 contracts that may attempt to abuse the Uniswap market
that calls them. By having an `unlocked` variable as part of the contract, we
can prevent functions from being called while they are running (within the
same transaction).

    
    
    1    modifier lock() {
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

This function is a [modifier(opens in a new
tab)](https://docs.soliditylang.org/en/v0.8.3/contracts.html#function-
modifiers), a function that wraps around a normal function to change its
behavior is some way.

    
    
    1        require(unlocked == 1, 'UniswapV2: LOCKED');
    
    2        unlocked = 0;
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

If `unlocked` is equal to one, set it to zero. If it is already zero revert
the call, make it fail.

    
    
    1        _;
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

In a modifier `_;` is the original function call (with all the parameters).
Here it means that the function call only happens if `unlocked` was one when
it was called, and while it is running the value of `unlocked` is zero.

    
    
    1        unlocked = 1;
    
    2    }
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

After the main function returns, release the lock.

#### Misc. functions

    
    
    1    function getReserves() public view returns (uint112 _reserve0, uint112 _reserve1, uint32 _blockTimestampLast) {
    
    2        _reserve0 = reserve0;
    
    3        _reserve1 = reserve1;
    
    4        _blockTimestampLast = blockTimestampLast;
    
    5    }
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

This function provides callers with the current state of the exchange. Notice
that Solidity functions [can return multiple values(opens in a new
tab)](https://docs.soliditylang.org/en/v0.8.3/contracts.html#returning-
multiple-values).

    
    
    1    function _safeTransfer(address token, address to, uint value) private {
    
    2        (bool success, bytes memory data) = token.call(abi.encodeWithSelector(SELECTOR, to, value));
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

This internal function transfers an amount of ERC20 tokens from the exchange
to somebody else. `SELECTOR` specifies that the function we are calling is
`transfer(address,uint)` (see definition above).

To avoid having to import an interface for the token function, we "manually"
create the call using one of the [ABI functions(opens in a new
tab)](https://docs.soliditylang.org/en/v0.8.3/units-and-global-
variables.html#abi-encoding-and-decoding-functions).

    
    
    1        require(success && (data.length == 0 || abi.decode(data, (bool))), 'UniswapV2: TRANSFER_FAILED');
    
    2    }
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

There are two ways in which an ERC-20 transfer call can report failure:

  1. Revert. If a call to an external contract reverts, then the boolean return value is `false`
  2. End normally but report a failure. In that case the return value buffer has a non-zero length, and when decoded as a boolean value it is `false`

If either of these conditions happen, revert.

#### Events

    
    
    1    event Mint(address indexed sender, uint amount0, uint amount1);
    
    2    event Burn(address indexed sender, uint amount0, uint amount1, address indexed to);
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

These two events are emitted when a liquidity provider either deposits
liquidity (`Mint`) or withdraws it (`Burn`). In either case, the amounts of
token0 and token1 that are deposited or withdrawn are part of the event, as
well as the identity of the account that called us (`sender`). In the case of
a withdrawal, the event also includes the target that received the tokens
(`to`), which may not be the same as the sender.

    
    
    1    event Swap(
    
    2        address indexed sender,
    
    3        uint amount0In,
    
    4        uint amount1In,
    
    5        uint amount0Out,
    
    6        uint amount1Out,
    
    7        address indexed to
    
    8    );
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

This event is emitted when a trader swaps one token for the other. Again, the
sender and the destination may not be the same. Each token may be either sent
to the exchange, or received from it.

    
    
    1    event Sync(uint112 reserve0, uint112 reserve1);
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Finally, `Sync` is emitted every time tokens are added or withdrawn,
regardless of the reason, to provide the latest reserve information (and
therefore the exchange rate).

#### Setup Functions

These functions are supposed to be called once when the new pair exchange is
set up.

    
    
    1    constructor() public {
    
    2        factory = msg.sender;
    
    3    }
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

The constructor makes sure we'll keep track of the address of the factory that
created the pair. This information is required for `initialize` and for the
factory fee (if one exists)

    
    
    1    // called once by the factory at time of deployment
    
    2    function initialize(address _token0, address _token1) external {
    
    3        require(msg.sender == factory, 'UniswapV2: FORBIDDEN'); // sufficient check
    
    4        token0 = _token0;
    
    5        token1 = _token1;
    
    6    }
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

This function allows the factory (and only the factory) to specify the two
ERC-20 tokens that this pair will exchange.

#### Internal Update Functions

##### _update

    
    
    1    // update reserves and, on the first call per block, price accumulators
    
    2    function _update(uint balance0, uint balance1, uint112 _reserve0, uint112 _reserve1) private {
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

This function is called every time tokens are deposited or withdrawn.

    
    
    1        require(balance0 <= uint112(-1) && balance1 <= uint112(-1), 'UniswapV2: OVERFLOW');
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

If either balance0 or balance1 (uint256) is higher than uint112(-1) (=2^112-1)
(so it overflows & wraps back to 0 when converted to uint112) refuse to
continue the _update to prevent overflows. With a normal token that can be
subdivided into 10^18 units, this means each exchange is limited to about
5.1*10^15 of each tokens. So far that has not been a problem.

    
    
    1        uint32 blockTimestamp = uint32(block.timestamp % 2**32);
    
    2        uint32 timeElapsed = blockTimestamp - blockTimestampLast; // overflow is desired
    
    3        if (timeElapsed > 0 && _reserve0 != 0 && _reserve1 != 0) {
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

If the time elapsed is not zero, it means we are the first exchange
transaction on this block. In that case, we need to update the cost
accumulators.

    
    
    1            // * never overflows, and + overflow is desired
    
    2            price0CumulativeLast += uint(UQ112x112.encode(_reserve1).uqdiv(_reserve0)) * timeElapsed;
    
    3            price1CumulativeLast += uint(UQ112x112.encode(_reserve0).uqdiv(_reserve1)) * timeElapsed;
    
    4        }
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Each cost accumulator is updated with the latest cost (reserve of the other
token/reserve of this token) times the elapsed time in seconds. To get an
average price, you read the cumulative price in two points in time and divide
by the time difference between them. For example, assume this sequence of
events:

Event| reserve0| reserve1| timestamp| Marginal exchange rate (reserve1 /
reserve0)| price0CumulativeLast  
---|---|---|---|---|---  
Initial setup| 1,000.000| 1,000.000| 5,000| 1.000| 0  
Trader A deposits 50 token0 and gets 47.619 token1 back| 1,050.000| 952.381|
5,020| 0.907| 20  
Trader B deposits 10 token0 and gets 8.984 token1 back| 1,060.000| 943.396|
5,030| 0.890| 20+10*0.907 = 29.07  
Trader C deposits 40 token0 and gets 34.305 token1 back| 1,100.000| 909.090|
5,100| 0.826| 29.07+70*0.890 = 91.37  
Trader D deposits 100 token1 and gets 109.01 token0 back| 990.990| 1,009.090|
5,110| 1.018| 91.37+10*0.826 = 99.63  
Trader E deposits 10 token0 and gets 10.079 token1 back| 1,000.990| 999.010|
5,150| 0.998| 99.63+40*1.1018 = 143.702  
  
Let's say we want to calculate the average price of **Token0** between the
timestamps 5,030 and 5,150. The difference in the value of `price0Cumulative`
is 143.702-29.07=114.632. This is the average across two minutes (120
seconds). So the average price is 114.632/120 = 0.955.

This price calculation is the reason we need to know the old reserve sizes.

    
    
    1        reserve0 = uint112(balance0);
    
    2        reserve1 = uint112(balance1);
    
    3        blockTimestampLast = blockTimestamp;
    
    4        emit Sync(reserve0, reserve1);
    
    5    }
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Finally, update the global variables and emit a `Sync` event.

##### _mintFee

    
    
    1    // if fee is on, mint liquidity equivalent to 1/6th of the growth in sqrt(k)
    
    2    function _mintFee(uint112 _reserve0, uint112 _reserve1) private returns (bool feeOn) {
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

In Uniswap 2.0 traders pay a 0.30% fee to use the market. Most of that fee
(0.25% of the trade) always goes to the liquidity providers. The remaining
0.05% can go either to the liquidity providers or to an address specified by
the factory as a protocol fee, which pays Uniswap for their development
effort.

To reduce calculations (and therefore gas costs), this fee is only calculated
when liquidity is added or removed from the pool, rather than at each
transaction.

    
    
    1        address feeTo = IUniswapV2Factory(factory).feeTo();
    
    2        feeOn = feeTo != address(0);
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Read the fee destination of the factory. If it is zero then there is no
protocol fee and no need to calculate it that fee.

    
    
    1        uint _kLast = kLast; // gas savings
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

The `kLast` state variable is located in storage, so it will have a value
between different calls to the contract. Access to storage is a lot more
expensive than access to the volatile memory that is released when the
function call to the contract ends, so we use an internal variable to save on
gas.

    
    
    1        if (feeOn) {
    
    2            if (_kLast != 0) {
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

The liquidity providers get their cut simply by the appreciation of their
liquidity tokens. But the protocol fee requires new liquidity tokens to be
minted and provided to the `feeTo` address.

    
    
    1                uint rootK = Math.sqrt(uint(_reserve0).mul(_reserve1));
    
    2                uint rootKLast = Math.sqrt(_kLast);
    
    3                if (rootK > rootKLast) {
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

If there is new liquidity on which to collect a protocol fee. You can see the
square root function later in this article

    
    
    1                    uint numerator = totalSupply.mul(rootK.sub(rootKLast));
    
    2                    uint denominator = rootK.mul(5).add(rootKLast);
    
    3                    uint liquidity = numerator / denominator;
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

This complicated calculation of fees is explained in [the whitepaper(opens in
a new tab)](https://uniswap.org/whitepaper.pdf) on page 5. We know that
between the time `kLast` was calculated and the present no liquidity was added
or removed (because we run this calculation every time liquidity is added or
removed, before it actually changes), so any change in `reserve0 * reserve1`
has to come from transaction fees (without them we'd keep `reserve0 *
reserve1` constant).

    
    
    1                    if (liquidity > 0) _mint(feeTo, liquidity);
    
    2                }
    
    3            }
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Use the `UniswapV2ERC20._mint` function to actually create the additional
liquidity tokens and assign them to `feeTo`.

    
    
    1        } else if (_kLast != 0) {
    
    2            kLast = 0;
    
    3        }
    
    4    }
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

If there is no fee set `kLast` to zero (if it isn't that already). When this
contract was written there was a [gas refund feature(opens in a new
tab)](https://eips.ethereum.org/EIPS/eip-3298) that encouraged contracts to
reduce the overall size of the Ethereum state by zeroing out storage they did
not need. This code gets that refund when possible.

#### Externally Accessible Functions

Note that while any transaction or contract _can_ call these functions, they
are designed to be called from the periphery contract. If you call them
directly you won't be able to cheat the pair exchange, but you might lose
value through a mistake.

##### mint

    
    
    1    // this low-level function should be called from a contract which performs important safety checks
    
    2    function mint(address to) external lock returns (uint liquidity) {
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

This function is called when a liquidity provider adds liquidity to the pool.
It mints additional liquidity tokens as a reward. It should be called from a
periphery contract that calls it after adding the liquidity in the same
transaction (so nobody else would be able to submit a transaction that claims
the new liquidity before the legitimate owner).

    
    
    1        (uint112 _reserve0, uint112 _reserve1,) = getReserves(); // gas savings
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

This is the way to read the results of a Solidity function that returns
multiple values. We discard the last returned values, the block timestamp,
because we don't need it.

    
    
    1        uint balance0 = IERC20(token0).balanceOf(address(this));
    
    2        uint balance1 = IERC20(token1).balanceOf(address(this));
    
    3        uint amount0 = balance0.sub(_reserve0);
    
    4        uint amount1 = balance1.sub(_reserve1);
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Get the current balances and see how much was added of each token type.

    
    
    1        bool feeOn = _mintFee(_reserve0, _reserve1);
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Calculate the protocol fees to collect, if any, and mint liquidity tokens
accordingly. Because the parameters to `_mintFee` are the old reserve values,
the fee is calculated accurately based only on pool changes due to fees.

    
    
    1        uint _totalSupply = totalSupply; // gas savings, must be defined here since totalSupply can update in _mintFee
    
    2        if (_totalSupply == 0) {
    
    3            liquidity = Math.sqrt(amount0.mul(amount1)).sub(MINIMUM_LIQUIDITY);
    
    4           _mint(address(0), MINIMUM_LIQUIDITY); // permanently lock the first MINIMUM_LIQUIDITY tokens
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

If this is the first deposit, create `MINIMUM_LIQUIDITY` tokens and send them
to address zero to lock them. They can never be redeemed, which means the pool
will never be emptied completely (this saves us from division by zero in some
places). The value of `MINIMUM_LIQUIDITY` is a thousand, which considering
most ERC-20 are subdivided into units of 10^-18'th of a token, as ETH is
divided into wei, is 10^-15 to the value of a single token. Not a high cost.

In the time of the first deposit we don't know the relative value of the two
tokens, so we just multiply the amounts and take a square root, assuming that
the deposit provides us with equal value in both tokens.

We can trust this because it is in the depositor's interest to provide equal
value, to avoid losing value to arbitrage. Let's say that the value of the two
tokens is identical, but our depositor deposited four times as many of
**Token1** as of **Token0**. A trader can use the fact the pair exchange
thinks that **Token0** is more valuable to extract value out of it.

Event| reserve0| reserve1| reserve0 * reserve1| Value of the pool (reserve0 +
reserve1)  
---|---|---|---|---  
Initial setup| 8| 32| 256| 40  
Trader deposits 8 **Token0** tokens, gets back 16 **Token1**|  16| 16| 256| 32  
  
As you can see, the trader earned an extra 8 tokens, which come from a
reduction in the value of the pool, hurting the depositor that owns it.

    
    
    1        } else {
    
    2            liquidity = Math.min(amount0.mul(_totalSupply) / _reserve0, amount1.mul(_totalSupply) / _reserve1);
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

With every subsequent deposit we already know the exchange rate between the
two assets, and we expect liquidity providers to provide equal value in both.
If they don't, we give them liquidity tokens based on the lesser value they
provided as a punishment.

Whether it is the initial deposit or a subsequent one, the number of liquidity
tokens we provide is equal to the square root of the change in
`reserve0*reserve1` and the value of the liquidity token doesn't change
(unless we get a deposit that doesn't have equal values of both types, in
which case the "fine" gets distributed). Here is another example with two
tokens that have the same value, with three good deposits and one bad one
(deposit of only one token type, so it doesn't produce any liquidity tokens).

Event| reserve0| reserve1| reserve0 * reserve1| Pool value (reserve0 +
reserve1)| Liquidity tokens minted for this deposit| Total liquidity tokens|
value of each liquidity token  
---|---|---|---|---|---|---|---  
Initial setup| 8.000| 8.000| 64| 16.000| 8| 8| 2.000  
Deposit four of each type| 12.000| 12.000| 144| 24.000| 4| 12| 2.000  
Deposit two of each type| 14.000| 14.000| 196| 28.000| 2| 14| 2.000  
Unequal value deposit| 18.000| 14.000| 252| 32.000| 0| 14| ~2.286  
After arbitrage| ~15.874| ~15.874| 252| ~31.748| 0| 14| ~2.267  
      
    
    1        }
    
    2        require(liquidity > 0, 'UniswapV2: INSUFFICIENT_LIQUIDITY_MINTED');
    
    3        _mint(to, liquidity);
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Use the `UniswapV2ERC20._mint` function to actually create the additional
liquidity tokens and give them to the correct account.

    
    
    1
    
    2        _update(balance0, balance1, _reserve0, _reserve1);
    
    3        if (feeOn) kLast = uint(reserve0).mul(reserve1); // reserve0 and reserve1 are up-to-date
    
    4        emit Mint(msg.sender, amount0, amount1);
    
    5    }
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Update the state variables (`reserve0`, `reserve1`, and if needed `kLast`) and
emit the appropriate event.

##### burn

    
    
    1    // this low-level function should be called from a contract which performs important safety checks
    
    2    function burn(address to) external lock returns (uint amount0, uint amount1) {
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

This function is called when liquidity is withdrawn and the appropriate
liquidity tokens need to be burned. It should also be called from a periphery
account.

    
    
    1        (uint112 _reserve0, uint112 _reserve1,) = getReserves(); // gas savings
    
    2        address _token0 = token0;                                // gas savings
    
    3        address _token1 = token1;                                // gas savings
    
    4        uint balance0 = IERC20(_token0).balanceOf(address(this));
    
    5        uint balance1 = IERC20(_token1).balanceOf(address(this));
    
    6        uint liquidity = balanceOf[address(this)];
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

The periphery contract transferred the liquidity to be burned to this contract
before the call. That way we know how much liquidity to burn, and we can make
sure that it gets burned.

    
    
    1        bool feeOn = _mintFee(_reserve0, _reserve1);
    
    2        uint _totalSupply = totalSupply; // gas savings, must be defined here since totalSupply can update in _mintFee
    
    3        amount0 = liquidity.mul(balance0) / _totalSupply; // using balances ensures pro-rata distribution
    
    4        amount1 = liquidity.mul(balance1) / _totalSupply; // using balances ensures pro-rata distribution
    
    5        require(amount0 > 0 && amount1 > 0, 'UniswapV2: INSUFFICIENT_LIQUIDITY_BURNED');
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

The liquidity provider receives equal value of both tokens. This way we don't
change the exchange rate.

    
    
    1        _burn(address(this), liquidity);
    
    2        _safeTransfer(_token0, to, amount0);
    
    3        _safeTransfer(_token1, to, amount1);
    
    4        balance0 = IERC20(_token0).balanceOf(address(this));
    
    5        balance1 = IERC20(_token1).balanceOf(address(this));
    
    6
    
    7        _update(balance0, balance1, _reserve0, _reserve1);
    
    8        if (feeOn) kLast = uint(reserve0).mul(reserve1); // reserve0 and reserve1 are up-to-date
    
    9        emit Burn(msg.sender, amount0, amount1, to);
    
    10    }
    
    11
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

The rest of the `burn` function is the mirror image of the `mint` function
above.

##### swap

    
    
    1    // this low-level function should be called from a contract which performs important safety checks
    
    2    function swap(uint amount0Out, uint amount1Out, address to, bytes calldata data) external lock {
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

This function is also supposed to be called from a periphery contract.

    
    
    1        require(amount0Out > 0 || amount1Out > 0, 'UniswapV2: INSUFFICIENT_OUTPUT_AMOUNT');
    
    2        (uint112 _reserve0, uint112 _reserve1,) = getReserves(); // gas savings
    
    3        require(amount0Out < _reserve0 && amount1Out < _reserve1, 'UniswapV2: INSUFFICIENT_LIQUIDITY');
    
    4
    
    5        uint balance0;
    
    6        uint balance1;
    
    7        { // scope for _token{0,1}, avoids stack too deep errors
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Local variables can be stored either in memory or, if there aren't too many of
them, directly on the stack. If we can limit the number so we'll use the stack
we use less gas. For more details see [the yellow paper, the formal Ethereum
specifications(opens in a new
tab)](https://ethereum.github.io/yellowpaper/paper.pdf), p. 26, equation 298.

    
    
    1            address _token0 = token0;
    
    2            address _token1 = token1;
    
    3            require(to != _token0 && to != _token1, 'UniswapV2: INVALID_TO');
    
    4            if (amount0Out > 0) _safeTransfer(_token0, to, amount0Out); // optimistically transfer tokens
    
    5            if (amount1Out > 0) _safeTransfer(_token1, to, amount1Out); // optimistically transfer tokens
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

This transfer is optimistic, because we transfer before we are sure all the
conditions are met. This is OK in Ethereum because if the conditions aren't
met later in the call we revert out of it and any changes it created.

    
    
    1            if (data.length > 0) IUniswapV2Callee(to).uniswapV2Call(msg.sender, amount0Out, amount1Out, data);
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Inform the receiver about the swap if requested.

    
    
    1            balance0 = IERC20(_token0).balanceOf(address(this));
    
    2            balance1 = IERC20(_token1).balanceOf(address(this));
    
    3        }
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Get the current balances. The periphery contract sends us the tokens before
calling us for the swap. This makes it easy for the contract to check that it
is not being cheated, a check that _has_ to happen in the core contract
(because we can be called by other entities than our periphery contract).

    
    
    1        uint amount0In = balance0 > _reserve0 - amount0Out ? balance0 - (_reserve0 - amount0Out) : 0;
    
    2        uint amount1In = balance1 > _reserve1 - amount1Out ? balance1 - (_reserve1 - amount1Out) : 0;
    
    3        require(amount0In > 0 || amount1In > 0, 'UniswapV2: INSUFFICIENT_INPUT_AMOUNT');
    
    4        { // scope for reserve{0,1}Adjusted, avoids stack too deep errors
    
    5            uint balance0Adjusted = balance0.mul(1000).sub(amount0In.mul(3));
    
    6            uint balance1Adjusted = balance1.mul(1000).sub(amount1In.mul(3));
    
    7            require(balance0Adjusted.mul(balance1Adjusted) >= uint(_reserve0).mul(_reserve1).mul(1000**2), 'UniswapV2: K');
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

This is a sanity check to make sure we don't lose from the swap. There is no
circumstance in which a swap should reduce `reserve0*reserve1`. This is also
where we ensure a fee of 0.3% is being sent on the swap; before sanity
checking the value of K, we multiply both balances by 1000 subtracted by the
amounts multiplied by 3, this means 0.3% (3/1000 = 0.003 = 0.3%) is being
deducted from the balance before comparing its K value with the current
reserves K value.

    
    
    1        }
    
    2
    
    3        _update(balance0, balance1, _reserve0, _reserve1);
    
    4        emit Swap(msg.sender, amount0In, amount1In, amount0Out, amount1Out, to);
    
    5    }
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Update `reserve0` and `reserve1`, and if necessary the price accumulators and
the timestamp and emit an event.

##### Sync or Skim

It is possible for the real balances to get out of sync with the reserves that
the pair exchange thinks it has. There is no way to withdraw tokens without
the contract's consent, but deposits are a different matter. An account can
transfer tokens to the exchange without calling either `mint` or `swap`.

In that case there are two solutions:

  * `sync`, update the reserves to the current balances
  * `skim`, withdraw the extra amount. Note that any account is allowed to call `skim` because we don't know who deposited the tokens. This information is emitted in an event, but events are not accessible from the blockchain.

    
    
    1    // force balances to match reserves
    
    2    function skim(address to) external lock {
    
    3        address _token0 = token0; // gas savings
    
    4        address _token1 = token1; // gas savings
    
    5        _safeTransfer(_token0, to, IERC20(_token0).balanceOf(address(this)).sub(reserve0));
    
    6        _safeTransfer(_token1, to, IERC20(_token1).balanceOf(address(this)).sub(reserve1));
    
    7    }
    
    8
    
    9
    
    10
    
    11    // force reserves to match balances
    
    12    function sync() external lock {
    
    13        _update(IERC20(token0).balanceOf(address(this)), IERC20(token1).balanceOf(address(this)), reserve0, reserve1);
    
    14    }
    
    15}
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

### UniswapV2Factory.sol

[This contract(opens in a new
tab)](https://github.com/Uniswap/uniswap-v2-core/blob/master/contracts/UniswapV2Factory.sol)
creates the pair exchanges.

    
    
    1pragma solidity =0.5.16;
    
    2
    
    3import './interfaces/IUniswapV2Factory.sol';
    
    4import './UniswapV2Pair.sol';
    
    5
    
    6contract UniswapV2Factory is IUniswapV2Factory {
    
    7    address public feeTo;
    
    8    address public feeToSetter;
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

These state variables are necessary to implement the protocol fee (see [the
whitepaper(opens in a new tab)](https://uniswap.org/whitepaper.pdf), p. 5).
The `feeTo` address accumulates the liquidity tokens for the protocol fee, and
`feeToSetter` is the address allowed to change `feeTo` to a different address.

    
    
    1    mapping(address => mapping(address => address)) public getPair;
    
    2    address[] public allPairs;
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

These variables keep track of the pairs, the exchanges between two token
types.

The first one, `getPair`, is a mapping that identifies a pair exchange
contract based on the two ERC-20 tokens it exchanges. ERC-20 tokens are
identified by the addresses of the contracts that implement them, so the keys
and the value are all addresses. To get the address of the pair exchange that
lets you convert from `tokenA` to `tokenB`, you use `getPair[<tokenA
address>][<tokenB address>]` (or the other way around).

The second variable, `allPairs`, is an array that includes all the addresses
of pair exchanges created by this factory. In Ethereum you cannot iterate over
the content of a mapping, or get a list of all the keys, so this variable is
the only way to know which exchanges this factory manages.

Note: The reason you cannot iterate over all the keys of a mapping is that
contract data storage is _expensive_ , so the less of it we use the better,
and the less often we change it the better. You can create [mappings that
support iteration(opens in a new tab)](https://github.com/ethereum/dapp-
bin/blob/master/library/iterable_mapping.sol), but they require extra storage
for a list of keys. In most applications you do not need that.

    
    
    1    event PairCreated(address indexed token0, address indexed token1, address pair, uint);
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

This event is emitted when a new pair exchange is created. It includes the
tokens' addresses, the pair exchange's address, and the total number of
exchanges managed by the factory.

    
    
    1    constructor(address _feeToSetter) public {
    
    2        feeToSetter = _feeToSetter;
    
    3    }
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

The only thing the constructor does is specify the `feeToSetter`. Factories
start without a fee, and only `feeSetter` can change that.

    
    
    1    function allPairsLength() external view returns (uint) {
    
    2        return allPairs.length;
    
    3    }
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

This function returns the number of exchange pairs.

    
    
    1    function createPair(address tokenA, address tokenB) external returns (address pair) {
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

This is the main function of the factory, to create a pair exchange between
two ERC-20 tokens. Note that anybody can call this function. You do not need
permission from Uniswap to create a new pair exchange.

    
    
    1        require(tokenA != tokenB, 'UniswapV2: IDENTICAL_ADDRESSES');
    
    2        (address token0, address token1) = tokenA < tokenB ? (tokenA, tokenB) : (tokenB, tokenA);
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

We want the address of the new exchange to be deterministic, so it can be
calculated in advance off chain (this can be useful for [layer 2
transactions](/en/developers/docs/scaling/)). To do this we need to have a
consistent order of the token addresses, regardless of the order in which we
have received them, so we sort them here.

    
    
    1        require(token0 != address(0), 'UniswapV2: ZERO_ADDRESS');
    
    2        require(getPair[token0][token1] == address(0), 'UniswapV2: PAIR_EXISTS'); // single check is sufficient
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Large liquidity pools are better than small ones, because they have more
stable prices. We don't want to have more than a single liquidity pool per
pair of tokens. If there is already an exchange, there's no need to create
another one for the same pair.

    
    
    1        bytes memory bytecode = type(UniswapV2Pair).creationCode;
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

To create a new contract we need the code that creates it (both the
constructor function and code that writes to memory the EVM bytecode of the
actual contract). Normally in Solidity we just use `addr = new <name of
contract>(<constructor parameters>)` and the compiler takes care of everything
for us, but to have a deterministic contract address we need to use [the
CREATE2 opcode(opens in a new tab)](https://eips.ethereum.org/EIPS/eip-1014).
When this code was written that opcode was not yet supported by Solidity, so
it was necessary to manually get the code. This is no longer an issue, because
[Solidity now supports CREATE2(opens in a new
tab)](https://docs.soliditylang.org/en/v0.8.3/control-structures.html#salted-
contract-creations-create2).

    
    
    1        bytes32 salt = keccak256(abi.encodePacked(token0, token1));
    
    2        assembly {
    
    3            pair := create2(0, add(bytecode, 32), mload(bytecode), salt)
    
    4        }
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

When an opcode is not supported by Solidity yet we can call it using [inline
assembly(opens in a new
tab)](https://docs.soliditylang.org/en/v0.8.3/assembly.html).

    
    
    1        IUniswapV2Pair(pair).initialize(token0, token1);
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Call the `initialize` function to tell the new exchange what two tokens it
exchanges.

    
    
    1        getPair[token0][token1] = pair;
    
    2        getPair[token1][token0] = pair; // populate mapping in the reverse direction
    
    3        allPairs.push(pair);
    
    4        emit PairCreated(token0, token1, pair, allPairs.length);
    
    5    }
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Save the new pair information in the state variables and emit an event to
inform the world of the new pair exchange.

    
    
    1    function setFeeTo(address _feeTo) external {
    
    2        require(msg.sender == feeToSetter, 'UniswapV2: FORBIDDEN');
    
    3        feeTo = _feeTo;
    
    4    }
    
    5
    
    6    function setFeeToSetter(address _feeToSetter) external {
    
    7        require(msg.sender == feeToSetter, 'UniswapV2: FORBIDDEN');
    
    8        feeToSetter = _feeToSetter;
    
    9    }
    
    10}
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

These two functions allow `feeSetter` to control the fee recipient (if any),
and to change `feeSetter` to a new address.

### UniswapV2ERC20.sol

[This contract(opens in a new
tab)](https://github.com/Uniswap/uniswap-v2-core/blob/master/contracts/UniswapV2ERC20.sol)
implements the ERC-20 liquidity token. It is similar to the [OpenZeppelin
ERC-20 contract](/en/developers/tutorials/erc20-annotated-code/), so I will
only explain the part that is different, the `permit` functionality.

Transactions on Ethereum cost ether (ETH), which is equivalent to real money.
If you have ERC-20 tokens but not ETH, you can't send transactions, so you
can't do anything with them. One solution to avoid this problem is [meta-
transactions(opens in a new
tab)](https://docs.uniswap.org/contracts/v2/guides/smart-contract-
integration/supporting-meta-transactions). The owner of the tokens signs a
transaction that allows somebody else to withdraw tokens off chain and sends
it using the Internet to the recipient. The recipient, which does have ETH,
then submits the permit on behalf of the owner.

    
    
    1    bytes32 public DOMAIN_SEPARATOR;
    
    2    // keccak256("Permit(address owner,address spender,uint256 value,uint256 nonce,uint256 deadline)");
    
    3    bytes32 public constant PERMIT_TYPEHASH = 0x6e71edae12b1b97f4d1f60370fef10105fa2faae0126114a169c64845d6126c9;
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

This hash is the [identifier for the transaction type(opens in a new
tab)](https://eips.ethereum.org/EIPS/eip-712#rationale-for-typehash). The only
one we support here is `Permit` with these parameters.

    
    
    1    mapping(address => uint) public nonces;
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

It is not feasible for a recipient to fake a digital signature. However, it is
trivial to send the same transaction twice (this is a form of [replay
attack(opens in a new tab)](https://wikipedia.org/wiki/Replay_attack)). To
prevent this, we use a [nonce(opens in a new
tab)](https://wikipedia.org/wiki/Cryptographic_nonce). If the nonce of a new
`Permit` is not one more than the last one used, we assume it is invalid.

    
    
    1    constructor() public {
    
    2        uint chainId;
    
    3        assembly {
    
    4            chainId := chainid
    
    5        }
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

This is the code to retrieve the [chain identifier(opens in a new
tab)](https://chainid.network/). It uses an EVM assembly dialect called
[Yul(opens in a new tab)](https://docs.soliditylang.org/en/v0.8.4/yul.html).
Note that in the current version of Yul you have to use `chainid()`, not
`chainid`.

    
    
    1        DOMAIN_SEPARATOR = keccak256(
    
    2            abi.encode(
    
    3                keccak256('EIP712Domain(string name,string version,uint256 chainId,address verifyingContract)'),
    
    4                keccak256(bytes(name)),
    
    5                keccak256(bytes('1')),
    
    6                chainId,
    
    7                address(this)
    
    8            )
    
    9        );
    
    10    }
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Calculate the [domain separator(opens in a new
tab)](https://eips.ethereum.org/EIPS/eip-712#rationale-for-domainseparator)
for EIP-712.

    
    
    1    function permit(address owner, address spender, uint value, uint deadline, uint8 v, bytes32 r, bytes32 s) external {
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

This is the function that implements the permissions. It receives as
parameters the relevant fields, and the three scalar values for [the
signature(opens in a new tab)](https://yos.io/2018/11/16/ethereum-signatures/)
(v, r, and s).

    
    
    1        require(deadline >= block.timestamp, 'UniswapV2: EXPIRED');
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Don't accept transactions after the deadline.

    
    
    1        bytes32 digest = keccak256(
    
    2            abi.encodePacked(
    
    3                '\x19\x01',
    
    4                DOMAIN_SEPARATOR,
    
    5                keccak256(abi.encode(PERMIT_TYPEHASH, owner, spender, value, nonces[owner]++, deadline))
    
    6            )
    
    7        );
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

`abi.encodePacked(...)` is the message we expect to get. We know what the
nonce should be, so there is no need for us to get it as a parameter.

The Ethereum signature algorithm expects to get 256 bits to sign, so we use
the `keccak256` hash function.

    
    
    1        address recoveredAddress = ecrecover(digest, v, r, s);
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

From the digest and the signature we can get the address that signed it using
[ecrecover(opens in a new tab)](https://coders-errand.com/ecrecover-signature-
verification-ethereum/).

    
    
    1        require(recoveredAddress != address(0) && recoveredAddress == owner, 'UniswapV2: INVALID_SIGNATURE');
    
    2        _approve(owner, spender, value);
    
    3    }
    
    4
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

If everything is OK, treat this as [an ERC-20 approve(opens in a new
tab)](https://eips.ethereum.org/EIPS/eip-20#approve).

## The Periphery Contracts

The periphery contracts are the API (application program interface) for
Uniswap. They are available for external calls, either from other contracts or
decentralized applications. You could call the core contracts directly, but
that's more complicated and you might lose value if you make a mistake. The
core contracts only contain tests to make sure they aren't cheated, not sanity
checks for anybody else. Those are in the periphery so they can be updated as
needed.

### UniswapV2Router01.sol

[This contract(opens in a new
tab)](https://github.com/Uniswap/uniswap-v2-periphery/blob/master/contracts/UniswapV2Router01.sol)
has problems, and [should no longer be used(opens in a new
tab)](https://docs.uniswap.org/contracts/v2/reference/smart-
contracts/router-01). Luckily, the periphery contracts are stateless and don't
hold any assets, so it is easy to deprecate it and suggest people use the
replacement, `UniswapV2Router02`, instead.

### UniswapV2Router02.sol

In most cases you would use Uniswap through [this contract(opens in a new
tab)](https://github.com/Uniswap/uniswap-v2-periphery/blob/master/contracts/UniswapV2Router02.sol).
You can see how to use it [here(opens in a new
tab)](https://docs.uniswap.org/contracts/v2/reference/smart-
contracts/router-02).

    
    
    1pragma solidity =0.6.6;
    
    2
    
    3import '@uniswap/v2-core/contracts/interfaces/IUniswapV2Factory.sol';
    
    4import '@uniswap/lib/contracts/libraries/TransferHelper.sol';
    
    5
    
    6import './interfaces/IUniswapV2Router02.sol';
    
    7import './libraries/UniswapV2Library.sol';
    
    8import './libraries/SafeMath.sol';
    
    9import './interfaces/IERC20.sol';
    
    10import './interfaces/IWETH.sol';
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Most of these we either encountered before, or are fairly obvious. The one
exception is `IWETH.sol`. Uniswap v2 allows exchanges for any pair of ERC-20
tokens, but ether (ETH) itself isn't an ERC-20 token. It predates the standard
and is transferred by unique mechanisms. To enable the use of ETH in contracts
that apply to ERC-20 tokens people came up with the [wrapped ether
(WETH)(opens in a new tab)](https://weth.tkn.eth.limo/) contract. You send
this contract ETH, and it mints you an equivalent amount of WETH. Or you can
burn WETH, and get ETH back.

    
    
    1contract UniswapV2Router02 is IUniswapV2Router02 {
    
    2    using SafeMath for uint;
    
    3
    
    4    address public immutable override factory;
    
    5    address public immutable override WETH;
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

The router needs to know what factory to use, and for transactions that
require WETH what WETH contract to use. These values are [immutable(opens in a
new tab)](https://docs.soliditylang.org/en/v0.8.3/contracts.html#constant-and-
immutable-state-variables), meaning they can only be set in the constructor.
This gives users the confidence that nobody would be able to change them to
point to less honest contracts.

    
    
    1    modifier ensure(uint deadline) {
    
    2        require(deadline >= block.timestamp, 'UniswapV2Router: EXPIRED');
    
    3        _;
    
    4    }
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

This modifier makes sure that time limited transactions ("do X before time Y
if you can") don't happen after their time limit.

    
    
    1    constructor(address _factory, address _WETH) public {
    
    2        factory = _factory;
    
    3        WETH = _WETH;
    
    4    }
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

The constructor just sets the immutable state variables.

    
    
    1    receive() external payable {
    
    2        assert(msg.sender == WETH); // only accept ETH via fallback from the WETH contract
    
    3    }
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

This function is called when we redeem tokens from the WETH contract back into
ETH. Only the WETH contract we use is authorized to do that.

#### Add Liquidity

These functions add tokens to the pair exchange, which increases the liquidity
pool.

    
    
    1
    
    2    // **** ADD LIQUIDITY ****
    
    3    function _addLiquidity(
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

This function is used to calculate the amount of A and B tokens that should be
deposited into the pair exchange.

    
    
    1        address tokenA,
    
    2        address tokenB,
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

These are the addresses of the ERC-20 token contracts.

    
    
    1        uint amountADesired,
    
    2        uint amountBDesired,
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

These are the amounts the liquidity provider wants to deposit. They are also
the maximum amounts of A and B to be deposited.

    
    
    1        uint amountAMin,
    
    2        uint amountBMin
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

These are the minimum acceptable amounts to deposit. If the transaction cannot
take place with these amounts or more, revert out of it. If you don't want
this feature, just specify zero.

Liquidity providers specify a minimum, typically, because they want to limit
the transaction to an exchange rate that is close to the current one. If the
exchange rate fluctuates too much it might mean news that change the
underlying values, and they want to decide manually what to do.

For example, imagine a case where the exchange rate is one to one and the
liquidity provider specifies these values:

Parameter| Value  
---|---  
amountADesired| 1000  
amountBDesired| 1000  
amountAMin| 900  
amountBMin| 800  
  
As long as the exchange rate stays between 0.9 and 1.25, the transaction takes
place. If the exchange rate gets out of that range, the transaction gets
cancelled.

The reason for this precaution is that transactions are not immediate, you
submit them and eventually a validator is going to include them in a block
(unless your gas price is very low, in which case you'll need to submit
another transaction with the same nonce and a higher gas price to overwrite
it). You cannot control what happens during the interval between submission
and inclusion.

    
    
    1    ) internal virtual returns (uint amountA, uint amountB) {
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

The function returns the amounts the liquidity provider should deposit to have
a ratio equal to the current ratio between reserves.

    
    
    1        // create the pair if it doesn't exist yet
    
    2        if (IUniswapV2Factory(factory).getPair(tokenA, tokenB) == address(0)) {
    
    3            IUniswapV2Factory(factory).createPair(tokenA, tokenB);
    
    4        }
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

If there is no exchange for this token pair yet, create it.

    
    
    1        (uint reserveA, uint reserveB) = UniswapV2Library.getReserves(factory, tokenA, tokenB);
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Get the current reserves in the pair.

    
    
    1        if (reserveA == 0 && reserveB == 0) {
    
    2            (amountA, amountB) = (amountADesired, amountBDesired);
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

If the current reserves are empty then this is a new pair exchange. The
amounts to be deposited should be exactly the same as those the liquidity
provider wants to provide.

    
    
    1        } else {
    
    2            uint amountBOptimal = UniswapV2Library.quote(amountADesired, reserveA, reserveB);
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

If we need to see what amounts will be, we get the optimal amount using [this
function(opens in a new
tab)](https://github.com/Uniswap/uniswap-v2-periphery/blob/master/contracts/libraries/UniswapV2Library.sol#L35).
We want the same ratio as the current reserves.

    
    
    1            if (amountBOptimal <= amountBDesired) {
    
    2                require(amountBOptimal >= amountBMin, 'UniswapV2Router: INSUFFICIENT_B_AMOUNT');
    
    3                (amountA, amountB) = (amountADesired, amountBOptimal);
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

If `amountBOptimal` is smaller than the amount the liquidity provider wants to
deposit it means that token B is more valuable currently than the liquidity
depositor thinks, so a smaller amount is required.

    
    
    1            } else {
    
    2                uint amountAOptimal = UniswapV2Library.quote(amountBDesired, reserveB, reserveA);
    
    3                assert(amountAOptimal <= amountADesired);
    
    4                require(amountAOptimal >= amountAMin, 'UniswapV2Router: INSUFFICIENT_A_AMOUNT');
    
    5                (amountA, amountB) = (amountAOptimal, amountBDesired);
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

If the optimal B amount is more than the desired B amount it means B tokens
are less valuable currently than the liquidity depositor thinks, so a higher
amount is required. However, the desired amount is a maximum, so we cannot do
that. Instead we calculate the optimal number of A tokens for the desired
amount of B tokens.

Putting it all together we get this graph. Assume you're trying to deposit a
thousand A tokens (blue line) and a thousand B tokens (red line). The x axis
is the exchange rate, A/B. If x=1, they are equal in value and you deposit a
thousand of each. If x=2, A is twice the value of B (you get two B tokens for
each A token) so you deposit a thousand B tokens, but only 500 A tokens. If
x=0.5, the situation is reversed, a thousand A tokens and five hundred B
tokens.

[![Graph](/_next/image/?url=%2Fcontent%2Fdevelopers%2Ftutorials%2Funiswap-v2-annotated-
code%2FliquidityProviderDeposit.png&w=1920&q=75)](/content/developers/tutorials/uniswap-v2-annotated-
code/liquidityProviderDeposit.png)

You could deposit liquidity directly into the core contract (using
[UniswapV2Pair::mint(opens in a new
tab)](https://github.com/Uniswap/uniswap-v2-core/blob/master/contracts/UniswapV2Pair.sol#L110)),
but the core contract only checks that it is not getting cheated itself, so
you run the risk of losing value if the exchange rate changes between the time
you submit your transaction and the time it is executed. If you use the
periphery contract, it figures the amount you should deposit and deposits it
immediately, so the exchange rate doesn't change and you don't lose anything.

    
    
    1    function addLiquidity(
    
    2        address tokenA,
    
    3        address tokenB,
    
    4        uint amountADesired,
    
    5        uint amountBDesired,
    
    6        uint amountAMin,
    
    7        uint amountBMin,
    
    8        address to,
    
    9        uint deadline
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

This function can be called by a transaction to deposit liquidity. Most
parameters are the same as in `_addLiquidity` above, with two exceptions:

. `to` is the address that gets the new liquidity tokens minted to show the
liquidity provider's portion of the pool . `deadline` is a time limit on the
transaction

    
    
    1    ) external virtual override ensure(deadline) returns (uint amountA, uint amountB, uint liquidity) {
    
    2        (amountA, amountB) = _addLiquidity(tokenA, tokenB, amountADesired, amountBDesired, amountAMin, amountBMin);
    
    3        address pair = UniswapV2Library.pairFor(factory, tokenA, tokenB);
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

We calculate the amounts to actually deposit and then find the address of the
liquidity pool. To save gas we don't do this by asking the factory, but using
the library function `pairFor` (see below in libraries)

    
    
    1        TransferHelper.safeTransferFrom(tokenA, msg.sender, pair, amountA);
    
    2        TransferHelper.safeTransferFrom(tokenB, msg.sender, pair, amountB);
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Transfer the correct amounts of tokens from the user into the pair exchange.

    
    
    1        liquidity = IUniswapV2Pair(pair).mint(to);
    
    2    }
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

In return give the `to` address liquidity tokens for partial ownership of the
pool. The `mint` function of the core contract sees how many extra tokens it
has (compared to what it had the last time liquidity changed) and mints
liquidity accordingly.

    
    
    1    function addLiquidityETH(
    
    2        address token,
    
    3        uint amountTokenDesired,
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

When a liquidity provider wants to provide liquidity to a Token/ETH pair
exchange, there are a few differences. The contract handles wrapping the ETH
for the liquidity provider. There is no need to specify how many ETH the user
wants to deposit, because the user just sends them with the transaction (the
amount is available in `msg.value`).

    
    
    1        uint amountTokenMin,
    
    2        uint amountETHMin,
    
    3        address to,
    
    4        uint deadline
    
    5    ) external virtual override payable ensure(deadline) returns (uint amountToken, uint amountETH, uint liquidity) {
    
    6        (amountToken, amountETH) = _addLiquidity(
    
    7            token,
    
    8            WETH,
    
    9            amountTokenDesired,
    
    10            msg.value,
    
    11            amountTokenMin,
    
    12            amountETHMin
    
    13        );
    
    14        address pair = UniswapV2Library.pairFor(factory, token, WETH);
    
    15        TransferHelper.safeTransferFrom(token, msg.sender, pair, amountToken);
    
    16        IWETH(WETH).deposit{value: amountETH}();
    
    17        assert(IWETH(WETH).transfer(pair, amountETH));
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

To deposit the ETH the contract first wraps it into WETH and then transfers
the WETH into the pair. Notice that the transfer is wrapped in an `assert`.
This means that if the transfer fails this contract call also fails, and
therefore the wrapping doesn't really happen.

    
    
    1        liquidity = IUniswapV2Pair(pair).mint(to);
    
    2        // refund dust eth, if any
    
    3        if (msg.value > amountETH) TransferHelper.safeTransferETH(msg.sender, msg.value - amountETH);
    
    4    }
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

The user has already sent us the ETH, so if there is any extra left over
(because the other token is less valuable than the user thought), we need to
issue a refund.

#### Remove Liquidity

These functions will remove liquidity and pay back the liquidity provider.

    
    
    1    // **** REMOVE LIQUIDITY ****
    
    2    function removeLiquidity(
    
    3        address tokenA,
    
    4        address tokenB,
    
    5        uint liquidity,
    
    6        uint amountAMin,
    
    7        uint amountBMin,
    
    8        address to,
    
    9        uint deadline
    
    10    ) public virtual override ensure(deadline) returns (uint amountA, uint amountB) {
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

The simplest case of removing liquidity. There is a minimum amount of each
token the liquidity provider agrees to accept, and it must happen before the
deadline.

    
    
    1        address pair = UniswapV2Library.pairFor(factory, tokenA, tokenB);
    
    2        IUniswapV2Pair(pair).transferFrom(msg.sender, pair, liquidity); // send liquidity to pair
    
    3        (uint amount0, uint amount1) = IUniswapV2Pair(pair).burn(to);
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

The core contract's `burn` function handles paying the user back the tokens.

    
    
    1        (address token0,) = UniswapV2Library.sortTokens(tokenA, tokenB);
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

When a function returns multiple values, but we are only interested in some of
them, this is how we only get those values. It is somewhat cheaper in gas
terms than reading a value and never using it.

    
    
    1        (amountA, amountB) = tokenA == token0 ? (amount0, amount1) : (amount1, amount0);
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Translate the amounts from the way the core contract returns them (lower
address token first) to the way the user expects them (corresponding to
`tokenA` and `tokenB`).

    
    
    1        require(amountA >= amountAMin, 'UniswapV2Router: INSUFFICIENT_A_AMOUNT');
    
    2        require(amountB >= amountBMin, 'UniswapV2Router: INSUFFICIENT_B_AMOUNT');
    
    3    }
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

It is OK to do the transfer first and then verify it is legitimate, because if
it isn't we'll revert out of all the state changes.

    
    
    1    function removeLiquidityETH(
    
    2        address token,
    
    3        uint liquidity,
    
    4        uint amountTokenMin,
    
    5        uint amountETHMin,
    
    6        address to,
    
    7        uint deadline
    
    8    ) public virtual override ensure(deadline) returns (uint amountToken, uint amountETH) {
    
    9        (amountToken, amountETH) = removeLiquidity(
    
    10            token,
    
    11            WETH,
    
    12            liquidity,
    
    13            amountTokenMin,
    
    14            amountETHMin,
    
    15            address(this),
    
    16            deadline
    
    17        );
    
    18        TransferHelper.safeTransfer(token, to, amountToken);
    
    19        IWETH(WETH).withdraw(amountETH);
    
    20        TransferHelper.safeTransferETH(to, amountETH);
    
    21    }
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Remove liquidity for ETH is almost the same, except that we receive the WETH
tokens and then redeem them for ETH to give back to the liquidity provider.

    
    
    1    function removeLiquidityWithPermit(
    
    2        address tokenA,
    
    3        address tokenB,
    
    4        uint liquidity,
    
    5        uint amountAMin,
    
    6        uint amountBMin,
    
    7        address to,
    
    8        uint deadline,
    
    9        bool approveMax, uint8 v, bytes32 r, bytes32 s
    
    10    ) external virtual override returns (uint amountA, uint amountB) {
    
    11        address pair = UniswapV2Library.pairFor(factory, tokenA, tokenB);
    
    12        uint value = approveMax ? uint(-1) : liquidity;
    
    13        IUniswapV2Pair(pair).permit(msg.sender, address(this), value, deadline, v, r, s);
    
    14        (amountA, amountB) = removeLiquidity(tokenA, tokenB, liquidity, amountAMin, amountBMin, to, deadline);
    
    15    }
    
    16
    
    17
    
    18    function removeLiquidityETHWithPermit(
    
    19        address token,
    
    20        uint liquidity,
    
    21        uint amountTokenMin,
    
    22        uint amountETHMin,
    
    23        address to,
    
    24        uint deadline,
    
    25        bool approveMax, uint8 v, bytes32 r, bytes32 s
    
    26    ) external virtual override returns (uint amountToken, uint amountETH) {
    
    27        address pair = UniswapV2Library.pairFor(factory, token, WETH);
    
    28        uint value = approveMax ? uint(-1) : liquidity;
    
    29        IUniswapV2Pair(pair).permit(msg.sender, address(this), value, deadline, v, r, s);
    
    30        (amountToken, amountETH) = removeLiquidityETH(token, liquidity, amountTokenMin, amountETHMin, to, deadline);
    
    31    }
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

These functions relay meta-transactions to allow users without ether to
withdraw from the pool, using the permit mechanism.

    
    
    1
    
    2    // **** REMOVE LIQUIDITY (supporting fee-on-transfer tokens) ****
    
    3    function removeLiquidityETHSupportingFeeOnTransferTokens(
    
    4        address token,
    
    5        uint liquidity,
    
    6        uint amountTokenMin,
    
    7        uint amountETHMin,
    
    8        address to,
    
    9        uint deadline
    
    10    ) public virtual override ensure(deadline) returns (uint amountETH) {
    
    11        (, amountETH) = removeLiquidity(
    
    12            token,
    
    13            WETH,
    
    14            liquidity,
    
    15            amountTokenMin,
    
    16            amountETHMin,
    
    17            address(this),
    
    18            deadline
    
    19        );
    
    20        TransferHelper.safeTransfer(token, to, IERC20(token).balanceOf(address(this)));
    
    21        IWETH(WETH).withdraw(amountETH);
    
    22        TransferHelper.safeTransferETH(to, amountETH);
    
    23    }
    
    24
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

This function can be used for tokens that have transfer or storage fees. When
a token has such fees we cannot rely on the `removeLiquidity` function to tell
us how much of the token we get back, so we need to withdraw first and then
get the balance.

    
    
    1
    
    2
    
    3    function removeLiquidityETHWithPermitSupportingFeeOnTransferTokens(
    
    4        address token,
    
    5        uint liquidity,
    
    6        uint amountTokenMin,
    
    7        uint amountETHMin,
    
    8        address to,
    
    9        uint deadline,
    
    10        bool approveMax, uint8 v, bytes32 r, bytes32 s
    
    11    ) external virtual override returns (uint amountETH) {
    
    12        address pair = UniswapV2Library.pairFor(factory, token, WETH);
    
    13        uint value = approveMax ? uint(-1) : liquidity;
    
    14        IUniswapV2Pair(pair).permit(msg.sender, address(this), value, deadline, v, r, s);
    
    15        amountETH = removeLiquidityETHSupportingFeeOnTransferTokens(
    
    16            token, liquidity, amountTokenMin, amountETHMin, to, deadline
    
    17        );
    
    18    }
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

The final function combines storage fees with meta-transactions.

#### Trade

    
    
    1    // **** SWAP ****
    
    2    // requires the initial amount to have already been sent to the first pair
    
    3    function _swap(uint[] memory amounts, address[] memory path, address _to) internal virtual {
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

This function performs internal processing that is required for the functions
that are exposed to traders.

    
    
    1        for (uint i; i < path.length - 1; i++) {
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

As I'm writing this there are [388,160 ERC-20 tokens(opens in a new
tab)](https://etherscan.io/tokens). If there was a pair exchange for each
token pair, it would be over a 150 billion pair exchanges. The entire chain,
at the moment, [only has 0.1% that number of accounts(opens in a new
tab)](https://etherscan.io/chart/address). Instead, the swap functions support
the concept of a path. A trader can exchange A for B, B for C, and C for D, so
there is no need for a direct A-D pair exchange.

The prices on these markets tend to be synchronized, because when they are out
of sync it creates an opportunity for arbitrage. Imagine, for example, three
tokens, A, B, and C. There are three pair exchanges, one for each pair.

  1. The initial situation
  2. A trader sells 24.695 A tokens and gets 25.305 B tokens.
  3. The trader sells 24.695 B tokens for 25.305 C tokens, keeping approximately 0.61 B tokens as profit.
  4. Then the trader sells 24.695 C tokens for 25.305 A tokens, keeping approximately 0.61 C tokens as profit. The trader also has 0.61 extra A tokens (the 25.305 the trader ends up with, minus the original investment of 24.695).

Step| A-B Exchange| B-C Exchange| A-C Exchange  
---|---|---|---  
1| A:1000 B:1050 A/B=1.05| B:1000 C:1050 B/C=1.05| A:1050 C:1000 C/A=1.05  
2| A:1024.695 B:1024.695 A/B=1| B:1000 C:1050 B/C=1.05| A:1050 C:1000 C/A=1.05  
3| A:1024.695 B:1024.695 A/B=1| B:1024.695 C:1024.695 B/C=1| A:1050 C:1000
C/A=1.05  
4| A:1024.695 B:1024.695 A/B=1| B:1024.695 C:1024.695 B/C=1| A:1024.695
C:1024.695 C/A=1  
      
    
    1            (address input, address output) = (path[i], path[i + 1]);
    
    2            (address token0,) = UniswapV2Library.sortTokens(input, output);
    
    3            uint amountOut = amounts[i + 1];
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Get the pair we are currently handling, sort it (for use with the pair) and
get the expected output amount.

    
    
    1            (uint amount0Out, uint amount1Out) = input == token0 ? (uint(0), amountOut) : (amountOut, uint(0));
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Get the expected out amounts, sorted the way the pair exchange expects them to
be.

    
    
    1            address to = i < path.length - 2 ? UniswapV2Library.pairFor(factory, output, path[i + 2]) : _to;
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Is this the last exchange? If so, send the tokens received for the trade to
the destination. If not, send it to the next pair exchange.

    
    
    1
    
    2            IUniswapV2Pair(UniswapV2Library.pairFor(factory, input, output)).swap(
    
    3                amount0Out, amount1Out, to, new bytes(0)
    
    4            );
    
    5        }
    
    6    }
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Actually call the pair exchange to swap the tokens. We don't need a callback
to be told about the exchange, so we don't send any bytes in that field.

    
    
    1    function swapExactTokensForTokens(
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

This function is used directly by traders to swap one token for another.

    
    
    1        uint amountIn,
    
    2        uint amountOutMin,
    
    3        address[] calldata path,
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

This parameter contains the addresses of the ERC-20 contracts. As explained
above, this is an array because you might need to go through several pair
exchanges to get from the asset you have to the asset you want.

A function parameter in solidity can be stored either in `memory` or the
`calldata`. If the function is an entry point to the contract, called directly
from a user (using a transaction) or from a different contract, then the
parameter's value can be taken directly from the call data. If the function is
called internally, as `_swap` above, then the parameters have to be stored in
`memory`. From the perspective of the called contract `calldata` is read only.

With scalar types such as `uint` or `address` the compiler handles the choice
of storage for us, but with arrays, which are longer and more expensive, we
specify the type of storage to be used.

    
    
    1        address to,
    
    2        uint deadline
    
    3    ) external virtual override ensure(deadline) returns (uint[] memory amounts) {
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Return values are always returned in memory.

    
    
    1        amounts = UniswapV2Library.getAmountsOut(factory, amountIn, path);
    
    2        require(amounts[amounts.length - 1] >= amountOutMin, 'UniswapV2Router: INSUFFICIENT_OUTPUT_AMOUNT');
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Calculate the amount to be purchased in each swap. If the result is less than
the minimum the trader is willing to accept, revert out of the transaction.

    
    
    1        TransferHelper.safeTransferFrom(
    
    2            path[0], msg.sender, UniswapV2Library.pairFor(factory, path[0], path[1]), amounts[0]
    
    3        );
    
    4        _swap(amounts, path, to);
    
    5    }
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Finally, transfer the initial ERC-20 token to the account for the first pair
exchange and call `_swap`. This is all happening in the same transaction, so
the pair exchange knows that any unexpected tokens are part of this transfer.

    
    
    1    function swapTokensForExactTokens(
    
    2        uint amountOut,
    
    3        uint amountInMax,
    
    4        address[] calldata path,
    
    5        address to,
    
    6        uint deadline
    
    7    ) external virtual override ensure(deadline) returns (uint[] memory amounts) {
    
    8        amounts = UniswapV2Library.getAmountsIn(factory, amountOut, path);
    
    9        require(amounts[0] <= amountInMax, 'UniswapV2Router: EXCESSIVE_INPUT_AMOUNT');
    
    10        TransferHelper.safeTransferFrom(
    
    11            path[0], msg.sender, UniswapV2Library.pairFor(factory, path[0], path[1]), amounts[0]
    
    12        );
    
    13        _swap(amounts, path, to);
    
    14    }
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

The previous function, `swapTokensForTokens`, allows a trader to specify an
exact number of input tokens he is willing to give and the minimum number of
output tokens he is willing to receive in return. This function does the
reverse swap, it lets a trader specify the number of output tokens he wants,
and the maximum number of input tokens he is willing to pay for them.

In both cases, the trader has to give this periphery contract first an
allowance to allow it to transfer them.

    
    
    1    function swapExactETHForTokens(uint amountOutMin, address[] calldata path, address to, uint deadline)
    
    2        external
    
    3        virtual
    
    4        override
    
    5        payable
    
    6        ensure(deadline)
    
    7        returns (uint[] memory amounts)
    
    8    {
    
    9        require(path[0] == WETH, 'UniswapV2Router: INVALID_PATH');
    
    10        amounts = UniswapV2Library.getAmountsOut(factory, msg.value, path);
    
    11        require(amounts[amounts.length - 1] >= amountOutMin, 'UniswapV2Router: INSUFFICIENT_OUTPUT_AMOUNT');
    
    12        IWETH(WETH).deposit{value: amounts[0]}();
    
    13        assert(IWETH(WETH).transfer(UniswapV2Library.pairFor(factory, path[0], path[1]), amounts[0]));
    
    14        _swap(amounts, path, to);
    
    15    }
    
    16
    
    17
    
    18    function swapTokensForExactETH(uint amountOut, uint amountInMax, address[] calldata path, address to, uint deadline)
    
    19        external
    
    20        virtual
    
    21        override
    
    22        ensure(deadline)
    
    23        returns (uint[] memory amounts)
    
    24    {
    
    25        require(path[path.length - 1] == WETH, 'UniswapV2Router: INVALID_PATH');
    
    26        amounts = UniswapV2Library.getAmountsIn(factory, amountOut, path);
    
    27        require(amounts[0] <= amountInMax, 'UniswapV2Router: EXCESSIVE_INPUT_AMOUNT');
    
    28        TransferHelper.safeTransferFrom(
    
    29            path[0], msg.sender, UniswapV2Library.pairFor(factory, path[0], path[1]), amounts[0]
    
    30        );
    
    31        _swap(amounts, path, address(this));
    
    32        IWETH(WETH).withdraw(amounts[amounts.length - 1]);
    
    33        TransferHelper.safeTransferETH(to, amounts[amounts.length - 1]);
    
    34    }
    
    35
    
    36
    
    37
    
    38    function swapExactTokensForETH(uint amountIn, uint amountOutMin, address[] calldata path, address to, uint deadline)
    
    39        external
    
    40        virtual
    
    41        override
    
    42        ensure(deadline)
    
    43        returns (uint[] memory amounts)
    
    44    {
    
    45        require(path[path.length - 1] == WETH, 'UniswapV2Router: INVALID_PATH');
    
    46        amounts = UniswapV2Library.getAmountsOut(factory, amountIn, path);
    
    47        require(amounts[amounts.length - 1] >= amountOutMin, 'UniswapV2Router: INSUFFICIENT_OUTPUT_AMOUNT');
    
    48        TransferHelper.safeTransferFrom(
    
    49            path[0], msg.sender, UniswapV2Library.pairFor(factory, path[0], path[1]), amounts[0]
    
    50        );
    
    51        _swap(amounts, path, address(this));
    
    52        IWETH(WETH).withdraw(amounts[amounts.length - 1]);
    
    53        TransferHelper.safeTransferETH(to, amounts[amounts.length - 1]);
    
    54    }
    
    55
    
    56
    
    57    function swapETHForExactTokens(uint amountOut, address[] calldata path, address to, uint deadline)
    
    58        external
    
    59        virtual
    
    60        override
    
    61        payable
    
    62        ensure(deadline)
    
    63        returns (uint[] memory amounts)
    
    64    {
    
    65        require(path[0] == WETH, 'UniswapV2Router: INVALID_PATH');
    
    66        amounts = UniswapV2Library.getAmountsIn(factory, amountOut, path);
    
    67        require(amounts[0] <= msg.value, 'UniswapV2Router: EXCESSIVE_INPUT_AMOUNT');
    
    68        IWETH(WETH).deposit{value: amounts[0]}();
    
    69        assert(IWETH(WETH).transfer(UniswapV2Library.pairFor(factory, path[0], path[1]), amounts[0]));
    
    70        _swap(amounts, path, to);
    
    71        // refund dust eth, if any
    
    72        if (msg.value > amounts[0]) TransferHelper.safeTransferETH(msg.sender, msg.value - amounts[0]);
    
    73    }
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

These four variants all involve trading between ETH and tokens. The only
difference is that we either receive ETH from the trader and use it to mint
WETH, or we receive WETH from the last exchange in the path and burn it,
sending the trader back the resulting ETH.

    
    
    1    // **** SWAP (supporting fee-on-transfer tokens) ****
    
    2    // requires the initial amount to have already been sent to the first pair
    
    3    function _swapSupportingFeeOnTransferTokens(address[] memory path, address _to) internal virtual {
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

This is the internal function to swap tokens that have transfer or storage
fees to solve ([this issue(opens in a new
tab)](https://github.com/Uniswap/uniswap-interface/issues/835)).

    
    
    1        for (uint i; i < path.length - 1; i++) {
    
    2            (address input, address output) = (path[i], path[i + 1]);
    
    3            (address token0,) = UniswapV2Library.sortTokens(input, output);
    
    4            IUniswapV2Pair pair = IUniswapV2Pair(UniswapV2Library.pairFor(factory, input, output));
    
    5            uint amountInput;
    
    6            uint amountOutput;
    
    7            { // scope to avoid stack too deep errors
    
    8            (uint reserve0, uint reserve1,) = pair.getReserves();
    
    9            (uint reserveInput, uint reserveOutput) = input == token0 ? (reserve0, reserve1) : (reserve1, reserve0);
    
    10            amountInput = IERC20(input).balanceOf(address(pair)).sub(reserveInput);
    
    11            amountOutput = UniswapV2Library.getAmountOut(amountInput, reserveInput, reserveOutput);
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Because of the transfer fees we cannot rely on the `getAmountsOut` function to
tell us how much we get out of each transfer (the way we do before calling the
original `_swap`). Instead we have to transfer first and then see how many
tokens we got back.

Note: In theory we could just use this function instead of `_swap`, but in
certain cases (for example, if the transfer ends up being reverted because
there isn't enough at the end to meet the required minimum) that would end up
costing more gas. Transfer fee tokens are pretty rare, so while we need to
accommodate them there's no need to all swaps to assume they go through at
least one of them.

    
    
    1            }
    
    2            (uint amount0Out, uint amount1Out) = input == token0 ? (uint(0), amountOutput) : (amountOutput, uint(0));
    
    3            address to = i < path.length - 2 ? UniswapV2Library.pairFor(factory, output, path[i + 2]) : _to;
    
    4            pair.swap(amount0Out, amount1Out, to, new bytes(0));
    
    5        }
    
    6    }
    
    7
    
    8
    
    9    function swapExactTokensForTokensSupportingFeeOnTransferTokens(
    
    10        uint amountIn,
    
    11        uint amountOutMin,
    
    12        address[] calldata path,
    
    13        address to,
    
    14        uint deadline
    
    15    ) external virtual override ensure(deadline) {
    
    16        TransferHelper.safeTransferFrom(
    
    17            path[0], msg.sender, UniswapV2Library.pairFor(factory, path[0], path[1]), amountIn
    
    18        );
    
    19        uint balanceBefore = IERC20(path[path.length - 1]).balanceOf(to);
    
    20        _swapSupportingFeeOnTransferTokens(path, to);
    
    21        require(
    
    22            IERC20(path[path.length - 1]).balanceOf(to).sub(balanceBefore) >= amountOutMin,
    
    23            'UniswapV2Router: INSUFFICIENT_OUTPUT_AMOUNT'
    
    24        );
    
    25    }
    
    26
    
    27
    
    28    function swapExactETHForTokensSupportingFeeOnTransferTokens(
    
    29        uint amountOutMin,
    
    30        address[] calldata path,
    
    31        address to,
    
    32        uint deadline
    
    33    )
    
    34        external
    
    35        virtual
    
    36        override
    
    37        payable
    
    38        ensure(deadline)
    
    39    {
    
    40        require(path[0] == WETH, 'UniswapV2Router: INVALID_PATH');
    
    41        uint amountIn = msg.value;
    
    42        IWETH(WETH).deposit{value: amountIn}();
    
    43        assert(IWETH(WETH).transfer(UniswapV2Library.pairFor(factory, path[0], path[1]), amountIn));
    
    44        uint balanceBefore = IERC20(path[path.length - 1]).balanceOf(to);
    
    45        _swapSupportingFeeOnTransferTokens(path, to);
    
    46        require(
    
    47            IERC20(path[path.length - 1]).balanceOf(to).sub(balanceBefore) >= amountOutMin,
    
    48            'UniswapV2Router: INSUFFICIENT_OUTPUT_AMOUNT'
    
    49        );
    
    50    }
    
    51
    
    52
    
    53    function swapExactTokensForETHSupportingFeeOnTransferTokens(
    
    54        uint amountIn,
    
    55        uint amountOutMin,
    
    56        address[] calldata path,
    
    57        address to,
    
    58        uint deadline
    
    59    )
    
    60        external
    
    61        virtual
    
    62        override
    
    63        ensure(deadline)
    
    64    {
    
    65        require(path[path.length - 1] == WETH, 'UniswapV2Router: INVALID_PATH');
    
    66        TransferHelper.safeTransferFrom(
    
    67            path[0], msg.sender, UniswapV2Library.pairFor(factory, path[0], path[1]), amountIn
    
    68        );
    
    69        _swapSupportingFeeOnTransferTokens(path, address(this));
    
    70        uint amountOut = IERC20(WETH).balanceOf(address(this));
    
    71        require(amountOut >= amountOutMin, 'UniswapV2Router: INSUFFICIENT_OUTPUT_AMOUNT');
    
    72        IWETH(WETH).withdraw(amountOut);
    
    73        TransferHelper.safeTransferETH(to, amountOut);
    
    74    }
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

These are the same variants used for normal tokens, but they call
`_swapSupportingFeeOnTransferTokens` instead.

    
    
    1    // **** LIBRARY FUNCTIONS ****
    
    2    function quote(uint amountA, uint reserveA, uint reserveB) public pure virtual override returns (uint amountB) {
    
    3        return UniswapV2Library.quote(amountA, reserveA, reserveB);
    
    4    }
    
    5
    
    6    function getAmountOut(uint amountIn, uint reserveIn, uint reserveOut)
    
    7        public
    
    8        pure
    
    9        virtual
    
    10        override
    
    11        returns (uint amountOut)
    
    12    {
    
    13        return UniswapV2Library.getAmountOut(amountIn, reserveIn, reserveOut);
    
    14    }
    
    15
    
    16    function getAmountIn(uint amountOut, uint reserveIn, uint reserveOut)
    
    17        public
    
    18        pure
    
    19        virtual
    
    20        override
    
    21        returns (uint amountIn)
    
    22    {
    
    23        return UniswapV2Library.getAmountIn(amountOut, reserveIn, reserveOut);
    
    24    }
    
    25
    
    26    function getAmountsOut(uint amountIn, address[] memory path)
    
    27        public
    
    28        view
    
    29        virtual
    
    30        override
    
    31        returns (uint[] memory amounts)
    
    32    {
    
    33        return UniswapV2Library.getAmountsOut(factory, amountIn, path);
    
    34    }
    
    35
    
    36    function getAmountsIn(uint amountOut, address[] memory path)
    
    37        public
    
    38        view
    
    39        virtual
    
    40        override
    
    41        returns (uint[] memory amounts)
    
    42    {
    
    43        return UniswapV2Library.getAmountsIn(factory, amountOut, path);
    
    44    }
    
    45}
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

These functions are just proxies that call the UniswapV2Library functions.

### UniswapV2Migrator.sol

This contract was used to migrate exchanges from the old v1 to v2. Now that
they have been migrated, it is no longer relevant.

## The Libraries

The [SafeMath library(opens in a new
tab)](https://docs.openzeppelin.com/contracts/2.x/api/math) is well
documented, so there's no need to document it here.

### Math

This library contains some math functions that are not normally needed in
Solidity code, so they aren't part of the language.

    
    
    1pragma solidity =0.5.16;
    
    2
    
    3// a library for performing various math operations
    
    4
    
    5library Math {
    
    6    function min(uint x, uint y) internal pure returns (uint z) {
    
    7        z = x < y ? x : y;
    
    8    }
    
    9
    
    10    // babylonian method (https://wikipedia.org/wiki/Methods_of_computing_square_roots#Babylonian_method)
    
    11    function sqrt(uint y) internal pure returns (uint z) {
    
    12        if (y > 3) {
    
    13            z = y;
    
    14            uint x = y / 2 + 1;
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Start with x as an estimate that is higher than the square root (that is the
reason we need to treat 1-3 as special cases).

    
    
    1            while (x < z) {
    
    2                z = x;
    
    3                x = (y / x + x) / 2;
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Get a closer estimate, the average of the previous estimate and the number
whose square root we're trying to find divided by the previous estimate.
Repeat until the new estimate isn't lower than the existing one. For more
details, [see here(opens in a new
tab)](https://wikipedia.org/wiki/Methods_of_computing_square_roots#Babylonian_method).

    
    
    1            }
    
    2        } else if (y != 0) {
    
    3            z = 1;
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

We should never need the square root of zero. The square roots of one, two,
and three are roughly one (we use integers, so we ignore the fraction).

    
    
    1        }
    
    2    }
    
    3}
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

### Fixed Point Fractions (UQ112x112)

This library handles fractions, which are normally not part of Ethereum
arithmetic. It does this by encoding the number _x_ as _x *2^112_. This lets
us use the original addition and subtraction opcodes without a change.

    
    
    1pragma solidity =0.5.16;
    
    2
    
    3// a library for handling binary fixed point numbers (https://wikipedia.org/wiki/Q_(number_format))
    
    4
    
    5// range: [0, 2**112 - 1]
    
    6// resolution: 1 / 2**112
    
    7
    
    8library UQ112x112 {
    
    9    uint224 constant Q112 = 2**112;
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

`Q112` is the encoding for one.

    
    
    1    // encode a uint112 as a UQ112x112
    
    2    function encode(uint112 y) internal pure returns (uint224 z) {
    
    3        z = uint224(y) * Q112; // never overflows
    
    4    }
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Because y is `uint112`, the most it can be is 2^112-1. That number can still
be encoded as a `UQ112x112`.

    
    
    1    // divide a UQ112x112 by a uint112, returning a UQ112x112
    
    2    function uqdiv(uint224 x, uint112 y) internal pure returns (uint224 z) {
    
    3        z = x / uint224(y);
    
    4    }
    
    5}
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

If we divide two `UQ112x112` values, the result is no longer multiplied by
2^112. So instead we take an integer for the denominator. We would have needed
to use a similar trick to do multiplication, but we don't need to do
multiplication of `UQ112x112` values.

### UniswapV2Library

This library is used only by the periphery contracts

    
    
    1pragma solidity >=0.5.0;
    
    2
    
    3import '@uniswap/v2-core/contracts/interfaces/IUniswapV2Pair.sol';
    
    4
    
    5import "./SafeMath.sol";
    
    6
    
    7library UniswapV2Library {
    
    8    using SafeMath for uint;
    
    9
    
    10    // returns sorted token addresses, used to handle return values from pairs sorted in this order
    
    11    function sortTokens(address tokenA, address tokenB) internal pure returns (address token0, address token1) {
    
    12        require(tokenA != tokenB, 'UniswapV2Library: IDENTICAL_ADDRESSES');
    
    13        (token0, token1) = tokenA < tokenB ? (tokenA, tokenB) : (tokenB, tokenA);
    
    14        require(token0 != address(0), 'UniswapV2Library: ZERO_ADDRESS');
    
    15    }
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Sort the two tokens by address, so we'll be able to get the address of the
pair exchange for them. This is necessary because otherwise we'd have two
possibilities, one for the parameters A,B and another for the parameters B,A,
leading to two exchanges instead of one.

    
    
    1    // calculates the CREATE2 address for a pair without making any external calls
    
    2    function pairFor(address factory, address tokenA, address tokenB) internal pure returns (address pair) {
    
    3        (address token0, address token1) = sortTokens(tokenA, tokenB);
    
    4        pair = address(uint(keccak256(abi.encodePacked(
    
    5                hex'ff',
    
    6                factory,
    
    7                keccak256(abi.encodePacked(token0, token1)),
    
    8                hex'96e8ac4277198ff8b6f785478aa9a39f403cb768dd02cbee326c3e7da348845f' // init code hash
    
    9            ))));
    
    10    }
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

This function calculates the address of the pair exchange for the two tokens.
This contract is created using [the CREATE2 opcode(opens in a new
tab)](https://eips.ethereum.org/EIPS/eip-1014), so we can calculate the
address using the same algorithm if we know the parameters it uses. This is a
lot cheaper than asking the factory, and

    
    
    1    // fetches and sorts the reserves for a pair
    
    2    function getReserves(address factory, address tokenA, address tokenB) internal view returns (uint reserveA, uint reserveB) {
    
    3        (address token0,) = sortTokens(tokenA, tokenB);
    
    4        (uint reserve0, uint reserve1,) = IUniswapV2Pair(pairFor(factory, tokenA, tokenB)).getReserves();
    
    5        (reserveA, reserveB) = tokenA == token0 ? (reserve0, reserve1) : (reserve1, reserve0);
    
    6    }
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

This function returns the reserves of the two tokens that the pair exchange
has. Note that it can receive the tokens in either order, and sorts them for
internal use.

    
    
    1    // given some amount of an asset and pair reserves, returns an equivalent amount of the other asset
    
    2    function quote(uint amountA, uint reserveA, uint reserveB) internal pure returns (uint amountB) {
    
    3        require(amountA > 0, 'UniswapV2Library: INSUFFICIENT_AMOUNT');
    
    4        require(reserveA > 0 && reserveB > 0, 'UniswapV2Library: INSUFFICIENT_LIQUIDITY');
    
    5        amountB = amountA.mul(reserveB) / reserveA;
    
    6    }
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

This function gives you the amount of token B you'll get in return for token A
if there is no fee involved. This calculation takes into account that the
transfer changes the exchange rate.

    
    
    1    // given an input amount of an asset and pair reserves, returns the maximum output amount of the other asset
    
    2    function getAmountOut(uint amountIn, uint reserveIn, uint reserveOut) internal pure returns (uint amountOut) {
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

The `quote` function above works great if there is no fee to use the pair
exchange. However, if there is a 0.3% exchange fee the amount you actually get
is lower. This function calculates the amount after the exchange fee.

    
    
    1
    
    2        require(amountIn > 0, 'UniswapV2Library: INSUFFICIENT_INPUT_AMOUNT');
    
    3        require(reserveIn > 0 && reserveOut > 0, 'UniswapV2Library: INSUFFICIENT_LIQUIDITY');
    
    4        uint amountInWithFee = amountIn.mul(997);
    
    5        uint numerator = amountInWithFee.mul(reserveOut);
    
    6        uint denominator = reserveIn.mul(1000).add(amountInWithFee);
    
    7        amountOut = numerator / denominator;
    
    8    }
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Solidity does not handle fractions natively, so we can't just multiply the
amount out by 0.997. Instead, we multiply the numerator by 997 and the
denominator by 1000, achieving the same effect.

    
    
    1    // given an output amount of an asset and pair reserves, returns a required input amount of the other asset
    
    2    function getAmountIn(uint amountOut, uint reserveIn, uint reserveOut) internal pure returns (uint amountIn) {
    
    3        require(amountOut > 0, 'UniswapV2Library: INSUFFICIENT_OUTPUT_AMOUNT');
    
    4        require(reserveIn > 0 && reserveOut > 0, 'UniswapV2Library: INSUFFICIENT_LIQUIDITY');
    
    5        uint numerator = reserveIn.mul(amountOut).mul(1000);
    
    6        uint denominator = reserveOut.sub(amountOut).mul(997);
    
    7        amountIn = (numerator / denominator).add(1);
    
    8    }
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

This function does roughly the same thing, but it gets the output amount and
provides the input.

    
    
    1
    
    2    // performs chained getAmountOut calculations on any number of pairs
    
    3    function getAmountsOut(address factory, uint amountIn, address[] memory path) internal view returns (uint[] memory amounts) {
    
    4        require(path.length >= 2, 'UniswapV2Library: INVALID_PATH');
    
    5        amounts = new uint[](path.length);
    
    6        amounts[0] = amountIn;
    
    7        for (uint i; i < path.length - 1; i++) {
    
    8            (uint reserveIn, uint reserveOut) = getReserves(factory, path[i], path[i + 1]);
    
    9            amounts[i + 1] = getAmountOut(amounts[i], reserveIn, reserveOut);
    
    10        }
    
    11    }
    
    12
    
    13    // performs chained getAmountIn calculations on any number of pairs
    
    14    function getAmountsIn(address factory, uint amountOut, address[] memory path) internal view returns (uint[] memory amounts) {
    
    15        require(path.length >= 2, 'UniswapV2Library: INVALID_PATH');
    
    16        amounts = new uint[](path.length);
    
    17        amounts[amounts.length - 1] = amountOut;
    
    18        for (uint i = path.length - 1; i > 0; i--) {
    
    19            (uint reserveIn, uint reserveOut) = getReserves(factory, path[i - 1], path[i]);
    
    20            amounts[i - 1] = getAmountIn(amounts[i], reserveIn, reserveOut);
    
    21        }
    
    22    }
    
    23}
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

These two functions handle identifying the values when it is necessary to go
through several pair exchanges.

### Transfer Helper

[This library(opens in a new tab)](https://github.com/Uniswap/uniswap-
lib/blob/master/contracts/libraries/TransferHelper.sol) adds success checks
around ERC-20 and Ethereum transfers to treat a revert and a `false` value
return the same way.

    
    
    1// SPDX-License-Identifier: GPL-3.0-or-later
    
    2
    
    3pragma solidity >=0.6.0;
    
    4
    
    5// helper methods for interacting with ERC20 tokens and sending ETH that do not consistently return true/false
    
    6library TransferHelper {
    
    7    function safeApprove(
    
    8        address token,
    
    9        address to,
    
    10        uint256 value
    
    11    ) internal {
    
    12        // bytes4(keccak256(bytes('approve(address,uint256)')));
    
    13        (bool success, bytes memory data) = token.call(abi.encodeWithSelector(0x095ea7b3, to, value));
    
    14
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

We can call a different contract in one of two ways:

  * Use an interface definition to create a function call
  * Use the [application binary interface (ABI)(opens in a new tab)](https://docs.soliditylang.org/en/v0.8.3/abi-spec.html) "manually" to create the call. This is what the author of the code decided to do it.

    
    
    1        require(
    
    2            success && (data.length == 0 || abi.decode(data, (bool))),
    
    3            'TransferHelper::safeApprove: approve failed'
    
    4        );
    
    5    }
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

For the sake of backwards compatibility with token that were created prior to
the ERC-20 standard, an ERC-20 call can fail either by reverting (in which
case `success` is `false`) or by being successful and returning a `false`
value (in which case there is output data, and if you decode it as a boolean
you get `false`).

    
    
    1
    
    2
    
    3    function safeTransfer(
    
    4        address token,
    
    5        address to,
    
    6        uint256 value
    
    7    ) internal {
    
    8        // bytes4(keccak256(bytes('transfer(address,uint256)')));
    
    9        (bool success, bytes memory data) = token.call(abi.encodeWithSelector(0xa9059cbb, to, value));
    
    10        require(
    
    11            success && (data.length == 0 || abi.decode(data, (bool))),
    
    12            'TransferHelper::safeTransfer: transfer failed'
    
    13        );
    
    14    }
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

This function implements [ERC-20's transfer functionality(opens in a new
tab)](https://eips.ethereum.org/EIPS/eip-20#transfer), which allows an account
to spend out the allowance provided by a different account.

    
    
    1
    
    2    function safeTransferFrom(
    
    3        address token,
    
    4        address from,
    
    5        address to,
    
    6        uint256 value
    
    7    ) internal {
    
    8        // bytes4(keccak256(bytes('transferFrom(address,address,uint256)')));
    
    9        (bool success, bytes memory data) = token.call(abi.encodeWithSelector(0x23b872dd, from, to, value));
    
    10        require(
    
    11            success && (data.length == 0 || abi.decode(data, (bool))),
    
    12            'TransferHelper::transferFrom: transferFrom failed'
    
    13        );
    
    14    }
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

This function implements [ERC-20's transferFrom functionality(opens in a new
tab)](https://eips.ethereum.org/EIPS/eip-20#transferfrom), which allows an
account to spend out the allowance provided by a different account.

    
    
    1
    
    2    function safeTransferETH(address to, uint256 value) internal {
    
    3        (bool success, ) = to.call{value: value}(new bytes(0));
    
    4        require(success, 'TransferHelper::safeTransferETH: ETH transfer failed');
    
    5    }
    
    6}
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

This function transfers ether to an account. Any call to a different contract
can attempt to send ether. Because we don't need to actually call any
function, we don't send any data with the call.

## Conclusion

This is a long article of about 50 pages. If you made it here,
congratulations! Hopefully by now you've understood the considerations in
writing a real-life application (as opposed to short sample programs) and are
better to be able to write contracts for your own use cases.

Now go and write something useful and amaze us.

w

Last edit: [@wackerow(opens in a new tab)](https://github.com/wackerow), April
2, 2024

See contributors

### Was this tutorial helpful?

YesNo

  * [Edit page(opens in a new tab)](https://github.com/ethereum/ethereum-org-website/tree/dev/public/content/developers/tutorials/uniswap-v2-annotated-code/index.md)
  * On this page

    * Introduction
      * What Does Uniswap Do?
      * Why v2? Why not v3?
      * Core Contracts vs Periphery Contracts
    * Data and Control Flows
      * Swap
      * Add Liquidity
      * Remove Liquidity
    * The Core Contracts
      * UniswapV2Pair.sol
      * UniswapV2Factory.sol
      * UniswapV2ERC20.sol
    * The Periphery Contracts
      * UniswapV2Router01.sol
      * UniswapV2Router02.sol
      * UniswapV2Migrator.sol
    * The Libraries
      * Math
      * Fixed Point Fractions (UQ112x112)
      * UniswapV2Library
      * Transfer Helper
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

