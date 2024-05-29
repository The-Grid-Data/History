Skip to main content

[](/en/)

  * Learn
  * Use
  * Build
  * Participate
  * Research

Search```K`

Languages EN

# All you can cache

layer 2cachingstorage

Intermediate

![✍️](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/270d.svg)Ori
Pomerantz

![📆](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4c6.svg)
September 15, 2022

![⏱️](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/23f1.svg)23
minute read minute read

On this page

  * Overall design
  * Cache manipulation
    * Testing the cache
  * A sample application
    * The contract
    * The testing code
    * The client
  * Conclusion

When using rollups the cost of a byte in the transaction is a lot more
expensive than the cost of a storage slot. Therefore, it makes sense to cache
as much information as possible on chain.

In this article you learn how to create and use a caching contract in such a
way that any parameter value that is likely to be used multiple times will be
cached and available for use (after the first time) with a much smaller number
of bytes, and how to write off chain code that uses this cache.

If you want to skip the article and just see the source code, [it is
here(opens in a new tab)](https://github.com/qbzzt/20220915-all-you-can-
cache). The development stack is [Foundry(opens in a new
tab)](https://book.getfoundry.sh/getting-started/installation).

## Overall design

For the sake of simplicity we'll assume all transaction parameters are
`uint256`, 32 bytes long. When we receive a transaction, we'll parse each
parameter like this:

  1. If the first byte is `0xFF`, take the next 32 bytes as a parameter value and write it to the cache.

  2. If the first byte is `0xFE`, take the next 32 bytes as a parameter value but do _not_ write it to the cache.

  3. For any other value, take the top four bits as the number of additional bytes, and the bottom four bits as the most significant bits of the cache key. Here are some examples:

Bytes in calldata| Cache key  
---|---  
0x0F| 0x0F  
0x10,0x10| 0x10  
0x12,0xAC| 0x02AC  
0x2D,0xEA, 0xD6| 0x0DEAD6  
  

## Cache manipulation

The cache is implemented in [`Cache.sol`(opens in a new
tab)](https://github.com/qbzzt/20220915-all-you-can-
cache/blob/main/src/Cache.sol). Let's go over it line by line.

    
    
    1// SPDX-License-Identifier: UNLICENSED
    
    2pragma solidity ^0.8.13;
    
    3
    
    4
    
    5contract Cache {
    
    6
    
    7    bytes1 public constant INTO_CACHE = 0xFF;
    
    8    bytes1 public constant DONT_CACHE = 0xFE;
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

These constants are used to interpret the special cases where we provide all
the information and either want it written into the cache or not. Writing into
the cache requires two [`SSTORE`(opens in a new
tab)](https://www.evm.codes/#55) operations into previously unused storage
slots at a cost of 22100 gas each, so we make it optional.

    
    
    1
    
    2    mapping(uint => uint) public val2key;
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

A [mapping(opens in a new tab)](https://www.geeksforgeeks.org/solidity-
mappings/) between the values and their keys. This information is necessary to
encode values before you send out the transaction.

    
    
    1    // Location n has the value for key n+1, because we need to preserve
    
    2    // zero as "not in the cache".
    
    3    uint[] public key2val;
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

We can use an array for the mapping from keys to values because we assign the
keys, and for simplicity we do it sequentially.

    
    
    1    function cacheRead(uint _key) public view returns (uint) {
    
    2        require(_key <= key2val.length, "Reading uninitialize cache entry");
    
    3        return key2val[_key-1];
    
    4    }  // cacheRead
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Read a value from the cache.

    
    
    1    // Write a value to the cache if it's not there already
    
    2    // Only public to enable the test to work
    
    3    function cacheWrite(uint _value) public returns (uint) {
    
    4        // If the value is already in the cache, return the current key
    
    5        if (val2key[_value] != 0) {
    
    6            return val2key[_value];
    
    7        }
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

There is no point in putting the same value in the cache more than once. If
the value is already there, just return the existing key.

    
    
    1        // Since 0xFE is a special case, the largest key the cache can
    
    2        // hold is 0x0D followed by 15 0xFF's. If the cache length is already that
    
    3        // large, fail.
    
    4        //                              1 2 3 4 5 6 7 8 9 A B C D E F
    
    5        require(key2val.length+1 < 0x0DFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF,
    
    6            "cache overflow");
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

I don't think we'll ever get a cache that big (approximately 1.8*1037 entries,
which would require about 1027 TB to store). However, I'm old enough to
remember ["640kB would always be enough"(opens in a new
tab)](https://quoteinvestigator.com/2011/09/08/640k-enough/). This test is
very cheap.

    
    
    1        // Write the value using the next key
    
    2        val2key[_value] = key2val.length+1;
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Add the reverse lookup (from the value to the key).

    
    
    1        key2val.push(_value);
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Add the forward lookup (from the key to the value). Because we assign values
sequentially we can just add it after the last array value.

    
    
    1        return key2val.length;
    
    2    }  // cacheWrite
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Return the new length of `key2val`, which is the cell where the new value is
stored.

    
    
    1    function _calldataVal(uint startByte, uint length)
    
    2        private pure returns (uint)
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

This function reads a value from the calldata of arbitrary length (up to 32
bytes, the word size).

    
    
    1    {
    
    2        uint _retVal;
    
    3
    
    4        require(length < 0x21,
    
    5            "_calldataVal length limit is 32 bytes");
    
    6        require(length + startByte <= msg.data.length,
    
    7            "_calldataVal trying to read beyond calldatasize");
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

This function is internal, so if the rest of the code is written correctly
these tests are not required. However, they don't cost much so we might as
well have them.

    
    
    1        assembly {
    
    2            _retVal := calldataload(startByte)
    
    3        }
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

This code is in [Yul(opens in a new
tab)](https://docs.soliditylang.org/en/v0.8.16/yul.html). It reads a 32 byte
value from the calldata. This works even if the calldata stops before
`startByte+32` because uninitialized space in EVM is considered to be zero.

    
    
    1        _retVal = _retVal >> (256-length*8);
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

We don't necessarily want a 32 byte value. This gets rid of the excess bytes.

    
    
    1        return _retVal;
    
    2    } // _calldataVal
    
    3
    
    4
    
    5    // Read a single parameter from the calldata, starting at _fromByte
    
    6    function _readParam(uint _fromByte) internal
    
    7        returns (uint _nextByte, uint _parameterValue)
    
    8    {
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Read a single parameter from the calldata. Note that we need to return not
just the value we read, but also the location of the next byte because
parameters can range from 1 byte long to 33 bytes.

    
    
    1        // The first byte tells us how to interpret the rest
    
    2        uint8 _firstByte;
    
    3
    
    4        _firstByte = uint8(_calldataVal(_fromByte, 1));
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Solidity tries to reduce the number of bugs by forbidding potentially
dangerous [implicit type conversions(opens in a new
tab)](https://docs.soliditylang.org/en/v0.8.16/types.html#implicit-
conversions). A downgrade, for example from 256 bits to 8 bits, needs to be
explicit.

    
    
    1
    
    2        // Read the value, but do not write it to the cache
    
    3        if (_firstByte == uint8(DONT_CACHE))
    
    4            return(_fromByte+33, _calldataVal(_fromByte+1, 32));
    
    5
    
    6        // Read the value, and write it to the cache
    
    7        if (_firstByte == uint8(INTO_CACHE)) {
    
    8            uint _param = _calldataVal(_fromByte+1, 32);
    
    9            cacheWrite(_param);
    
    10            return(_fromByte+33, _param);
    
    11        }
    
    12
    
    13        // If we got here it means that we need to read from the cache
    
    14
    
    15        // Number of extra bytes to read
    
    16        uint8 _extraBytes = _firstByte / 16;
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Take the lower [nibble(opens in a new
tab)](https://en.wikipedia.org/wiki/Nibble) and combine it with the other
bytes to read the value from the cache.

    
    
    1        uint _key = (uint256(_firstByte & 0x0F) << (8*_extraBytes)) +
    
    2            _calldataVal(_fromByte+1, _extraBytes);
    
    3
    
    4        return (_fromByte+_extraBytes+1, cacheRead(_key));
    
    5
    
    6    }  // _readParam
    
    7
    
    8
    
    9    // Read n parameters (functions know how many parameters they expect)
    
    10    function _readParams(uint _paramNum) internal returns (uint[] memory) {
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

We could get the number of parameters we have from the calldata itself, but
the functions that call us know how many parameters they expect. It's easier
to let them tell us.

    
    
    1        // The parameters we read
    
    2        uint[] memory params = new uint[](_paramNum);
    
    3
    
    4        // Parameters start at byte 4, before that it's the function signature
    
    5        uint _atByte = 4;
    
    6
    
    7        for(uint i=0; i<_paramNum; i++) {
    
    8            (_atByte, params[i]) = _readParam(_atByte);
    
    9        }
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Read the parameters until you have the number you need. If we go past the end
of the calldata, `_readParams` will revert the call.

    
    
    1
    
    2        return(params);
    
    3    }   // readParams
    
    4
    
    5    // For testing _readParams, test reading four parameters
    
    6    function fourParam() public
    
    7        returns (uint256,uint256,uint256,uint256)
    
    8    {
    
    9        uint[] memory params;
    
    10        params = _readParams(4);
    
    11        return (params[0], params[1], params[2], params[3]);
    
    12    }    // fourParam
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

One big advantage of Foundry is that it allows tests to be written in Solidity
(see Testing the cache below). This makes unit tests a lot easier. This is a
function that reads four parameters and returns them so the test can verify
they were correct.

    
    
    1    // Get a value, return bytes that will encode it (using the cache if possible)
    
    2    function encodeVal(uint _val) public view returns(bytes memory) {
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

`encodeVal` is a function that off-chain code calls to help create calldata
that uses the cache. It receives a single value and returns the bytes that
encode it. This function is a `view`, so it does not require a transaction and
when called externally does not cost any gas.

    
    
    1        uint _key = val2key[_val];
    
    2
    
    3        // The value isn't in the cache yet, add it
    
    4        if (_key == 0)
    
    5            return bytes.concat(INTO_CACHE, bytes32(_val));
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

In the [EVM](/en/developers/docs/evm/) all uninitialized storage is assumed to
be zeros. So if we look for the key for a value that isn't there, we get a
zero. In that case the bytes that encode it are `INTO_CACHE` (so it will be
cached next time), followed by the actual value.

    
    
    1        // If the key is <0x10, return it as a single byte
    
    2        if (_key < 0x10)
    
    3            return bytes.concat(bytes1(uint8(_key)));
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Single bytes are the easiest. We just use [`bytes.concat`(opens in a new
tab)](https://docs.soliditylang.org/en/v0.8.16/types.html#the-functions-bytes-
concat-and-string-concat) to turn a `bytes<n>` type into a byte array which
can be any length. Despite the name, it works fine when provided with just one
argument.

    
    
    1        // Two byte value, encoded as 0x1vvv
    
    2        if (_key < 0x1000)
    
    3            return bytes.concat(bytes2(uint16(_key) | 0x1000));
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

When we have a key that is less than 163, we can express it in two bytes. We
first convert `_key`, which is a 256 bit value, to a 16 bit value and use
logical or to add the number of extra bytes to the first byte. Then we just it
into a `bytes2` value, which can be converted to `bytes`.

    
    
    1        // There is probably a clever way to do the following lines as a loop,
    
    2        // but it's a view function so I'm optimizing for programmer time and
    
    3        // simplicity.
    
    4
    
    5        if (_key < 16*256**2)
    
    6            return bytes.concat(bytes3(uint24(_key) | (0x2 * 16 * 256**2)));
    
    7        if (_key < 16*256**3)
    
    8            return bytes.concat(bytes4(uint32(_key) | (0x3 * 16 * 256**3)));
    
    9             .
    
    10             .
    
    11             .
    
    12        if (_key < 16*256**14)
    
    13            return bytes.concat(bytes15(uint120(_key) | (0xE * 16 * 256**14)));
    
    14        if (_key < 16*256**15)
    
    15            return bytes.concat(bytes16(uint128(_key) | (0xF * 16 * 256**15)));
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

The other values (3 bytes, 4 bytes, etc.) are handled the same way, just with
different field sizes.

    
    
    1        // If we get here, something is wrong.
    
    2        revert("Error in encodeVal, should not happen");
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

If we get here it means we got a key that's not less than 16*25615. But
`cacheWrite` limits the keys so we can't even get up to 14*25616 (which would
have a first byte of 0xFE, so it would look like `DONT_CACHE`). But it doesn't
cost us much to add a test in case a future programmer introduces a bug.

    
    
    1    } // encodeVal
    
    2
    
    3}  // Cache
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

### Testing the cache

One of the advantages of Foundry is that [it lets you write tests in
Solidity(opens in a new tab)](https://book.getfoundry.sh/forge/tests), which
makes it easier to write unit tests. The tests for the `Cache` class are
[here(opens in a new tab)](https://github.com/qbzzt/20220915-all-you-can-
cache/blob/main/test/Cache.t.sol). Because the testing code is repetitive, as
tests tend to be, this article only explains the interesting parts.

    
    
    1// SPDX-License-Identifier: UNLICENSED
    
    2pragma solidity ^0.8.13;
    
    3
    
    4import "forge-std/Test.sol";
    
    5
    
    6
    
    7// Need to run `forge test -vv` for the console.
    
    8import "forge-std/console.sol";
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

This is just boilerplate that is necessary to use the test package and
`console.log`.

    
    
    1import "src/Cache.sol";
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

We need to know the contract we are testing.

    
    
    1contract CacheTest is Test {
    
    2    Cache cache;
    
    3
    
    4    function setUp() public {
    
    5        cache = new Cache();
    
    6    }
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

The `setUp` function is called before each test. In this case we just create a
new cache, so that our tests won't affect each other.

    
    
    1    function testCaching() public {
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Tests are functions whose names start with `test`. This function checks the
basic cache functionality, writing values and reading them again.

    
    
    1        for(uint i=1; i<5000; i++) {
    
    2            cache.cacheWrite(i*i);
    
    3        }
    
    4
    
    5        for(uint i=1; i<5000; i++) {
    
    6            assertEq(cache.cacheRead(i), i*i);
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

This is how you do the actual testing, using [`assert...` functions(opens in a
new tab)](https://book.getfoundry.sh/reference/forge-std/std-assertions). In
this case, we check that the value we wrote is the one we read. We can discard
the result of `cache.cacheWrite` because we know that cache keys are assigned
linearly.

    
    
    1        }
    
    2    }    // testCaching
    
    3
    
    4
    
    5    // Cache the same value multiple times, ensure that the key stays
    
    6    // the same
    
    7    function testRepeatCaching() public {
    
    8        for(uint i=1; i<100; i++) {
    
    9            uint _key1 = cache.cacheWrite(i);
    
    10            uint _key2 = cache.cacheWrite(i);
    
    11            assertEq(_key1, _key2);
    
    12        }
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

First we write each value twice to the cache and make sure the keys are the
same (meaning the second write didn't really happen).

    
    
    1        for(uint i=1; i<100; i+=3) {
    
    2            uint _key = cache.cacheWrite(i);
    
    3            assertEq(_key, i);
    
    4        }
    
    5    }    // testRepeatCaching
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

In theory there could be a bug that doesn't affect consecutive cache writes.
So here we do some writes that aren't consecutive and see the values are still
not rewritten.

    
    
    1    // Read a uint from a memory buffer (to make sure we get back the parameters
    
    2    // we sent out)
    
    3    function toUint256(bytes memory _bytes, uint256 _start) internal pure
    
    4        returns (uint256)
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Read a 256 bit word from a `bytes memory` buffer. This utility function lets
us verify that we receive the correct results when we run a function call that
uses the cache.

    
    
    1    {
    
    2        require(_bytes.length >= _start + 32, "toUint256_outOfBounds");
    
    3        uint256 tempUint;
    
    4
    
    5        assembly {
    
    6            tempUint := mload(add(add(_bytes, 0x20), _start))
    
    7        }
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Yul does not support data structures beyond `uint256`, so when you refer to a
more sophisticated data structure, such as the memory buffer `_bytes`, you get
the address of that structure. Solidity stores `bytes memory` values as a 32
byte word that contains the length, followed by the actual bytes, so to get
byte number `_start` we need to calculate `_bytes+32+_start`.

    
    
    1
    
    2        return tempUint;
    
    3    }     // toUint256
    
    4
    
    5    // Function signature for fourParams(), courtesy of
    
    6    // https://www.4byte.directory/signatures/?bytes4_signature=0x3edc1e6d
    
    7    bytes4 constant FOUR_PARAMS = 0x3edc1e6d;
    
    8
    
    9    // Just some constant values to see we're getting the correct values back
    
    10    uint256 constant VAL_A = 0xDEAD60A7;
    
    11    uint256 constant VAL_B =     0xBEEF;
    
    12    uint256 constant VAL_C =     0x600D;
    
    13    uint256 constant VAL_D = 0x600D60A7;
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Some constants we need for testing.

    
    
    1    function testReadParam() public {
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Call `fourParams()`, a function that uses `readParams`, to test we can read
parameters correctly.

    
    
    1        address _cacheAddr = address(cache);
    
    2        bool _success;
    
    3        bytes memory _callInput;
    
    4        bytes memory _callOutput;
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

We can't use the normal ABI mechanism to call a function using the cache, so
we need to use the low level [`<address>.call()`(opens in a new
tab)](https://docs.soliditylang.org/en/v0.8.16/types.html#members-of-
addresses) mechanism. That mechanism takes a `bytes memory` as input, and
returns that (as well as a Boolean value) as output.

    
    
    1        // First call, the cache is empty
    
    2        _callInput = bytes.concat(
    
    3            FOUR_PARAMS,
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

It is useful for the same contract to support both cached functions (for calls
directly from transactions) and non-cached functions (for calls from other
smart contracts). To do that we need to continue to rely on the Solidity
mechanism to call the correct function, instead of putting everything in [a
`fallback` function(opens in a new
tab)](https://docs.soliditylang.org/en/v0.8.16/contracts.html#fallback-
function). Doing this makes composability a lot easier. A single byte would be
enough to identify the function in most cases, so we are wasting three bytes
(16*3=48 gas). However, as I'm writing this those 48 gas cost 0.07 cents,
which is a reasonable cost of simpler, less bug prone, code.

    
    
    1            // First value, add it to the cache
    
    2            cache.INTO_CACHE(),
    
    3            bytes32(VAL_A),
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

The first value: A flag saying it's a full value that needs to be written to
the cache, followed by the 32 bytes of the value. The other three values are
similar, except that `VAL_B` isn't written to the cache and `VAL_C` is both
the third parameter and the fourth one.

    
    
    1             .
    
    2             .
    
    3             .
    
    4        );
    
    5        (_success, _callOutput) = _cacheAddr.call(_callInput);
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

This is where we actually call the `Cache` contract.

    
    
    1        assertEq(_success, true);
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

We expect the call to be successful.

    
    
    1        assertEq(cache.cacheRead(1), VAL_A);
    
    2        assertEq(cache.cacheRead(2), VAL_C);
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

We start with an empty cache and then add `VAL_A` followed by `VAL_C`. We'd
expect the first one to have the key 1, and the second one to have 2.

    
    
    1        assertEq(toUint256(_callOutput,0), VAL_A);
    
    2        assertEq(toUint256(_callOutput,32), VAL_B);
    
    3        assertEq(toUint256(_callOutput,64), VAL_C);
    
    4        assertEq(toUint256(_callOutput,96), VAL_C);

The output is the four parameters. Here we verify it is correct.

    
    
    1        // Second call, we can use the cache
    
    2        _callInput = bytes.concat(
    
    3            FOUR_PARAMS,
    
    4
    
    5            // First value in the Cache
    
    6            bytes1(0x01),
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Cache keys below 16 are just one byte.

    
    
    1            // Second value, don't add it to the cache
    
    2            cache.DONT_CACHE(),
    
    3            bytes32(VAL_B),
    
    4
    
    5            // Third and fourth values, same value
    
    6            bytes1(0x02),
    
    7            bytes1(0x02)
    
    8        );
    
    9        .
    
    10        .
    
    11        .
    
    12    }   // testReadParam
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

The tests after the call are identical to those after the first call.

    
    
    1    function testEncodeVal() public {
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

This function is similar to `testReadParam`, except that instead of writing
the parameters explicitly we use `encodeVal()`.

    
    
    1        .
    
    2        .
    
    3        .
    
    4        _callInput = bytes.concat(
    
    5            FOUR_PARAMS,
    
    6            cache.encodeVal(VAL_A),
    
    7            cache.encodeVal(VAL_B),
    
    8            cache.encodeVal(VAL_C),
    
    9            cache.encodeVal(VAL_D)
    
    10        );
    
    11        .
    
    12        .
    
    13        .
    
    14        assertEq(_callInput.length, 4+1*4);
    
    15    }   // testEncodeVal
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

The only additional test in `testEncodeVal()` is to verify that the length of
`_callInput` is correct. For the first call it is 4+33*4\. For the second,
where every value is already in the cache, it is 4+1*4.

    
    
    1    // Test encodeVal when the key is more than a single byte
    
    2    // Maximum three bytes because filling the cache to four bytes takes
    
    3    // too long.
    
    4    function testEncodeValBig() public {
    
    5        // Put a number of values in the cache.
    
    6        // To keep things simple, use key n for value n.
    
    7        for(uint i=1; i<0x1FFF; i++) {
    
    8            cache.cacheWrite(i);
    
    9        }
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

The `testEncodeVal` function above only writes four values into the cache, so
[the part of the function that deals with multi-byte values(opens in a new
tab)](https://github.com/qbzzt/20220915-all-you-can-
cache/blob/main/src/Cache.sol#L144-L171) is not checked. But that code is
complicated and error-prone.

The first part of this function is a loop that writes all the values from 1 to
0x1FFF to the cache in order, so we'll be able to encode those values and know
where they are going.

    
    
    1        .
    
    2        .
    
    3        .
    
    4
    
    5        _callInput = bytes.concat(
    
    6            FOUR_PARAMS,
    
    7            cache.encodeVal(0x000F),   // One byte        0x0F
    
    8            cache.encodeVal(0x0010),   // Two bytes     0x1010
    
    9            cache.encodeVal(0x0100),   // Two bytes     0x1100
    
    10            cache.encodeVal(0x1000)    // Three bytes 0x201000
    
    11        );
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Test one byte, two byte, and three byte values. We don't test beyond that
because it would take too long to write enough stack entries (at least
0x10000000, approximately a quarter of a billion).

    
    
    1        .
    
    2        .
    
    3        .
    
    4        .
    
    5    }    // testEncodeValBig
    
    6
    
    7
    
    8    // Test what with an excessively small buffer we get a revert
    
    9    function testShortCalldata() public {
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Test what happens in the abnormal case where there aren't enough parameters.

    
    
    1        .
    
    2        .
    
    3        .
    
    4        (_success, _callOutput) = _cacheAddr.call(_callInput);
    
    5        assertEq(_success, false);
    
    6    }   // testShortCalldata
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Since it reverts, the result we should get is `false`.

    
    
    1    // Call with cache keys that aren't there
    
    2    function testNoCacheKey() public {
    
    3        .
    
    4        .
    
    5        .
    
    6        _callInput = bytes.concat(
    
    7            FOUR_PARAMS,
    
    8
    
    9            // First value, add it to the cache
    
    10            cache.INTO_CACHE(),
    
    11            bytes32(VAL_A),
    
    12
    
    13            // Second value
    
    14            bytes1(0x0F),
    
    15            bytes2(0x1234),
    
    16            bytes11(0xA10102030405060708090A)
    
    17        );
    
    Show all

This function gets four perfectly legitimate parameters, except that the cache
is empty so there are no values there to read.

    
    
    1        .
    
    2        .
    
    3        .
    
    4    // Test what with an excessively long buffer everything works file
    
    5    function testLongCalldata() public {
    
    6        address _cacheAddr = address(cache);
    
    7        bool _success;
    
    8        bytes memory _callInput;
    
    9        bytes memory _callOutput;
    
    10
    
    11        // First call, the cache is empty
    
    12        _callInput = bytes.concat(
    
    13            FOUR_PARAMS,
    
    14
    
    15            // First value, add it to the cache
    
    16            cache.INTO_CACHE(), bytes32(VAL_A),
    
    17
    
    18            // Second value, add it to the cache
    
    19            cache.INTO_CACHE(), bytes32(VAL_B),
    
    20
    
    21            // Third value, add it to the cache
    
    22            cache.INTO_CACHE(), bytes32(VAL_C),
    
    23
    
    24            // Fourth value, add it to the cache
    
    25            cache.INTO_CACHE(), bytes32(VAL_D),
    
    26
    
    27            // And another value for "good luck"
    
    28            bytes4(0x31112233)
    
    29        );
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

This function sends five values. We know that the fifth value is ignored
because it is not a valid cache entry, which would have caused a revert had it
not been included.

    
    
    1        (_success, _callOutput) = _cacheAddr.call(_callInput);
    
    2        assertEq(_success, true);
    
    3        .
    
    4        .
    
    5        .
    
    6    }   // testLongCalldata
    
    7
    
    8}        // CacheTest
    
    9
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

## A sample application

Writing tests in Solidity is all very well, but at the end of the day a dapp
needs to be able to process requests from outside the chain to be useful. This
article demonstrates how to use caching in a dapp with `WORM`, which stands
for "Write Once, Read Many". If a key is not yet written, you can write a
value to it. If the key is written already, you get a revert.

### The contract

[This is the contract(opens in a new
tab)](https://github.com/qbzzt/20220915-all-you-can-
cache/blob/main/src/WORM.sol). It mostly repeats what we have already done
with `Cache` and `CacheTest`, so we only cover the parts that are interesting.

    
    
    1import "./Cache.sol";
    
    2
    
    3contract WORM is Cache {
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

The easiest way to use `Cache` is to inherit it in our own contract.

    
    
    1    function writeEntryCached() external {
    
    2        uint[] memory params = _readParams(2);
    
    3        writeEntry(params[0], params[1]);
    
    4    }    // writeEntryCached
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

This function is similar to `fourParam` in `CacheTest` above. Because we don't
follow the ABI specifications, it is best not to declare any parameters into
the function.

    
    
    1    // Make it easier to call us
    
    2    // Function signature for writeEntryCached(), courtesy of
    
    3    // https://www.4byte.directory/signatures/?bytes4_signature=0xe4e4f2d3
    
    4    bytes4 constant public WRITE_ENTRY_CACHED = 0xe4e4f2d3;
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

The external code that calls `writeEntryCached` will need to manually build
the calldata, instead of using `worm.writeEntryCached`, because we do not
follow the ABI specifications. Having this constant value just makes it easier
to write it.

Note that even though we define `WRITE_ENTRY_CACHED` as a state variable, to
read it externally it is necessary to use the getter function for it,
`worm.WRITE_ENTRY_CACHED()`.

    
    
    1    function readEntry(uint key) public view
    
    2        returns (uint _value, address _writtenBy, uint _writtenAtBlock)
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

The read function is a `view`, so it does not require a transaction and does
not cost gas. As a result, there is no benefit to using the cache for the
parameter. With view functions it is best to use the standard mechanism that
is simpler.

### The testing code

[This is the testing code for the contract(opens in a new
tab)](https://github.com/qbzzt/20220915-all-you-can-
cache/blob/main/test/WORM.t.sol). Again, let us look only at what is
interesting.

    
    
    1    function testWReadWrite() public {
    
    2        worm.writeEntry(0xDEAD, 0x60A7);
    
    3
    
    4        vm.expectRevert(bytes("entry already written"));
    
    5        worm.writeEntry(0xDEAD, 0xBEEF);
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

[This (`vm.expectRevert`)(opens in a new
tab)](https://book.getfoundry.sh/cheatcodes/expect-revert#expectrevert) is how
we specify in a Foundry test that the next call should fail, and the reported
reason for a failure. This applies when we use the syntax
`<contract>.<function name>()` rather than building the calldata and calling
the contract using the low level interface (`<contract>.call()`, etc.).

    
    
    1    function testReadWriteCached() public {
    
    2        uint cacheGoat = worm.cacheWrite(0x60A7);
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Here we use the fact that `cacheWrite` returns the cache key. This is not
something we'd expect to use in production, because `cacheWrite` changes the
state, and therefore can only be called during a transaction. Transactions
don't have return values, if they have results those results are supposed to
be emitted as events. So the `cacheWrite` return value is only accessible from
on-chain code, and on-chain code does not need parameter caching.

    
    
    1        (_success,) = address(worm).call(_callInput);
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

This is how we tell Solidity that while `<contract address>.call()` has two
return values, we only care about the first.

    
    
    1        (_success,) = address(worm).call(_callInput);
    
    2        assertEq(_success, false);
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Since we use the low level `<address>.call()` function, we can't use
`vm.expectRevert()` and have to look at the boolean success value we get from
the call.

    
    
    1    event EntryWritten(uint indexed key, uint indexed value);
    
    2
    
    3        .
    
    4        .
    
    5        .
    
    6
    
    7        _callInput = bytes.concat(
    
    8            worm.WRITE_ENTRY_CACHED(), worm.encodeVal(a), worm.encodeVal(b));
    
    9        vm.expectEmit(true, true, false, false);
    
    10        emit EntryWritten(a, b);
    
    11        (_success,) = address(worm).call(_callInput);
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

This is the way we verify that code [emits an event correctly(opens in a new
tab)](https://book.getfoundry.sh/cheatcodes/expect-emit) in Foundry.

### The client

One thing you don't get with Solidity tests is JavaScript code you can cut and
paste into your own application. To write that code I deployed WORM to
[Optimism Goerli(opens in a new
tab)](https://community.optimism.io/docs/useful-tools/networks/#optimism-
goerli), [Optimism's(opens in a new tab)](https://www.optimism.io/) new
testnet. It is at address [`0xd34335b1d818cee54e3323d3246bd31d94e6a78a`(opens
in a new tab)](https://goerli-
optimism.etherscan.io/address/0xd34335b1d818cee54e3323d3246bd31d94e6a78a).

[You can see JavaScript code for the client here(opens in a new
tab)](https://github.com/qbzzt/20220915-all-you-can-
cache/blob/main/javascript/index.js). To use it:

  1. Clone the git repository:
    
        1git clone https://github.com/qbzzt/20220915-all-you-can-cache.git

  2. Install the necessary packages:
    
        1cd javascript
    
    2yarn

  3. Copy the configuration file:
    
        1cp .env.example .env

  4. Edit `.env` for your configuration:

Parameter| Value  
---|---  
MNEMONIC| The mnemonic for an account that has enough ETH to pay for a
transaction. [You can get free ETH for the Optimism Goerli network here(opens
in a new tab)](https://optimismfaucet.xyz/).  
OPTIMISM_GOERLI_URL| URL to Optimism Goerli. The public endpoint,
`https://goerli.optimism.io`, is rate limited but sufficient to what we need
here  
  
  5. Run `index.js`.
    
        1node index.js

This sample application first writes an entry to WORM, displaying the calldata
and a link to the transaction on Etherscan. Then it reads back that entry, and
displays the key it uses and the values in the entry (value, block number, and
author).

Most of the client is normal Dapp JavaScript. So again we'll only go over the
interesting parts.

    
    
    1.
    
    2.
    
    3.
    
    4const main = async () => {
    
    5    const func = await worm.WRITE_ENTRY_CACHED()
    
    6
    
    7    // Need a new key every time
    
    8    const key = await worm.encodeVal(Number(new Date()))

A given slot can only be written into once, so we use the timestamp to make
sure we don't reuse slots.

    
    
    1const val = await worm.encodeVal("0x600D")
    
    2
    
    3// Write an entry
    
    4const calldata = func + key.slice(2) + val.slice(2)

Ethers expects the call data to be a hex string, `0x` followed by an even
number of hexadecimal digits. As `key` and `val` both start with `0x`, we need
to remove those headers.

    
    
    1const tx = await worm.populateTransaction.writeEntryCached()
    
    2tx.data = calldata
    
    3
    
    4sentTx = await wallet.sendTransaction(tx)

As with the Solidity testing code, we cannot call a cached function normally.
Instead, we need to use a lower level mechanism.

    
    
    1    .
    
    2    .
    
    3    .
    
    4    // Read the entry just written
    
    5    const realKey = '0x' + key.slice(4)  // remove the FF flag
    
    6    const entryRead = await worm.readEntry(realKey)
    
    7    .
    
    8    .
    
    9    .
    
    Show all

For reading entries we can use the normal mechanism. There's no need to use
parameter caching with `view` functions.

## Conclusion

The code in this article is a proof of concept, the purpose is to make the
idea easy to understand. For a production-ready system you might want to
implement some additional functionality:

  * Handle values that aren't `uint256`. For example, strings.

  * Instead of a global cache, maybe have a mapping between users and caches. Different users use different values.

  * Values used for addresses are distinct from those used for other purposes. It might make sense to have a separate cache just for addresses.

  * Currently, the cache keys are on a "first come, smallest key" algorithm. The first sixteen values can be sent as a single byte. The next 4080 values can be sent as two bytes. The next approximately million values are three bytes, etc. A production system should keep usage counters on cache entries and reorganize them so that the sixteen _most common_ values are one byte, the next 4080 most common values two bytes, etc.

However, that is a potentially dangerous operation. Imagine the following
sequence of events:

    1. Noam Naive calls `encodeVal` to encode the address to which he wants to send tokens. That address is one of the first used on the application, so the encoded value is 0x06. This is a `view` function, not a transaction, so it's between Noam and the node he uses, and nobody else knows about it

    2. Owen Owner runs the cache reordering operation. Very few people actually use that address, so it is now encoded as 0x201122. A different value, 1018, is assigned 0x06.

    3. Noam Naive sends his tokens to 0x06. They go to the address `0x0000000000000000000000000de0b6b3a7640000`, and since nobody knows the private key for that address, they are just stuck there. Noam is _not happy_.

There are ways to solve this problem, and the related problem of transactions
that are in the mempool during the cache reorder, but you must be aware of it.

I demonstrated caching here with Optimism, because I'm an Optimism employee
and this is the rollup I know best. But it should work with any rollup that
charges a minimal cost for internal processing, so that in comparison writing
the transaction data to L1 is the major expense.

n

Last edit: [@nhsz(opens in a new tab)](https://github.com/nhsz), August 15,
2023

See contributors

### Was this tutorial helpful?

YesNo

  * [Edit page(opens in a new tab)](https://github.com/ethereum/ethereum-org-website/tree/dev/public/content/developers/tutorials/all-you-can-cache/index.md)
  * On this page

    * Overall design
    * Cache manipulation
      * Testing the cache
    * A sample application
      * The contract
      * The testing code
      * The client
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

