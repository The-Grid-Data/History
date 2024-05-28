This website uses cookies to offer you a better browsing experience. Find out
more on how we use cookies.

Opt-out[Details](/vi/privacy-policy#collection-of-information)

Accept

[![Solana](/_next/static/media/logotype-dark.f79d530d.svg)](/vi)

  * Tìm hiểu
  * Developers
  * Solutions
  * Network
  * Cộng đồng 

Search```K`

[Documentation](/vi/docs)[RPC
API](/vi/docs/rpc)[Cookbook](/vi/developers/cookbook)[Guides](/vi/developers/guides)[Terminology](/vi/docs/terminology)

##### Table of Contents

  * [account](/vi/docs/terminology#account)
  * [account owner](/vi/docs/terminology#account-owner)
  * [app](/vi/docs/terminology#app)
  * [bank state](/vi/docs/terminology#bank-state)
  * [block](/vi/docs/terminology#block)
  * [blockhash](/vi/docs/terminology#blockhash)
  * [block height](/vi/docs/terminology#block-height)
  * [bootstrap validator](/vi/docs/terminology#bootstrap-validator)
  * [BPF loader](/vi/docs/terminology#bpf-loader)
  * [client](/vi/docs/terminology#client)
  * [commitment](/vi/docs/terminology#commitment)
  * [cluster](/vi/docs/terminology#cluster)
  * [compute budget](/vi/docs/terminology#compute-budget)
  * [compute units](/vi/docs/terminology#compute-units)
  * [confirmation time](/vi/docs/terminology#confirmation-time)
  * [confirmed block](/vi/docs/terminology#confirmed-block)
  * [control plane](/vi/docs/terminology#control-plane)
  * [cooldown period](/vi/docs/terminology#cooldown-period)
  * [credit](/vi/docs/terminology#credit)
  * [cross-program invocation (CPI](/vi/docs/terminology#cross-program-invocation-cpi)
  * [data plane](/vi/docs/terminology#data-plane)
  * [drone](/vi/docs/terminology#drone)
  * [entry](/vi/docs/terminology#entry)
  * [entry id](/vi/docs/terminology#entry-id)
  * [epoch](/vi/docs/terminology#epoch)
  * [fee account](/vi/docs/terminology#fee-account)
  * [finality](/vi/docs/terminology#finality)
  * [fork](/vi/docs/terminology#fork)
  * [genesis block](/vi/docs/terminology#genesis-block)
  * [genesis config](/vi/docs/terminology#genesis-config)
  * [hash](/vi/docs/terminology#hash)
  * [inflation](/vi/docs/terminology#inflation)
  * [inner instruction](/vi/docs/terminology#inner-instruction)
  * [instruction](/vi/docs/terminology#instruction)
  * [instruction handler](/vi/docs/terminology#instruction-handler)
  * [keypair](/vi/docs/terminology#keypair)
  * [lamport](/vi/docs/terminology#lamport)
  * [leader](/vi/docs/terminology#leader)
  * [leader schedule](/vi/docs/terminology#leader-schedule)
  * [ledger](/vi/docs/terminology#ledger)
  * [ledger vote](/vi/docs/terminology#ledger-vote)
  * [light client](/vi/docs/terminology#light-client)
  * [loader](/vi/docs/terminology#loader)
  * [lockout](/vi/docs/terminology#lockout)
  * [message](/vi/docs/terminology#message)
  * [Nakamoto coefficient](/vi/docs/terminology#nakamoto-coefficient)
  * [native token](/vi/docs/terminology#native-token)
  * [node](/vi/docs/terminology#node)
  * [node count](/vi/docs/terminology#node-count)
  * [onchain program](/vi/docs/terminology#onchain-program)
  * [PoH](/vi/docs/terminology#poh)
  * [point](/vi/docs/terminology#point)
  * [private key](/vi/docs/terminology#private-key)
  * [program](/vi/docs/terminology#program)
  * [program derived account (PDA](/vi/docs/terminology#program-derived-account-pda)
  * [program id](/vi/docs/terminology#program-id)
  * [proof of history (PoH](/vi/docs/terminology#proof-of-history-poh)
  * [prioritization fee](/vi/docs/terminology#prioritization-fee)
  * [public key (pubkey](/vi/docs/terminology#public-key-pubkey)
  * [rent](/vi/docs/terminology#rent)
  * [rent exempt](/vi/docs/terminology#rent-exempt)
  * [root](/vi/docs/terminology#root)
  * [runtime](/vi/docs/terminology#runtime)
  * [Sealevel](/vi/docs/terminology#sealevel)
  * [shred](/vi/docs/terminology#shred)
  * [signature](/vi/docs/terminology#signature)
  * [skip rate](/vi/docs/terminology#skip-rate)
  * [skipped slot](/vi/docs/terminology#skipped-slot)
  * [slot](/vi/docs/terminology#slot)
  * [smart contract](/vi/docs/terminology#smart-contract)
  * [sol](/vi/docs/terminology#sol)
  * [Solana Program Library (SPL](/vi/docs/terminology#solana-program-library-spl)
  * [stake](/vi/docs/terminology#stake)
  * [stake-weighted quality of service (SWQoS](/vi/docs/terminology#stake-weighted-quality-of-service-swqos)
  * [supermajority](/vi/docs/terminology#supermajority)
  * [sysvar](/vi/docs/terminology#sysvar)
  * [thin client](/vi/docs/terminology#thin-client)
  * [tick](/vi/docs/terminology#tick)
  * [tick height](/vi/docs/terminology#tick-height)
  * [token](/vi/docs/terminology#token)
  * [Token Extensions Program](/vi/docs/terminology#token-extensions-program)
  * [Token Program](/vi/docs/terminology#token-program)
  * [tps](/vi/docs/terminology#tps)
  * [tpu](/vi/docs/terminology#tpu)
  * [transaction](/vi/docs/terminology#transaction)
  * [transaction id](/vi/docs/terminology#transaction-id)
  * [transaction confirmations](/vi/docs/terminology#transaction-confirmations)
  * [transactions entry](/vi/docs/terminology#transactions-entry)
  * [tvu](/vi/docs/terminology#tvu)
  * [validator](/vi/docs/terminology#validator)
  * [VDF](/vi/docs/terminology#vdf)
  * [verifiable delay function (VDF](/vi/docs/terminology#verifiable-delay-function-vdf)
  * [vote](/vi/docs/terminology#vote)
  * [vote credit](/vi/docs/terminology#vote-credit)
  * [wallet](/vi/docs/terminology#wallet)
  * [warmup period](/vi/docs/terminology#warmup-period)

[Scroll to Top](/vi/docs/terminology#)

[Edit Page](https://github.com/solana-foundation/developer-
content/tree/main/docs/terminology.md)

[Home](/vi)>[Solana Documentation](/vi/docs)

# [Terminology](/vi/docs/terminology)

The following terms are used throughout the Solana documentation and
development ecosystem.

## account #

A record in the Solana ledger that either holds data or is an executable
program.

Like an account at a traditional bank, a Solana account may hold funds called
[lamports](/vi/docs/terminology#lamport). Like a file in Linux, it is
addressable by a key, often referred to as a [public
key](/vi/docs/terminology#public-key-pubkey) or pubkey.

The key may be one of:

  * an ed25519 public key
  * a program-derived account address (32byte value forced off the ed25519 curve)
  * a hash of an ed25519 public key with a 32 character string

## account owner #

The address of the program that owns the account. Only the owning program is
capable of modifying the account.

## app #

A front-end application that interacts with a Solana cluster.

## bank state #

The result of interpreting all programs on the ledger at a given [tick
height](/vi/docs/terminology#tick-height). It includes at least the set of all
[accounts](/vi/docs/terminology#account) holding nonzero [native
tokens](/vi/docs/terminology#native-token).

## block #

A contiguous set of [entries](/vi/docs/terminology#entry) on the ledger
covered by a [vote](/vi/docs/terminology#ledger-vote). A
[leader](/vi/docs/terminology#leader) produces at most one block per
[slot](/vi/docs/terminology#slot).

## blockhash #

A unique value ([hash](/vi/docs/terminology#hash)) that identifies a record
(block). Solana computes a blockhash from the last [entry
id](/vi/docs/terminology#entry-id) of the block.

## block height #

The number of [blocks](/vi/docs/terminology#block) beneath the current block.
The first block after the [genesis block](/vi/docs/terminology#genesis-block)
has height one.

## bootstrap validator #

The [validator](/vi/docs/terminology#validator) that produces the genesis
(first) [block](/vi/docs/terminology#block) of a block chain.

## BPF loader #

The Solana program that owns and loads [BPF](/vi/docs/programs/faq#berkeley-
packet-filter-bpf) [onchain programs](/vi/docs/terminology#onchain-program),
allowing the program to interface with the runtime.

## client #

A computer program that accesses the Solana server network
[cluster](/vi/docs/terminology#cluster).

## commitment #

A measure of the network confirmation for the
[block](/vi/docs/terminology#block).

## cluster #

A set of [validators](/vi/docs/terminology#validator) maintaining a single
[ledger](/vi/docs/terminology#ledger).

## compute budget #

The maximum number of [compute units](/vi/docs/terminology#compute-units)
consumed per transaction.

## compute units #

The smallest unit of measure for consumption of computational resources of the
blockchain.

## confirmation time #

The wallclock duration between a [leader](/vi/docs/terminology#leader)
creating a [tick entry](/vi/docs/terminology#tick) and creating a [confirmed
block](/vi/docs/terminology#confirmed-block).

## confirmed block #

A [block](/vi/docs/terminology#block) that has received a [super
majority](/vi/docs/terminology#supermajority) of [ledger
votes](/vi/docs/terminology#ledger-vote).

## control plane #

A gossip network connecting all [nodes](/vi/docs/terminology#node) of a
[cluster](/vi/docs/terminology#cluster).

## cooldown period #

Some number of [epochs](/vi/docs/terminology#epoch) after
[stake](/vi/docs/terminology#stake) has been deactivated while it
progressively becomes available for withdrawal. During this period, the stake
is considered to be "deactivating". More info about: [warmup and
cooldown](https://docs.solanalabs.com/implemented-proposals/staking-
rewards#stake-warmup-cooldown-withdrawal)

## credit #

See [vote credit](/vi/docs/terminology#vote-credit).

## cross-program invocation (CPI) #

A call from one [onchain program](/vi/docs/terminology#onchain-program) to
another. For more information, see [calling between
programs](/vi/docs/core/cpi).

## data plane #

A multicast network used to efficiently validate
[entries](/vi/docs/terminology#entry) and gain consensus.

## drone #

An off-chain service that acts as a custodian for a user's private key. It
typically serves to validate and sign transactions.

## entry #

An entry on the [ledger](/vi/docs/terminology#ledger) either a
[tick](/vi/docs/terminology#tick) or a [transaction's
entry](/vi/docs/terminology#transactions-entry).

## entry id #

A preimage resistant [hash](/vi/docs/terminology#hash) over the final contents
of an entry, which acts as the [entry's](/vi/docs/terminology#entry) globally
unique identifier. The hash serves as evidence of:

  * The entry being generated after a duration of time
  * The specified [transactions](/vi/docs/terminology#transaction) are those included in the entry
  * The entry's position with respect to other entries in [ledger](/vi/docs/terminology#ledger)

See [proof of history](/vi/docs/terminology#proof-of-history-poh).

## epoch #

The time, i.e. number of [slots](/vi/docs/terminology#slot), for which a
[leader schedule](/vi/docs/terminology#leader-schedule) is valid.

## fee account #

The fee account in the transaction is the account that pays for the cost of
including the transaction in the ledger. This is the first account in the
transaction. This account must be declared as Read-Write (writable) in the
transaction since paying for the transaction reduces the account balance.

## finality #

When nodes representing 2/3rd of the [stake](/vi/docs/terminology#stake) have
a common [root](/vi/docs/terminology#root).

## fork #

A [ledger](/vi/docs/terminology#ledger) derived from common entries but then
diverged.

## genesis block #

The first [block](/vi/docs/terminology#block) in the chain.

## genesis config #

The configuration file that prepares the [ledger](/vi/docs/terminology#ledger)
for the [genesis block](/vi/docs/terminology#genesis-block).

## hash #

A digital fingerprint of a sequence of bytes.

## inflation #

An increase in token supply over time used to fund rewards for validation and
to fund continued development of Solana.

## inner instruction #

See [cross-program invocation](/vi/docs/terminology#cross-program-invocation-
cpi).

## instruction #

A call to invoke a specific [instruction
handler](/vi/docs/terminology#instruction-handler) in a
[program](/vi/docs/terminology#program). An instruction also specifies which
accounts it wants to read or modify, and additional data that serves as
auxiliary input to the [instruction handler](/vi/docs/terminology#instruction-
handler). A [client](/vi/docs/terminology#client) must include at least one
instruction in a [transaction](/vi/docs/terminology#transaction), and all
instructions must complete for the transaction to be considered successful.

## instruction handler #

Instruction handlers are [program](/vi/docs/terminology#program) functions
that process [instructions](/vi/docs/terminology#instruction) from
[transactions](/vi/docs/terminology#transaction). An instruction handler may
contain one or more [cross-program invocations](/vi/docs/terminology#cross-
program-invocation-cpi).

## keypair #

A [public key](/vi/docs/terminology#public-key-pubkey) and corresponding
[private key](/vi/docs/terminology#private-key) for accessing an account.

## lamport #

A fractional [native token](/vi/docs/terminology#native-token) with the value
of 0.000000001 [sol](/vi/docs/terminology#sol).

Info

Within the compute budget, a quantity of _[micro-
lamports](https://github.com/solana-
labs/solana/blob/ced8f6a512c61e0dd5308095ae8457add4a39e94/program-
runtime/src/prioritization_fee.rs#L1-L2)_ is used in the calculation of
[prioritization fees](/vi/docs/terminology#prioritization-fee).

## leader #

The role of a [validator](/vi/docs/terminology#validator) when it is appending
[entries](/vi/docs/terminology#entry) to the
[ledger](/vi/docs/terminology#ledger).

## leader schedule #

A sequence of [validator](/vi/docs/terminology#validator) [public
keys](/vi/docs/terminology#public-key-pubkey) mapped to
[slots](/vi/docs/terminology#slot). The cluster uses the leader schedule to
determine which validator is the [leader](/vi/docs/terminology#leader) at any
moment in time.

## ledger #

A list of [entries](/vi/docs/terminology#entry) containing
[transactions](/vi/docs/terminology#transaction) signed by
[clients](/vi/docs/terminology#client). Conceptually, this can be traced back
to the [genesis block](/vi/docs/terminology#genesis-block), but an actual
[validator](/vi/docs/terminology#validator)'s ledger may have only newer
[blocks](/vi/docs/terminology#block) to reduce storage, as older ones are not
needed for validation of future blocks by design.

## ledger vote #

A [hash](/vi/docs/terminology#hash) of the [validator's
state](/vi/docs/terminology#bank-state) at a given [tick
height](/vi/docs/terminology#tick-height). It comprises a
[validator's](/vi/docs/terminology#validator) affirmation that a
[block](/vi/docs/terminology#block) it has received has been verified, as well
as a promise not to vote for a conflicting [block](/vi/docs/terminology#block)
(i.e. [fork](/vi/docs/terminology#fork)) for a specific amount of time, the
[lockout](/vi/docs/terminology#lockout) period.

## light client #

A type of [client](/vi/docs/terminology#client) that can verify it's pointing
to a valid [cluster](/vi/docs/terminology#cluster). It performs more ledger
verification than a [thin client](/vi/docs/terminology#thin-client) and less
than a [validator](/vi/docs/terminology#validator).

## loader #

A [program](/vi/docs/terminology#program) with the ability to interpret the
binary encoding of other on-chain programs.

## lockout #

The duration of time for which a [validator](/vi/docs/terminology#validator)
is unable to [vote](/vi/docs/terminology#ledger-vote) on another
[fork](/vi/docs/terminology#fork).

## message #

The structured contents of a [transaction](/vi/docs/terminology#transaction).
Generally containing a header, array of account addresses, recent
[blockhash](/vi/docs/terminology#blockhash), and an array of
[instructions](/vi/docs/terminology#instruction).

Learn more about the [message formatting inside of
transactions](/vi/docs/core/transactions#message-header) here.

## Nakamoto coefficient #

A measure of decentralization, the Nakamoto Coefficient is the smallest number
of independent entities that can act collectively to shut down a blockchain.
The term was coined by Balaji S. Srinivasan and Leland Lee in [Quantifying
Decentralization](https://news.earn.com/quantifying-
decentralization-e39db233c28e).

## native token #

The [token](/vi/docs/terminology#token) used to track work done by
[nodes](/vi/docs/terminology#node) in a cluster.

## node #

A computer participating in a [cluster](/vi/docs/terminology#cluster).

## node count #

The number of [validators](/vi/docs/terminology#validator) participating in a
[cluster](/vi/docs/terminology#cluster).

## onchain program #

The executable code on Solana blockchain that interprets the
[instructions](/vi/docs/terminology#instruction) sent inside of each
[transaction](/vi/docs/terminology#transaction) to read and modify accounts
over which it has control. These programs are often referred to as "[_smart
contracts_](/vi/docs/core/programs)" on other blockchains.

## PoH #

See [Proof of History](/vi/docs/terminology#proof-of-history-poh).

## point #

A weighted [credit](/vi/docs/terminology#credit) in a rewards regime. In the
[validator](/vi/docs/terminology#validator) [rewards
regime](https://docs.solanalabs.com/consensus/stake-delegation-and-rewards),
the number of points owed to a [stake](/vi/docs/terminology#stake) during
redemption is the product of the [vote credits](/vi/docs/terminology#vote-
credit) earned and the number of lamports staked.

## private key #

The private key of a [keypair](/vi/docs/terminology#keypair).

## program #

See [onchain program](/vi/docs/terminology#onchain-program).

## program derived account (PDA) #

An account whose signing authority is a program and thus is not controlled by
a private key like other accounts.

## program id #

The public key of the [account](/vi/docs/terminology#account) containing a
[program](/vi/docs/terminology#program).

## proof of history (PoH) #

A stack of proofs, each of which proves that some data existed before the
proof was created and that a precise duration of time passed before the
previous proof. Like a [VDF](/vi/docs/terminology#verifiable-delay-function-
vdf), a Proof of History can be verified in less time than it took to produce.

## prioritization fee #

An additional fee user can specify in the compute budget
[instruction](/vi/docs/terminology#instruction) to prioritize their
[transactions](/vi/docs/terminology#transaction).

The prioritization fee is calculated by multiplying the requested maximum
compute units by the compute-unit price (specified in increments of 0.000001
lamports per compute unit) rounded up to the nearest lamport.

Transactions should request the minimum amount of compute units required for
execution to minimize fees.

## public key (pubkey) #

The public key of a [keypair](/vi/docs/terminology#keypair).

## rent #

Fee paid by [Accounts](/vi/docs/terminology#account) and
[Programs](/vi/docs/terminology#program) to store data on the blockchain. When
accounts do not have enough balance to pay rent, they may be Garbage
Collected.

See also [rent exempt](/vi/docs/terminology#rent-exempt) below. Learn more
about rent here: [What is rent?](/vi/docs/intro/rent).

## rent exempt #

Accounts that maintain a minimum lamport balance that is proportional to the
amount of data stored on the account. All newly created accounts are stored
on-chain permanently until the account is closed. It is not possible to create
an account that falls below the rent exemption threshold.

## root #

A [block](/vi/docs/terminology#block) or [slot](/vi/docs/terminology#slot)
that has reached maximum [lockout](/vi/docs/terminology#lockout) on a
[validator](/vi/docs/terminology#validator). The root is the highest block
that is an ancestor of all active forks on a validator. All ancestor blocks of
a root are also transitively a root. Blocks that are not an ancestor and not a
descendant of the root are excluded from consideration for consensus and can
be discarded.

## runtime #

The component of a [validator](/vi/docs/terminology#validator) responsible for
[program](/vi/docs/terminology#program) execution.

## Sealevel #

Solana's parallel run-time for [onchain
programs](/vi/docs/terminology#onchain-program).

## shred #

A fraction of a [block](/vi/docs/terminology#block); the smallest unit sent
between [validators](/vi/docs/terminology#validator).

## signature #

A 64-byte ed25519 signature of R (32-bytes) and S (32-bytes). With the
requirement that R is a packed Edwards point not of small order and S is a
scalar in the range of `0 <= S < L`. This requirement ensures no signature
malleability. Each transaction must have at least one signature for [fee
account](/vi/docs/terminology#fee-account). Thus, the first signature in
transaction can be treated as [transaction
id](/vi/docs/terminology#transaction-id)

## skip rate #

The percentage of [skipped slots](/vi/docs/terminology#skipped-slot) out of
the total leader slots in the current epoch. This metric can be misleading as
it has high variance after the epoch boundary when the sample size is small,
as well as for validators with a low number of leader slots, however can also
be useful in identifying node misconfigurations at times.

## skipped slot #

A past [slot](/vi/docs/terminology#slot) that did not produce a
[block](/vi/docs/terminology#block), because the leader was offline or the
[fork](/vi/docs/terminology#fork) containing the slot was abandoned for a
better alternative by cluster consensus. A skipped slot will not appear as an
ancestor for blocks at subsequent slots, nor increment the [block
height](/vi/docs/terminology#block-height), nor expire the oldest
`recent_blockhash`.

Whether a slot has been skipped can only be determined when it becomes older
than the latest [rooted](/vi/docs/terminology#root) (thus not-skipped) slot.

## slot #

The period of time for which each [leader](/vi/docs/terminology#leader)
ingests transactions and produces a [block](/vi/docs/terminology#block).

Collectively, slots create a logical clock. Slots are ordered sequentially and
non-overlapping, comprising roughly equal real-world time as per
[PoH](/vi/docs/terminology#proof-of-history-poh).

## smart contract #

See [onchain program](/vi/docs/terminology#onchain-program).

## sol #

The [native token](/vi/docs/terminology#native-token) of a Solana
[cluster](/vi/docs/terminology#cluster).

## Solana Program Library (SPL) #

A [library of programs](https://spl.solana.com/) on Solana such as spl-token
that facilitates tasks such as creating and using tokens.

## stake #

Tokens forfeit to the [cluster](/vi/docs/terminology#cluster) if malicious
[validator](/vi/docs/terminology#validator) behavior can be proven.

## stake-weighted quality of service (SWQoS) #

SWQoS allows [preferential treatment for transactions that come from staked
validators](/vi/developers/guides/advanced/stake-weighted-qos).

## supermajority #

2/3 of a [cluster](/vi/docs/terminology#cluster).

## sysvar #

A system [account](/vi/docs/terminology#account).
[Sysvars](https://docs.solanalabs.com/runtime/sysvars) provide cluster state
information such as current tick height, rewards
[points](/vi/docs/terminology#point) values, etc. Programs can access Sysvars
via a Sysvar account (pubkey) or by querying via a syscall.

## thin client #

A type of [client](/vi/docs/terminology#client) that trusts it is
communicating with a valid [cluster](/vi/docs/terminology#cluster).

## tick #

A ledger [entry](/vi/docs/terminology#entry) that estimates wallclock
duration.

## tick height #

The Nth [tick](/vi/docs/terminology#tick) in the
[ledger](/vi/docs/terminology#ledger).

## token #

A digitally transferable asset.

## Token Extensions Program #

The [Token Extensions Program](https://spl.solana.com/token-2022) has the
program ID `TokenzQdBNbLqP5VEhdkAS6EPFLC1PHnBqCXEpPxuEb` and includes all the
same features as the [Token Program](/vi/docs/terminology#token-program), but
comes with extensions such as confidential transfers, custom transfer logic,
extended metadata, and much more.

## Token Program #

The [Token Program](https://spl.solana.com/token) has the program ID
`TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA`, and provides the basic
capabilities of transferring, freezing, and minting tokens.

## tps #

[Transactions](/vi/docs/terminology#transaction) per second.

## tpu #

[Transaction processing unit](https://docs.solanalabs.com/validator/tpu).

## transaction #

One or more [instructions](/vi/docs/terminology#instruction) signed by a
[client](/vi/docs/terminology#client) using one or more
[keypairs](/vi/docs/terminology#keypair) and executed atomically with only two
possible outcomes: success or failure.

## transaction id #

The first [signature](/vi/docs/terminology#signature) in a
[transaction](/vi/docs/terminology#transaction), which can be used to uniquely
identify the transaction across the complete
[ledger](/vi/docs/terminology#ledger).

## transaction confirmations #

The number of [confirmed blocks](/vi/docs/terminology#confirmed-block) since
the transaction was accepted onto the [ledger](/vi/docs/terminology#ledger). A
transaction is finalized when its block becomes a
[root](/vi/docs/terminology#root).

## transactions entry #

A set of [transactions](/vi/docs/terminology#transaction) that may be executed
in parallel.

## tvu #

[Transaction validation unit](https://docs.solanalabs.com/validator/tvu).

## validator #

A full participant in a Solana network [cluster](/vi/docs/terminology#cluster)
that produces new [blocks](/vi/docs/terminology#block). A validator validates
the transactions added to the [ledger](/vi/docs/terminology#ledger)

## VDF #

See [verifiable delay function](/vi/docs/terminology#verifiable-delay-
function-vdf).

## verifiable delay function (VDF) #

A function that takes a fixed amount of time to execute that produces a proof
that it ran, which can then be verified in less time than it took to produce.

## vote #

See [ledger vote](/vi/docs/terminology#ledger-vote).

## vote credit #

A reward tally for [validators](/vi/docs/terminology#validator). A vote credit
is awarded to a validator in its vote account when the validator reaches a
[root](/vi/docs/terminology#root).

## wallet #

A collection of [keypairs](/vi/docs/terminology#keypair) that allows users to
manage their funds.

## warmup period #

Some number of [epochs](/vi/docs/terminology#epoch) after
[stake](/vi/docs/terminology#stake) has been delegated while it progressively
becomes effective. During this period, the stake is considered to be
"activating". More info about: [warmup and
cooldown](https://docs.solanalabs.com/consensus/stake-delegation-and-
rewards#stake-warmup-cooldown-withdrawal)

[Previous« JSON RPC Methods](/vi/docs/rpc)[NextOverview
»](/vi/docs/intro/overview)

  * [Solana Documentation](/vi/docs)

    * [JSON RPC Methods](/vi/docs/rpc)
    * [Terminology](/vi/docs/terminology)
  * Introduction

    * [Overview](/vi/docs/intro/overview)
    * [Wallets](/vi/docs/intro/wallets)
    * [Intro to Development](/vi/docs/intro/dev)
  * Core Concepts

    * [Solana Account Model](/vi/docs/core/accounts)
    * [Transactions and Instructions](/vi/docs/core/transactions)
    * [Fees on Solana](/vi/docs/core/fees)
    * [Programs on Solana](/vi/docs/core/programs)
    * [Program Derived Address](/vi/docs/core/pda)
    * [Cross Program Invocation](/vi/docs/core/cpi)
    * [Tokens on Solana](/vi/docs/core/tokens)
    * [Clusters & Endpoints](/vi/docs/core/clusters)
  * Advanced Concepts

    * [Versioned Transactions](/vi/docs/advanced/versions)
    * [Address Lookup Tables](/vi/docs/advanced/lookup-tables)
    * [Confirmation & Expiration](/vi/docs/advanced/confirmation)
    * [Retrying Transactions](/vi/docs/advanced/retry)
    * [State Compression](/vi/docs/advanced/state-compression)
  * Solana Clients

    * [Rust](/vi/docs/clients/rust)
    * [JavaScript / TypeScript](/vi/docs/clients/javascript)
    * [Web3.js API Examples](/vi/docs/clients/javascript-reference)
  * [Economics](/vi/docs/economics)

    * Inflation
      * [Proposed Inflation Schedule](/vi/docs/economics/inflation/inflation-schedule)
      * [Inflation Terminology](/vi/docs/economics/inflation/terminology)
    * [Staking](/vi/docs/economics/staking)
      * [Stake Accounts](/vi/docs/economics/staking/stake-accounts)
      * [Stake Programming](/vi/docs/economics/staking/stake-programming)
  * Developing Programs

    * [Overview](/vi/docs/programs/overview)
    * [Debugging Programs](/vi/docs/programs/debugging)
    * [Deploying Programs](/vi/docs/programs/deploying)
    * [Program Examples](/vi/docs/programs/examples)
    * [FAQ](/vi/docs/programs/faq)
    * [Developing with C](/vi/docs/programs/lang-c)
    * [Developing with Rust](/vi/docs/programs/lang-rust)
    * [Limitations](/vi/docs/programs/limitations)
  * More Information

    * [Add Solana to Your Exchange](/vi/docs/more/exchange)

Managed by

[](/vi)

[](/youtube)[](/twitter)[](/discord)[](/reddit)[](/github)[](/telegram)

© 2024 Solana Foundation. All rights reserved.

Solana

  * [Trợ cấp](https://solana.org/grants)
  * [Solana Break](https://break.solana.com/)
  * [Media Kit](/vi/branding)
  * [Nghề nghiệp ](https://jobs.solana.com/)
  * [Từ chối](/vi/tos)
  * [Privacy Policy](/vi/privacy-policy)

Get Connected

  * [Hệ sinh thái](/vi/ecosystem)
  * [Blog](/vi/news)
  * [Bản tin](/vi/newsletter)

vi

© 2024 Solana Foundation. All rights reserved.

