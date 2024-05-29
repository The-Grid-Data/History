Skip to main content

[](/en/)

  * Learn
  * Use
  * Build
  * Participate
  * Research

Search```K`

Languages EN

# Optimism standard bridge contract walkthrough

soliditybridgelayer 2

Intermediate

![✍️](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/270d.svg)Ori
Pomerantz

![📆](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4c6.svg)
March 30, 2022

![⏱️](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/23f1.svg)33
minute read minute read

On this page

  * Control flows
    * Deposit flow
    * Withdrawal flow
  * Layer 1 code
    * IL1ERC20Bridge
    * IL1StandardBridge
    * CrossDomainEnabled
    * The L1 bridge contract
  * ERC-20 Tokens on L2
    * IL2StandardERC20
    * L2StandardERC20
  * L2 Bridge Code
  * Conclusion

[Optimism(opens in a new tab)](https://www.optimism.io/) is an [Optimistic
Rollup](/en/developers/docs/scaling/optimistic-rollups/). Optimistic rollups
can process transactions for a much lower price than Ethereum Mainnet (also
known as layer 1 or L1) because transactions are only processed by a few
nodes, instead of every node on the network. At the same time, the data is all
written to L1 so everything can be proved and reconstructed with all the
integrity and availability guarantees of Mainnet.

To use L1 assets on Optimism (or any other L2), the assets need to be
[bridged](/en/bridges/#prerequisites). One way to achieve this is for users to
lock assets (ETH and [ERC-20
tokens](/en/developers/docs/standards/tokens/erc-20/) are the most common
ones) on L1, and receive equivalent assets to use on L2. Eventually, whoever
ends up with them might want to bridge them back to L1. When doing this, the
assets are burned on L2 and then released back to the user on L1.

This is the way the [Optimism standard bridge(opens in a new
tab)](https://community.optimism.io/docs/developers/bridge/standard-bridge)
works. In this article we go over the source code for that bridge to see how
it works and study it as an example of well written Solidity code.

## Control flows

The bridge has two main flows:

  * Deposit (from L1 to L2)
  * Withdrawal (from L2 to L1)

### Deposit flow

#### Layer 1

  1. If depositing an ERC-20, the depositor gives the bridge an allowance to spend the amount being deposited
  2. The depositor calls the L1 bridge (`depositERC20`, `depositERC20To`, `depositETH`, or `depositETHTo`)
  3. The L1 bridge takes possession of the bridged asset
     * ETH: The asset is transferred by the depositor as part of the call
     * ERC-20: The asset is transferred by the bridge to itself using the allowance provided by the depositor
  4. The L1 bridge uses the cross-domain message mechanism to call `finalizeDeposit` on the L2 bridge

#### Layer 2

  5. The L2 bridge verifies the call to `finalizeDeposit` is legitimate:
     * Came from the cross domain message contract
     * Was originally from the bridge on L1
  6. The L2 bridge checks if the ERC-20 token contract on L2 is the correct one:
     * The L2 contract reports that its L1 counterpart is the same as the one the tokens came from on L1
     * The L2 contract reports that it supports the correct interface ([using ERC-165(opens in a new tab)](https://eips.ethereum.org/EIPS/eip-165)).
  7. If the L2 contract is the correct one, call it to mint the appropriate number of tokens to the appropriate address. If not, start a withdrawal process to allow the user to claim the tokens on L1.

### Withdrawal flow

#### Layer 2

  1. The withdrawer calls the L2 bridge (`withdraw` or `withdrawTo`)
  2. The L2 bridge burns the appropriate number of tokens belonging to `msg.sender`
  3. The L2 bridge uses the cross-domain message mechanism to call `finalizeETHWithdrawal` or `finalizeERC20Withdrawal` on the L1 bridge

#### Layer 1

  4. The L1 bridge verifies the call to `finalizeETHWithdrawal` or `finalizeERC20Withdrawal` is legitimate:
     * Came from the cross domain message mechanism
     * Was originally from the bridge on L2
  5. The L1 bridge transfers the appropriate asset (ETH or ERC-20) to the appropriate address

## Layer 1 code

This is the code that runs on L1, the Ethereum Mainnet.

### IL1ERC20Bridge

[This interface is defined here(opens in a new
tab)](https://github.com/ethereum-
optimism/optimism/blob/develop/packages/contracts/contracts/L1/messaging/IL1ERC20Bridge.sol).
It includes functions and definitions required for bridging ERC-20 tokens.

    
    
    1// SPDX-License-Identifier: MIT
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

[Most of Optimism's code is released under the MIT license(opens in a new
tab)](https://help.optimism.io/hc/en-us/articles/4411908707995-What-software-
license-does-Optimism-use-).

    
    
    1pragma solidity >0.5.0 <0.9.0;
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

At writing the latest version of Solidity is 0.8.12. Until version 0.9.0 is
released, we don't know if this code is compatible with it or not.

    
    
    1/**
    
    2 * @title IL1ERC20Bridge
    
    3 */
    
    4interface IL1ERC20Bridge {
    
    5    /**********
    
    6     * Events *
    
    7     **********/
    
    8
    
    9    event ERC20DepositInitiated(
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

In Optimism bridge terminology _deposit_ means transfer from L1 to L2, and
_withdrawal_ means a transfer from L2 to L1.

    
    
    1        address indexed _l1Token,
    
    2        address indexed _l2Token,
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

In most cases the address of an ERC-20 on L1 is not the same the address of
the equivalent ERC-20 on L2. [You can see the list of token addresses
here(opens in a new tab)](https://static.optimism.io/optimism.tokenlist.json).
The address with `chainId` 1 is on L1 (Mainnet) and the address with `chainId`
10 is on L2 (Optimism). The other two `chainId` values are for the Kovan test
network (42) and the Optimistic Kovan test network (69).

    
    
    1        address indexed _from,
    
    2        address _to,
    
    3        uint256 _amount,
    
    4        bytes _data
    
    5    );
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

It is possible to add notes to transfers, in which case they are added to the
events that report them.

    
    
    1    event ERC20WithdrawalFinalized(
    
    2        address indexed _l1Token,
    
    3        address indexed _l2Token,
    
    4        address indexed _from,
    
    5        address _to,
    
    6        uint256 _amount,
    
    7        bytes _data
    
    8    );
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

The same bridge contract handles transfers in both directions. In the case of
the L1 bridge, this means initialization of deposits and finalization of
withdrawals.

    
    
    1
    
    2    /********************
    
    3     * Public Functions *
    
    4     ********************/
    
    5
    
    6    /**
    
    7     * @dev get the address of the corresponding L2 bridge contract.
    
    8     * @return Address of the corresponding L2 bridge contract.
    
    9     */
    
    10    function l2TokenBridge() external returns (address);
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

This function is not really needed, because on L2 it is a predeployed
contract, so it is always at address
`0x4200000000000000000000000000000000000010`. It is here for symmetry with the
L2 bridge, because the address of the L1 bridge is _not_ trivial to know.

    
    
    1    /**
    
    2     * @dev deposit an amount of the ERC20 to the caller's balance on L2.
    
    3     * @param _l1Token Address of the L1 ERC20 we are depositing
    
    4     * @param _l2Token Address of the L1 respective L2 ERC20
    
    5     * @param _amount Amount of the ERC20 to deposit
    
    6     * @param _l2Gas Gas limit required to complete the deposit on L2.
    
    7     * @param _data Optional data to forward to L2. This data is provided
    
    8     *        solely as a convenience for external contracts. Aside from enforcing a maximum
    
    9     *        length, these contracts provide no guarantees about its content.
    
    10     */
    
    11    function depositERC20(
    
    12        address _l1Token,
    
    13        address _l2Token,
    
    14        uint256 _amount,
    
    15        uint32 _l2Gas,
    
    16        bytes calldata _data
    
    17    ) external;
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

The `_l2Gas` parameter is the amount of L2 gas the transaction is allowed to
spend. [Up to a certain (high) limit, this is free(opens in a new
tab)](https://community.optimism.io/docs/developers/bridge/messaging/#for-l1-%E2%87%92-l2-transactions-2),
so unless the ERC-20 contract does something really strange when minting, it
should not be an issue. This function takes care of the common scenario, where
a user bridges assets to the same address on a different blockchain.

    
    
    1    /**
    
    2     * @dev deposit an amount of ERC20 to a recipient's balance on L2.
    
    3     * @param _l1Token Address of the L1 ERC20 we are depositing
    
    4     * @param _l2Token Address of the L1 respective L2 ERC20
    
    5     * @param _to L2 address to credit the withdrawal to.
    
    6     * @param _amount Amount of the ERC20 to deposit.
    
    7     * @param _l2Gas Gas limit required to complete the deposit on L2.
    
    8     * @param _data Optional data to forward to L2. This data is provided
    
    9     *        solely as a convenience for external contracts. Aside from enforcing a maximum
    
    10     *        length, these contracts provide no guarantees about its content.
    
    11     */
    
    12    function depositERC20To(
    
    13        address _l1Token,
    
    14        address _l2Token,
    
    15        address _to,
    
    16        uint256 _amount,
    
    17        uint32 _l2Gas,
    
    18        bytes calldata _data
    
    19    ) external;
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

This function is almost identical to `depositERC20`, but it lets you send the
ERC-20 to a different address.

    
    
    1    /*************************
    
    2     * Cross-chain Functions *
    
    3     *************************/
    
    4
    
    5    /**
    
    6     * @dev Complete a withdrawal from L2 to L1, and credit funds to the recipient's balance of the
    
    7     * L1 ERC20 token.
    
    8     * This call will fail if the initialized withdrawal from L2 has not been finalized.
    
    9     *
    
    10     * @param _l1Token Address of L1 token to finalizeWithdrawal for.
    
    11     * @param _l2Token Address of L2 token where withdrawal was initiated.
    
    12     * @param _from L2 address initiating the transfer.
    
    13     * @param _to L1 address to credit the withdrawal to.
    
    14     * @param _amount Amount of the ERC20 to deposit.
    
    15     * @param _data Data provided by the sender on L2. This data is provided
    
    16     *   solely as a convenience for external contracts. Aside from enforcing a maximum
    
    17     *   length, these contracts provide no guarantees about its content.
    
    18     */
    
    19    function finalizeERC20Withdrawal(
    
    20        address _l1Token,
    
    21        address _l2Token,
    
    22        address _from,
    
    23        address _to,
    
    24        uint256 _amount,
    
    25        bytes calldata _data
    
    26    ) external;
    
    27}
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Withdrawals (and other messages from L2 to L1) in Optimism are a two step
process:

  1. An initiating transaction on L2.
  2. A finalizing or claiming transaction on L1. This transaction needs to happen after the [fault challenge period(opens in a new tab)](https://community.optimism.io/docs/how-optimism-works/#fault-proofs) for the L2 transaction ends.

### IL1StandardBridge

[This interface is defined here(opens in a new
tab)](https://github.com/ethereum-
optimism/optimism/blob/develop/packages/contracts/contracts/L1/messaging/IL1StandardBridge.sol).
This file contains event and function definitions for ETH. These definitions
are very similar to those defined in `IL1ERC20Bridge` above for ERC-20.

The bridge interface is divided between two files because some ERC-20 tokens
require custom processing and cannot be handled by the standard bridge. This
way the custom bridge that handles such a token can implement `IL1ERC20Bridge`
and not have to also bridge ETH.

    
    
    1// SPDX-License-Identifier: MIT
    
    2pragma solidity >0.5.0 <0.9.0;
    
    3
    
    4import "./IL1ERC20Bridge.sol";
    
    5
    
    6/**
    
    7 * @title IL1StandardBridge
    
    8 */
    
    9interface IL1StandardBridge is IL1ERC20Bridge {
    
    10    /**********
    
    11     * Events *
    
    12     **********/
    
    13    event ETHDepositInitiated(
    
    14        address indexed _from,
    
    15        address indexed _to,
    
    16        uint256 _amount,
    
    17        bytes _data
    
    18    );
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

This event is nearly identical to the ERC-20 version
(`ERC20DepositInitiated`), except without the L1 and L2 token addresses. The
same is true for the other events and the functions.

    
    
    1    event ETHWithdrawalFinalized(
    
    2        .
    
    3        .
    
    4        .
    
    5    );
    
    6
    
    7    /********************
    
    8     * Public Functions *
    
    9     ********************/
    
    10
    
    11    /**
    
    12     * @dev Deposit an amount of the ETH to the caller's balance on L2.
    
    13            .
    
    14            .
    
    15            .
    
    16     */
    
    17    function depositETH(uint32 _l2Gas, bytes calldata _data) external payable;
    
    18
    
    19    /**
    
    20     * @dev Deposit an amount of ETH to a recipient's balance on L2.
    
    21            .
    
    22            .
    
    23            .
    
    24     */
    
    25    function depositETHTo(
    
    26        address _to,
    
    27        uint32 _l2Gas,
    
    28        bytes calldata _data
    
    29    ) external payable;
    
    30
    
    31    /*************************
    
    32     * Cross-chain Functions *
    
    33     *************************/
    
    34
    
    35    /**
    
    36     * @dev Complete a withdrawal from L2 to L1, and credit funds to the recipient's balance of the
    
    37     * L1 ETH token. Since only the xDomainMessenger can call this function, it will never be called
    
    38     * before the withdrawal is finalized.
    
    39                .
    
    40                .
    
    41                .
    
    42     */
    
    43    function finalizeETHWithdrawal(
    
    44        address _from,
    
    45        address _to,
    
    46        uint256 _amount,
    
    47        bytes calldata _data
    
    48    ) external;
    
    49}
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

### CrossDomainEnabled

[This contract(opens in a new tab)](https://github.com/ethereum-
optimism/optimism/blob/develop/packages/contracts/contracts/libraries/bridge/CrossDomainEnabled.sol)
is inherited by both bridges (L1 and L2) to send messages to the other layer.

    
    
    1// SPDX-License-Identifier: MIT
    
    2pragma solidity >0.5.0 <0.9.0;
    
    3
    
    4/* Interface Imports */
    
    5import { ICrossDomainMessenger } from "./ICrossDomainMessenger.sol";
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

[This interface(opens in a new tab)](https://github.com/ethereum-
optimism/optimism/blob/develop/packages/contracts/contracts/libraries/bridge/ICrossDomainMessenger.sol)
tells the contract how to send messages to the other layer, using the cross
domain messenger. This cross domain messenger is a whole other system, and
deserves its own article, which I hope to write in the future.

    
    
    1/**
    
    2 * @title CrossDomainEnabled
    
    3 * @dev Helper contract for contracts performing cross-domain communications
    
    4 *
    
    5 * Compiler used: defined by inheriting contract
    
    6 */
    
    7contract CrossDomainEnabled {
    
    8    /*************
    
    9     * Variables *
    
    10     *************/
    
    11
    
    12    // Messenger contract used to send and receive messages from the other domain.
    
    13    address public messenger;
    
    14
    
    15    /***************
    
    16     * Constructor *
    
    17     ***************/
    
    18
    
    19    /**
    
    20     * @param _messenger Address of the CrossDomainMessenger on the current layer.
    
    21     */
    
    22    constructor(address _messenger) {
    
    23        messenger = _messenger;
    
    24    }
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

The one parameter that the contract needs to know, the address of the cross
domain messenger on this layer. This parameter is set once, in the
constructor, and never changes.

    
    
    1
    
    2    /**********************
    
    3     * Function Modifiers *
    
    4     **********************/
    
    5
    
    6    /**
    
    7     * Enforces that the modified function is only callable by a specific cross-domain account.
    
    8     * @param _sourceDomainAccount The only account on the originating domain which is
    
    9     *  authenticated to call this function.
    
    10     */
    
    11    modifier onlyFromCrossDomainAccount(address _sourceDomainAccount) {
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

The cross domain messaging is accessible by any contract on the blockchain
where it is running (either Ethereum mainnet or Optimism). But we need the
bridge on each side to _only_ trust certain messages if they come from the
bridge on the other side.

    
    
    1        require(
    
    2            msg.sender == address(getCrossDomainMessenger()),
    
    3            "OVM_XCHAIN: messenger contract unauthenticated"
    
    4        );
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Only messages from the appropriate cross domain messenger (`messenger`, as you
see below) can be trusted.

    
    
    1
    
    2        require(
    
    3            getCrossDomainMessenger().xDomainMessageSender() == _sourceDomainAccount,
    
    4            "OVM_XCHAIN: wrong sender of cross-domain message"
    
    5        );
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

The way the cross domain messenger provides the address that sent a message
with the other layer is [the `.xDomainMessageSender()` function(opens in a new
tab)](https://github.com/ethereum-
optimism/optimism/blob/develop/packages/contracts/contracts/L1/messaging/L1CrossDomainMessenger.sol#L122-L128).
As long as it is called in the transaction that was initiated by the message
it can provide this information.

We need to make sure that the message we received came from the other bridge.

    
    
    1
    
    2        _;
    
    3    }
    
    4
    
    5    /**********************
    
    6     * Internal Functions *
    
    7     **********************/
    
    8
    
    9    /**
    
    10     * Gets the messenger, usually from storage. This function is exposed in case a child contract
    
    11     * needs to override.
    
    12     * @return The address of the cross-domain messenger contract which should be used.
    
    13     */
    
    14    function getCrossDomainMessenger() internal virtual returns (ICrossDomainMessenger) {
    
    15        return ICrossDomainMessenger(messenger);
    
    16    }
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

This function returns the cross domain messenger. We use a function rather
than the variable `messenger` to allow contracts that inherit from this one to
use an algorithm to specify which cross domain messenger to use.

    
    
    1
    
    2    /**
    
    3     * Sends a message to an account on another domain
    
    4     * @param _crossDomainTarget The intended recipient on the destination domain
    
    5     * @param _message The data to send to the target (usually calldata to a function with
    
    6     *  `onlyFromCrossDomainAccount()`)
    
    7     * @param _gasLimit The gasLimit for the receipt of the message on the target domain.
    
    8     */
    
    9    function sendCrossDomainMessage(
    
    10        address _crossDomainTarget,
    
    11        uint32 _gasLimit,
    
    12        bytes memory _message
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Finally, the function that sends a message to the other layer.

    
    
    1    ) internal {
    
    2        // slither-disable-next-line reentrancy-events, reentrancy-benign
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

[Slither(opens in a new tab)](https://github.com/crytic/slither) is a static
analyzer Optimism runs on every contract to look for vulnerabilities and other
potential problems. In this case, the following line triggers two
vulnerabilities:

  1. [Reentrancy events(opens in a new tab)](https://github.com/crytic/slither/wiki/Detector-Documentation#reentrancy-vulnerabilities-3)
  2. [Benign reentrancy(opens in a new tab)](https://github.com/crytic/slither/wiki/Detector-Documentation#reentrancy-vulnerabilities-2)

    
    
    1        getCrossDomainMessenger().sendMessage(_crossDomainTarget, _message, _gasLimit);
    
    2    }
    
    3}
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

In this case we are not worried about reentrancy we know
`getCrossDomainMessenger()` returns a trustworthy address, even if Slither has
no way to know that.

### The L1 bridge contract

[The source code for this contract is here(opens in a new
tab)](https://github.com/ethereum-
optimism/optimism/blob/develop/packages/contracts/contracts/L1/messaging/L1StandardBridge.sol).

    
    
    1// SPDX-License-Identifier: MIT
    
    2pragma solidity ^0.8.9;
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

The interfaces can be part of other contracts, so they have to support a wide
range of Solidity versions. But the bridge itself is our contract, and we can
be strict about what Solidity version it uses.

    
    
    1/* Interface Imports */
    
    2import { IL1StandardBridge } from "./IL1StandardBridge.sol";
    
    3import { IL1ERC20Bridge } from "./IL1ERC20Bridge.sol";
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

IL1ERC20Bridge and IL1StandardBridge are explained above.

    
    
    1import { IL2ERC20Bridge } from "../../L2/messaging/IL2ERC20Bridge.sol";
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

[This interface(opens in a new tab)](https://github.com/ethereum-
optimism/optimism/blob/develop/packages/contracts/contracts/L2/messaging/IL2ERC20Bridge.sol)
lets us create messages to control the standard bridge on L2.

    
    
    1import { IERC20 } from "@openzeppelin/contracts/token/ERC20/IERC20.sol";
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

[This interface(opens in a new
tab)](https://github.com/OpenZeppelin/openzeppelin-
contracts/blob/master/contracts/token/ERC20/IERC20.sol) lets us control ERC-20
contracts. [You can read more about it
here](/en/developers/tutorials/erc20-annotated-code/#the-interface).

    
    
    1/* Library Imports */
    
    2import { CrossDomainEnabled } from "../../libraries/bridge/CrossDomainEnabled.sol";
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

As explained above, this contract is used for interlayer messaging.

    
    
    1import { Lib_PredeployAddresses } from "../../libraries/constants/Lib_PredeployAddresses.sol";
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

[`Lib_PredeployAddresses`(opens in a new tab)](https://github.com/ethereum-
optimism/optimism/blob/develop/packages/contracts/contracts/libraries/constants/Lib_PredeployAddresses.sol)
has the addresses for the L2 contracts that always have the same address. This
includes the standard bridge on L2.

    
    
    1import { Address } from "@openzeppelin/contracts/utils/Address.sol";
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

[OpenZeppelin's Address utilities(opens in a new
tab)](https://github.com/OpenZeppelin/openzeppelin-
contracts/blob/master/contracts/utils/Address.sol). It is used to distinguish
between contract addresses and those belonging to externally owned accounts
(EOA).

Note that this isn't a perfect solution, because there is no way to
distinguish between direct calls and calls made from a contract's constructor,
but at least this lets us identify and prevent some common user errors.

    
    
    1import { SafeERC20 } from "@openzeppelin/contracts/token/ERC20/utils/SafeERC20.sol";
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

[The ERC-20 standard(opens in a new
tab)](https://eips.ethereum.org/EIPS/eip-20) supports two ways for a contract
to report failure:

  1. Revert
  2. Return `false`

Handling both cases would make our code more complicated, so instead we use
[OpenZeppelin's `SafeERC20`(opens in a new
tab)](https://github.com/OpenZeppelin/openzeppelin-
contracts/blob/master/contracts/token/ERC20/utils/SafeERC20.sol), which makes
sure [all failures result in a revert(opens in a new
tab)](https://github.com/OpenZeppelin/openzeppelin-
contracts/blob/master/contracts/token/ERC20/utils/SafeERC20.sol#L96).

    
    
    1/**
    
    2 * @title L1StandardBridge
    
    3 * @dev The L1 ETH and ERC20 Bridge is a contract which stores deposited L1 funds and standard
    
    4 * tokens that are in use on L2. It synchronizes a corresponding L2 Bridge, informing it of deposits
    
    5 * and listening to it for newly finalized withdrawals.
    
    6 *
    
    7 */
    
    8contract L1StandardBridge is IL1StandardBridge, CrossDomainEnabled {
    
    9    using SafeERC20 for IERC20;
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

This line is how we specify to use the `SafeERC20` wrapper every time we use
the `IERC20` interface.

    
    
    1
    
    2    /********************************
    
    3     * External Contract References *
    
    4     ********************************/
    
    5
    
    6    address public l2TokenBridge;
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

The address of L2StandardBridge.

    
    
    1
    
    2    // Maps L1 token to L2 token to balance of the L1 token deposited
    
    3    mapping(address => mapping(address => uint256)) public deposits;
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

A double [mapping(opens in a new
tab)](https://www.tutorialspoint.com/solidity/solidity_mappings.htm) like this
is the way you define a [two-dimensional sparse array(opens in a new
tab)](https://en.wikipedia.org/wiki/Sparse_matrix). Values in this data
structure are identified as `deposit[L1 token addr][L2 token addr]`. The
default value is zero. Only cells that are set to a different value are
written to storage.

    
    
    1
    
    2    /***************
    
    3     * Constructor *
    
    4     ***************/
    
    5
    
    6    // This contract lives behind a proxy, so the constructor parameters will go unused.
    
    7    constructor() CrossDomainEnabled(address(0)) {}
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

To want to be able to upgrade this contract without having to copy all the
variables in the storage. To do that we use a [`Proxy`(opens in a new
tab)](https://docs.openzeppelin.com/contracts/3.x/api/proxy), a contract that
uses [`delegatecall`(opens in a new tab)](https://solidity-by-
example.org/delegatecall/) to transfer calls to a separate contact whose
address is stored by the proxy contract (when you upgrade you tell the proxy
to change that address). When you use `delegatecall` the storage remains the
storage of the _calling_ contract, so the values of all the contract state
variables are unaffected.

One effect of this pattern is that the storage of the contract that is the
_called_ of `delegatecall` is not used and therefore the constructor values
passed to it do not matter. This is the reason we can provide a nonsensical
value to the `CrossDomainEnabled` constructor. It is also the reason the
initialization below is separate from the constructor.

    
    
    1    /******************
    
    2     * Initialization *
    
    3     ******************/
    
    4
    
    5    /**
    
    6     * @param _l1messenger L1 Messenger address being used for cross-chain communications.
    
    7     * @param _l2TokenBridge L2 standard bridge address.
    
    8     */
    
    9    // slither-disable-next-line external-function
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

This [Slither test(opens in a new
tab)](https://github.com/crytic/slither/wiki/Detector-Documentation#public-
function-that-could-be-declared-external) identifies functions that are not
called from the contract code and could therefore be declared `external`
instead of `public`. The gas cost of `external` functions can be lower,
because they can be provided with parameters in the calldata. Functions
declared `public` have to be accessible from within the contract. Contracts
cannot modify their own calldata, so the parameters have to be in memory. When
such a function is called externally, it is necessary to copy the calldata to
memory, which costs gas. In this case the function is only called once, so the
inefficiency does not matter to us.

    
    
    1    function initialize(address _l1messenger, address _l2TokenBridge) public {
    
    2        require(messenger == address(0), "Contract has already been initialized.");
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

The `initialize` function should only be called once. If the address of either
the L1 cross domain messenger or the L2 token bridge changes, we create a new
proxy and a new bridge that calls it. This is unlikely to happen except when
the entire system is upgraded, a very rare occurrence.

Note that this function does not have any mechanism that restricts _who_ can
call it. This means that in theory an attacker could wait until we deploy the
proxy and the first version of the bridge and then [front-run(opens in a new
tab)](https://solidity-by-example.org/hacks/front-running/) to get to the
`initialize` function before the legitimate user does. But there are two
methods to prevent this:

  1. If the contracts are deployed not directly by an EOA but [in a transaction that has another contract create them(opens in a new tab)](https://medium.com/upstate-interactive/creating-a-contract-with-a-smart-contract-bdb67c5c8595) the entire process can be atomic, and finish before any other transaction is executed.
  2. If the legitimate call to `initialize` fails it is always possible to ignore the newly created proxy and bridge and create new ones.

    
    
    1        messenger = _l1messenger;
    
    2        l2TokenBridge = _l2TokenBridge;
    
    3    }
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

These are the two parameters that the bridge needs to know.

    
    
    1
    
    2    /**************
    
    3     * Depositing *
    
    4     **************/
    
    5
    
    6    /** @dev Modifier requiring sender to be EOA.  This check could be bypassed by a malicious
    
    7     *  contract via initcode, but it takes care of the user error we want to avoid.
    
    8     */
    
    9    modifier onlyEOA() {
    
    10        // Used to stop deposits from contracts (avoid accidentally lost tokens)
    
    11        require(!Address.isContract(msg.sender), "Account not EOA");
    
    12        _;
    
    13    }
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

This is the reason we needed OpenZeppelin's `Address` utilities.

    
    
    1    /**
    
    2     * @dev This function can be called with no data
    
    3     * to deposit an amount of ETH to the caller's balance on L2.
    
    4     * Since the receive function doesn't take data, a conservative
    
    5     * default amount is forwarded to L2.
    
    6     */
    
    7    receive() external payable onlyEOA {
    
    8        _initiateETHDeposit(msg.sender, msg.sender, 200_000, bytes(""));
    
    9    }
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

This function exists for testing purposes. Notice that it doesn't appear in
the interface definitions - it isn't for normal use.

    
    
    1    /**
    
    2     * @inheritdoc IL1StandardBridge
    
    3     */
    
    4    function depositETH(uint32 _l2Gas, bytes calldata _data) external payable onlyEOA {
    
    5        _initiateETHDeposit(msg.sender, msg.sender, _l2Gas, _data);
    
    6    }
    
    7
    
    8    /**
    
    9     * @inheritdoc IL1StandardBridge
    
    10     */
    
    11    function depositETHTo(
    
    12        address _to,
    
    13        uint32 _l2Gas,
    
    14        bytes calldata _data
    
    15    ) external payable {
    
    16        _initiateETHDeposit(msg.sender, _to, _l2Gas, _data);
    
    17    }
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

These two functions are wrappers around `_initiateETHDeposit`, the function
that handles the actual ETH deposit.

    
    
    1    /**
    
    2     * @dev Performs the logic for deposits by storing the ETH and informing the L2 ETH Gateway of
    
    3     * the deposit.
    
    4     * @param _from Account to pull the deposit from on L1.
    
    5     * @param _to Account to give the deposit to on L2.
    
    6     * @param _l2Gas Gas limit required to complete the deposit on L2.
    
    7     * @param _data Optional data to forward to L2. This data is provided
    
    8     *        solely as a convenience for external contracts. Aside from enforcing a maximum
    
    9     *        length, these contracts provide no guarantees about its content.
    
    10     */
    
    11    function _initiateETHDeposit(
    
    12        address _from,
    
    13        address _to,
    
    14        uint32 _l2Gas,
    
    15        bytes memory _data
    
    16    ) internal {
    
    17        // Construct calldata for finalizeDeposit call
    
    18        bytes memory message = abi.encodeWithSelector(
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

The way that cross domain messages work is that the destination contract is
called with the message as its calldata. Solidity contracts always interpret
their calldata in accordance with [the ABI specifications(opens in a new
tab)](https://docs.soliditylang.org/en/v0.8.12/abi-spec.html). The Solidity
function [`abi.encodeWithSelector`(opens in a new
tab)](https://docs.soliditylang.org/en/v0.8.12/units-and-global-
variables.html#abi-encoding-and-decoding-functions) creates that calldata.

    
    
    1            IL2ERC20Bridge.finalizeDeposit.selector,
    
    2            address(0),
    
    3            Lib_PredeployAddresses.OVM_ETH,
    
    4            _from,
    
    5            _to,
    
    6            msg.value,
    
    7            _data
    
    8        );
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

The message here is to call [the `finalizeDeposit` function(opens in a new
tab)](https://github.com/ethereum-
optimism/optimism/blob/develop/packages/contracts/contracts/L2/messaging/L2StandardBridge.sol#L141-L148)
with these parameters:

Parameter| Value| Meaning  
---|---|---  
_l1Token| address(0)| Special value to stand for ETH (which isn't an ERC-20
token) on L1  
_l2Token| Lib_PredeployAddresses.OVM_ETH| The L2 contract that manages ETH on
Optimism, `0xDeadDeAddeAddEAddeadDEaDDEAdDeaDDeAD0000` (this contract is for
internal Optimism use only)  
_from| _from| The address on L1 that sends the ETH  
_to| _to| The address on L2 that receives the ETH  
amount| msg.value| Amount of wei sent (which has already been sent to the
bridge)  
_data| _data| Additional data to attach to the deposit  
      
    
    1        // Send calldata into L2
    
    2        // slither-disable-next-line reentrancy-events
    
    3        sendCrossDomainMessage(l2TokenBridge, _l2Gas, message);
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Send the message through the cross domain messenger.

    
    
    1        // slither-disable-next-line reentrancy-events
    
    2        emit ETHDepositInitiated(_from, _to, msg.value, _data);
    
    3    }
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Emit an event to inform any decentralized application that listens of this
transfer.

    
    
    1    /**
    
    2     * @inheritdoc IL1ERC20Bridge
    
    3     */
    
    4    function depositERC20(
    
    5        .
    
    6        .
    
    7        .
    
    8    ) external virtual onlyEOA {
    
    9        _initiateERC20Deposit(_l1Token, _l2Token, msg.sender, msg.sender, _amount, _l2Gas, _data);
    
    10    }
    
    11
    
    12    /**
    
    13     * @inheritdoc IL1ERC20Bridge
    
    14     */
    
    15    function depositERC20To(
    
    16        .
    
    17        .
    
    18        .
    
    19    ) external virtual {
    
    20        _initiateERC20Deposit(_l1Token, _l2Token, msg.sender, _to, _amount, _l2Gas, _data);
    
    21    }
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

These two functions are wrappers around `_initiateERC20Deposit`, the function
that handles the actual ERC-20 deposit.

    
    
    1    /**
    
    2     * @dev Performs the logic for deposits by informing the L2 Deposited Token
    
    3     * contract of the deposit and calling a handler to lock the L1 funds. (e.g. transferFrom)
    
    4     *
    
    5     * @param _l1Token Address of the L1 ERC20 we are depositing
    
    6     * @param _l2Token Address of the L1 respective L2 ERC20
    
    7     * @param _from Account to pull the deposit from on L1
    
    8     * @param _to Account to give the deposit to on L2
    
    9     * @param _amount Amount of the ERC20 to deposit.
    
    10     * @param _l2Gas Gas limit required to complete the deposit on L2.
    
    11     * @param _data Optional data to forward to L2. This data is provided
    
    12     *        solely as a convenience for external contracts. Aside from enforcing a maximum
    
    13     *        length, these contracts provide no guarantees about its content.
    
    14     */
    
    15    function _initiateERC20Deposit(
    
    16        address _l1Token,
    
    17        address _l2Token,
    
    18        address _from,
    
    19        address _to,
    
    20        uint256 _amount,
    
    21        uint32 _l2Gas,
    
    22        bytes calldata _data
    
    23    ) internal {
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

This function is similar to `_initiateETHDeposit` above, with a few important
differences. The first difference is that this function receives the token
addresses and the amount to transfer as parameters. In the case of ETH the
call to the bridge already includes the transfer of asset to the bridge
account (`msg.value`).

    
    
    1        // When a deposit is initiated on L1, the L1 Bridge transfers the funds to itself for future
    
    2        // withdrawals. safeTransferFrom also checks if the contract has code, so this will fail if
    
    3        // _from is an EOA or address(0).
    
    4        // slither-disable-next-line reentrancy-events, reentrancy-benign
    
    5        IERC20(_l1Token).safeTransferFrom(_from, address(this), _amount);
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

ERC-20 token transfers follow a different process from ETH:

  1. The user (`_from`) gives an allowance to the bridge to transfer the appropriate tokens.
  2. The user calls the bridge with the address of the token contract, the amount, etc.
  3. The bridge transfers the tokens (to itself) as part of the deposit process.

The first step may happen in a separate transaction from the last two.
However, front-running is not a problem because the two functions that call
`_initiateERC20Deposit` (`depositERC20` and `depositERC20To`) only call this
function with `msg.sender` as the `_from` parameter.

    
    
    1        // Construct calldata for _l2Token.finalizeDeposit(_to, _amount)
    
    2        bytes memory message = abi.encodeWithSelector(
    
    3            IL2ERC20Bridge.finalizeDeposit.selector,
    
    4            _l1Token,
    
    5            _l2Token,
    
    6            _from,
    
    7            _to,
    
    8            _amount,
    
    9            _data
    
    10        );
    
    11
    
    12        // Send calldata into L2
    
    13        // slither-disable-next-line reentrancy-events, reentrancy-benign
    
    14        sendCrossDomainMessage(l2TokenBridge, _l2Gas, message);
    
    15
    
    16        // slither-disable-next-line reentrancy-benign
    
    17        deposits[_l1Token][_l2Token] = deposits[_l1Token][_l2Token] + _amount;
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Add the deposited amount of tokens to the `deposits` data structure. There
could be multiple addresses on L2 that correspond to the same L1 ERC-20 token,
so it is not sufficient to use the bridge's balance of the L1 ERC-20 token to
keep track of deposits.

    
    
    1
    
    2        // slither-disable-next-line reentrancy-events
    
    3        emit ERC20DepositInitiated(_l1Token, _l2Token, _from, _to, _amount, _data);
    
    4    }
    
    5
    
    6    /*************************
    
    7     * Cross-chain Functions *
    
    8     *************************/
    
    9
    
    10    /**
    
    11     * @inheritdoc IL1StandardBridge
    
    12     */
    
    13    function finalizeETHWithdrawal(
    
    14        address _from,
    
    15        address _to,
    
    16        uint256 _amount,
    
    17        bytes calldata _data
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

The L2 bridge sends a message to the L2 cross domain messenger which causes
the L1 cross domain messenger to call this function (once the [transaction
that finalizes the message(opens in a new
tab)](https://community.optimism.io/docs/developers/bridge/messaging/#fees-
for-l2-%E2%87%92-l1-transactions) is submitted on L1, of course).

    
    
    1    ) external onlyFromCrossDomainAccount(l2TokenBridge) {
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Make sure that this is a _legitimate_ message, coming from the cross domain
messenger and originating with the L2 token bridge. This function is used to
withdraw ETH from the bridge, so we have to make sure it is only called by the
authorized caller.

    
    
    1        // slither-disable-next-line reentrancy-events
    
    2        (bool success, ) = _to.call{ value: _amount }(new bytes(0));
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

The way to transfer ETH is to call the recipient with the amount of wei in the
`msg.value`.

    
    
    1        require(success, "TransferHelper::safeTransferETH: ETH transfer failed");
    
    2
    
    3        // slither-disable-next-line reentrancy-events
    
    4        emit ETHWithdrawalFinalized(_from, _to, _amount, _data);
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Emit an event about the withdrawal.

    
    
    1    }
    
    2
    
    3    /**
    
    4     * @inheritdoc IL1ERC20Bridge
    
    5     */
    
    6    function finalizeERC20Withdrawal(
    
    7        address _l1Token,
    
    8        address _l2Token,
    
    9        address _from,
    
    10        address _to,
    
    11        uint256 _amount,
    
    12        bytes calldata _data
    
    13    ) external onlyFromCrossDomainAccount(l2TokenBridge) {
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

This function is similar to `finalizeETHWithdrawal` above, with the necessary
changes for ERC-20 tokens.

    
    
    1        deposits[_l1Token][_l2Token] = deposits[_l1Token][_l2Token] - _amount;
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Update the `deposits` data structure.

    
    
    1
    
    2        // When a withdrawal is finalized on L1, the L1 Bridge transfers the funds to the withdrawer
    
    3        // slither-disable-next-line reentrancy-events
    
    4        IERC20(_l1Token).safeTransfer(_to, _amount);
    
    5
    
    6        // slither-disable-next-line reentrancy-events
    
    7        emit ERC20WithdrawalFinalized(_l1Token, _l2Token, _from, _to, _amount, _data);
    
    8    }
    
    9
    
    10
    
    11    /*****************************
    
    12     * Temporary - Migrating ETH *
    
    13     *****************************/
    
    14
    
    15    /**
    
    16     * @dev Adds ETH balance to the account. This is meant to allow for ETH
    
    17     * to be migrated from an old gateway to a new gateway.
    
    18     * NOTE: This is left for one upgrade only so we are able to receive the migrated ETH from the
    
    19     * old contract
    
    20     */
    
    21    function donateETH() external payable {}
    
    22}
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

There was an earlier implementation of the bridge. When we moved from the
implementation to this one, we had to move all the assets. ERC-20 tokens can
just be moved. However, to transfer ETH to a contract you need that contract's
approval, which is what `donateETH` provides us.

## ERC-20 Tokens on L2

For an ERC-20 token to fit into the standard bridge, it needs to allow the
standard bridge, and _only_ the standard bridge, to mint token. This is
necessary because the bridges need to ensure that the number of tokens
circulating on Optimism is equal to the number of tokens locked inside the L1
bridge contract. If there are too many tokens on L2 some users would be unable
to bridge their assets back to L1. Instead of a trusted bridge, we would
essentially recreate [fractional reserve banking(opens in a new
tab)](https://www.investopedia.com/terms/f/fractionalreservebanking.asp). If
there are too many tokens on L1, some of those tokens would stay locked inside
the bridge contract forever because there is no way to release them without
burning L2 tokens.

### IL2StandardERC20

Every ERC-20 token on L2 that uses the standard bridge needs to provide [this
interface(opens in a new tab)](https://github.com/ethereum-
optimism/optimism/blob/develop/packages/contracts/contracts/standards/IL2StandardERC20.sol),
which has the functions and events that the standard bridge needs.

    
    
    1// SPDX-License-Identifier: MIT
    
    2pragma solidity ^0.8.9;
    
    3
    
    4import { IERC20 } from "@openzeppelin/contracts/token/ERC20/IERC20.sol";
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

[The standard ERC-20 interface(opens in a new
tab)](https://github.com/OpenZeppelin/openzeppelin-
contracts/blob/master/contracts/token/ERC20/IERC20.sol) does not include the
`mint` and `burn` functions. Those methods are not required by [the ERC-20
standard(opens in a new tab)](https://eips.ethereum.org/EIPS/eip-20), which
leaves unspecified the mechanisms to create and destroy tokens.

    
    
    1import { IERC165 } from "@openzeppelin/contracts/utils/introspection/IERC165.sol";
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

[The ERC-165 interface(opens in a new
tab)](https://github.com/OpenZeppelin/openzeppelin-
contracts/blob/master/contracts/utils/introspection/IERC165.sol) is used to
specify what functions a contract provides. [You can read the standard
here(opens in a new tab)](https://eips.ethereum.org/EIPS/eip-165).

    
    
    1interface IL2StandardERC20 is IERC20, IERC165 {
    
    2    function l1Token() external returns (address);
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

This function provides the address of the L1 token which is bridged to this
contract. Note that we do not have a similar function in the opposite
direction. We need to be able to bridge any L1 token, regardless of whether L2
support was planned when it was implemented or not.

    
    
    1
    
    2    function mint(address _to, uint256 _amount) external;
    
    3
    
    4    function burn(address _from, uint256 _amount) external;
    
    5
    
    6    event Mint(address indexed _account, uint256 _amount);
    
    7    event Burn(address indexed _account, uint256 _amount);
    
    8}
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Functions and events to mint (create) and burn (destroy) tokens. The bridge
should be the only entity that can run these functions to ensure the number of
tokens is correct (equal to the number of tokens locked on L1).

### L2StandardERC20

[This is our implementation of the `IL2StandardERC20` interface(opens in a new
tab)](https://github.com/ethereum-
optimism/optimism/blob/develop/packages/contracts/contracts/standards/L2StandardERC20.sol).
Unless you need some kind of custom logic, you should use this one.

    
    
    1// SPDX-License-Identifier: MIT
    
    2pragma solidity ^0.8.9;
    
    3
    
    4import { ERC20 } from "@openzeppelin/contracts/token/ERC20/ERC20.sol";
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

[The OpenZeppelin ERC-20 contract(opens in a new
tab)](https://github.com/OpenZeppelin/openzeppelin-
contracts/blob/master/contracts/token/ERC20/ERC20.sol). Optimism does not
believe in reinventing the wheel, especially when the wheel is well audited
and needs to be trustworthy enough to hold assets.

    
    
    1import "./IL2StandardERC20.sol";
    
    2
    
    3contract L2StandardERC20 is IL2StandardERC20, ERC20 {
    
    4    address public l1Token;
    
    5    address public l2Bridge;
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

These are the two additional configuration parameters that we require and
ERC-20 normally does not.

    
    
    1
    
    2    /**
    
    3     * @param _l2Bridge Address of the L2 standard bridge.
    
    4     * @param _l1Token Address of the corresponding L1 token.
    
    5     * @param _name ERC20 name.
    
    6     * @param _symbol ERC20 symbol.
    
    7     */
    
    8    constructor(
    
    9        address _l2Bridge,
    
    10        address _l1Token,
    
    11        string memory _name,
    
    12        string memory _symbol
    
    13    ) ERC20(_name, _symbol) {
    
    14        l1Token = _l1Token;
    
    15        l2Bridge = _l2Bridge;
    
    16    }
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

First call the constructor for the contract we inherit from (`ERC20(_name,
_symbol)`) and then set our own variables.

    
    
    1
    
    2    modifier onlyL2Bridge() {
    
    3        require(msg.sender == l2Bridge, "Only L2 Bridge can mint and burn");
    
    4        _;
    
    5    }
    
    6
    
    7
    
    8    // slither-disable-next-line external-function
    
    9    function supportsInterface(bytes4 _interfaceId) public pure returns (bool) {
    
    10        bytes4 firstSupportedInterface = bytes4(keccak256("supportsInterface(bytes4)")); // ERC165
    
    11        bytes4 secondSupportedInterface = IL2StandardERC20.l1Token.selector ^
    
    12            IL2StandardERC20.mint.selector ^
    
    13            IL2StandardERC20.burn.selector;
    
    14        return _interfaceId == firstSupportedInterface || _interfaceId == secondSupportedInterface;
    
    15    }
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

This is the way [ERC-165(opens in a new
tab)](https://eips.ethereum.org/EIPS/eip-165) works. Every interface is a
number of supported functions, and is identified as the [exclusive or(opens in
a new tab)](https://en.wikipedia.org/wiki/Exclusive_or) of the [ABI function
selectors(opens in a new tab)](https://docs.soliditylang.org/en/v0.8.12/abi-
spec.html#function-selector) of those functions.

The L2 bridge uses ERC-165 as a sanity check to make sure that the ERC-20
contract to which it sends assets is an `IL2StandardERC20`.

**Note:** There is nothing to prevent rogue contract from providing false
answers to `supportsInterface`, so this is a sanity check mechanism, _not_ a
security mechanism.

    
    
    1    // slither-disable-next-line external-function
    
    2    function mint(address _to, uint256 _amount) public virtual onlyL2Bridge {
    
    3        _mint(_to, _amount);
    
    4
    
    5        emit Mint(_to, _amount);
    
    6    }
    
    7
    
    8    // slither-disable-next-line external-function
    
    9    function burn(address _from, uint256 _amount) public virtual onlyL2Bridge {
    
    10        _burn(_from, _amount);
    
    11
    
    12        emit Burn(_from, _amount);
    
    13    }
    
    14}
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Only the L2 bridge is allowed to mint and burn assets.

`_mint` and `_burn` are actually defined in the [OpenZeppelin ERC-20
contract](/en/developers/tutorials/erc20-annotated-code/#the-_mint-and-_burn-
functions-_mint-and-_burn). That contract just doesn't expose them externally,
because the conditions to mint and burn tokens are as varied as the number of
ways to use ERC-20.

## L2 Bridge Code

This is code that runs the bridge on Optimism. [The source for this contract
is here(opens in a new tab)](https://github.com/ethereum-
optimism/optimism/blob/develop/packages/contracts/contracts/L2/messaging/L2StandardBridge.sol).

    
    
    1// SPDX-License-Identifier: MIT
    
    2pragma solidity ^0.8.9;
    
    3
    
    4/* Interface Imports */
    
    5import { IL1StandardBridge } from "../../L1/messaging/IL1StandardBridge.sol";
    
    6import { IL1ERC20Bridge } from "../../L1/messaging/IL1ERC20Bridge.sol";
    
    7import { IL2ERC20Bridge } from "./IL2ERC20Bridge.sol";
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

The [IL2ERC20Bridge(opens in a new tab)](https://github.com/ethereum-
optimism/optimism/blob/develop/packages/contracts/contracts/L2/messaging/IL2ERC20Bridge.sol)
interface is very similar to the L1 equivalent we saw above. There are two
significant differences:

  1. On L1 you initiate deposits and finalize withdrawals. Here you initiate withdrawals and finalize deposits.
  2. On L1 it is necessary to distinguish between ETH and ERC-20 tokens. On L2 we can use the same functions for both because internally ETH balances on Optimism are handled as an ERC-20 token with the address [0xDeadDeAddeAddEAddeadDEaDDEAdDeaDDeAD0000(opens in a new tab)](https://optimistic.etherscan.io/address/0xDeadDeAddeAddEAddeadDEaDDEAdDeaDDeAD0000).

    
    
    1/* Library Imports */
    
    2import { ERC165Checker } from "@openzeppelin/contracts/utils/introspection/ERC165Checker.sol";
    
    3import { CrossDomainEnabled } from "../../libraries/bridge/CrossDomainEnabled.sol";
    
    4import { Lib_PredeployAddresses } from "../../libraries/constants/Lib_PredeployAddresses.sol";
    
    5
    
    6/* Contract Imports */
    
    7import { IL2StandardERC20 } from "../../standards/IL2StandardERC20.sol";
    
    8
    
    9/**
    
    10 * @title L2StandardBridge
    
    11 * @dev The L2 Standard bridge is a contract which works together with the L1 Standard bridge to
    
    12 * enable ETH and ERC20 transitions between L1 and L2.
    
    13 * This contract acts as a minter for new tokens when it hears about deposits into the L1 Standard
    
    14 * bridge.
    
    15 * This contract also acts as a burner of the tokens intended for withdrawal, informing the L1
    
    16 * bridge to release L1 funds.
    
    17 */
    
    18contract L2StandardBridge is IL2ERC20Bridge, CrossDomainEnabled {
    
    19    /********************************
    
    20     * External Contract References *
    
    21     ********************************/
    
    22
    
    23    address public l1TokenBridge;
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Keep track of the address of the L1 bridge. Note that in contrast to the L1
equivalent, here we _need_ this variable. The address of the L1 bridge is not
known in advance.

    
    
    1
    
    2    /***************
    
    3     * Constructor *
    
    4     ***************/
    
    5
    
    6    /**
    
    7     * @param _l2CrossDomainMessenger Cross-domain messenger used by this contract.
    
    8     * @param _l1TokenBridge Address of the L1 bridge deployed to the main chain.
    
    9     */
    
    10    constructor(address _l2CrossDomainMessenger, address _l1TokenBridge)
    
    11        CrossDomainEnabled(_l2CrossDomainMessenger)
    
    12    {
    
    13        l1TokenBridge = _l1TokenBridge;
    
    14    }
    
    15
    
    16    /***************
    
    17     * Withdrawing *
    
    18     ***************/
    
    19
    
    20    /**
    
    21     * @inheritdoc IL2ERC20Bridge
    
    22     */
    
    23    function withdraw(
    
    24        address _l2Token,
    
    25        uint256 _amount,
    
    26        uint32 _l1Gas,
    
    27        bytes calldata _data
    
    28    ) external virtual {
    
    29        _initiateWithdrawal(_l2Token, msg.sender, msg.sender, _amount, _l1Gas, _data);
    
    30    }
    
    31
    
    32    /**
    
    33     * @inheritdoc IL2ERC20Bridge
    
    34     */
    
    35    function withdrawTo(
    
    36        address _l2Token,
    
    37        address _to,
    
    38        uint256 _amount,
    
    39        uint32 _l1Gas,
    
    40        bytes calldata _data
    
    41    ) external virtual {
    
    42        _initiateWithdrawal(_l2Token, msg.sender, _to, _amount, _l1Gas, _data);
    
    43    }
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

These two functions initiate withdrawals. Note that there is no needs to
specify the L1 token address. L2 tokens are expected to tell us the L1
equivalent's address.

    
    
    1
    
    2    /**
    
    3     * @dev Performs the logic for withdrawals by burning the token and informing
    
    4     *      the L1 token Gateway of the withdrawal.
    
    5     * @param _l2Token Address of L2 token where withdrawal is initiated.
    
    6     * @param _from Account to pull the withdrawal from on L2.
    
    7     * @param _to Account to give the withdrawal to on L1.
    
    8     * @param _amount Amount of the token to withdraw.
    
    9     * @param _l1Gas Unused, but included for potential forward compatibility considerations.
    
    10     * @param _data Optional data to forward to L1. This data is provided
    
    11     *        solely as a convenience for external contracts. Aside from enforcing a maximum
    
    12     *        length, these contracts provide no guarantees about its content.
    
    13     */
    
    14    function _initiateWithdrawal(
    
    15        address _l2Token,
    
    16        address _from,
    
    17        address _to,
    
    18        uint256 _amount,
    
    19        uint32 _l1Gas,
    
    20        bytes calldata _data
    
    21    ) internal {
    
    22        // When a withdrawal is initiated, we burn the withdrawer's funds to prevent subsequent L2
    
    23        // usage
    
    24        // slither-disable-next-line reentrancy-events
    
    25        IL2StandardERC20(_l2Token).burn(msg.sender, _amount);
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Notice that we are _not_ relying on the `_from` parameter but on `msg.sender`
which is a lot harder to fake (impossible, as far as I know).

    
    
    1
    
    2        // Construct calldata for l1TokenBridge.finalizeERC20Withdrawal(_to, _amount)
    
    3        // slither-disable-next-line reentrancy-events
    
    4        address l1Token = IL2StandardERC20(_l2Token).l1Token();
    
    5        bytes memory message;
    
    6
    
    7        if (_l2Token == Lib_PredeployAddresses.OVM_ETH) {
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

On L1 it is necessary to distinguish between ETH and ERC-20.

    
    
    1            message = abi.encodeWithSelector(
    
    2                IL1StandardBridge.finalizeETHWithdrawal.selector,
    
    3                _from,
    
    4                _to,
    
    5                _amount,
    
    6                _data
    
    7            );
    
    8        } else {
    
    9            message = abi.encodeWithSelector(
    
    10                IL1ERC20Bridge.finalizeERC20Withdrawal.selector,
    
    11                l1Token,
    
    12                _l2Token,
    
    13                _from,
    
    14                _to,
    
    15                _amount,
    
    16                _data
    
    17            );
    
    18        }
    
    19
    
    20        // Send message up to L1 bridge
    
    21        // slither-disable-next-line reentrancy-events
    
    22        sendCrossDomainMessage(l1TokenBridge, _l1Gas, message);
    
    23
    
    24        // slither-disable-next-line reentrancy-events
    
    25        emit WithdrawalInitiated(l1Token, _l2Token, msg.sender, _to, _amount, _data);
    
    26    }
    
    27
    
    28    /************************************
    
    29     * Cross-chain Function: Depositing *
    
    30     ************************************/
    
    31
    
    32    /**
    
    33     * @inheritdoc IL2ERC20Bridge
    
    34     */
    
    35    function finalizeDeposit(
    
    36        address _l1Token,
    
    37        address _l2Token,
    
    38        address _from,
    
    39        address _to,
    
    40        uint256 _amount,
    
    41        bytes calldata _data
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

This function is called by `L1StandardBridge`.

    
    
    1    ) external virtual onlyFromCrossDomainAccount(l1TokenBridge) {
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Make sure the source of the message is legitimate. This is important because
this function calls `_mint` and could be used to give tokens that are not
covered by tokens the bridge owns on L1.

    
    
    1        // Check the target token is compliant and
    
    2        // verify the deposited token on L1 matches the L2 deposited token representation here
    
    3        if (
    
    4            // slither-disable-next-line reentrancy-events
    
    5            ERC165Checker.supportsInterface(_l2Token, 0x1d1d8b63) &&
    
    6            _l1Token == IL2StandardERC20(_l2Token).l1Token()
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Sanity checks:

  1. The correct interface is supported
  2. The L2 ERC-20 contract's L1 address matches the L1 source of the tokens

    
    
    1        ) {
    
    2            // When a deposit is finalized, we credit the account on L2 with the same amount of
    
    3            // tokens.
    
    4            // slither-disable-next-line reentrancy-events
    
    5            IL2StandardERC20(_l2Token).mint(_to, _amount);
    
    6            // slither-disable-next-line reentrancy-events
    
    7            emit DepositFinalized(_l1Token, _l2Token, _from, _to, _amount, _data);
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

If the sanity checks pass, finalize the deposit:

  1. Mint the tokens
  2. Emit the appropriate event

    
    
    1        } else {
    
    2            // Either the L2 token which is being deposited-into disagrees about the correct address
    
    3            // of its L1 token, or does not support the correct interface.
    
    4            // This should only happen if there is a  malicious L2 token, or if a user somehow
    
    5            // specified the wrong L2 token address to deposit into.
    
    6            // In either case, we stop the process here and construct a withdrawal
    
    7            // message so that users can get their funds out in some cases.
    
    8            // There is no way to prevent malicious token contracts altogether, but this does limit
    
    9            // user error and mitigate some forms of malicious contract behavior.
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

If a user made a detectable error by using the wrong L2 token address, we want
to cancel the deposit and return the tokens on L1. The only way we can do this
from L2 is to send a message that will have to wait the fault challenge
period, but that is much better for the user than losing the tokens
permanently.

    
    
    1            bytes memory message = abi.encodeWithSelector(
    
    2                IL1ERC20Bridge.finalizeERC20Withdrawal.selector,
    
    3                _l1Token,
    
    4                _l2Token,
    
    5                _to, // switched the _to and _from here to bounce back the deposit to the sender
    
    6                _from,
    
    7                _amount,
    
    8                _data
    
    9            );
    
    10
    
    11            // Send message up to L1 bridge
    
    12            // slither-disable-next-line reentrancy-events
    
    13            sendCrossDomainMessage(l1TokenBridge, 0, message);
    
    14            // slither-disable-next-line reentrancy-events
    
    15            emit DepositFailed(_l1Token, _l2Token, _from, _to, _amount, _data);
    
    16        }
    
    17    }
    
    18}
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

## Conclusion

The standard bridge is the most flexible mechanism for asset transfers.
However, because it is so generic it is not always the easiest mechanism to
use. Especially for withdrawals, most users prefer to use [third party
bridges(opens in a new tab)](https://www.optimism.io/apps/bridges) that do not
wait the challenge period and do not require a Merkle proof to finalize the
withdrawal.

These bridges typically work by having assets on L1, which they provide
immediately for a small fee (often less than the cost of gas for a standard
bridge withdrawal). When the bridge (or the people running it) anticipates
being short on L1 assets it transfers sufficient assets from L2. As these are
very big withdrawals, the withdrawal cost is amortized over a large amount and
is a much smaller percentage.

Hopefully this article helped you understand more about how layer 2 works, and
how to write Solidity code that is clear and secure.

l

Last edit: [@lukassim(opens in a new tab)](https://github.com/lukassim), April
26, 2024

See contributors

### Was this tutorial helpful?

YesNo

  * [Edit page(opens in a new tab)](https://github.com/ethereum/ethereum-org-website/tree/dev/public/content/developers/tutorials/optimism-std-bridge-annotated-code/index.md)
  * On this page

    * Control flows
      * Deposit flow
      * Withdrawal flow
    * Layer 1 code
      * IL1ERC20Bridge
      * IL1StandardBridge
      * CrossDomainEnabled
      * The L1 bridge contract
    * ERC-20 Tokens on L2
      * IL2StandardERC20
      * L2StandardERC20
    * L2 Bridge Code
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

