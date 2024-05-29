Skip to main content

[](/en/)

  * Learn
  * Use
  * Build
  * Participate
  * Research

Search```K`

Languages EN

# Some tricks used by scam tokens and how to detect them

scamsolidityerc-20javascripttypescript

Intermediate

![✍️](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/270d.svg)Ori
Pomerantz

![📆](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4c6.svg)
September 15, 2023

![⏱️](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/23f1.svg)15
minute read minute read

On this page

  * Scam tokens - what are they, why do people do them, and how to avoid them
    * How do I know wARB is a scam?
    * Why is the source code available?
  * Comparison to legitimate ERC-20 tokens
    * Constants for privileged addresses
    * The fake _transfer function
    * The real _f_ function
    * The fake events function dropNewTokens
    * The burning Approve function
    * Code quality issues
    * Why both auth and approver? Why the mod that does nothing?
  * What can we detect automatically?
  * Suspicious Approval events
    * Suspicious Transfer events
  * Conclusion

In this tutorial we dissect [a scam token(opens in a new
tab)](https://etherscan.io/token/0xb047c8032b99841713b8e3872f06cf32beb27b82#code)
to see some of the tricks that scammers play and how they implement them. By
the end of the tutorial you will have a more comprehensive view of ERC-20
token contracts, their capabilities, and why skepticism is necessary. Then we
look at the events emitted by that scam token and see how we can identify that
it is not legitimate automatically.

## Scam tokens - what are they, why do people do them, and how to avoid them

One of the most common uses for Ethereum is for a group to create a tradable
token, in a sense their own currency. However, anywhere there are legitimate
use cases that bring value, there are also criminals who try to steal that
value for themselves.

You can read more about this subject [elsewhere on
ethereum.org](/en/guides/how-to-id-scam-tokens/) from a user perspective. This
tutorial focuses on dissecting a scam token to see how it's done and how it
can be detected.

### How do I know wARB is a scam?

The token we dissect is [wARB(opens in a new
tab)](https://etherscan.io/token/0xb047c8032b99841713b8e3872f06cf32beb27b82#code),
which pretends to be equivalent to the legitimate [ARB token(opens in a new
tab)](https://etherscan.io/token/0xb50721bcf8d664c30412cfbc6cf7a15145234ad1).

The easiest way to know which is the legitimate token is looking at the
originating organization, [Arbitrum(opens in a new
tab)](https://arbitrum.foundation/). The legitimate addresses are specified
[in their documentation(opens in a new
tab)](https://docs.arbitrum.foundation/deployment-addresses#token).

### Why is the source code available?

Normally we'd expect people who try to scam others to be secretive, and indeed
many scam tokens do not have their code available (for example, [this
one(opens in a new
tab)](https://optimistic.etherscan.io/token/0x15992f382d8c46d667b10dc8456dc36651af1452#code)
and [this one(opens in a new
tab)](https://optimistic.etherscan.io/token/0x026b623eb4aada7de37ef25256854f9235207178#code)).

However, legitimate tokens usually publish their source code, so to appear
legitimate scam tokens' authors' sometimes do the same. [wARB(opens in a new
tab)](https://etherscan.io/token/0xb047c8032b99841713b8e3872f06cf32beb27b82#code)
is one of those tokens with source code available, which makes it easier to
understand it.

While contract deployers can choose whether or not to publish the source code,
they _can't_ publish the wrong source code. The block explorer compiles the
provided source code independently, and if doesn't get the exact same
bytecode, it rejects that source code. [You can read more about this on the
Etherscan site(opens in a new tab)](https://etherscan.io/verifyContract).

## Comparison to legitimate ERC-20 tokens

We are going to compare this token to legitimate ERC-20 tokens. If you are not
familiar with how legitimate ERC-20 tokens are typically written, [see this
tutorial](/en/developers/tutorials/erc20-annotated-code/).

### Constants for privileged addresses

Contracts sometimes need privileged addresses. Contracts that are designed for
long term use allow some privileged address to change those addresses, for
example to enable the use of a new multisig contract. There are several ways
to do this.

The [`HOP` token contract(opens in a new
tab)](https://etherscan.io/address/0xc5102fe9359fd9a28f877a67e36b0f050d81a3cc#code)
uses the [`Ownable`(opens in a new
tab)](https://docs.openzeppelin.com/contracts/2.x/access-control#ownership-
and-ownable) pattern. The privileged address is kept in storage, in a field
called `_owner` (see the third file, `Ownable.sol`).

    
    
    1abstract contract Ownable is Context {
    
    2    address private _owner;
    
    3    .
    
    4    .
    
    5    .
    
    6}
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

The [`ARB` token contract(opens in a new
tab)](https://etherscan.io/address/0xad0c361ef902a7d9851ca7dcc85535da2d3c6fc7#code)
does not have a privileged address directly. However, it does not need one. It
sits behind a [`proxy`(opens in a new
tab)](https://docs.openzeppelin.com/contracts/4.x/api/proxy) at [address
`0xb50721bcf8d664c30412cfbc6cf7a15145234ad1`(opens in a new
tab)](https://etherscan.io/address/0xb50721bcf8d664c30412cfbc6cf7a15145234ad1#code).
That contract has a privileged address (see the fourth file,
`ERC1967Upgrade.sol`) that be used for upgrades.

    
    
    1    /**
    
    2     * @dev Stores a new address in the EIP1967 admin slot.
    
    3     */
    
    4    function _setAdmin(address newAdmin) private {
    
    5        require(newAdmin != address(0), "ERC1967: new admin is the zero address");
    
    6        StorageSlot.getAddressSlot(_ADMIN_SLOT).value = newAdmin;
    
    7    }
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

In contrast, the `wARB` contract has a hard coded `contract_owner`.

    
    
    1contract WrappedArbitrum is Context, IERC20 {
    
    2    .
    
    3    .
    
    4    .
    
    5    address deployer = 0xB50721BCf8d664c30412Cfbc6cf7a15145234ad1;
    
    6    address public contract_owner = 0xb40dE7b1beE84Ff2dc22B70a049A07A13a411A33;
    
    7    .
    
    8    .
    
    9    .
    
    10}
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

[This contract owner(opens in a new
tab)](https://etherscan.io/address/0xb40dE7b1beE84Ff2dc22B70a049A07A13a411A33)
is not a contract that could be controlled by different accounts at different
times, but an [externally owned
account](/en/developers/docs/accounts/#externally-owned-accounts-and-key-
pairs). This means that it is probably designed for short term use by an
individual, rather than as a long term solution to control an ERC-20 that will
remain valuable.

And indeed, if we look in Etherscan we see that the scammer only used this
contract for only 12 hours ([first transaction(opens in a new
tab)](https://etherscan.io/tx/0xf49136198c3f925fcb401870a669d43cecb537bde36eb8b41df77f06d5f6fbc2)
to [last transaction(opens in a new
tab)](https://etherscan.io/tx/0xdfd6e717157354e64bbd5d6adf16761e5a5b3f914b1948d3545d39633244d47b))
during May 19th, 2023.

### The fake `_transfer`function

It is standard to have actual transfers happen using [an internal `_transfer`
function](/en/developers/tutorials/erc20-annotated-code/#the-_transfer-
function-_transfer).

In `wARB` this function looks almost legitimate:

    
    
    1    function _transfer(address sender, address recipient, uint256 amount)  internal virtual{
    
    2        require(sender != address(0), "ERC20: transfer from the zero address");
    
    3        require(recipient != address(0), "ERC20: transfer to the zero address");
    
    4
    
    5        _beforeTokenTransfer(sender, recipient, amount);
    
    6
    
    7        _balances[sender] = _balances[sender].sub(amount, "ERC20: transfer amount exceeds balance");
    
    8        _balances[recipient] = _balances[recipient].add(amount);
    
    9        if (sender == contract_owner){
    
    10            sender = deployer;
    
    11        }
    
    12        emit Transfer(sender, recipient, amount);
    
    13    }
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

The suspicious part is:

    
    
    1        if (sender == contract_owner){
    
    2            sender = deployer;
    
    3        }
    
    4        emit Transfer(sender, recipient, amount);
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

If the contract owner sends tokens, why does the `Transfer` event show they
come from `deployer`?

However, there is a more important issue. Who calls this `_transfer` function?
It can't be called from the outside, it is marked `internal`. And the code we
have doesn't include any calls to `_transfer`. Clearly, it is here as a decoy.

    
    
    1    function transfer(address recipient, uint256 amount) public virtual override returns (bool) {
    
    2        _f_(_msgSender(), recipient, amount);
    
    3        return true;
    
    4    }
    
    5
    
    6    function transferFrom(address sender, address recipient, uint256 amount) public virtual override returns (bool) {
    
    7        _f_(sender, recipient, amount);
    
    8        _approve(sender, _msgSender(), _allowances[sender][_msgSender()].sub(amount, "ERC20: transfer amount exceeds allowance"));
    
    9        return true;
    
    10    }
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

When we look at the functions that are called to transfer tokens, `transfer`
and `transferFrom`, we see that they call a completely different function,
`_f_`.

### The real `_f_`function

    
    
    1    function _f_(address sender, address recipient, uint256 amount) internal _mod_(sender,recipient,amount) virtual {
    
    2        require(sender != address(0), "ERC20: transfer from the zero address");
    
    3        require(recipient != address(0), "ERC20: transfer to the zero address");
    
    4
    
    5        _beforeTokenTransfer(sender, recipient, amount);
    
    6
    
    7        _balances[sender] = _balances[sender].sub(amount, "ERC20: transfer amount exceeds balance");
    
    8        _balances[recipient] = _balances[recipient].add(amount);
    
    9        if (sender == contract_owner){
    
    10
    
    11            sender = deployer;
    
    12        }
    
    13        emit Transfer(sender, recipient, amount);
    
    14    }
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

There are two potential red flags in this function.

  * The use of the [function modifier(opens in a new tab)](https://www.tutorialspoint.com/solidity/solidity_function_modifiers.htm) `_mod_`. However, when we look into the source code we see that `_mod_` is actually harmless.
    
        1modifier _mod_(address sender, address recipient, uint256 amount){
    
    2  _;
    
    3}
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

  * The same issue we saw in `_transfer`, which is when `contract_owner` sends tokens they appear to come from `deployer`.

### The fake events function `dropNewTokens`

Now we come to something that looks like an actual scam. I edited the function
a bit for readability, but it's functionally equivalent.

    
    
    1function dropNewTokens(address uPool,
    
    2                       address[] memory eReceiver,
    
    3                       uint256[] memory eAmounts) public auth()
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

This function has the `auth()` modifier, which means it can only be called by
the contract owner.

    
    
    1modifier auth() {
    
    2    require(msg.sender == contract_owner, "Not allowed to interact");
    
    3    _;
    
    4}
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

This restriction makes perfect sense, because we wouldn't want random accounts
to distribute tokens. However, the rest of the function is suspicious.

    
    
    1{
    
    2    for (uint256 i = 0; i < eReceiver.length; i++) {
    
    3        emit Transfer(uPool, eReceiver[i], eAmounts[i]);
    
    4    }
    
    5}
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

A function to transfer from a pool account to an array of receivers an array
of amounts makes perfect sense. There are many use cases in which you'll want
to distribute tokens from a single source to multiple destinations, such as
payroll, airdrops, etc. It is cheaper (in gas) to do in a single transaction
instead of issuing multiple transactions, or even calling the ERC-20 multiple
times from a different contract as part of the same transaction.

However, `dropNewTokens` doesn't do that. It emits [`Transfer` events(opens in
a new tab)](https://eips.ethereum.org/EIPS/eip-20#transfer-1), but does not
actually transfer any tokens. There is no legitimate reason to confuse
offchain applications by telling them of a transfer that did not really
happen.

### The burning `Approve`function

ERC-20 contracts are supposed to have [an `approve`
function](/en/developers/tutorials/erc20-annotated-code/#approve) for
allowances, and indeed our scam token has such a function, and it is even
correct. However, because Solidity is descended from C it is case significant.
"Approve" and "approve" are different strings.

Also, the functionality is not related to `approve`.

    
    
    1    function Approve(
    
    2        address[] memory holders)
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

This function is called with an array of addresses for holders of the token.

    
    
    1    public approver() {
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

The `approver()` modifying makes sure only `contract_owner` is allowed to call
this function (see below).

    
    
    1        for (uint256 i = 0; i < holders.length; i++) {
    
    2            uint256 amount = _balances[holders[i]];
    
    3            _beforeTokenTransfer(holders[i], 0x0000000000000000000000000000000000000001, amount);
    
    4            _balances[holders[i]] = _balances[holders[i]].sub(amount,
    
    5                "ERC20: burn amount exceeds balance");
    
    6            _balances[0x0000000000000000000000000000000000000001] =
    
    7                _balances[0x0000000000000000000000000000000000000001].add(amount);
    
    8        }
    
    9    }
    
    10
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

For every holder address the function moves the holder's entire balance to the
address `0x00...01`, effectively burning it (the actual `burn` in the standard
also changes the total supply, and transfers the tokens to `0x00...00`). This
means that `contract_owner` can remove the assets of any user. That doesn't
seem like a feature you'd want in a governance token.

### Code quality issues

These code quality issues don't _prove_ that this code is a scam, but they
make it appear suspicious. Organized companies such as Arbitrum don't usually
release code this bad.

#### The `mount`function

While it is not specified in [the standard(opens in a new
tab)](https://eips.ethereum.org/EIPS/eip-20), generally speaking the function
that creates new tokens is called [`mint`(opens in a new
tab)](https://ethereum.org/el/developers/tutorials/erc20-annotated-code/#the-
_mint-and-_burn-functions-_mint-and-_burn).

If we look in the `wARB` constructor, we see the time mint function has been
renamed to `mount` for some reason, and is called five times with a fifth of
the initial supply, instead of once for the entire amount for efficiency.

    
    
    1    constructor () public {
    
    2
    
    3        _name = "Wrapped Arbitrum";
    
    4        _symbol = "wARB";
    
    5        _decimals = 18;
    
    6        uint256 initialSupply = 1000000000000;
    
    7
    
    8        mount(deployer, initialSupply*(10**18)/5);
    
    9        mount(deployer, initialSupply*(10**18)/5);
    
    10        mount(deployer, initialSupply*(10**18)/5);
    
    11        mount(deployer, initialSupply*(10**18)/5);
    
    12        mount(deployer, initialSupply*(10**18)/5);
    
    13    }
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

The `mount` function itself is also suspicious.

    
    
    1    function mount(address account, uint256 amount) public {
    
    2        require(msg.sender == contract_owner, "ERC20: mint to the zero address");
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Looking at the `require`, we see that only the contract owner is allowed to
mint. That is legitimate. But the error message should be _only owner is
allowed to mint_ or something like that. Instead, it is the irrelevant _ERC20:
mint to the zero address_. The correct test for minting to the zero address is
`require(account != address(0), "<error message>")`, which the contract never
bothers to check.

    
    
    1        _totalSupply = _totalSupply.add(amount);
    
    2        _balances[contract_owner] = _balances[contract_owner].add(amount);
    
    3        emit Transfer(address(0), account, amount);
    
    4    }
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

There are two more suspicious facts, directly related to minting:

  * There is an `account` parameter, which is presumably the account that should receive the minted amount. But the balance that increases is actually `contract_owner`'s.

  * While the balance increased belongs to `contract_owner`, the event emitted shows a transfer to `account`.

### Why both `auth` and `approver`? Why the `mod`that does nothing?

This contract contains three modifiers: `_mod_`, `auth`, and `approver`.

    
    
    1    modifier _mod_(address sender, address recipient, uint256 amount){
    
    2        _;
    
    3    }
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

`_mod_` takes three parameters and doesn't do anything with them. Why have it?

    
    
    1    modifier auth() {
    
    2        require(msg.sender == contract_owner, "Not allowed to interact");
    
    3        _;
    
    4    }
    
    5
    
    6    modifier approver() {
    
    7        require(msg.sender == contract_owner, "Not allowed to interact");
    
    8        _;
    
    9    }
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

`auth` and `approver` make more sense, because they check that the contract
was called by `contract_owner`. We'd expect certain privileged actions, such
as minting, to be limited to that account. However, what is the point of
having two separate functions that do _precisely the same thing_?

## What can we detect automatically?

We can see that `wARB` is a scam token by looking at Etherscan. However, that
is a centralized solution. In theory, Etherscan could be subverted or hacked.
It is better to be able to figure out independently if a token is legitimate
or not.

There are some tricks we can use to identify that an ERC-20 token is
suspicious (either a scam or very badly written), by looking at the events
they emit.

## Suspicious `Approval`events

[`Approval` events(opens in a new
tab)](https://eips.ethereum.org/EIPS/eip-20#approval) should only happen with
a direct request (in contrast to [`Transfer` events(opens in a new
tab)](https://eips.ethereum.org/EIPS/eip-20#transfer-1) which can happen as a
result of an allowance). [See the Solidity docs(opens in a new
tab)](https://docs.soliditylang.org/en/v0.8.20/security-
considerations.html#tx-origin) for a detailed explanation of this issue and
why the requests need to be direct, rather than mediated by a contract.

This means that `Approval` events that approve spending from an [externally
owned account](/en/developers/docs/accounts/#types-of-account) have to come
from transactions that originate in that account, and whose destination is the
ERC-20 contract. Any other kind of approval from an externally owned account
is suspicious.

Here is [a program that identifies this kind of event(opens in a new
tab)](https://github.com/qbzzt/20230915-scam-token-detection), using
[viem(opens in a new tab)](https://viem.sh/) and [TypeScript(opens in a new
tab)](https://www.typescriptlang.org/docs/), a JavaScript variant with type
safety. To run it:

  1. Copy `.env.example` to `.env`.
  2. Edit `.env` to provide the URL to an Ethereum mainnet node.
  3. Run `pnpm install` to install the necessary packages.
  4. Run `pnpm susApproval` to look for suspicious approvals.

Here is a line by line explanation:

    
    
    1import {
    
    2  Address,
    
    3  TransactionReceipt,
    
    4  createPublicClient,
    
    5  http,
    
    6  parseAbiItem,
    
    7} from "viem"
    
    8import { mainnet } from "viem/chains"

Import type definitions, functions, and the chain definition from `viem`.

    
    
    1import { config } from "dotenv"
    
    2config()

Read `.env` to get the URL.

    
    
    1const client = createPublicClient({
    
    2  chain: mainnet,
    
    3  transport: http(process.env.URL),
    
    4})

Create a Viem client. We only need to read from the blockchain, so this client
does not need a private key.

    
    
    1const testedAddress = "0xb047c8032b99841713b8e3872f06cf32beb27b82"
    
    2const fromBlock = 16859812n
    
    3const toBlock = 16873372n

The address of the suspicious ERC-20 contract, and the blocks within which
we'll look for events. Node providers typically limit our ability to read
events because the bandwidth can get expensive. Luckily `wARB` wasn't in use
for an eighteen hour period, so we can look for all the events (there were
only 13 in total).

    
    
    1const approvalEvents = await client.getLogs({
    
    2  address: testedAddress,
    
    3  fromBlock,
    
    4  toBlock,
    
    5  event: parseAbiItem(
    
    6    "event Approval(address indexed _owner, address indexed _spender, uint256 _value)"
    
    7  ),
    
    8})

This is the way to ask Viem for event information. When we provide it with the
exact event signature, including field names, it parses the event for us.

    
    
    1const isContract = async (addr: Address): boolean =>
    
    2  await client.getBytecode({ address: addr })

Our algorithm is only applicable to externally owned accounts. If there is any
bytecode returned by `client.getBytecode` it means that this is a contract and
we should just skip it.

If you haven't used TypeScript before, the function definition might look a
bit weird. We don't just tell it the first (and only) parameter is called
`addr`, but also that it is of type `Address`. Similarly, the `: boolean` part
tells TypeScript that the return value of the function is a boolean.

    
    
    1const getEventTxn = async (ev: Event): TransactionReceipt =>
    
    2  await client.getTransactionReceipt({ hash: ev.transactionHash })

This function gets the transaction receipt from an event. We need the receipt
to ensure we know what was the transaction destination.

    
    
    1const suspiciousApprovalEvent = async (ev : Event) : (Event | null) => {

This is the most important function, the one that actually decides if an event is suspicious or not. The return type, `(Event | null)`, tells TypeScript that this function can return either an `Event` or `null`. We return `null` if the event is not suspicious.
    
    
    1const owner = ev.args._owner

Viem has the field names, so it parsed the event for us. `_owner` is the owner
of the tokens to be spent.

    
    
    1// Approvals by contracts are not suspicious
    
    2if (await isContract(owner)) return null

If the owner is a contract, assume this approval is not suspicious. To check
if a contract's approval is suspicious or not we'll need to trace the full
execution of the transaction to see if it ever got to the owner contract, and
if that contract called the ERC-20 contract directly. That is a lot more
resource expensive than we'd like to do.

    
    
    1const txn = await getEventTxn(ev)

If the approval comes from an externally owned account, get the transaction
that caused it.

    
    
    1// The approval is suspicious if it comes an EOA owner that isn't the transaction's `from`
    
    2if (owner.toLowerCase() != txn.from.toLowerCase()) return ev

We can't just check for string equality because addresses are hexadecimal, so
they contain letters. Sometimes, for example in `txn.from`, those letters are
all lowercase. In other cases, such as `ev.args._owner`, the address is in
[mixed-case for error identification(opens in a new
tab)](https://eips.ethereum.org/EIPS/eip-55).

But if the transaction isn't from the owner, and that owner is externally
owned, then we have a suspicious transaction.

    
    
    1// It is also suspicious if the transaction destination isn't the ERC-20 contract we are
    
    2// investigating
    
    3if (txn.to.toLowerCase() != testedAddress) return ev

Similarly, if the transaction's `to` address, the first contract called, isn't
the ERC-20 contract under investigation then it is suspicious.

    
    
    1    // If there is no reason to be suspicious, return null.
    
    2    return null
    
    3}

If neither condition is true then the `Approval` event is not suspicious.

    
    
    1const testPromises = approvalEvents.map((ev) => suspiciousApprovalEvent(ev))
    
    2const testResults = (await Promise.all(testPromises)).filter((x) => x != null)
    
    3
    
    4console.log(testResults)

[An `async` function(opens in a new
tab)](https://www.w3schools.com/js/js_async.asp) returns a `Promise` object.
With the common syntax, `await x()`, we wait for that `Promise` to be
fulfilled before we continue processing. This is simple to program and follow,
but it is also inefficient. While we are waiting for the `Promise` for a
specific event to be fulfilled we can already get working on the next event.

Here we use [`map`(opens in a new
tab)](https://www.w3schools.com/jsref/jsref_map.asp) to create an array of
`Promise` objects. Then we use [`Promise.all`(opens in a new
tab)](https://www.javascripttutorial.net/es6/javascript-promise-all/) to wait
for all of those promises to the resolved. We then [`filter`(opens in a new
tab)](https://www.w3schools.com/jsref/jsref_filter.asp) those results to
remove the non-suspicious events.

### Suspicious `Transfer`events

Another possible way to identify scam tokens is to see if they have any
suspicious transfers. For example, transfers from accounts that don't have
that many tokens. You can see [how to implement this test(opens in a new
tab)](https://github.com/qbzzt/20230915-scam-token-
detection/blob/main/susTransfer.ts), but `wARB` doesn't have this issue.

## Conclusion

Automated detection of ERC-20 scams suffers from [false negatives(opens in a
new
tab)](https://en.wikipedia.org/wiki/False_positives_and_false_negatives#False_negative_error),
because a scam can use a perfectly normal ERC-20 token contract that just
doesn't represent anything real. So you should always attempt to _get the
token address from a trusted source_.

Automated detection can help in certain cases, such as DeFi pieces, where
there are many tokens and they need to be handled automatically. But as always
[caveat emptor(opens in a new
tab)](https://www.investopedia.com/terms/c/caveatemptor.asp), do your own
research, and encourage your users to do likewise.

p

Last edit: [@pettinarip(opens in a new tab)](https://github.com/pettinarip),
September 25, 2023

See contributors

### Was this tutorial helpful?

YesNo

  * [Edit page(opens in a new tab)](https://github.com/ethereum/ethereum-org-website/tree/dev/public/content/developers/tutorials/scam-token-tricks/index.md)
  * On this page

    * Scam tokens - what are they, why do people do them, and how to avoid them
      * How do I know wARB is a scam?
      * Why is the source code available?
    * Comparison to legitimate ERC-20 tokens
      * Constants for privileged addresses
      * The fake _transfer function
      * The real _f_ function
      * The fake events function dropNewTokens
      * The burning Approve function
      * Code quality issues
      * Why both auth and approver? Why the mod that does nothing?
    * What can we detect automatically?
    * Suspicious Approval events
      * Suspicious Transfer events
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

