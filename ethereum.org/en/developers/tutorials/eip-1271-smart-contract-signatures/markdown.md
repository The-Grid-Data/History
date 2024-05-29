Skip to main content

[](/en/)

  * Learn
  * Use
  * Build
  * Participate
  * Research

Search```K`

Languages EN

# EIP-1271: Signing and Verifying Smart Contract Signatures

eip-1271smart contractsverifyingsigning

Intermediate

![✍️](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/270d.svg)Nathan
H. Leung

![📆](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4c6.svg)
January 12, 2023

![⏱️](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/23f1.svg)6
minute read minute read

On this page

  * What is a signature?
  * Why does EIP-1271 exist?
  * How does EIP-1271 work?
    * Interface
  * Example EIP-1271 Implementation: Safe
  * What exactly is the _hash parameter? Why not pass the whole message?
    * Previous EIP-1271 Specifications
  * How should EIP-1271 be implemented in my own contracts?
  * Conclusion

The [EIP-1271(opens in a new tab)](https://eips.ethereum.org/EIPS/eip-1271)
standard allows smart contracts to verify signatures.

In this tutorial, we give an overview of digital signatures, EIP-1271's
background, and the specific implementation of EIP-1271 used by [Safe(opens in
a new tab)](https://safe.global/) (previously Gnosis Safe). All together, this
can serve as a starting point for implementing EIP-1271 in your own contracts.

## What is a signature?

In this context, a signature (more precisely, a “digital signature”) is a
message plus some sort of proof that the message came from a specific
person/sender/address.

For instance, a digital signature might look like this:

  1. Message: “I want to log in to this website with my Ethereum wallet.”
  2. Signer: My address is `0x000…`
  3. Proof: Here is some proof that I, `0x000…`, actually created this entire message (this is usually something cryptographic).

It’s important to note that a digital signature includes both a “message” and
a “signature”.

Why? For instance, if you gave me a contract to sign, and then I cut off the
signature page and gave you back only my signatures without the rest of the
contract, the contract would not be valid.

In the same way, a digital signature doesn’t mean anything without an
associated message!

## Why does EIP-1271 exist?

In order to create a digital signature for use on Ethereum-based blockchains,
you generally need a secret private key which no one else knows. This is what
makes your signature, yours (no one else can create the same signature without
knowledge of the secret key).

Your Ethereum account (i.e. your externally-owned account/EOA) has a private
key associated with it, and this is the private key that’s typically used when
a website or dapp asks you for a signature (e.g. for “Log in with Ethereum”).

An app can [verify a signature(opens in a new
tab)](https://docs.alchemy.com/docs/how-to-verify-a-message-signature-on-
ethereum) you create using a third-party library like ethers.js [without
knowing your private key(opens in a new
tab)](https://en.wikipedia.org/wiki/Public-key_cryptography) and be confident
that _you_ were the one that created the signature.

> In fact, because EOA digital signatures use public-key cryptography, they
> can be generated and verified **off-chain**! This is how gasless DAO voting
> works — instead of submitting votes on-chain, digital signatures can be
> created and verified off-chain using cryptographic libraries.

While EOA accounts have a private key, smart contract accounts do not have any
sort of private or secret key (so "Log in with Ethereum", etc. cannot natively
work with smart contract accounts).

The problem EIP-1271 aims to solve: how can we tell that a smart contract
signature is valid if the smart contract has no “secret” it can incorporate
into the signature?

## How does EIP-1271 work?

Smart contracts don’t have private keys that can be used to sign messages. So
how can we tell if a signature is authentic?

Well, one idea is that we can just _ask_ the smart contract if a signature is
authentic!

What EIP-1271 does is it standardizes this idea “asking” a smart contract if a
given signature is valid.

A contract that implements EIP-1271 must have a function called
`isValidSignature` which takes in a message and a signature. The contract can
then run some validation logic (the spec does not enforce anything specific
here) and then return a value indicating whether the signature is valid or
not.

If `isValidSignature` returns a valid result, that’s pretty much the contract
saying “yes, I approve this signature + message!”

### Interface

Here’s the exact interface in the EIP-1271 spec (we’ll talk about the `_hash`
parameter below, but for now, think of it as the message that is being
verified):

    
    
    1pragma solidity ^0.5.0;
    
    2
    
    3contract ERC1271 {
    
    4
    
    5  // bytes4(keccak256("isValidSignature(bytes32,bytes)")
    
    6  bytes4 constant internal MAGICVALUE = 0x1626ba7e;
    
    7
    
    8  /**
    
    9   * @dev Should return whether the signature provided is valid for the provided hash
    
    10   * @param _hash      Hash of the data to be signed
    
    11   * @param _signature Signature byte array associated with _hash
    
    12   *
    
    13   * MUST return the bytes4 magic value 0x1626ba7e when function passes.
    
    14   * MUST NOT modify state (using STATICCALL for solc < 0.5, view modifier for solc > 0.5)
    
    15   * MUST allow external calls
    
    16   */
    
    17  function isValidSignature(
    
    18    bytes32 _hash,
    
    19    bytes memory _signature)
    
    20    public
    
    21    view
    
    22    returns (bytes4 magicValue);
    
    23}
    
    Show all

## Example EIP-1271 Implementation: Safe

Contracts can implement `isValidSignature` in many ways — the spec only
doesn’t say much about the exact implementation.

One notable contract which implements EIP-1271 is Safe (previously Gnosis
Safe).

In Safe’s code, `isValidSignature` [is implemented(opens in a new
tab)](https://github.com/safe-global/safe-
contracts/blob/main/contracts/handler/CompatibilityFallbackHandler.sol) so
that signatures can be created and verified in [two ways(opens in a new
tab)](https://ethereum.stackexchange.com/questions/122635/signing-messages-as-
a-gnosis-safe-eip1271-support):

  1. On-chain messages
    1. Creation: a safe owner creates a new safe transaction to “sign” a message, passing the message as data into the transaction. Once enough owners sign the transaction to reach the multisig threshold, the transaction is broadcast and run. In the transaction, there is a safe function called which adds the message to a list of “approved” messages.
    2. Verification: call `isValidSignature` on the Safe contract, and pass in the message to verify as the message parameter and [an empty value for the signature parameter(opens in a new tab)](https://github.com/safe-global/safe-contracts/blob/main/contracts/handler/CompatibilityFallbackHandler.sol#L32) (i.e. `0x`). The Safe will see that the signature parameter is empty and instead of cryptographically verifying the signature, it will know to just go ahead and check whether the message is on the list of “approved” messages.
  2. Off-chain messages:
    1. Creation: a safe owner creates a message off-chain, then gets other safe owners to sign the message each individually until there are enough signatures to overcome the multisig approval threshold.
    2. Verification: call `isValidSignature`. In the message parameter, pass in the message to be verified. In the signature parameter, pass in each safe owner’s individual signatures all concatenated together, back-to-back. The Safe will check that there are enough signatures to meet the threshold **and** that each signature is valid. If so, it will return a value indicating successful signature verification.

## What exactly is the `_hash` parameter? Why not pass the whole message?

You might have noticed that the `isValidSignature` function in the [EIP-1271
interface(opens in a new tab)](https://eips.ethereum.org/EIPS/eip-1271)
doesn’t take in the message itself, but instead a `_hash` parameter. What this
means is that instead of passing the full arbitrary-length message to
`isValidSignature`, we instead pass a 32-byte hash of the message (generally
keccak256).

Each byte of calldata — i.e. function parameter data passed to a smart
contract function — [costs 16 gas (4 gas if zero byte)(opens in a new
tab)](https://eips.ethereum.org/EIPS/eip-2028), so this can save a lot of gas
if a message is long.

### Previous EIP-1271 Specifications

There are EIP-1271 specifications in the wild that have an `isValidSignature`
function with a first parameter of type `bytes` (arbitrary-length, instead of
a fixed-length `bytes32`) and parameter name `message`. This is an [older
version(opens in a new tab)](https://github.com/safe-global/safe-
contracts/issues/391#issuecomment-1075427206) of the EIP-1271 standard.

## How should EIP-1271 be implemented in my own contracts?

The spec is very open-ended here. The Safe implementation has some good ideas:

  * You can consider EOA signatures from the "owner" of the contract to be valid.
  * You could store a list of approved messages and only consider those to be valid.

In the end, it is up to you as the contract developer!

## Conclusion

[EIP-1271(opens in a new tab)](https://eips.ethereum.org/EIPS/eip-1271) is a
versatile standard that allows smart contracts to verify signatures. It opens
the door for smart contracts to act more like EOAs — for instance providing a
way for "Log in with Ethereum" to work with smart contracts — and it can be
implemented in many ways (Safe having a nontrivial, interesting implementation
to consider).

n

Last edit: [@nhsz(opens in a new tab)](https://github.com/nhsz), August 15,
2023

See contributors

### Was this tutorial helpful?

YesNo

  * [Edit page(opens in a new tab)](https://github.com/ethereum/ethereum-org-website/tree/dev/public/content/developers/tutorials/eip-1271-smart-contract-signatures/index.md)
  * On this page

    * What is a signature?
    * Why does EIP-1271 exist?
    * How does EIP-1271 work?
      * Interface
    * Example EIP-1271 Implementation: Safe
    * What exactly is the _hash parameter? Why not pass the whole message?
      * Previous EIP-1271 Specifications
    * How should EIP-1271 be implemented in my own contracts?
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

