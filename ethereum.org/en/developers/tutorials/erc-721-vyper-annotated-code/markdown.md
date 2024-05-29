Skip to main content

[](/en/)

  * Learn
  * Use
  * Build
  * Participate
  * Research

Search```K`

Languages EN

# Vyper ERC-721 Contract Walkthrough

vypererc-721python

Beginner

![✍️](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/270d.svg)Ori
Pomerantz

![📆](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4c6.svg)
April 1, 2021

![⏱️](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/23f1.svg)20
minute read minute read

On this page

  * Introduction
  * The Contract
    * The ERC721Receiver Interface
    * Events
    * State Variables
    * Functions

## Introduction

The [ERC-721](/en/developers/docs/standards/tokens/erc-721/) standard is used
to hold the ownership of Non-Fungible Tokens (NFT).
[ERC-20](/en/developers/docs/standards/tokens/erc-20/) tokens behave as a
commodity, because there is no difference between individual tokens. In
contrast to that, ERC-721 tokens are designed for assets that are similar but
not identical, such as different [cat cartoons(opens in a new
tab)](https://www.cryptokitties.co/) or titles to different pieces of real
estate.

In this article we will analyze [Ryuya Nakamura's ERC-721 contract(opens in a
new
tab)](https://github.com/vyperlang/vyper/blob/master/examples/tokens/ERC721.vy).
This contract is written in [Vyper(opens in a new
tab)](https://vyper.readthedocs.io/en/latest/index.html), a Python-like
contract language designed to make it harder to write insecure code than it is
in Solidity.

## The Contract

    
    
    1# @dev Implementation of ERC-721 non-fungible token standard.
    
    2# @author Ryuya Nakamura (@nrryuya)
    
    3# Modified from: https://github.com/vyperlang/vyper/blob/de74722bf2d8718cca46902be165f9fe0e3641dd/examples/tokens/ERC721.vy
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Comments in Vyper, as in Python, start with a hash (`#`) and continue to the
end of the line. Comments that include `@<keyword>` are used by [NatSpec(opens
in a new tab)](https://vyper.readthedocs.io/en/latest/natspec.html) to produce
human-readable documentation.

    
    
    1from vyper.interfaces import ERC721
    
    2
    
    3implements: ERC721
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

The ERC-721 interface is built into the Vyper language. [You can see the code
definition here(opens in a new
tab)](https://github.com/vyperlang/vyper/blob/master/vyper/builtin_interfaces/ERC721.py).
The interface definition is written in Python, rather than Vyper, because
interfaces are used not only within the blockchain, but also when sending the
blockchain a transaction from an external client, which may be written in
Python.

The first line imports the interface, and the second specifies that we are
implementing it here.

### The ERC721Receiver Interface

    
    
    1# Interface for the contract called by safeTransferFrom()
    
    2interface ERC721Receiver:
    
    3    def onERC721Received(
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

ERC-721 supports two types of transfer:

  * `transferFrom`, which lets the sender specify any destination address and places the responsibility for the transfer on the sender. This means that you can transfer to an invalid address, in which case the NFT is lost for good.
  * `safeTransferFrom`, which checks if the destination address is a contract. If so, the ERC-721 contract asks the receiving contract if it wants to receive the NFT.

To answer `safeTransferFrom` requests a receiving contract has to implement
`ERC721Receiver`.

    
    
    1            _operator: address,
    
    2            _from: address,
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

The `_from` address is the current owner of the token. The `_operator` address
is the one that requested the transfer (those two may not be the same, because
of allowances).

    
    
    1            _tokenId: uint256,
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

ERC-721 token IDs are 256 bits. Typically they are created by hashing a
description of whatever the token represents.

    
    
    1            _data: Bytes[1024]
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

The request can have up to 1024 bytes of user data.

    
    
    1        ) -> bytes32: view
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

To prevent cases in which a contract accidentally accepts a transfer the
return value is not a boolean, but 256 bits with a specific value.

This function is a `view`, which means it can read the state of the
blockchain, but not modify it.

### Events

[Events(opens in a new tab)](https://media.consensys.net/technical-
introduction-to-events-and-logs-in-ethereum-a074d65dd61e) are emitted to
inform users and servers outside of the blockchain of events. Note that the
content of events is not available to contracts on the blockchain.

    
    
    1# @dev Emits when ownership of any NFT changes by any mechanism. This event emits when NFTs are
    
    2#      created (`from` == 0) and destroyed (`to` == 0). Exception: during contract creation, any
    
    3#      number of NFTs may be created and assigned without emitting Transfer. At the time of any
    
    4#      transfer, the approved address for that NFT (if any) is reset to none.
    
    5# @param _from Sender of NFT (if address is zero address it indicates token creation).
    
    6# @param _to Receiver of NFT (if address is zero address it indicates token destruction).
    
    7# @param _tokenId The NFT that got transferred.
    
    8event Transfer:
    
    9    sender: indexed(address)
    
    10    receiver: indexed(address)
    
    11    tokenId: indexed(uint256)
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

This is similar to the ERC-20 Transfer event, except that we report a
`tokenId` instead of an amount. Nobody owns address zero, so by convention we
use it to report creation and destruction of tokens.

    
    
    1# @dev This emits when the approved address for an NFT is changed or reaffirmed. The zero
    
    2#      address indicates there is no approved address. When a Transfer event emits, this also
    
    3#      indicates that the approved address for that NFT (if any) is reset to none.
    
    4# @param _owner Owner of NFT.
    
    5# @param _approved Address that we are approving.
    
    6# @param _tokenId NFT which we are approving.
    
    7event Approval:
    
    8    owner: indexed(address)
    
    9    approved: indexed(address)
    
    10    tokenId: indexed(uint256)
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

An ERC-721 approval is similar to an ERC-20 allowance. A specific address is
allowed to transfer a specific token. This gives a mechanism for contracts to
respond when they accept a token. Contracts cannot listen for events, so if
you just transfer the token to them they don't "know" about it. This way the
owner first submits an approval and then sends a request to the contract: "I
approved for you to transfer token X, please do ...".

This is a design choice to make the ERC-721 standard similar to the ERC-20
standard. Because ERC-721 tokens are not fungible, a contract can also
identify that it got a specific token by looking at the token's ownership.

    
    
    1# @dev This emits when an operator is enabled or disabled for an owner. The operator can manage
    
    2#      all NFTs of the owner.
    
    3# @param _owner Owner of NFT.
    
    4# @param _operator Address to which we are setting operator rights.
    
    5# @param _approved Status of operator rights(true if operator rights are given and false if
    
    6# revoked).
    
    7event ApprovalForAll:
    
    8    owner: indexed(address)
    
    9    operator: indexed(address)
    
    10    approved: bool
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

It is sometimes useful to have an _operator_ that can manage all of an
account's tokens of a specific type (those that are managed by a specific
contract), similar to a power of attorney. For example, I might want to give
such a power to a contract that checks if I haven't contacted it for six
months, and if so distributes my assets to my heirs (if one of them asks for
it, contracts can't do anything without being called by a transaction). In
ERC-20 we can just give a high allowance to an inheritance contract, but that
doesn't work for ERC-721 because the tokens are not fungible. This is the
equivalent.

The `approved` value tells us whether the event is for an approval, or the
withdrawal of an approval.

### State Variables

These variables contain the current state of the tokens: which ones are
available and who owns them. Most of these are `HashMap` objects,
[unidirectional mappings that exist between two types(opens in a new
tab)](https://vyper.readthedocs.io/en/latest/types.html#mappings).

    
    
    1# @dev Mapping from NFT ID to the address that owns it.
    
    2idToOwner: HashMap[uint256, address]
    
    3
    
    4# @dev Mapping from NFT ID to approved address.
    
    5idToApprovals: HashMap[uint256, address]
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

User and contract identities in Ethereum are represented by 160-bit addresses.
These two variables map from token IDs to their owners and those approved to
transfer them (at a maximum of one for each). In Ethereum, uninitialized data
is always zero, so if there is no owner or approved transferor the value for
that token is zero.

    
    
    1# @dev Mapping from owner address to count of his tokens.
    
    2ownerToNFTokenCount: HashMap[address, uint256]
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

This variable holds the count of tokens for each owner. There is no mapping
from owners to tokens, so the only way to identify the tokens that a specific
owner owns is to look back in the blockchain's event history and see the
appropriate `Transfer` events. We can use this variable to know when we have
all the NFTs and don't need to look even further in time.

Note that this algorithm only works for user interfaces and external servers.
Code running on the blockchain itself cannot read past events.

    
    
    1# @dev Mapping from owner address to mapping of operator addresses.
    
    2ownerToOperators: HashMap[address, HashMap[address, bool]]
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

An account may have more than a single operator. A simple `HashMap` is
insufficient to keep track of them, because each key leads to a single value.
Instead, you can use `HashMap[address, bool]` as the value. By default the
value for each address is `False`, which means it is not an operator. You can
set values to `True` as needed.

    
    
    1# @dev Address of minter, who can mint a token
    
    2minter: address
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

New tokens have to be created somehow. In this contract there is a single
entity that is allowed to do so, the `minter`. This is likely to be sufficient
for a game, for example. For other purposes, it might be necessary to create a
more complicated business logic.

    
    
    1# @dev Mapping of interface id to bool about whether or not it's supported
    
    2supportedInterfaces: HashMap[bytes32, bool]
    
    3
    
    4# @dev ERC165 interface ID of ERC165
    
    5ERC165_INTERFACE_ID: constant(bytes32) = 0x0000000000000000000000000000000000000000000000000000000001ffc9a7
    
    6
    
    7# @dev ERC165 interface ID of ERC721
    
    8ERC721_INTERFACE_ID: constant(bytes32) = 0x0000000000000000000000000000000000000000000000000000000080ac58cd
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

[ERC-165(opens in a new tab)](https://eips.ethereum.org/EIPS/eip-165)
specifies a mechanism for a contract to disclose how applications can
communicate with it, to which ERCs it conforms. In this case, the contract
conforms to ERC-165 and ERC-721.

### Functions

These are the functions that actually implement ERC-721.

#### Constructor

    
    
    1@external
    
    2def __init__():
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

In Vyper, as in Python, the constructor function is called `__init__`.

    
    
    1    """
    
    2    @dev Contract constructor.
    
    3    """
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

In Python, and in Vyper, you can also create a comment by specifying a multi-
line string (which starts and ends with `"""`), and not using it in any way.
These comments can also include [NatSpec(opens in a new
tab)](https://vyper.readthedocs.io/en/latest/natspec.html).

    
    
    1    self.supportedInterfaces[ERC165_INTERFACE_ID] = True
    
    2    self.supportedInterfaces[ERC721_INTERFACE_ID] = True
    
    3    self.minter = msg.sender
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

To access state variables you use `self.<variable name>` (again, same as in
Python).

#### View Functions

These are functions that do not modify the state of the blockchain, and
therefore can be executed for free if they are called externally. If the view
functions are called by a contract they still have to be executed on every
node and therefore cost gas.

    
    
    1@view
    
    2@external
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

These keywords prior to a function definition that start with an at sign (`@`)
are called _decorations_. They specify the circumstances in which a function
can be called.

  * `@view` specifies that this function is a view.
  * `@external` specifies that this particular function can be called by transactions and by other contracts.

    
    
    1def supportsInterface(_interfaceID: bytes32) -> bool:
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

In contrast to Python, Vyper is a [static typed language(opens in a new
tab)](https://wikipedia.org/wiki/Type_system#Static_type_checking). You can't
declare a variable, or a function parameter, without identifying the [data
type(opens in a new tab)](https://vyper.readthedocs.io/en/latest/types.html).
In this case the input parameter is `bytes32`, a 256-bit value (256 bits is
the native word size of the [Ethereum Virtual
Machine](/en/developers/docs/evm/)). The output is a boolean value. By
convention, the names of function parameters start with an underscore (`_`).

    
    
    1    """
    
    2    @dev Interface identification is specified in ERC-165.
    
    3    @param _interfaceID Id of the interface
    
    4    """
    
    5    return self.supportedInterfaces[_interfaceID]
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Return the value from the `self.supportedInterfaces` HashMap, which is set in
the constructor (`__init__`).

    
    
    1### VIEW FUNCTIONS ###
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

These are the view functions that make information about the tokens available
to users and other contracts.

    
    
    1@view
    
    2@external
    
    3def balanceOf(_owner: address) -> uint256:
    
    4    """
    
    5    @dev Returns the number of NFTs owned by `_owner`.
    
    6         Throws if `_owner` is the zero address. NFTs assigned to the zero address are considered invalid.
    
    7    @param _owner Address for whom to query the balance.
    
    8    """
    
    9    assert _owner != ZERO_ADDRESS
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

This line [asserts(opens in a new
tab)](https://vyper.readthedocs.io/en/latest/statements.html#assert) that
`_owner` is not zero. If it is, there is an error and the operation is
reverted.

    
    
    1    return self.ownerToNFTokenCount[_owner]
    
    2
    
    3@view
    
    4@external
    
    5def ownerOf(_tokenId: uint256) -> address:
    
    6    """
    
    7    @dev Returns the address of the owner of the NFT.
    
    8         Throws if `_tokenId` is not a valid NFT.
    
    9    @param _tokenId The identifier for an NFT.
    
    10    """
    
    11    owner: address = self.idToOwner[_tokenId]
    
    12    # Throws if `_tokenId` is not a valid NFT
    
    13    assert owner != ZERO_ADDRESS
    
    14    return owner
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

In the Ethereum Virtual Machine (evm) any storage that does not have a value
stored in it is zero. If there is no token at `_tokenId` then the value of
`self.idToOwner[_tokenId]` is zero. In that case the function reverts.

    
    
    1@view
    
    2@external
    
    3def getApproved(_tokenId: uint256) -> address:
    
    4    """
    
    5    @dev Get the approved address for a single NFT.
    
    6         Throws if `_tokenId` is not a valid NFT.
    
    7    @param _tokenId ID of the NFT to query the approval of.
    
    8    """
    
    9    # Throws if `_tokenId` is not a valid NFT
    
    10    assert self.idToOwner[_tokenId] != ZERO_ADDRESS
    
    11    return self.idToApprovals[_tokenId]
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Note that `getApproved` _can_ return zero. If the token is valid it returns
`self.idToApprovals[_tokenId]`. If there is no approver that value is zero.

    
    
    1@view
    
    2@external
    
    3def isApprovedForAll(_owner: address, _operator: address) -> bool:
    
    4    """
    
    5    @dev Checks if `_operator` is an approved operator for `_owner`.
    
    6    @param _owner The address that owns the NFTs.
    
    7    @param _operator The address that acts on behalf of the owner.
    
    8    """
    
    9    return (self.ownerToOperators[_owner])[_operator]
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

This function checks if `_operator` is allowed to manage all of `_owner`'s
tokens in this contract. Because there can be multiple operators, this is a
two level HashMap.

#### Transfer Helper Functions

These functions implement operations that are part of transferring or managing
tokens.

    
    
    1
    
    2### TRANSFER FUNCTION HELPERS ###
    
    3
    
    4@view
    
    5@internal
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

This decoration, `@internal`, means that the function is only accessible from
other functions within the same contract. By convention, these function names
also start with an underscore (`_`).

    
    
    1def _isApprovedOrOwner(_spender: address, _tokenId: uint256) -> bool:
    
    2    """
    
    3    @dev Returns whether the given spender can transfer a given token ID
    
    4    @param spender address of the spender to query
    
    5    @param tokenId uint256 ID of the token to be transferred
    
    6    @return bool whether the msg.sender is approved for the given token ID,
    
    7        is an operator of the owner, or is the owner of the token
    
    8    """
    
    9    owner: address = self.idToOwner[_tokenId]
    
    10    spenderIsOwner: bool = owner == _spender
    
    11    spenderIsApproved: bool = _spender == self.idToApprovals[_tokenId]
    
    12    spenderIsApprovedForAll: bool = (self.ownerToOperators[owner])[_spender]
    
    13    return (spenderIsOwner or spenderIsApproved) or spenderIsApprovedForAll
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

There are three ways in which an address can be allowed to transfer a token:

  1. The address is the owner of the token
  2. The address is approved to spend that token
  3. The address is an operator for the owner of the token

The function above can be a view because it doesn't change the state. To
reduce operating costs, any function that _can_ be a view _should_ be a view.

    
    
    1@internal
    
    2def _addTokenTo(_to: address, _tokenId: uint256):
    
    3    """
    
    4    @dev Add a NFT to a given address
    
    5         Throws if `_tokenId` is owned by someone.
    
    6    """
    
    7    # Throws if `_tokenId` is owned by someone
    
    8    assert self.idToOwner[_tokenId] == ZERO_ADDRESS
    
    9    # Change the owner
    
    10    self.idToOwner[_tokenId] = _to
    
    11    # Change count tracking
    
    12    self.ownerToNFTokenCount[_to] += 1
    
    13
    
    14
    
    15@internal
    
    16def _removeTokenFrom(_from: address, _tokenId: uint256):
    
    17    """
    
    18    @dev Remove a NFT from a given address
    
    19         Throws if `_from` is not the current owner.
    
    20    """
    
    21    # Throws if `_from` is not the current owner
    
    22    assert self.idToOwner[_tokenId] == _from
    
    23    # Change the owner
    
    24    self.idToOwner[_tokenId] = ZERO_ADDRESS
    
    25    # Change count tracking
    
    26    self.ownerToNFTokenCount[_from] -= 1
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

When there's a problem with a transfer we revert the call.

    
    
    1@internal
    
    2def _clearApproval(_owner: address, _tokenId: uint256):
    
    3    """
    
    4    @dev Clear an approval of a given address
    
    5         Throws if `_owner` is not the current owner.
    
    6    """
    
    7    # Throws if `_owner` is not the current owner
    
    8    assert self.idToOwner[_tokenId] == _owner
    
    9    if self.idToApprovals[_tokenId] != ZERO_ADDRESS:
    
    10        # Reset approvals
    
    11        self.idToApprovals[_tokenId] = ZERO_ADDRESS
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Only change the value if necessary. State variables live in storage. Writing
to storage is one of the most expensive operations the EVM (Ethereum Virtual
Machine) does (in terms of [gas](/en/developers/docs/gas/)). Therefore, it is
a good idea to minimize it, even writing the existing value has a high cost.

    
    
    1@internal
    
    2def _transferFrom(_from: address, _to: address, _tokenId: uint256, _sender: address):
    
    3    """
    
    4    @dev Execute transfer of a NFT.
    
    5         Throws unless `msg.sender` is the current owner, an authorized operator, or the approved
    
    6         address for this NFT. (NOTE: `msg.sender` not allowed in private function so pass `_sender`.)
    
    7         Throws if `_to` is the zero address.
    
    8         Throws if `_from` is not the current owner.
    
    9         Throws if `_tokenId` is not a valid NFT.
    
    10    """
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

We have this internal function because there are two ways to transfer tokens
(regular and safe), but we want only a single location in the code where we do
it to make auditing easier.

    
    
    1    # Check requirements
    
    2    assert self._isApprovedOrOwner(_sender, _tokenId)
    
    3    # Throws if `_to` is the zero address
    
    4    assert _to != ZERO_ADDRESS
    
    5    # Clear approval. Throws if `_from` is not the current owner
    
    6    self._clearApproval(_from, _tokenId)
    
    7    # Remove NFT. Throws if `_tokenId` is not a valid NFT
    
    8    self._removeTokenFrom(_from, _tokenId)
    
    9    # Add NFT
    
    10    self._addTokenTo(_to, _tokenId)
    
    11    # Log the transfer
    
    12    log Transfer(_from, _to, _tokenId)
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

To emit an event in Vyper you use a `log` statement ([see here for more
details(opens in a new tab)](https://vyper.readthedocs.io/en/latest/event-
logging.html#event-logging)).

#### Transfer Functions

    
    
    1
    
    2### TRANSFER FUNCTIONS ###
    
    3
    
    4@external
    
    5def transferFrom(_from: address, _to: address, _tokenId: uint256):
    
    6    """
    
    7    @dev Throws unless `msg.sender` is the current owner, an authorized operator, or the approved
    
    8         address for this NFT.
    
    9         Throws if `_from` is not the current owner.
    
    10         Throws if `_to` is the zero address.
    
    11         Throws if `_tokenId` is not a valid NFT.
    
    12    @notice The caller is responsible to confirm that `_to` is capable of receiving NFTs or else
    
    13            they maybe be permanently lost.
    
    14    @param _from The current owner of the NFT.
    
    15    @param _to The new owner.
    
    16    @param _tokenId The NFT to transfer.
    
    17    """
    
    18    self._transferFrom(_from, _to, _tokenId, msg.sender)
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

This function lets you transfer to an arbitrary address. Unless the address is
a user, or a contract that knows how to transfer tokens, any token you
transfer will be stuck in that address and useless.

    
    
    1@external
    
    2def safeTransferFrom(
    
    3        _from: address,
    
    4        _to: address,
    
    5        _tokenId: uint256,
    
    6        _data: Bytes[1024]=b""
    
    7    ):
    
    8    """
    
    9    @dev Transfers the ownership of an NFT from one address to another address.
    
    10         Throws unless `msg.sender` is the current owner, an authorized operator, or the
    
    11         approved address for this NFT.
    
    12         Throws if `_from` is not the current owner.
    
    13         Throws if `_to` is the zero address.
    
    14         Throws if `_tokenId` is not a valid NFT.
    
    15         If `_to` is a smart contract, it calls `onERC721Received` on `_to` and throws if
    
    16         the return value is not `bytes4(keccak256("onERC721Received(address,address,uint256,bytes)"))`.
    
    17         NOTE: bytes4 is represented by bytes32 with padding
    
    18    @param _from The current owner of the NFT.
    
    19    @param _to The new owner.
    
    20    @param _tokenId The NFT to transfer.
    
    21    @param _data Additional data with no specified format, sent in call to `_to`.
    
    22    """
    
    23    self._transferFrom(_from, _to, _tokenId, msg.sender)
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

It is OK to do the transfer first because if there's a problem we are going to
revert anyway, so everything done in the call will be cancelled.

    
    
    1    if _to.is_contract: # check if `_to` is a contract address
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

First check to see if the address is a contract (if it has code). If not,
assume it is a user address and the user will be able to use the token or
transfer it. But don't let it lull you into a false sense of security. You can
lose tokens, even with `safeTransferFrom`, if you transfer them to an address
for which nobody knows the private key.

    
    
    1        returnValue: bytes32 = ERC721Receiver(_to).onERC721Received(msg.sender, _from, _tokenId, _data)
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Call the target contract to see if it can receive ERC-721 tokens.

    
    
    1        # Throws if transfer destination is a contract which does not implement 'onERC721Received'
    
    2        assert returnValue == method_id("onERC721Received(address,address,uint256,bytes)", output_type=bytes32)
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

If the destination is a contract, but one that doesn't accept ERC-721 tokens
(or that decided not to accept this particular transfer), revert.

    
    
    1@external
    
    2def approve(_approved: address, _tokenId: uint256):
    
    3    """
    
    4    @dev Set or reaffirm the approved address for an NFT. The zero address indicates there is no approved address.
    
    5         Throws unless `msg.sender` is the current NFT owner, or an authorized operator of the current owner.
    
    6         Throws if `_tokenId` is not a valid NFT. (NOTE: This is not written the EIP)
    
    7         Throws if `_approved` is the current owner. (NOTE: This is not written the EIP)
    
    8    @param _approved Address to be approved for the given NFT ID.
    
    9    @param _tokenId ID of the token to be approved.
    
    10    """
    
    11    owner: address = self.idToOwner[_tokenId]
    
    12    # Throws if `_tokenId` is not a valid NFT
    
    13    assert owner != ZERO_ADDRESS
    
    14    # Throws if `_approved` is the current owner
    
    15    assert _approved != owner
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

By convention if you want not to have an approver you appoint the zero
address, not yourself.

    
    
    1    # Check requirements
    
    2    senderIsOwner: bool = self.idToOwner[_tokenId] == msg.sender
    
    3    senderIsApprovedForAll: bool = (self.ownerToOperators[owner])[msg.sender]
    
    4    assert (senderIsOwner or senderIsApprovedForAll)
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

To set an approval you can either be the owner, or an operator authorized by
the owner.

    
    
    1    # Set the approval
    
    2    self.idToApprovals[_tokenId] = _approved
    
    3    log Approval(owner, _approved, _tokenId)
    
    4
    
    5
    
    6@external
    
    7def setApprovalForAll(_operator: address, _approved: bool):
    
    8    """
    
    9    @dev Enables or disables approval for a third party ("operator") to manage all of
    
    10         `msg.sender`'s assets. It also emits the ApprovalForAll event.
    
    11         Throws if `_operator` is the `msg.sender`. (NOTE: This is not written the EIP)
    
    12    @notice This works even if sender doesn't own any tokens at the time.
    
    13    @param _operator Address to add to the set of authorized operators.
    
    14    @param _approved True if the operators is approved, false to revoke approval.
    
    15    """
    
    16    # Throws if `_operator` is the `msg.sender`
    
    17    assert _operator != msg.sender
    
    18    self.ownerToOperators[msg.sender][_operator] = _approved
    
    19    log ApprovalForAll(msg.sender, _operator, _approved)
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

#### Mint New Tokens and Destroy Existing Ones

The account that created the contract is the `minter`, the super user that is
authorized to mint new NFTs. However, even it is not allowed to burn existing
tokens. Only the owner, or an entity authorized by the owner, can do that.

    
    
    1### MINT & BURN FUNCTIONS ###
    
    2
    
    3@external
    
    4def mint(_to: address, _tokenId: uint256) -> bool:
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

This function always returns `True`, because if the operation fails it is
reverted.

    
    
    1    """
    
    2    @dev Function to mint tokens
    
    3         Throws if `msg.sender` is not the minter.
    
    4         Throws if `_to` is zero address.
    
    5         Throws if `_tokenId` is owned by someone.
    
    6    @param _to The address that will receive the minted tokens.
    
    7    @param _tokenId The token id to mint.
    
    8    @return A boolean that indicates if the operation was successful.
    
    9    """
    
    10    # Throws if `msg.sender` is not the minter
    
    11    assert msg.sender == self.minter
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Only the minter (the account that created the ERC-721 contract) can mint new
tokens. This can be a problem in the future if we want to change the minter's
identity. In a production contract you would probably want a function that
allows the minter to transfer minter privileges to somebody else.

    
    
    1    # Throws if `_to` is zero address
    
    2    assert _to != ZERO_ADDRESS
    
    3    # Add NFT. Throws if `_tokenId` is owned by someone
    
    4    self._addTokenTo(_to, _tokenId)
    
    5    log Transfer(ZERO_ADDRESS, _to, _tokenId)
    
    6    return True
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

By convention, the minting of new tokens counts as a transfer from address
zero.

    
    
    1
    
    2@external
    
    3def burn(_tokenId: uint256):
    
    4    """
    
    5    @dev Burns a specific ERC721 token.
    
    6         Throws unless `msg.sender` is the current owner, an authorized operator, or the approved
    
    7         address for this NFT.
    
    8         Throws if `_tokenId` is not a valid NFT.
    
    9    @param _tokenId uint256 id of the ERC721 token to be burned.
    
    10    """
    
    11    # Check requirements
    
    12    assert self._isApprovedOrOwner(msg.sender, _tokenId)
    
    13    owner: address = self.idToOwner[_tokenId]
    
    14    # Throws if `_tokenId` is not a valid NFT
    
    15    assert owner != ZERO_ADDRESS
    
    16    self._clearApproval(owner, _tokenId)
    
    17    self._removeTokenFrom(owner, _tokenId)
    
    18    log Transfer(owner, ZERO_ADDRESS, _tokenId)
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Anybody who is allowed to transfer a token is allowed to burn it. While a burn
appears equivalent to transfer to the zero address, the zero address does not
actually receives the token. This allows us to free up all the storage that
was used for the token, which can reduce the gas cost of the transaction.

# Using this Contract

In contrast to Solidity, Vyper does not have inheritance. This is a deliberate
design choice to make the code clearer and therefore easier to secure. So to
create your own Vyper ERC-721 contract you take [this contract(opens in a new
tab)](https://github.com/vyperlang/vyper/blob/master/examples/tokens/ERC721.vy)
and modify it to implement the business logic you want.

# Conclusion

For review, here are some of the most important ideas in this contract:

  * To receive ERC-721 tokens with a safe transfer, contracts have to implement the `ERC721Receiver` interface.
  * Even if you use safe transfer, tokens can still get stuck if you send them to an address whose private key is unknown.
  * When there is a problem with an operation it is a good idea to `revert` the call, rather than just return a failure value.
  * ERC-721 tokens exist when they have an owner.
  * There are three ways to be authorized to transfer an NFT. You can be the owner, be approved for a specific token, or be an operator for all of the owner's tokens.
  * Past events are visible only outside the blockchain. Code running inside the blockchain cannot view them.

Now go and implement secure Vyper contracts.

n

Last edit: [@nhsz(opens in a new tab)](https://github.com/nhsz), August 15,
2023

See contributors

### Was this tutorial helpful?

YesNo

  * [Edit page(opens in a new tab)](https://github.com/ethereum/ethereum-org-website/tree/dev/public/content/developers/tutorials/erc-721-vyper-annotated-code/index.md)
  * On this page

    * Introduction
    * The Contract
      * The ERC721Receiver Interface
      * Events
      * State Variables
      * Functions

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

