This website uses cookies to offer you a better browsing experience. Find out
more on how we use cookies.

Opt-out[Details](/privacy-policy#collection-of-information)

Accept

[![Solana](/_next/static/media/logotype.e4df684f.svg)](/)

  * Learn
  * Developers
  * Solutions
  * Network
  * Community

Search```K`

[Documentation](/docs)[RPC
API](/docs/rpc)[Cookbook](/developers/cookbook)[Guides](/developers/guides)[Terminology](/docs/terminology)

# EVM vs. SVM: Accounts

See how accounts differ when building on Ethereum and Solana.

**Table of Contents**

  

'Account' in Ethereum

'Account' in Solana

Account abstraction

[Is account abstraction implemented in Solana?](account-abstraction-solana)

Summary

As blockchain networks, Ethereum and Solana possess unique data structures,
functioning as global public world computers that store and share data on
their networks. In this chapter, we aim to explore how these chains structure
their data sets.

### **'Account' in Ethereum**

In Ethereum, an 'account' refers to an entity that owns Ether and can send
transactions. It includes addresses necessary for deposits and withdrawals and
is categorized as follows:

  * **EOA (Externally Owned Account):** An account owned externally, possessing a private key. Think of it as an account for an individual's wallet.
  * **CA (Contract Account):** An account for contracts, holding smart contract code.

A key difference between EOA and CA in Ethereum is that EOA, not being a smart
contract, typically does not have its own storage. Therefore, the code hash of
an EOA is set to a 'null' hash, indicating that the account does not have
storage.

Field | Description  
---|---  
`address` | An Account’s address  
`balance` | The amount of ETH (in wei) an address owns.  
`nonce` |  A counter that shows the number of transactions sent from the account to ensure transactions are processed only once. with smart contracts, it reflects the number of contracts created by the account.   
`code hash` | The code of an account on the EVM.  
`storage hash (storage root)` |  A 256-bit hash of the root node of a Merkle Patricia Tree that encodes the storage contents of the account. This tree encodes the hash of the storage contents of this account, and is empty by default.   
  
An Externally Owned Account (EOA) is an account with a private key, and
possessing a private key means controlling access to funds or contracts. The
private key implies control over access to funds or contracts. The following
data are included in an EOA:

A Contract Account contains smart contract code that simply cannot be held by
an EOA. Additionally, a Contract Account does not have a private key. Instead,
it is controlled by the logic of the smart contract code. This smart contract
code, recorded on the Ethereum blockchain when the Contract Account is
created, is a software program executed by the EVM.

Like an EOA, a Contract Account has an address and can send and receive Ether.
However, when a transaction's destination is a Contract Account address, the
transaction and transaction data are used as input for the contract to be
executed in the EVM. In addition to Ether, the transaction can include data
indicating a specific function of the contract to execute and parameters to
pass to that function. Thus, a transaction can call functions within a
contract. If requested by an EOA, contracts can also call other contracts.
However, since a Contract Account does not have a private key, it cannot sign
for transactions and cannot initiate transactions on its own. The
relationships are summarized as follows:

  * EOA → EOA (OK)
  * EOA → CA (OK)
  * EOA → CA → CA (OK)
  * CA → CA (Impossible)

### **'Account' in Solana**

The concept of an Account in Solana is somewhat broader than in Ethereum. In
Solana, all data is stored and executed based on Accounts. This means that in
every case where state needs to be stored between transactions, it is saved
using accounts. Similar to files in operating systems like Linux, accounts can
store arbitrary data that persists beyond the lifespan of a program.
Additionally, like a file, an account contains metadata that informs the
runtime about who can access the data and how.

In Solana's Sealevel VM, all accounts are capable of storing data. So, where
can smart contract developers store their data? They can store data in non-
executable accounts (PDAs) owned by an executable account. Developers can
create new accounts by assigning an owner identical to the address of their
executable account to store data.

Field | Description  
---|---  
`lamports` |  The number of lamports owned by this account. The equivalent of `balance`.   
`owner` | The program owner of this account.  
`executable` |  Whether this account can process instructions.  
`data` | The raw data byte array stored by this account.  
`rent_epoch` |  The next epoch that this account will owe rent.  
  
However, 'accounts' on the Solana network, which store data, require the
payment of a fee. These accounts include metadata about the lifespan of the
data they contain, represented in terms of a native token called 'Lamports'.
Accounts are stored in validators' memory and pay 'Rent' to remain there.
Validators periodically scan all accounts and collect rent. Accounts whose
Lamports fall to zero are automatically deleted since they can't pay for their
rent. If an account contains a sufficient quantity of Lamports, it becomes
exempt from rent, and no rent fees are deducted separately.

Solana's accounts are divided into the following two types, similar to
Ethereum:

  * **Executable account (program account):** These are smart contracts that store code, often referred to more simply as "programs".
  * **Non-executable account (data account):** These can receive tokens or data but cannot execute code, as the executable variable is set to 'false'.

(*Unlike Ethereum, Solana uses the term 'Program' instead of 'Contract'.)

A comparison of the account structures in each chain reveals the following
differences.

Ethereum's Account | Solana's Account  
---|---  
`Account` | `owner`  
`balance` | `lamports`  
`nonce` | [no equivalent]  
`code hash` | `executable && data`  
`storage hash` | `data`  
`code hash` | `executable && data`  
[no equivalent] | `rent_epoch`  
  
Then, how do EOA and CA correspond to Solana's Account structure? They can be
mapped as follows.

**EOA (Externally Owned Account, Wallet)**

  * → non-executable, data accounts
  * However, individual wallets on Solana are composed of a collection of **data accounts,** which are a broader concept than **EOA.**

**CA (Contract Account)**

  * → executable, program accounts
  * While sharing the same concept, Ethereum's **CA** cannot execute transactions on their own; they must be executed by **EOA.**

EOA (Externally Owned Account, Wallet) | → non-executable, data accounts |  However, individual wallets on Solana are composed of a collection of **data accounts,** which are a broader concept than **EOA.**  
---|---|---  
CA (Contract Account) | → executable, program accounts |  While sharing the same concept, Ethereum's **CA** cannot execute transactions on their own; they must be executed by **EOA**.   
  
## **Account abstraction**

Ethereum has long been exploring the concept of account abstraction. There are
two types of accounts in Ethereum: EOAs and CAs, each with distinctly
different functions. Notably, contract accounts (CAs) cannot generate or sign
transactions, leading to significant limitations. Transactions must be
initiated and signed through an EOA, which implies the use of a base fee of
21,000 gas and adds to the complexity of account management. Account
abstraction aims to eliminate these constraints, allowing a single account to
perform the functions of both EOAs and contract accounts.

Consequently, the following adjustments can be made to the chart:

  * EOA → EOA (OK)
  * EOA → CA (OK)
  * EOA → CA → CA (OK)
  * EOA + CA (AA) → CA (now, OK!)

For example, multisig wallets or smart contract wallets need to store a small
amount of Ethereum in a separate EOA to pay for transaction fees, leading to
the inconvenience of having to replenish it over time. Account abstraction
allows a single account to execute contracts and issue transactions, improving
this inconvenience. Through ERC-4337, Vitalik proposed this concept to the
community, and it was adopted in 2021, now implemented in the Ethereum
network.

In summary, account abstraction offers the following benefits:

  * Others paying my transaction fees, or me paying for others.
  * Paying fees with ERC-20 tokens
  * Setting custom security rules.
  * Account recovery in case of key loss.
  * Sharing account security among trusted devices or individuals.
  * Batch transactions (e.g., authorizing and executing a swap in one go).
  * More opportunities for dapp and wallet developers to innovate the user experience.

### **Is account abstraction implemented in Solana?**

Solana had implemented Account Abstraction (AA) since its launch. As discussed
earlier, Solana stores all data in units called 'accounts', divided into
executable (program accounts) and non-executable (data accounts). From the
beginning, Solana supported the ability for programs to create and manage
specific accounts (i.e., directly initiate transactions). This feature,
extending account abstraction capabilities in Solana, is known as Program
Derived Addresses (PDAs). Solana programs, unlike data accounts, are
executable accounts containing executable code. With PDAs, developers can set
rules and mechanisms for transaction signatures, allowing various on-chain
actions to be autonomously authorized on behalf of a controlled account (PDA)
recognized and approved by the Solana network. Therefore, unlike Ethereum,
Solana allows direct control of another program based on a Solana program
without cumbersome layering.

### Summary

  * Solana's Account concept structures all data on the chain, with all data being based on Accounts.
  * Solana natively supports AA, enabling self-calling between programs.

EVM TO SVM

[Home](/developers/evm-to-svm)[Next: Smart Contracts](/developers/evm-to-
svm/smart-contracts)

## Start building on Solana

[![](/_next/image?url=https%3A%2F%2Fcdn.builder.io%2Fapi%2Fv1%2Fimage%2Fassets%252Fce0c7323a97a4d91bd0baa7490ec9139%252Fdfb1773873354d118d134beca2334288&w=3840&q=75)![](/_next/image?url=https%3A%2F%2Fcdn.builder.io%2Fapi%2Fv1%2Fimage%2Fassets%252Fce0c7323a97a4d91bd0baa7490ec9139%252Fdfb1773873354d118d134beca2334288&w=3840&q=75)Intro
to Solana Development](/developers/guides/getstarted/hello-world-in-your-
browser)

[![](/_next/image?url=https%3A%2F%2Fcdn.builder.io%2Fapi%2Fv1%2Fimage%2Fassets%252Fce0c7323a97a4d91bd0baa7490ec9139%252Fdfb1773873354d118d134beca2334288&w=3840&q=75)![](/_next/image?url=https%3A%2F%2Fcdn.builder.io%2Fapi%2Fv1%2Fimage%2Fassets%252Fce0c7323a97a4d91bd0baa7490ec9139%252Fdfb1773873354d118d134beca2334288&w=3840&q=75)
Intro to Solana Development](/developers/guides/getstarted/hello-world-in-
your-
browser)[![](/_next/image?url=https%3A%2F%2Fcdn.builder.io%2Fapi%2Fv1%2Fimage%2Fassets%252Fce0c7323a97a4d91bd0baa7490ec9139%252Fdfb1773873354d118d134beca2334288&w=3840&q=75)![](/_next/image?url=https%3A%2F%2Fcdn.builder.io%2Fapi%2Fv1%2Fimage%2Fassets%252Fce0c7323a97a4d91bd0baa7490ec9139%252Fdfb1773873354d118d134beca2334288&w=3840&q=75)
Solana Development
Course](https://www.soldev.app/course)[![](/_next/image?url=https%3A%2F%2Fcdn.builder.io%2Fapi%2Fv1%2Fimage%2Fassets%252Fce0c7323a97a4d91bd0baa7490ec9139%252Fdfb1773873354d118d134beca2334288&w=3840&q=75)![](/_next/image?url=https%3A%2F%2Fcdn.builder.io%2Fapi%2Fv1%2Fimage%2Fassets%252Fce0c7323a97a4d91bd0baa7490ec9139%252Fdfb1773873354d118d134beca2334288&w=3840&q=75)
Solana
Bootcamp](https://youtu.be/0P8JeL3TURU?feature=shared)[![](/_next/image?url=https%3A%2F%2Fcdn.builder.io%2Fapi%2Fv1%2Fimage%2Fassets%252Fce0c7323a97a4d91bd0baa7490ec9139%252Fdfb1773873354d118d134beca2334288&w=3840&q=75)![](/_next/image?url=https%3A%2F%2Fcdn.builder.io%2Fapi%2Fv1%2Fimage%2Fassets%252Fce0c7323a97a4d91bd0baa7490ec9139%252Fdfb1773873354d118d134beca2334288&w=3840&q=75)
More Solana Developer Tools](/developers)

![](https://cdn.builder.io/api/v1/pixel?apiKey=ce0c7323a97a4d91bd0baa7490ec9139)

Managed by

[](/)

[](/youtube)[](/twitter)[](/discord)[](/reddit)[](/github)[](/telegram)

© 2024 Solana Foundation. All rights reserved.

Solana

  * [Grants](https://solana.org/grants)
  * [Break Solana](https://break.solana.com/)
  * [Media Kit](/branding)
  * [Careers](https://jobs.solana.com/)
  * [Disclaimer](/tos)
  * [Privacy Policy](/privacy-policy)

Get Connected

  * [Ecosystem](/ecosystem)
  * [Blog](/news)
  * [Newsletter](/newsletter)

en

© 2024 Solana Foundation. All rights reserved.

