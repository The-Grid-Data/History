Skip to main content

[](/en/)

  * Learn
  * Use
  * Build
  * Participate
  * Research

Search```K`

Languages EN

  1. [Home](/en/)/
  2. [glossary](/en/glossary/)

Page last updated: March 1, 2024

On this page

  * #
  * A
  * B
  * C
  * D
  * E
  * F
  * G
  * H
  * I
  * K
  * L
  * M
  * N
  * O
  * P
  * R
  * S
  * T
  * V
  * W
  * Z
  * Sources
  * Contribute to this page

# Glossary

## #

### 51% attack

A type of attack where a group gains control of the majority of
[nodes](/en/glossary/#node). This would allow them to defraud the blockchain
by reversing [transactions](/en/glossary/#transaction) and double spending
[ether](/en/eth/) and other tokens.  
  
In Ethereum proof-of-stake this would be achieved by accumulating more than
half of the total staked ether. This would allow an attacker to decide which
new blocks are added to the blockchain. However, to revert the chain or
double-spend an attacker would require at least 66% of the total staked ether.

## A

### Account

An Ethereum account is a digital identity on the Ethereum blockchain, allowing
users to send, receive Ether, and interact with smart contracts.  
  
**Technical:**  
Its an object containing an address, balance, nonce, and optional storage and
code. An account can be a contract account or an externally owned account
(EOA).

### Address

An Ethereum address is a unique identifier used for receiving tokens,
functions similar to a bank account number for cryptocurrencies. Its used to
identify your Ethereum account.  
  
It is the rightmost 160 bits of a Keccak hash of an ECDSA public key.

### Application Binary Interface (ABI)

A JSON file that defines the functions and variables included in a smart
contract. The ABI allows bytecode to be mapped into human-readable formats.

### Anti-Sybil

Are ways to stop people from pretending to be many users at once on the
internet, ensuring each user is a real, separate person. This helps keep
online interactions fair and honest.

### Application Programming Interface (API)

An Application Programming Interface (API) is a set of definitions for how to
use a piece of software. An API sits between an application and a web server,
and facilitates the transfer of data between them.

### APR

APR, or Annual Percentage Rate, reflects the yearly cost of borrowing money,
including interest and fees, as a percentage.

### ASIC

Application-specific integrated circuit. This usually refers to an integrated
circuit, custom-built for cryptocurrency mining.

### assert

In [Solidity](/en/glossary/#solidity), `assert(false)` compiles to `0xfe`, an
invalid opcode, which uses up all remaining [gas](/en/glossary/#gas) and
reverts all changes. When an `assert()` statement fails, something very wrong
and unexpected is happening, and you will need to fix your code. You should
use `assert()` to avoid conditions that should never, ever occur. [More on
smart contract security](/en/developers/docs/smart-contracts/security/).

### Attestation

A claim made by an entity that something is true. In context of Ethereum,
consensus validators must make a claim as to what they believe the state of
the chain to be. At designated times, each validator is responsible for
publishing different attestations that formally declare this validator's view
of the chain, including the last finalized checkpoint and the current head of
the chain. [More on attestations](/en/developers/docs/consensus-
mechanisms/pos/attestations/).

## B

### Base fee

Every [block](/en/glossary/#block) has a reserve price known as the 'base
fee'. It is the minimum [gas](/en/glossary/#gas) fee a user must pay to
include a transaction in the next block. [More on gas and
fees](/en/developers/docs/gas/).

### Beacon chain

The Beacon Chain was the blockchain that introduced [proof-of-
stake](/en/glossary/#pos) and [validators](/en/glossary/#validator) to
Ethereum. It ran alongside the proof-of-work Ethereum Mainnet from December
2020 until the two chains were merged in September 2022 to form the Ethereum
of today. [More on beacon chain](/en/roadmap/beacon-chain/).

### Big-endian

A positional number representation where the most significant digit is first
in memory. The opposite of little-endian, where the least significant digit is
first.

### Block

A block is where transactions or digital actions are stored. Once a block is
full, it gets linked to the previous one, creating a chain of blocks or a
"blockchain". [More on blocks](/en/developers/docs/blocks/).  
  
A block is a bundled unit of information that includes an ordered list of
transactions and consensus-related information. Blocks are proposed by proof-
of-stake validators, at which point they are shared across the entire peer-to-
peer network, where they can easily be independently verified by all other
nodes. Consensus rules govern what contents of a block are considered valid,
and any invalid blocks are disregarded by the network. The ordering of these
blocks and the transactions therein create a deterministic chain of events
with the end representing the current state of the network.

### Block explorer

An interface that allows a user to search for information from, and about, a
blockchain. This includes retrieving individual transactions, activity
associated with specific addresses and information about the network.

### Block header

The block header is a collection of metadata about a block and a summary of
the transactions included in the execution payload.

### Block propagation

The process of transmitting a confirmed block to all other nodes in the
network.

### Block proposer

The specific validator chosen to create a block in a particular
[slot](/en/glossary/#slot).

### Block reward

The amount of ether rewarded to the proposer of a new valid block.

### Block status

The states that a block can exist in. The possible states include:  
  

  * proposed: the block was proposed by a validator
  * scheduled: validators are currently submitting data
  * missed/skipped: the proposer did not propose a block within the eligible time frame
  * orphaned: the block was reorg'd out by the [fork choice algorithm](/en/glossary/#fork-choice-algorithm)

### Block time

The time interval between blocks being added to the blockchain.

### Block validation

The process of checking that a new block contains valid transactions and
signatures, builds on the heaviest historical chain (meaning the one that has
accumulated the most attestations in its history), and follows all other
consensus rules. Valid blocks are added to the head of the chain and
propagated to others on the network. Invalid blocks are disregarded.

### Blockchain

A blockchain is a database of transactions, duplicated and shared on all
computers in the network, ensuring data cannot be altered retroactively.  
  
A sequence of [block](/en/glossary/#block) , each linking to its predecessor
all the way to the [genesis block](/en/glossary/#genesis-block) by referencing
the hash of the previous block. The integrity of the blockchain is crypto-
economically secured using a proof-of-stake-based consensus mechanism. [What
is a blockchain?](/en/developers/docs/intro-to-ethereum/#what-is-a-blockchain)

### Bootnode

The nodes which can be used to initiate the discovery process when running a
node. Bootnodes 'introduce' new nodes to other existing nodes so that they can
quickly gain peers, rather than having to search for an initial peer. The
endpoints of these nodes are usually provided in Ethereum client source code,
but users can provide their own list of bootnodes.

### Bridge

A blockchain bridge is used to transfer assets from one blockchain network to
another. For example you can use bridge to transfer ETH from the main Ethereum
network to cheaper Layer 2 scaling solutions.

### Bytecode

Code expressed in a compact, numeric form so that it can be executed
efficiently by the [EVM](/en/glossary/#evm).

### Byzantium fork

The first of two [hard forks](/en/glossary/#hard-fork) for the
[Metropolis](/en/glossary/#metropolis) development stage. It included EIP-649
Metropolis [Difficulty Bomb](/en/glossary/#difficulty-bomb) Delay and Block
Reward Reduction, where the [Ice Age](/en/glossary/#ice-age) was delayed by 1
year and the block reward was reduced from 5 to 3 ether.

## C

### Casper FFG

Casper-FFG is a proof-of-stake consensus protocol used in conjunction with the
[LMD-GHOST](/en/glossary/#lmd-ghost) fork choice algorithm to allow [consensus
clients](/en/glossary/#consensus-client) to agree on the head of the Beacon
Chain.

### Checkpoint

The [Beacon Chain](/en/glossary/#beacon-chain) has a tempo divided into slots
(12 seconds) and epochs (32 slots). The first slot in each epoch is a
checkpoint. When a [supermajority](/en/glossary/#supermajority) of validators
attests to the link between two checkpoints, they can be
[justified](/en/glossary/#justification) and then when another checkpoint is
justified on top, they can be [finalized](/en/glossary/#finality).

### Compiling

Converting code written in a high-level programming language (e.g.,
[Solidity](/en/glossary/#solidity)) into a lower-level language (e.g., EVM
[bytecode](/en/glossary/#bytecode)).[More on compiling smart
contracts](/en/developers/docs/smart-contracts/compiling/)

### Committee

A group of at least 128 [validators](/en/glossary/#validator) assigned to
validate blocks in each slot. One of the validators in the committee is the
aggregator, responsible for aggregating the signatures of all other validators
in the committee that agree on an attestation. Not to be confused with [sync
committee](/en/glossary/#sync-committee).

### Computational infeasibility

A process is computationally infeasible if it would take an impracticably long
time (e.g. billions of years) to do it for anyone who might conceivably have
an interest in carrying it out.

### Consensus

When more than 2/3 of the computers in a network agree that they have the same
set of records, making sure everyone is on the same page. This isn't about the
rules they follow, but making sure they all have the same information.

### Consensus client

Consensus clients (such as Prysm, Teku, Nimbus, Lighthouse, Lodestar) run
Ethereum's [proof-of-stake](/en/glossary/#pos) consensus algorithm allowing
the network to reach agreement about the head of the Beacon Chain. Consensus
clients do not participate in validating/broadcasting transactions or
executing state transitions. This is done by [execution
clients](/en/glossary/#execution-client). Consensus clients do not attest to,
or propose new blocks. This is done by the [validator
client](/en/glossary/#validator) which is an optional add-on to the consensus
client.

### Consensus layer

Ethereum's consensus layer is the network of [consensus
clients](/en/glossary/#consensus-client).

### Consensus rules

The block validation rules that full nodes follow to stay in consensus with
other nodes. Not to be confused with [consensus](/en/glossary/#consensus).

### Constantinople fork

The second part of the [Metropolis](/en/glossary/#metropolis) stage,
originally planned for mid-2018. Expected to include a switch to a hybrid
[proof-of-work](/en/glossary/#pow)/[proof-of-stake](/en/glossary/#pow)
consensus algorithm, among other changes.

### Contract account

An account containing code that executes whenever it receives a
[transaction](/en/glossary/#transaction) from another
[account](/en/glossary/#account) ([EOA]](/en/glossary/#eoa) or
[contract](/en/glossary/#contract-account)).

### Contract creation transaction

A special [transaction](/en/glossary/#transaction) that includes a contract's
initiation code. The recipient is set to `null` and the contract is deployed
to an address generated from the user address and `nonce`. that is used to
register a [contract](/en/glossary/#contract-account) and record it on the
Ethereum blockchain.

### Cryptography

It is the practice of securing communication and data through the use of
codes, so that only those for whom the information is intended can read and
process it.  
It involves techniques for encryption (converting readable information into an
unreadable format) and decryption (converting it back into a readable format),
ensuring confidentiality.

### Cryptoeconomics

The study of mathematical and economic principles to design secure and
trustworthy digital platforms. The goal is to ensure that all participants
follow the rules and are rewarded for contributing to the network's security
and operation.

## D

### Đ

Đ (D with stroke) is used in Old English, Middle English, Icelandic, and
Faroese to stand for an uppercase letter “Eth”. It is used in words like ĐEV
or Đapp (decentralized application), where the Đ is the Norse letter “eth”.
The uppercase eth (Ð) is also used to symbolize the cryptocurrency Dogecoin.
This is commonly seen in older Ethereum literature but is used less often
today.

### DAG

DAG stands for Directed Acyclic Graph. It is a data structure composed of
nodes and links between them. Before The Merge, Ethereum used a DAG in its
[proof-of-work](/en/glossary/#pow) algorithm, [Ethash](/en/glossary/#ethash),
but is no longer used in [proof-of-stake](/en/glossary/#pos).

### Dapp

A dApp is a decentralized application that runs on a blockchain network,
offering services without a central controlling authority. [More on
decentralized applications](/en/dapps/).  
At a minimum dapp has a smart contract connected to a web interface. In
addition, many dapps include decentralized storage and/or a message protocol
and platform.

### Data availability

Any node can independently verify transactions on a blockchain in order to
maintain transparency and trust in the system.

### Decentralization

The concept of moving the control and execution of processes away from a
central entity.

### Decentralized autonomous organization (DAO)

A DAO is a digital organization run by rules coded on a blockchain, where
decisions are made by member votes, not a central authority. [More on
decentralized autonomous organizations (DAOs)](/en/dao/).  
Each member's voting power often tied to the number of tokens they hold. DAOs
aim to democratize decision-making and operations, focusing on transparency
and community governance.

### Decentralized exchange (DEX)

A type of Ethereum app that lets you swap tokens with peers on the network.
DEXes are not subject to geographical restrictions like centralized exchanges
– anyone can participate.

### Deposit contract

The gateway to staking on Ethereum. The deposit contract is a smart contract
on Ethereum that accepts deposits of ETH and manages validator balances. A
validator cannot be activated without depositing ETH into this contract. The
contract requires ETH and input data. This input data includes the validator
public key and withdrawal public key, signed by the validator private key.
This data is needed for a validator to be identified and approved by the
[proof-of-stake](/en/glossary/#pos) network.

### DeFi

A broad category of Ethereum apps aiming to provide financial services backed
by the blockchain, without any intermediaries. [More on decentralized finance
(DeFi)](/en/defi/)

### Difficulty

A network-wide setting in [proof-of-work](/en/glossary/#pow) networks that
controls how much average computation is required to find a valid nonce. The
difficulty is represented by the number of leading zeroes that are required in
the resulting block hash for it to be considered valid. This concept is
deprecated in Ethereum since the transition to proof-of-stake.

### Difficulty bomb

Planned exponential increase in [proof-of-work](/en/glossary/#pow)
[difficulty](/en/glossary/#difficulty) setting that was designed to motivate
the transition to [proof-of-stake](/en/glossary/#pos), reducing the chances of
a [fork](/en/glossary/#hard-fork). The difficulty bomb was deprecated with
[the Merge](/en/roadmap/merge/).

### Digital signature

A short string of data a user produces for a document using a [private
key](/en/glossary/#private-key) such that anyone with the corresponding
[public key](/en/glossary/#public-key), the signature, and the document can
verify that (1) the document was "signed" by the owner of that particular
private key, and (2) the document was not changed after it was signed.

### Discovery

The process by which an Ethereum node finds other nodes to connect to.

### Distributed hash table (DHT)

A data structure containing `(key, value)` pairs used by Ethereum nodes to
identify peers to connect to and determine which protocols to use to
communicate.

### Double spend

A deliberate blockchain fork, where a user with a sufficiently large amount of
mining power/stake sends a transaction moving some currency off-chain (e.g.
exiting into fiat money or making an off-chain purchase) then reorganizing the
blockchain to remove that transaction. A successful double spend leaves the
attacker with both their on and off-chain assets.

## E

### Elliptic Curve Digital Signature Algorithm (ECDSA)

A cryptographic algorithm used by Ethereum to ensure that funds can only be
spent by their owners. It's the preferred method for creating public and
private keys. Relevant for account [address](/en/glossary/#address) generation
and [transaction](/en/glossary/#transaction) verification.

### Encryption

Encryption is the conversion of electronic data into a form unreadable by
anyone except the owner of the correct decryption key.

### Entropy

In the context of cryptography, lack of predictability or level of randomness.
When generating secret information, such as [private
keys](/en/glossary/#private-key), algorithms usually rely on a source of high
entropy to ensure the output is unpredictable.

### Epoch

A period of 32 [slots](/en/glossary/#slot), each slot being 12 seconds,
totalling 6.4 minutes. Validator [committees](/en/glossary/#committee) are
shuffled every epoch for security reasons. Each epoch has an opportunity for
the chain to be [finalized](/en/glossary/#finality). Each validator is
assigned new responsibilities at the start of each epoch. [More on proof-of-
stake](/en/developers/docs/consensus-mechanisms/pos/#how-does-validation-work)

### Equivocation

A validator sending two messages that contradict each other. One simple
example is a transaction sender sending two transactions with the same nonce.
Another is a block proposer proposing two blocks at the same block height (or
for the same slot).

### Eth1

'Eth1' is a term that referred to Mainnet Ethereum, the existing proof-of-work
blockchain. This term has since been deprecated in favor of the 'execution
layer'. [Learn more about this name change(opens in a new
tab)](https://blog.ethereum.org/2022/01/24/the-great-eth2-renaming/).

### Eth2

'Eth2' is a term that referred to a set of Ethereum protocol upgrades,
including Ethereum's transition to proof-of-stake. This term has since been
deprecated in favor of the 'consensus layer'. [Learn more about this name
change(opens in a new tab)](https://blog.ethereum.org/2022/01/24/the-great-
eth2-renaming/).

### Ethereum Improvement Proposal (EIP)

A design document providing information to the Ethereum community, describing
a proposed new feature or its processes or environment (see
[ERC](/en/glossary/#erc)). [Introduction to EIPs](/en/eips/)

### Ethereum Name Service (ENS)

Ethereum Name Service is like an internet phonebook for Ethereum addresses.
Instead of using long wallet addresses, ENS lets you use simple names like
"john.eth" to send and receive digital money and assets.  
  
**Technical:**  
The ENS registry is a single central [contract](/en/glossary/#smart-contract)
that provides a mapping from domain names to owners and resolvers, as
described in EIP-137. [Read more at ens.domains(opens in a new
tab)](https://ens.domains).

### Execution client

Execution clients (formerly known as "Eth1 clients"), such as Besu, Erigon,
Go-Ethereum (Geth), Nethermind, are tasked with processing and broadcasting
transactions and managing Ethereum's state. They run the computations for each
transaction using the [Ethereum Virtual Machine](/en/glossary/#evm) to ensure
that the rules of the protocol are followed.

### Execution layer

Ethereum's execution layer is the network of [execution
clients](/en/glossary/#execution-client).

### Externally owned account (EOA)

Externally Owned Accounts (EOAs) are the most common type of Ethereum account.
They are controlled by a person through private keys/recovery phrase. [More on
Ethereum wallets](/en/wallets/).

### Ethereum Request for Comments (ERC)

ERC (**Ethereum Request for Comments**) is a type of technical documentation
used in the Ethereum community to propose new standards of usage for the
Ethereum network.  
  
These proposals can cover a wide range of topics, including new token
standards (like ERC-20 used for tokens and ERC-721 for NFTs).

### ERC-20

ERC-20 is the standard that most tokens on Ethereum network use for their
creation.  
Popular examples are stablecoins like DAI and USDC or exchange tokens like UNI
from Uniswap. Akin to any form of alternative moneys that we have in
traditional systems… ie. rewards points, credit systems, or even stocks, etc.

### ERC-721

NFTs (non fungible tokens) are created using a standard set of rules referred
to as ERC-721.  
NFT tokens can represent ownership of anything unique, like digital art or
collectibles, with each token having its own special characteristics and
value. Each NFT is unique and easily distinguishable from any other NTF.

### ERC-1155

ERC-1155 is a newer type of Ethereum token standard similar to NFT (like
unique collectible items) that also allows to create interchangeable items
(like currency) within a single smart contract.  
This makes it easier and more efficient to manage various types of digital
assets, especially for applications like video games or digital collections.

### Ethash

A [proof-of-work](/en/glossary/#pow) algorithm that was used on Ethereum
before it transitioned to [proof-of-stake](/en/glossary/#pos). [Read
more](/en/developers/docs/consensus-mechanisms/pow/mining/mining-
algorithms/ethash/)

### Ether

The native cryptocurrency of Ethereum, commonly referred to as “ETH”. It is
used to cover transaction fees when using Ethereum ecosystem and applications.
[More on ether](/en/eth/).

### Events

Allows the use of [EVM](/en/glossary/#evm) logging facilities.
[Dapps](/en/glossary/#dapp) can listen for events and use them to trigger
JavaScript callbacks in the user interface. [More on events and
logs](/en/developers/docs/smart-contracts/anatomy/#events-and-logs)

### Ethereum Virtual Machine (EVM)

A stack-based virtual machine that executes
[bytecode](/en/glossary/#bytecode). In Ethereum, the execution model specifies
how the system state is altered given a series of bytecode instructions and a
small tuple of environmental data. This is specified through a formal model of
a virtual state machine. [More on Ethereum Virtual
Machine](/en/developers/docs/evm/).

### EVM assembly language

A human-readable form of EVM [bytecode.](/en/glossary/#bytecode)

## F

### Fallback function

A default function called in the absence of data or a declared function name.

### Faucet

A service carried out via [smart contract](/en/glossary/#smart-contract) that
dispenses funds in the form of free test ether that can be used on a testnet.

### Finality

Finality is the guarantee that a set of transactions cannot be changed without
a huge amount of ETH being lost.

### Finney

A denomination of [ether](/en/glossary/#ether). 1 finney = 1015
[wei](/en/glossary/#wei). 103 finney = 1 ether.

### Fork

A change in protocol causing the creation of an alternative chain.

### Fork choice algorithm

The algorithm used to identify the head of the blockchain. On Ethereum the
head of the chain is identified as the fork with the greatest 'weight' of
attestations. The weight is the product of the number of attestations and the
effective balance of the attesting validators. This means the true head of the
chain is the one that most staked ether has voted for. On the consensus layer
the fork choice algorithm is called [LMD_GHOST](/en/glossary/#lmd-ghost).

### Fraud proof

A security model for certain [layer 2](/en/glossary/#layer-2) solutions where,
to increase speed, transactions are [rolled up](/en/glossary/#rollups) into
batches and submitted to Ethereum in a single transaction. Other network
participants can re-execute the transactions to check that they were executed
honestly. If they uncover a discrepancy between the posted data and their own
version they can post a cryptographic proof that demonstrates where some fraud
took place. Some [rollups](/en/glossary/#rollups) use [validity
proofs](/en/glossary/#validity-proof).

### Frontier

The initial test development stage of Ethereum, which lasted from July 2015 to
March 2016.

## G

### Gas

Gas is the fee paid for transactions and smart contracts on a blockchain, like
Ethereum. [More on gas and fees](/en/gas/).

### Gas limit

The maximum amount of [gas](/en/glossary/#gas) a
[transaction](/en/glossary/#transaction) or [block](/en/glossary/#block) may
consume.

### Gas price

Price in ether of one unit of gas specified in a transaction.

### Genesis block

The first block in a [blockchain](/en/glossary/#blockchain), used to
initialize a particular network and its cryptocurrency.

### Geth

Go Ethereum. One of the most prominent implementations of the Ethereum
protocol, written in Go. [Read more at geth.ethereum.org(opens in a new
tab)](https://geth.ethereum.org)

### Gwei

Short for gigawei, a denomination of [ether](/en/glossary/#ether), commonly
utilized to price [gas](/en/glossary/#gas). 1 gwei = 109
[wei](/en/glossary/#wei). 109 gwei = 1 ether.

## H

### Hard fork

A permanent divergence in the [blockchain](/en/glossary/#blockchain); also
known as a hard-forking change. One commonly occurs when nonupgraded nodes
can't validate blocks created by upgraded nodes that follow newer [consensus
rules](/en/glossary/#consensus-rules). Not to be confused with a fork, soft
fork, software fork, or Git fork.

### Hash

A fixed-length fingerprint of variable-size input, produced by a hash
function. (See [keccak-256](/en/glossary/#keccak-256)).

### Hash rate

The number of hash calculations made per second by computers running mining
software.

### Holographic consensus

Refers to how a big group decision is made by letting a smaller group of
representative people vote. Then everyone else agrees to go along with it, as
long as they trust the small group did a good job.  
It's used in some online communities to make decisions quickly without needing
everyone to vote on everything, while still making sure the decisions are fair
and represent what most people want.

### Homestead

The second development stage of Ethereum, launched in March 2016 at block
1,150,000.

## I

### Index

A network structure meant to optimize the querying of information from across
the [blockchain](/en/glossary/#blockchain) by providing an efficient path to
its storage source.

### Integrated development environment (IDE)

A user interface that typically combines a code editor, compiler, runtime, and
debugger. [More on integrated development
environments](/en/developers/docs/ides/).

### Immutable deployed code problem

Once a [contract's](/en/glossary/#smart-contract) (or library's) code is
deployed, it becomes immutable. Standard software development practices rely
on being able to fix possible bugs and add new features, so this represents a
challenge for smart contract development. [More on deploying smart
contracts](/en/developers/docs/smart-contracts/deploying/).

### Internal transaction

A [transaction](/en/glossary/#transaction) sent from a [contract
account](/en/glossary/#contract-account) to another contract account or an
[EOA](/en/glossary/#eoa) (see [message](/en/glossary/#message)).

### Issuance

The minting of new ether to reward block proposal, attestation and whistle-
blowing.

## K

### Key derivation function (KDF)

Also known as a "password stretching algorithm," it is used by
[keystore](/en/glossary/#keystore) formats to protect against brute-force,
dictionary, and rainbow table attacks on passphrase encryption, by repeatedly
hashing the passphrase.

### Key

In the context of Ethereum, keys are digital codes: a public key for receiving
transactions and a private key for accessing and sending funds.  
Public keys: These can be shared openly.  
Private keys: These are kept secret by the owner.

### Keystore

Every account’s private key/address pair exists as a single keyfile in an
Ethereum client. These are JSON text files which contains the encrypted
private key of the account, which can only be decrypted with the password
entered during account creation.

### Keccak-256

Cryptographic [hash](/en/glossary/#hash) function used in Ethereum. Keccak-256
was standardized as [SHA](/en/glossary/#sha)-3.

## L

### Layer 1

Layer 1 refers to the main blockchain in a multi-level blockchain network. For
example, Ethereum and Bitcoin are layer one blockchains. Many layer two
blockchain offload resource-intense transactions to their separate blockchain,
while continuing to use Ethereum's or Bitcoin's layer one blockchain for
security purposes.

### Layer 2

Layer 2s are another networks built on top of Ethereum main network to make
transactions faster and cheaper. [More on layer 2](/en/layer-2/).

### Library

A special type of [contract](/en/glossary/#smart-contract) that has no payable
functions, no fallback function, and no data storage. Therefore, it cannot
receive or hold ether, or store data. A library serves as previously deployed
code that other contracts can call for read-only computation. [More on smart
contract libraries](/en/developers/docs/smart-contracts/libraries/).

### Light client

An Ethereum client that does not store a local copy of the
[blockchain](/en/glossary/#blockchain), or validate blocks and
[transactions](/en/glossary/#transaction). It offers the functions of a
[wallet](/en/glossary/#wallet) and can create and broadcast transactions.

### Liquidity

Liquidity is how quickly and easily an asset can be converted into cash or
another asset. Decentralized exchanges like Uniswap have multiple liquidity
pools where asset holders can deposit their assets where traders can buy and
sell them in a decentralized way in exchange for rewards.

### Liquidity tokens

Liquidity tokens (LST) are digital tokens issued to participants who deposit
assets into a liquidity pool, which is a collection of funds locked in a smart
contract and used to facilitate trading on a decentralized exchange (DEX).  
These tokens represent the participant's share of the pool and can be redeemed
later for the initial deposit plus a portion of the trading fees generated by
the pool's activity. Essentially, liquidity tokens serve as a proof of
ownership or stake in a liquidity pool, allowing holders to earn rewards while
providing the necessary liquidity for others to trade different cryptocurrency
pairs efficiently.

### LMD-GHOST

The [fork-choice algorithm](/en/glossary/#fork-choice-algorithm) used by
Ethereum's consensus clients to identify the head of the chain. LMD-GHOST is
an acronym standing for "Latest Message Driven Greediest Heaviest Observed
SubTree" which means that the head of the chain is the block with the greatest
accumulation of [attestations](/en/glossary/#attestation) in its history.

## M

### Mainnet

Short for "main network," this is the main public Ethereum
[blockchain](/en/glossary/#blockchain).

### Max Fee Per Gas

The Max Fee is the absolute maximum amount a user is willing to pay per unit
of gas ([gwei](/en/glossary/#gwei)) to get a transaction included in a block.

### Merkle Patricia Tree (MPT)

A data structure used in Ethereum to efficiently store key-value pairs.

### Merkle Root

A Merkle root is the single top hash of a Merkle tree. It verifies all
transactions within a block.

### Message

An [internal transaction](/en/glossary/#internal-transaction) that is never
serialized and only sent within the [EVM.](/en/glossary/#evm)

### Message call

The act of passing a [message](/en/glossary/#message) from one account to
another. If the destination account is associated with
[EVM](/en/glossary/#evm) code, then the VM will be started with the state of
that object and the message acted upon.

### Mining

The process of repeatedly hashing a block header while incrementing a
[nonce](/en/glossary/#nonce) until the result contains an arbitrary number of
leading binary zeros. This is the process by which new
[blocks](/en/glossary/#block) are added to a proof-of-work blockchain. This
was how Ethereum was secured before it moved to proof-of-stake.

### Miner

A network [node](/en/glossary/#node) that finds valid [proof-of-
work](/en/glossary/#pow) for new blocks, by repeated pass hashing (see
[Ethash](/en/glossary/#ethash)). Miners are no longer part of Ethereum - they
were replaced by validators when Ethereum moved to proof-of-stake.

### Mint

Minting is the process of creating new tokens and bringing them into
circulation so that they can be used. It's a decentralized mechanism to create
a new token without the involvement of the central authority.

### Multisig

Multisig (multi signature) refers to a digital wallet or account that requires
multiple signatures or approvals to execute transactions, enhancing security.  
This adds extra security compared to traditional single-signature accounts
where only one person's approval is needed.

## N

### Network

Referring to the Ethereum network, a peer-to-peer network that propagates
transactions and blocks to every Ethereum node (network participant). [More on
networks](/en/developers/docs/networks/).

### Network hashrate

The collective hashrate produced by an entire mining network. Mining on
Ethereum was switched off when Ethereum moved to proof-of-stake.

### Non-fungible token (NFT)

Non-fungible-token (NFT ) is a unique digital item you can own, like art or
collectibles, verified by blockchain technology. [More on Non-Fungible Tokens
(NFTs)](/en/nft/).

### Node

A software client that participates in the network. [More on nodes and
clients](/en/developers/docs/nodes-and-clients/).

### Nonce

In cryptography, a value that can only be used once. An account nonce is a
transaction counter in each account, which is used to prevent replay attacks.

## O

### Off-Chain

Off-chain means any transaction or data that exists outside the blockchain.
Because committing every transaction on-chain can be expensive and
inefficient, third-party tools like oracles that handle pricing data, or layer
2 solutions that execute a higher throughput of transactions, handle a bulk of
the processing work off-chain, and will submit information on-chain at less
frequent intervals.

### Ommer (uncle) block

When a proof-of-work [miner](/en/glossary/#miner) finds a valid
[block](/en/glossary/#block), another miner may have published a competing
block which is added to the tip of the blockchain first. This valid, but
stale, block can be included by newer blocks as _ommers_ and receive a partial
block reward. The term "ommer" is the preferred gender-neutral term for the
sibling of a parent block, but this is also sometimes referred to as an
"uncle". This was common for Ethereum when it was a [proof-of-
work](/en/glossary/#pow) network. Now that Ethereum uses [proof-of-
stake](/en/glossary/#pos), only one block proposer is selected per slot.

### On-Chain

Refers to actions or transactions that happen on the blockchain and are
publicly available.  
  
Think of it as writing something in a big, shared notebook that everyone can
see and check, making sure that whatever is written (like sending digital
money or making a contract) is permanent and can't be changed or erased.

### Optimistic rollup

Optimistic Rollup is a Layer 2 solution that speeds up transactions on
Ethereum, assuming they're valid by default unless challenged. [More on
Optimistic rollups](/en/developers/docs/scaling/optimistic-rollups/).

### Oracle

An oracle is a bridge between the [blockchain](/en/glossary/#blockchain) and
the real world. They act as on-chain [APIs](/en/glossary/#api) that can be
queried for information and used in [smart contracts](/en/glossary/#smart-
contract). [More on oracles](/en/developers/docs/oracles/)

## P

### Peer

Connected computers running Ethereum client software that have identical
copies of the [blockchain](/en/glossary/#blockchain).

### Peer-to-peer network

A network of computers ([peers](/en/glossary/#peer)) that are collectively
able to perform functionalities without the need for centralized, server-based
services.  
This setup is often used for sharing files (I.e. Bit torrent), information, or
digital currencies, allowing for more direct and potentially more efficient
exchanges between users.

### Permissionless

Permissionless means anyone can join and use a system like Ethereum. It's open
for everyone to participate and doesn't require any approval.

### Plasma

An off-chain scaling solution that uses [fraud proofs](/en/glossary/#fraud-
proof), like [optimistic rollups](/en/glossary/#optimistic-rollup). Plasma is
limited to simple transactions like basic token transfers and swaps. [More on
plasma](/en/developers/docs/scaling/plasma/).

### Private key

A private key is a secret code that proves you own your digital money and lets
you spend it, like a PIN for your account. **DO NOT SHARE IT**.

### Private chain

A fully private blockchain is one with permissioned access, not publicly
available for use.

### POAP

Proof of Attendance Protocol is used to create a digital collectible (NFT)
that proves you attended a specific event or activity.

### Proof-of-stake (PoS)

A method by which a cryptocurrency blockchain protocol aims to achieve
distributed [consensus](/en/glossary/#consensus). PoS asks users to prove
ownership of a certain amount of cryptocurrency (their "stake" in the network)
in order to be able to participate in the validation of transactions. [More on
proof-of-stake](/en/developers/docs/consensus-mechanisms/pos/).

### Proof-of-work (PoW)

A security mechanism for blockchains that requires nodes to expend energy in
the form of computation to find a certain value.

### Proto-Danksharding

A new transaction type which accepts "blobs" of data for Ethereum. This "blob"
data is temporarily stored on the beacon chain for 4096 epochs (~18.2 days),
and can optionally be pruned after to help reduce hardware requirements for
node operators.

### Public goods

Public goods are things everyone can use for free, like parks or clean air,
and using them doesn’t stop others from using them too. Governments often
provide these because businesses usually won’t, since they can’t easily charge
people for using them.

### Public key

A public key is a set of characters that lets others send you digital currency
securely, like an email address for money.

## R

### Receipt

Data returned by an Ethereum client to represent the result of a particular
[transaction](/en/glossary/#transaction), including a
[hash](/en/glossary/#hash) of the transaction, its
[block](/en/glossary/#block) number, the amount of [gas](/en/glossary/#gas)
used, and, in case of deployment of a [smart contract](/en/glossary/#smart-
contract), the [address](/en/glossary/#address) of the contract.

### Re-entrancy attack

An attack that consists of an attacker contract calling a victim contract
function in such a way that during execution the victim calls the attacker
contract again, recursively. This can result, for example, in the theft of
funds by skipping parts of the victim contract that update balances or count
withdrawal amounts.< href="/developers/docs/smart-contracts/security/#re-
entrancy">More on re-entrancy.

### Reward

An amount of ether [awarded to validators](/en/developers/docs/consensus-
mechanisms/pos/rewards-and-penalties/) that perform certain functions,
including proposing a block or participating in a sync-committee, in each
slot.

### Recursive Length Prefix (RLP)

An [encoding standard](/en/developers/docs/data-structures-and-encoding/)
designed by the Ethereum developers to encode and serialize objects (data
structures) of arbitrary complexity and length.

### Rollups

A type of [layer 2](/en/glossary/#layer-2) scaling solution that batches
multiple transactions and submits them to [the Ethereum main
chain](/en/glossary/#mainnet) in a single transaction. This allows for
reductions in [gas](/en/glossary/#gas) costs and increases in
[transaction](/en/glossary/#transaction) throughput. There are Optimistic and
Zero-knowledge rollups which use different security methods to offer these
scalability gains. [More on rollups](/en/developers/docs/scaling/#rollups).

### Remote procedure call (RPC)

RPC lets one computer request data or action from another over a network, like
asking for info with a remote control.

## S

### Secure Hash Algorithm (SHA)

A family of cryptographic hash functions published by the National Institute
of Standards and Technology (NIST).

### Seed phrase/recovery phrase

A list of words given to you when you create a digital wallet. It acts like a
password that can help you get back into your wallet if you lose access,
making sure you don't lose your digital money or tokens.

### Sequencer

A sequencer is a program responsible for ordering transactions in a blockchain
network, particularly within Layer 2 scaling solutions.

### Serialization

The process of converting a data structure into a sequence of bytes.

### Shard / shard chain

Shard chains are discrete sections of the total blockchain that subsets of
validators can be responsible for. This was originally intended to be the way
that Ethereum scaled to millions of transactions per second, but it has now
been superseded by the rapid development of scaling using
[rollups](/en/glossary/#rollups).

### Sidechain

A scaling solution that uses a separate chain with different, often faster,
[consensus rules](/en/glossary/#consensus-rules). A bridge is needed to
connect these sidechains to [Mainnet](/en/glossary/#mainnet).
[Rollups](/en/glossary/#rollups) also use sidechains, but they operate in
collaboration with [Mainnet](/en/glossary/#mainnet) instead. [More on
sidechains](/en/developers/docs/scaling/sidechains/).

### Signing

Demonstrating cryptographically that a transaction was approved by the holder
of a specific private key.

### Singleton

A computer programming term that describes an object of which only a single
instance can exist.

### Slasher

A slasher is an entity that scans attestations searching for slashable
offenses. Slashings are broadcast to the network, and the next block proposer
adds the proof to the block. The block proposer then receives a reward for
slashing the malicious validator.

### Slot

A period of time (12 seconds) in which new blocks can be proposed by a
[validator](/en/glossary/#validator) in the [proof-of-
stake](/en/glossary/#pos) system. A slot may be empty. 32 slots make up an
[epoch](/en/glossary/#epoch). [More on proof-of-
stake](/en/developers/docs/consensus-mechanisms/pos/#how-does-validation-
work).

### Smart contract

A smart contract is a program that automatically executes agreements on a
blockchain, like a self-enforcing digital contract. [Introduction to smart
contracts](/en/smart-contracts/).

### SNARK

Short for "succinct non-interactive argument of knowledge", a SNARK is a type
of [zero-knowledge proof](/en/glossary/#zk-proof). [More on zero-knowledge
rollups](/en/developers/docs/scaling/zk-rollups/).

### Soft fork

A divergence in a [blockchain](/en/glossary/#blockchain) that occurs when the
[consensus rules](/en/glossary/#consensus-rules) change. Contrary to a [hard
fork](/en/glossary/#hard-fork), a soft fork is backwards compatible; upgraded
nodes can validate blocks created by non-upgraded nodes as long as they follow
the new consensus rules.

### Solidity

A procedural (imperative) programming language with syntax that is similar to
JavaScript, C++, or Java. The most popular and most frequently used language
for Ethereum [smart contracts](/en/glossary/#smart-contract). Created by Dr.
Gavin Wood. [More on Solidity](/en/developers/docs/smart-
contracts/languages/#solidity).

### Solidity inline assembly

[EVM](/en/glossary/#evm) assembly language in a
[Solidity](/en/glossary/#solidity) program. Solidity's support for inline
assembly makes it easier to write certain operations.

### Stablecoin

A stablecoin is a type of cryptocurrency designed to have a stable value,
often pegged to a currency or commodity (like US dollar), to minimize price
volatility. [More on stablecoins](/en/stablecoins/).

### Staking

Depositing a quantity of [ether](/en/glossary/#ether) (your stake) to become a
validator and secure the [network](/en/glossary/#network). A validator checks
[transactions](/en/glossary/#transaction) and proposes
[blocks](/en/glossary/#block) under a [proof-of-stake](/en/glossary/#pos)
consensus model. Staking gives you an economic incentive to act in the best
interests of the network. You'll get rewards for carrying out your
[validator](/en/glossary/#validator) duties, but lose varying amounts of ETH
if you don't. [More on Ethereum staking](/en/staking/).

### Staking pool

The combined ETH of more than one Ethereum staker, used to reach the 32 ETH
required to activate a set of validator keys. A node operator uses these keys
to participate in consensus and the [block rewards](/en/glossary/#block-
reward) are split amongst contributing stakers. Staking pools or delegating
staking are not native to the Ethereum protocol, but many solutions have been
built by the community. [More on pooled staking](/en/staking/pools/).

### STARK

Short for "scalable transparent argument of knowledge", a STARK is a type of
[zero-knowledge proof](/en/glossary/#zk-proof). [More on zero-knowledge
rollups](/en/developers/docs/scaling/zk-rollups/).

### State

A snapshot of all balances and data at a particular point in time on the
blockchain, normally referring to the condition at a particular block.

### State channels

A [layer 2](/en/glossary/#layer-2) solution where a channel is set up between
participants, where they can transact freely and cheaply. Only a
[transaction](/en/glossary/#transaction) to set up the channel and close the
channel is sent to [Mainnet](/en/glossary/#mainnet). This allows for very high
transaction throughput, but does rely on knowing number of participants up
front and locking up of funds. [More on state
channels](/en/developers/docs/scaling/state-channels/#state-channels).

### Supermajority

Supermajority is the term given for an amount exceeding 2/3 (66%) of the total
staked ether securing Ethereum. A supermajority vote is required for blocks to
be [finalized](/en/glossary/#finality) on the Beacon Chain.

### Syncing

The process of downloading the entire latest version of a blockchain to a
node.

### Sync committee

A sync committee is a randomly selected group of
[validators](/en/glossary/#validator) that refresh every ~27 hours. Their
purpose is to add their signatures to valid block headers. Sync committees
allow [light clients](/en/glossary/#light-client) to keep track of the head of
the blockchain without needing to access the entire validator set.

### Szabo

A denomination of [ether](/en/glossary/#ether). 1 szabo = 1012
[wei](/en/glossary/#wei). 106 szabo = 1 ether.

## T

### Terminal total difficulty (TTD)

The total difficulty is the sum of the Ethash mining difficulty for all blocks
up to some specific point in the blockchain. The terminal total difficulty is
a specific value for the total difficulty that was used as the trigger for
execution clients to switch off their mining and block gossip functions
enabling the network to transition to proof-of-stake. It is no longer relevant
because Ethereum moved to [proof-of-stake](/en/glossary/#pos).

### Testnet

Short for "test network," a network used to simulate the behavior of the main
Ethereum network.

### Token

A tradable virtual good defined in smart contracts on the Ethereum blockchain.

### Transaction

Data committed to the Ethereum Blockchain signed by an originating
[account](/en/glossary/#account), targeting a specific
[address](/en/glossary/#address). The transaction contains metadata such as
the [gas limit](/en/glossary/#gas-limit) for that transaction. [More on
transactions](/en/developers/docs/transactions/).

### Transaction fee

A fee you need to pay whenever you use the Ethereum network. Examples include
sending funds from your [wallet](/en/glossary/#wallet) or a
[dapp](/en/glossary/#dapp) interaction, like swapping tokens or buying a
collectable. You can think of this like a service charge. This fee will change
based on how busy the network is. This is because
[validators](/en/glossary/#validator), the people responsible for processing
your transaction, are likely to prioritize transactions with higher fees – so
congestion forces the price up.  
  
At a technical level, your transaction fee relates to how much
[gas](/en/glossary/#gas) your transaction requires.  
  
Reducing transaction fees is a subject of intense interest right now. See
[Layer 2](/en/glossary/#layer-2).

### Trust assumptions

Trust assumptions are basic beliefs about a system's safety and dependability,
guiding what we trust for the system to function.

### Trustlessness

The ability of a network to mediate transactions without any of the involved
parties needing to trust a third party.

### Turing complete

A concept named after English mathematician and computer scientist Alan Turing
- a system of data-manipulation rules (such as a computer's instruction set, a
programming language, or a cellular automaton) is said to be "Turing complete"
or "computationally universal" if it can be used to simulate any Turing
machine.

## V

### Validator

A [node](/en/glossary/#node) in a [proof-of-stake](/en/glossary/#pos) system
responsible for storing data, processing transactions, and adding new blocks
to the blockchain. To activate validator software, you need to be able to
[stake](/en/glossary/#staking) 32 ETH. [More on staking in
Ethereum](/en/staking/).

### Validator lifecycle

The sequence of states that a validator can exist in. These include:  
  

  * deposited: At least 32 ETH has been deposited to the [deposit contract](/en/glossary/#deposit-contract) by the validator
  * pending: the validator is in the activation queue waiting to be voted into the network by existing validators
  * active: currently attesting and proposing blocks
  * slashing: the validator has misbehaved and is being slashed
  * exiting: the validator has been flagged for exiting the network, either voluntarily or because they have been ejected.

### Validity proof

A security model for certain [layer 2](/en/glossary/#layer-2) solutions where,
to increase speed, transactions are rolled up into batches and submitted to
Ethereum in a single transaction. The transaction computation is done off-
chain and then supplied to the main chain with a proof of their validity. This
method increases the amount of transactions possible while maintaining
security. Some [rollups](/en/glossary/#rollups) use [fraud
proof](/en/glossary/#fraud-proof). [More on zero-knowledge
rollups](/en/developers/docs/scaling/zk-rollups/).

### Validium

An off-chain solution that uses [validity proofs](/en/glossary/#validity-
proof) to improve transaction throughput. Unlike [Zero-knowledge
rollups](/en/glossary/#zk-rollup), validium data isn't stored on layer 1
Mainnet. [More on validium](/en/developers/docs/scaling/validium/).

### Vyper

A high-level programming language with Python-like syntax. Intended to get
closer to a pure functional language. Created by Vitalik Buterin. [More on
Vyper](/en/developers/docs/smart-contracts/languages/#vyper).

## W

### Wallet

A wallet is a digital tool to store, send, and receive digital currency, like
a virtual purse for your online money. [More on Ethereum
wallets](/en/wallets/).

### Web3

Web3 is the new internet with blockchain, where users control their data and
transactions, not companies. No need to share any personal information. [More
on web3](/en/web3/).

### Wei

The smallest denomination of ether. 1018 wei = 1 ether.

## Z

### Zero address

An Ethereum address, composed entirely of zeros, that is frequently used as an
address to remove tokens from owned circulation. A distinction is drawn
between tokens formally removed from a smart contract's index via the burn()
method and those sent to this address.

### Zero-knowledge proof

A zero-knowledge proof is a cryptographic method that allows an individual to
prove that a statement is true without conveying any additional information.
[More on zero-knowledge rollups](/en/developers/docs/scaling/zk-rollups/).

### Zero-knowledge rollup

A [rollup of transactions that use ](/en/glossary/#rollups)[validity
proofs](/en/glossary/#validity-proof) to offer increased [layer
2](/en/glossary/#layer-2) transaction throughput while using the security
provided by Mainnet (layer 1). Although they can't handle complex transaction
types, like [optimistic rollups](/en/glossary/#optimistic-rollup), they don't
have latency issues because transactions are provably valid when submitted.
[More on zero-knowledge rollups](/en/developers/docs/scaling/zk-rollups/).

## Sources

 _Provided in part by[Mastering Ethereum(opens in a new
tab)](https://github.com/ethereumbook/ethereumbook) by [Andreas M.
Antonopoulos, Gavin Wood(opens in a new tab)](https://ethereumbook.info) under
CC-BY-SA_

## Contribute to this page

Did we miss something? Is something incorrect? Help us improve by contributing
to this glossary on GitHub!

[Learn more about how to contribute](/en/contributing/adding-glossary-terms/)

### Was this article helpful?

YesNo

  * [Edit page(opens in a new tab)](https://github.com/ethereum/ethereum-org-website/tree/dev/public/content/glossary/index.md)
  * On this page

    * #
    * A
    * B
    * C
    * D
    * E
    * F
    * G
    * H
    * I
    * K
    * L
    * M
    * N
    * O
    * P
    * R
    * S
    * T
    * V
    * W
    * Z
    * Sources
    * Contribute to this page

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

