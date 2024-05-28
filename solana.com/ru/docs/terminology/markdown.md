This website uses cookies to offer you a better browsing experience. Find out
more on how we use cookies.

Opt-out[Details](/ru/privacy-policy#collection-of-information)

Accept

[![Solana](/_next/static/media/logotype-dark.f79d530d.svg)](/ru)

  * Узнать больше
  * Developers
  * Solutions
  * Network
  * Сообщество

Search```K`

[Documentation](/ru/docs)[RPC
API](/ru/docs/rpc)[Cookbook](/ru/developers/cookbook)[Guides](/ru/developers/guides)[Terminology](/ru/docs/terminology)

##### Table of Contents

  * [account](/ru/docs/terminology#account)
  * [account owner](/ru/docs/terminology#account-owner)
  * [app](/ru/docs/terminology#app)
  * [bank state](/ru/docs/terminology#bank-state)
  * [block](/ru/docs/terminology#block)
  * [blockhash](/ru/docs/terminology#blockhash)
  * [block height](/ru/docs/terminology#block-height)
  * [bootstrap validator](/ru/docs/terminology#bootstrap-validator)
  * [BPF loader](/ru/docs/terminology#bpf-loader)
  * [client](/ru/docs/terminology#client)
  * [commitment](/ru/docs/terminology#commitment)
  * [cluster](/ru/docs/terminology#cluster)
  * [compute budget](/ru/docs/terminology#compute-budget)
  * [compute units](/ru/docs/terminology#compute-units)
  * [confirmation time](/ru/docs/terminology#confirmation-time)
  * [confirmed block](/ru/docs/terminology#confirmed-block)
  * [control plane](/ru/docs/terminology#control-plane)
  * [cooldown period](/ru/docs/terminology#cooldown-period)
  * [credit](/ru/docs/terminology#credit)
  * [cross-program invocation (CPI](/ru/docs/terminology#cross-program-invocation-cpi)
  * [data plane](/ru/docs/terminology#data-plane)
  * [drone](/ru/docs/terminology#drone)
  * [entry](/ru/docs/terminology#entry)
  * [entry id](/ru/docs/terminology#entry-id)
  * [epoch](/ru/docs/terminology#epoch)
  * [fee account](/ru/docs/terminology#fee-account)
  * [finality](/ru/docs/terminology#finality)
  * [fork](/ru/docs/terminology#fork)
  * [genesis block](/ru/docs/terminology#genesis-block)
  * [genesis config](/ru/docs/terminology#genesis-config)
  * [hash](/ru/docs/terminology#hash)
  * [inflation](/ru/docs/terminology#inflation)
  * [inner instruction](/ru/docs/terminology#inner-instruction)
  * [instruction](/ru/docs/terminology#instruction)
  * [instruction handler](/ru/docs/terminology#instruction-handler)
  * [keypair](/ru/docs/terminology#keypair)
  * [lamport](/ru/docs/terminology#lamport)
  * [leader](/ru/docs/terminology#leader)
  * [leader schedule](/ru/docs/terminology#leader-schedule)
  * [ledger](/ru/docs/terminology#ledger)
  * [ledger vote](/ru/docs/terminology#ledger-vote)
  * [light client](/ru/docs/terminology#light-client)
  * [loader](/ru/docs/terminology#loader)
  * [lockout](/ru/docs/terminology#lockout)
  * [message](/ru/docs/terminology#message)
  * [Nakamoto coefficient](/ru/docs/terminology#nakamoto-coefficient)
  * [native token](/ru/docs/terminology#native-token)
  * [node](/ru/docs/terminology#node)
  * [node count](/ru/docs/terminology#node-count)
  * [onchain program](/ru/docs/terminology#onchain-program)
  * [PoH](/ru/docs/terminology#poh)
  * [point](/ru/docs/terminology#point)
  * [private key](/ru/docs/terminology#private-key)
  * [program](/ru/docs/terminology#program)
  * [program derived account (PDA](/ru/docs/terminology#program-derived-account-pda)
  * [program id](/ru/docs/terminology#program-id)
  * [proof of history (PoH](/ru/docs/terminology#proof-of-history-poh)
  * [prioritization fee](/ru/docs/terminology#prioritization-fee)
  * [public key (pubkey](/ru/docs/terminology#public-key-pubkey)
  * [rent](/ru/docs/terminology#rent)
  * [rent exempt](/ru/docs/terminology#rent-exempt)
  * [root](/ru/docs/terminology#root)
  * [runtime](/ru/docs/terminology#runtime)
  * [Sealevel](/ru/docs/terminology#sealevel)
  * [shred](/ru/docs/terminology#shred)
  * [signature](/ru/docs/terminology#signature)
  * [skip rate](/ru/docs/terminology#skip-rate)
  * [skipped slot](/ru/docs/terminology#skipped-slot)
  * [slot](/ru/docs/terminology#slot)
  * [smart contract](/ru/docs/terminology#smart-contract)
  * [sol](/ru/docs/terminology#sol)
  * [Solana Program Library (SPL](/ru/docs/terminology#solana-program-library-spl)
  * [stake](/ru/docs/terminology#stake)
  * [stake-weighted quality of service (SWQoS](/ru/docs/terminology#stake-weighted-quality-of-service-swqos)
  * [supermajority](/ru/docs/terminology#supermajority)
  * [sysvar](/ru/docs/terminology#sysvar)
  * [thin client](/ru/docs/terminology#thin-client)
  * [tick](/ru/docs/terminology#tick)
  * [tick height](/ru/docs/terminology#tick-height)
  * [token](/ru/docs/terminology#token)
  * [Token Extensions Program](/ru/docs/terminology#token-extensions-program)
  * [Token Program](/ru/docs/terminology#token-program)
  * [tps](/ru/docs/terminology#tps)
  * [tpu](/ru/docs/terminology#tpu)
  * [transaction](/ru/docs/terminology#transaction)
  * [transaction id](/ru/docs/terminology#transaction-id)
  * [transaction confirmations](/ru/docs/terminology#transaction-confirmations)
  * [transactions entry](/ru/docs/terminology#transactions-entry)
  * [tvu](/ru/docs/terminology#tvu)
  * [validator](/ru/docs/terminology#validator)
  * [VDF](/ru/docs/terminology#vdf)
  * [verifiable delay function (VDF](/ru/docs/terminology#verifiable-delay-function-vdf)
  * [vote](/ru/docs/terminology#vote)
  * [vote credit](/ru/docs/terminology#vote-credit)
  * [wallet](/ru/docs/terminology#wallet)
  * [warmup period](/ru/docs/terminology#warmup-period)

[Scroll to Top](/ru/docs/terminology#)

[Edit Page](https://github.com/solana-foundation/developer-
content/tree/main/docs/terminology.md)

[Home](/ru)>[Solana Documentation](/ru/docs)

# [Terminology](/ru/docs/terminology)

The following terms are used throughout the Solana documentation and
development ecosystem.

## account #

A record in the Solana ledger that either holds data or is an executable
program.

Like an account at a traditional bank, a Solana account may hold funds called
[lamports](/ru/docs/terminology#lamport). Like a file in Linux, it is
addressable by a key, often referred to as a [public
key](/ru/docs/terminology#public-key-pubkey) or pubkey.

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
height](/ru/docs/terminology#tick-height). It includes at least the set of all
[accounts](/ru/docs/terminology#account) holding nonzero [native
tokens](/ru/docs/terminology#native-token).

## block #

A contiguous set of [entries](/ru/docs/terminology#entry) on the ledger
covered by a [vote](/ru/docs/terminology#ledger-vote). A
[leader](/ru/docs/terminology#leader) produces at most one block per
[slot](/ru/docs/terminology#slot).

## blockhash #

A unique value ([hash](/ru/docs/terminology#hash)) that identifies a record
(block). Solana computes a blockhash from the last [entry
id](/ru/docs/terminology#entry-id) of the block.

## block height #

The number of [blocks](/ru/docs/terminology#block) beneath the current block.
The first block after the [genesis block](/ru/docs/terminology#genesis-block)
has height one.

## bootstrap validator #

The [validator](/ru/docs/terminology#validator) that produces the genesis
(first) [block](/ru/docs/terminology#block) of a block chain.

## BPF loader #

The Solana program that owns and loads [BPF](/ru/docs/programs/faq#berkeley-
packet-filter-bpf) [onchain programs](/ru/docs/terminology#onchain-program),
allowing the program to interface with the runtime.

## client #

A computer program that accesses the Solana server network
[cluster](/ru/docs/terminology#cluster).

## commitment #

A measure of the network confirmation for the
[block](/ru/docs/terminology#block).

## cluster #

A set of [validators](/ru/docs/terminology#validator) maintaining a single
[ledger](/ru/docs/terminology#ledger).

## compute budget #

The maximum number of [compute units](/ru/docs/terminology#compute-units)
consumed per transaction.

## compute units #

The smallest unit of measure for consumption of computational resources of the
blockchain.

## confirmation time #

The wallclock duration between a [leader](/ru/docs/terminology#leader)
creating a [tick entry](/ru/docs/terminology#tick) and creating a [confirmed
block](/ru/docs/terminology#confirmed-block).

## confirmed block #

A [block](/ru/docs/terminology#block) that has received a [super
majority](/ru/docs/terminology#supermajority) of [ledger
votes](/ru/docs/terminology#ledger-vote).

## control plane #

A gossip network connecting all [nodes](/ru/docs/terminology#node) of a
[cluster](/ru/docs/terminology#cluster).

## cooldown period #

Some number of [epochs](/ru/docs/terminology#epoch) after
[stake](/ru/docs/terminology#stake) has been deactivated while it
progressively becomes available for withdrawal. During this period, the stake
is considered to be "deactivating". More info about: [warmup and
cooldown](https://docs.solanalabs.com/implemented-proposals/staking-
rewards#stake-warmup-cooldown-withdrawal)

## credit #

See [vote credit](/ru/docs/terminology#vote-credit).

## cross-program invocation (CPI) #

A call from one [onchain program](/ru/docs/terminology#onchain-program) to
another. For more information, see [calling between
programs](/ru/docs/core/cpi).

## data plane #

A multicast network used to efficiently validate
[entries](/ru/docs/terminology#entry) and gain consensus.

## drone #

An off-chain service that acts as a custodian for a user's private key. It
typically serves to validate and sign transactions.

## entry #

An entry on the [ledger](/ru/docs/terminology#ledger) either a
[tick](/ru/docs/terminology#tick) or a [transaction's
entry](/ru/docs/terminology#transactions-entry).

## entry id #

A preimage resistant [hash](/ru/docs/terminology#hash) over the final contents
of an entry, which acts as the [entry's](/ru/docs/terminology#entry) globally
unique identifier. The hash serves as evidence of:

  * The entry being generated after a duration of time
  * The specified [transactions](/ru/docs/terminology#transaction) are those included in the entry
  * The entry's position with respect to other entries in [ledger](/ru/docs/terminology#ledger)

See [proof of history](/ru/docs/terminology#proof-of-history-poh).

## epoch #

The time, i.e. number of [slots](/ru/docs/terminology#slot), for which a
[leader schedule](/ru/docs/terminology#leader-schedule) is valid.

## fee account #

The fee account in the transaction is the account that pays for the cost of
including the transaction in the ledger. This is the first account in the
transaction. This account must be declared as Read-Write (writable) in the
transaction since paying for the transaction reduces the account balance.

## finality #

When nodes representing 2/3rd of the [stake](/ru/docs/terminology#stake) have
a common [root](/ru/docs/terminology#root).

## fork #

A [ledger](/ru/docs/terminology#ledger) derived from common entries but then
diverged.

## genesis block #

The first [block](/ru/docs/terminology#block) in the chain.

## genesis config #

The configuration file that prepares the [ledger](/ru/docs/terminology#ledger)
for the [genesis block](/ru/docs/terminology#genesis-block).

## hash #

A digital fingerprint of a sequence of bytes.

## inflation #

An increase in token supply over time used to fund rewards for validation and
to fund continued development of Solana.

## inner instruction #

See [cross-program invocation](/ru/docs/terminology#cross-program-invocation-
cpi).

## instruction #

A call to invoke a specific [instruction
handler](/ru/docs/terminology#instruction-handler) in a
[program](/ru/docs/terminology#program). An instruction also specifies which
accounts it wants to read or modify, and additional data that serves as
auxiliary input to the [instruction handler](/ru/docs/terminology#instruction-
handler). A [client](/ru/docs/terminology#client) must include at least one
instruction in a [transaction](/ru/docs/terminology#transaction), and all
instructions must complete for the transaction to be considered successful.

## instruction handler #

Instruction handlers are [program](/ru/docs/terminology#program) functions
that process [instructions](/ru/docs/terminology#instruction) from
[transactions](/ru/docs/terminology#transaction). An instruction handler may
contain one or more [cross-program invocations](/ru/docs/terminology#cross-
program-invocation-cpi).

## keypair #

A [public key](/ru/docs/terminology#public-key-pubkey) and corresponding
[private key](/ru/docs/terminology#private-key) for accessing an account.

## lamport #

A fractional [native token](/ru/docs/terminology#native-token) with the value
of 0.000000001 [sol](/ru/docs/terminology#sol).

Info

Within the compute budget, a quantity of _[micro-
lamports](https://github.com/solana-
labs/solana/blob/ced8f6a512c61e0dd5308095ae8457add4a39e94/program-
runtime/src/prioritization_fee.rs#L1-L2)_ is used in the calculation of
[prioritization fees](/ru/docs/terminology#prioritization-fee).

## leader #

The role of a [validator](/ru/docs/terminology#validator) when it is appending
[entries](/ru/docs/terminology#entry) to the
[ledger](/ru/docs/terminology#ledger).

## leader schedule #

A sequence of [validator](/ru/docs/terminology#validator) [public
keys](/ru/docs/terminology#public-key-pubkey) mapped to
[slots](/ru/docs/terminology#slot). The cluster uses the leader schedule to
determine which validator is the [leader](/ru/docs/terminology#leader) at any
moment in time.

## ledger #

A list of [entries](/ru/docs/terminology#entry) containing
[transactions](/ru/docs/terminology#transaction) signed by
[clients](/ru/docs/terminology#client). Conceptually, this can be traced back
to the [genesis block](/ru/docs/terminology#genesis-block), but an actual
[validator](/ru/docs/terminology#validator)'s ledger may have only newer
[blocks](/ru/docs/terminology#block) to reduce storage, as older ones are not
needed for validation of future blocks by design.

## ledger vote #

A [hash](/ru/docs/terminology#hash) of the [validator's
state](/ru/docs/terminology#bank-state) at a given [tick
height](/ru/docs/terminology#tick-height). It comprises a
[validator's](/ru/docs/terminology#validator) affirmation that a
[block](/ru/docs/terminology#block) it has received has been verified, as well
as a promise not to vote for a conflicting [block](/ru/docs/terminology#block)
(i.e. [fork](/ru/docs/terminology#fork)) for a specific amount of time, the
[lockout](/ru/docs/terminology#lockout) period.

## light client #

A type of [client](/ru/docs/terminology#client) that can verify it's pointing
to a valid [cluster](/ru/docs/terminology#cluster). It performs more ledger
verification than a [thin client](/ru/docs/terminology#thin-client) and less
than a [validator](/ru/docs/terminology#validator).

## loader #

A [program](/ru/docs/terminology#program) with the ability to interpret the
binary encoding of other on-chain programs.

## lockout #

The duration of time for which a [validator](/ru/docs/terminology#validator)
is unable to [vote](/ru/docs/terminology#ledger-vote) on another
[fork](/ru/docs/terminology#fork).

## message #

The structured contents of a [transaction](/ru/docs/terminology#transaction).
Generally containing a header, array of account addresses, recent
[blockhash](/ru/docs/terminology#blockhash), and an array of
[instructions](/ru/docs/terminology#instruction).

Learn more about the [message formatting inside of
transactions](/ru/docs/core/transactions#message-header) here.

## Nakamoto coefficient #

A measure of decentralization, the Nakamoto Coefficient is the smallest number
of independent entities that can act collectively to shut down a blockchain.
The term was coined by Balaji S. Srinivasan and Leland Lee in [Quantifying
Decentralization](https://news.earn.com/quantifying-
decentralization-e39db233c28e).

## native token #

The [token](/ru/docs/terminology#token) used to track work done by
[nodes](/ru/docs/terminology#node) in a cluster.

## node #

A computer participating in a [cluster](/ru/docs/terminology#cluster).

## node count #

The number of [validators](/ru/docs/terminology#validator) participating in a
[cluster](/ru/docs/terminology#cluster).

## onchain program #

The executable code on Solana blockchain that interprets the
[instructions](/ru/docs/terminology#instruction) sent inside of each
[transaction](/ru/docs/terminology#transaction) to read and modify accounts
over which it has control. These programs are often referred to as "[_smart
contracts_](/ru/docs/core/programs)" on other blockchains.

## PoH #

See [Proof of History](/ru/docs/terminology#proof-of-history-poh).

## point #

A weighted [credit](/ru/docs/terminology#credit) in a rewards regime. In the
[validator](/ru/docs/terminology#validator) [rewards
regime](https://docs.solanalabs.com/consensus/stake-delegation-and-rewards),
the number of points owed to a [stake](/ru/docs/terminology#stake) during
redemption is the product of the [vote credits](/ru/docs/terminology#vote-
credit) earned and the number of lamports staked.

## private key #

The private key of a [keypair](/ru/docs/terminology#keypair).

## program #

See [onchain program](/ru/docs/terminology#onchain-program).

## program derived account (PDA) #

An account whose signing authority is a program and thus is not controlled by
a private key like other accounts.

## program id #

The public key of the [account](/ru/docs/terminology#account) containing a
[program](/ru/docs/terminology#program).

## proof of history (PoH) #

A stack of proofs, each of which proves that some data existed before the
proof was created and that a precise duration of time passed before the
previous proof. Like a [VDF](/ru/docs/terminology#verifiable-delay-function-
vdf), a Proof of History can be verified in less time than it took to produce.

## prioritization fee #

An additional fee user can specify in the compute budget
[instruction](/ru/docs/terminology#instruction) to prioritize their
[transactions](/ru/docs/terminology#transaction).

The prioritization fee is calculated by multiplying the requested maximum
compute units by the compute-unit price (specified in increments of 0.000001
lamports per compute unit) rounded up to the nearest lamport.

Transactions should request the minimum amount of compute units required for
execution to minimize fees.

## public key (pubkey) #

The public key of a [keypair](/ru/docs/terminology#keypair).

## rent #

Fee paid by [Accounts](/ru/docs/terminology#account) and
[Programs](/ru/docs/terminology#program) to store data on the blockchain. When
accounts do not have enough balance to pay rent, they may be Garbage
Collected.

See also [rent exempt](/ru/docs/terminology#rent-exempt) below. Learn more
about rent here: [What is rent?](/ru/docs/intro/rent).

## rent exempt #

Accounts that maintain a minimum lamport balance that is proportional to the
amount of data stored on the account. All newly created accounts are stored
on-chain permanently until the account is closed. It is not possible to create
an account that falls below the rent exemption threshold.

## root #

A [block](/ru/docs/terminology#block) or [slot](/ru/docs/terminology#slot)
that has reached maximum [lockout](/ru/docs/terminology#lockout) on a
[validator](/ru/docs/terminology#validator). The root is the highest block
that is an ancestor of all active forks on a validator. All ancestor blocks of
a root are also transitively a root. Blocks that are not an ancestor and not a
descendant of the root are excluded from consideration for consensus and can
be discarded.

## runtime #

The component of a [validator](/ru/docs/terminology#validator) responsible for
[program](/ru/docs/terminology#program) execution.

## Sealevel #

Solana's parallel run-time for [onchain
programs](/ru/docs/terminology#onchain-program).

## shred #

A fraction of a [block](/ru/docs/terminology#block); the smallest unit sent
between [validators](/ru/docs/terminology#validator).

## signature #

A 64-byte ed25519 signature of R (32-bytes) and S (32-bytes). With the
requirement that R is a packed Edwards point not of small order and S is a
scalar in the range of `0 <= S < L`. This requirement ensures no signature
malleability. Each transaction must have at least one signature for [fee
account](/ru/docs/terminology#fee-account). Thus, the first signature in
transaction can be treated as [transaction
id](/ru/docs/terminology#transaction-id)

## skip rate #

The percentage of [skipped slots](/ru/docs/terminology#skipped-slot) out of
the total leader slots in the current epoch. This metric can be misleading as
it has high variance after the epoch boundary when the sample size is small,
as well as for validators with a low number of leader slots, however can also
be useful in identifying node misconfigurations at times.

## skipped slot #

A past [slot](/ru/docs/terminology#slot) that did not produce a
[block](/ru/docs/terminology#block), because the leader was offline or the
[fork](/ru/docs/terminology#fork) containing the slot was abandoned for a
better alternative by cluster consensus. A skipped slot will not appear as an
ancestor for blocks at subsequent slots, nor increment the [block
height](/ru/docs/terminology#block-height), nor expire the oldest
`recent_blockhash`.

Whether a slot has been skipped can only be determined when it becomes older
than the latest [rooted](/ru/docs/terminology#root) (thus not-skipped) slot.

## slot #

The period of time for which each [leader](/ru/docs/terminology#leader)
ingests transactions and produces a [block](/ru/docs/terminology#block).

Collectively, slots create a logical clock. Slots are ordered sequentially and
non-overlapping, comprising roughly equal real-world time as per
[PoH](/ru/docs/terminology#proof-of-history-poh).

## smart contract #

See [onchain program](/ru/docs/terminology#onchain-program).

## sol #

The [native token](/ru/docs/terminology#native-token) of a Solana
[cluster](/ru/docs/terminology#cluster).

## Solana Program Library (SPL) #

A [library of programs](https://spl.solana.com/) on Solana such as spl-token
that facilitates tasks such as creating and using tokens.

## stake #

Tokens forfeit to the [cluster](/ru/docs/terminology#cluster) if malicious
[validator](/ru/docs/terminology#validator) behavior can be proven.

## stake-weighted quality of service (SWQoS) #

SWQoS allows [preferential treatment for transactions that come from staked
validators](/ru/developers/guides/advanced/stake-weighted-qos).

## supermajority #

2/3 of a [cluster](/ru/docs/terminology#cluster).

## sysvar #

A system [account](/ru/docs/terminology#account).
[Sysvars](https://docs.solanalabs.com/runtime/sysvars) provide cluster state
information such as current tick height, rewards
[points](/ru/docs/terminology#point) values, etc. Programs can access Sysvars
via a Sysvar account (pubkey) or by querying via a syscall.

## thin client #

A type of [client](/ru/docs/terminology#client) that trusts it is
communicating with a valid [cluster](/ru/docs/terminology#cluster).

## tick #

A ledger [entry](/ru/docs/terminology#entry) that estimates wallclock
duration.

## tick height #

The Nth [tick](/ru/docs/terminology#tick) in the
[ledger](/ru/docs/terminology#ledger).

## token #

A digitally transferable asset.

## Token Extensions Program #

The [Token Extensions Program](https://spl.solana.com/token-2022) has the
program ID `TokenzQdBNbLqP5VEhdkAS6EPFLC1PHnBqCXEpPxuEb` and includes all the
same features as the [Token Program](/ru/docs/terminology#token-program), but
comes with extensions such as confidential transfers, custom transfer logic,
extended metadata, and much more.

## Token Program #

The [Token Program](https://spl.solana.com/token) has the program ID
`TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA`, and provides the basic
capabilities of transferring, freezing, and minting tokens.

## tps #

[Transactions](/ru/docs/terminology#transaction) per second.

## tpu #

[Transaction processing unit](https://docs.solanalabs.com/validator/tpu).

## transaction #

One or more [instructions](/ru/docs/terminology#instruction) signed by a
[client](/ru/docs/terminology#client) using one or more
[keypairs](/ru/docs/terminology#keypair) and executed atomically with only two
possible outcomes: success or failure.

## transaction id #

The first [signature](/ru/docs/terminology#signature) in a
[transaction](/ru/docs/terminology#transaction), which can be used to uniquely
identify the transaction across the complete
[ledger](/ru/docs/terminology#ledger).

## transaction confirmations #

The number of [confirmed blocks](/ru/docs/terminology#confirmed-block) since
the transaction was accepted onto the [ledger](/ru/docs/terminology#ledger). A
transaction is finalized when its block becomes a
[root](/ru/docs/terminology#root).

## transactions entry #

A set of [transactions](/ru/docs/terminology#transaction) that may be executed
in parallel.

## tvu #

[Transaction validation unit](https://docs.solanalabs.com/validator/tvu).

## validator #

A full participant in a Solana network [cluster](/ru/docs/terminology#cluster)
that produces new [blocks](/ru/docs/terminology#block). A validator validates
the transactions added to the [ledger](/ru/docs/terminology#ledger)

## VDF #

See [verifiable delay function](/ru/docs/terminology#verifiable-delay-
function-vdf).

## verifiable delay function (VDF) #

A function that takes a fixed amount of time to execute that produces a proof
that it ran, which can then be verified in less time than it took to produce.

## vote #

See [ledger vote](/ru/docs/terminology#ledger-vote).

## vote credit #

A reward tally for [validators](/ru/docs/terminology#validator). A vote credit
is awarded to a validator in its vote account when the validator reaches a
[root](/ru/docs/terminology#root).

## wallet #

A collection of [keypairs](/ru/docs/terminology#keypair) that allows users to
manage their funds.

## warmup period #

Some number of [epochs](/ru/docs/terminology#epoch) after
[stake](/ru/docs/terminology#stake) has been delegated while it progressively
becomes effective. During this period, the stake is considered to be
"activating". More info about: [warmup and
cooldown](https://docs.solanalabs.com/consensus/stake-delegation-and-
rewards#stake-warmup-cooldown-withdrawal)

[Previous« JSON RPC Methods](/ru/docs/rpc)[NextOverview
»](/ru/docs/intro/overview)

  * [Solana Documentation](/ru/docs)

    * [JSON RPC Methods](/ru/docs/rpc)
    * [Terminology](/ru/docs/terminology)
  * Introduction

    * [Overview](/ru/docs/intro/overview)
    * [Wallets](/ru/docs/intro/wallets)
    * [Intro to Development](/ru/docs/intro/dev)
  * Core Concepts

    * [Solana Account Model](/ru/docs/core/accounts)
    * [Transactions and Instructions](/ru/docs/core/transactions)
    * [Fees on Solana](/ru/docs/core/fees)
    * [Programs on Solana](/ru/docs/core/programs)
    * [Program Derived Address](/ru/docs/core/pda)
    * [Cross Program Invocation](/ru/docs/core/cpi)
    * [Tokens on Solana](/ru/docs/core/tokens)
    * [Clusters & Endpoints](/ru/docs/core/clusters)
  * Advanced Concepts

    * [Versioned Transactions](/ru/docs/advanced/versions)
    * [Address Lookup Tables](/ru/docs/advanced/lookup-tables)
    * [Confirmation & Expiration](/ru/docs/advanced/confirmation)
    * [Retrying Transactions](/ru/docs/advanced/retry)
    * [State Compression](/ru/docs/advanced/state-compression)
  * Solana Clients

    * [Rust](/ru/docs/clients/rust)
    * [JavaScript / TypeScript](/ru/docs/clients/javascript)
    * [Web3.js API Examples](/ru/docs/clients/javascript-reference)
  * [Economics](/ru/docs/economics)

    * Inflation
      * [Proposed Inflation Schedule](/ru/docs/economics/inflation/inflation-schedule)
      * [Inflation Terminology](/ru/docs/economics/inflation/terminology)
    * [Staking](/ru/docs/economics/staking)
      * [Stake Accounts](/ru/docs/economics/staking/stake-accounts)
      * [Stake Programming](/ru/docs/economics/staking/stake-programming)
  * Developing Programs

    * [Overview](/ru/docs/programs/overview)
    * [Debugging Programs](/ru/docs/programs/debugging)
    * [Deploying Programs](/ru/docs/programs/deploying)
    * [Program Examples](/ru/docs/programs/examples)
    * [FAQ](/ru/docs/programs/faq)
    * [Developing with C](/ru/docs/programs/lang-c)
    * [Developing with Rust](/ru/docs/programs/lang-rust)
    * [Limitations](/ru/docs/programs/limitations)
  * More Information

    * [Add Solana to Your Exchange](/ru/docs/more/exchange)

Managed by

[](/ru)

[](/youtube)[](/twitter)[](/discord)[](/reddit)[](/github)[](/telegram)

© 2024 Solana Foundation. All rights reserved.

Solana

  * [Гранты](https://solana.org/grants)
  * [Break Solana](https://break.solana.com/)
  * [Media Kit](/ru/branding)
  * [Вакансии](https://jobs.solana.com/)
  * [Отказ от ответственности](/ru/tos)
  * [Privacy Policy](/ru/privacy-policy)

Get Connected

  * [проектов и их число растёт](/ru/ecosystem)
  * [Блог](/ru/news)
  * [Рассылка](/ru/newsletter)

ru

© 2024 Solana Foundation. All rights reserved.

