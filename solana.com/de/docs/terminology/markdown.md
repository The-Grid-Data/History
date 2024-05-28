This website uses cookies to offer you a better browsing experience. Find out
more on how we use cookies.

Opt-out[Details](/de/privacy-policy#collection-of-information)

Accept

[![Solana](/_next/static/media/logotype-dark.f79d530d.svg)](/de)

  * Learn
  * Developers
  * Solutions
  * Network
  * Community

Search```K`

[Documentation](/de/docs)[RPC
API](/de/docs/rpc)[Cookbook](/de/developers/cookbook)[Guides](/de/developers/guides)[Terminology](/de/docs/terminology)

##### Table of Contents

  * [account](/de/docs/terminology#account)
  * [account owner](/de/docs/terminology#account-owner)
  * [app](/de/docs/terminology#app)
  * [bank state](/de/docs/terminology#bank-state)
  * [block](/de/docs/terminology#block)
  * [blockhash](/de/docs/terminology#blockhash)
  * [block height](/de/docs/terminology#block-height)
  * [bootstrap validator](/de/docs/terminology#bootstrap-validator)
  * [BPF loader](/de/docs/terminology#bpf-loader)
  * [client](/de/docs/terminology#client)
  * [commitment](/de/docs/terminology#commitment)
  * [cluster](/de/docs/terminology#cluster)
  * [compute budget](/de/docs/terminology#compute-budget)
  * [compute units](/de/docs/terminology#compute-units)
  * [confirmation time](/de/docs/terminology#confirmation-time)
  * [confirmed block](/de/docs/terminology#confirmed-block)
  * [control plane](/de/docs/terminology#control-plane)
  * [cooldown period](/de/docs/terminology#cooldown-period)
  * [credit](/de/docs/terminology#credit)
  * [cross-program invocation (CPI](/de/docs/terminology#cross-program-invocation-cpi)
  * [data plane](/de/docs/terminology#data-plane)
  * [drone](/de/docs/terminology#drone)
  * [entry](/de/docs/terminology#entry)
  * [entry id](/de/docs/terminology#entry-id)
  * [epoch](/de/docs/terminology#epoch)
  * [fee account](/de/docs/terminology#fee-account)
  * [finality](/de/docs/terminology#finality)
  * [fork](/de/docs/terminology#fork)
  * [genesis block](/de/docs/terminology#genesis-block)
  * [genesis config](/de/docs/terminology#genesis-config)
  * [hash](/de/docs/terminology#hash)
  * [inflation](/de/docs/terminology#inflation)
  * [inner instruction](/de/docs/terminology#inner-instruction)
  * [instruction](/de/docs/terminology#instruction)
  * [instruction handler](/de/docs/terminology#instruction-handler)
  * [keypair](/de/docs/terminology#keypair)
  * [lamport](/de/docs/terminology#lamport)
  * [leader](/de/docs/terminology#leader)
  * [leader schedule](/de/docs/terminology#leader-schedule)
  * [ledger](/de/docs/terminology#ledger)
  * [ledger vote](/de/docs/terminology#ledger-vote)
  * [light client](/de/docs/terminology#light-client)
  * [loader](/de/docs/terminology#loader)
  * [lockout](/de/docs/terminology#lockout)
  * [message](/de/docs/terminology#message)
  * [Nakamoto coefficient](/de/docs/terminology#nakamoto-coefficient)
  * [native token](/de/docs/terminology#native-token)
  * [node](/de/docs/terminology#node)
  * [node count](/de/docs/terminology#node-count)
  * [onchain program](/de/docs/terminology#onchain-program)
  * [PoH](/de/docs/terminology#poh)
  * [point](/de/docs/terminology#point)
  * [private key](/de/docs/terminology#private-key)
  * [program](/de/docs/terminology#program)
  * [program derived account (PDA](/de/docs/terminology#program-derived-account-pda)
  * [program id](/de/docs/terminology#program-id)
  * [proof of history (PoH](/de/docs/terminology#proof-of-history-poh)
  * [prioritization fee](/de/docs/terminology#prioritization-fee)
  * [public key (pubkey](/de/docs/terminology#public-key-pubkey)
  * [rent](/de/docs/terminology#rent)
  * [rent exempt](/de/docs/terminology#rent-exempt)
  * [root](/de/docs/terminology#root)
  * [runtime](/de/docs/terminology#runtime)
  * [Sealevel](/de/docs/terminology#sealevel)
  * [shred](/de/docs/terminology#shred)
  * [signature](/de/docs/terminology#signature)
  * [skip rate](/de/docs/terminology#skip-rate)
  * [skipped slot](/de/docs/terminology#skipped-slot)
  * [slot](/de/docs/terminology#slot)
  * [smart contract](/de/docs/terminology#smart-contract)
  * [sol](/de/docs/terminology#sol)
  * [Solana Program Library (SPL](/de/docs/terminology#solana-program-library-spl)
  * [stake](/de/docs/terminology#stake)
  * [stake-weighted quality of service (SWQoS](/de/docs/terminology#stake-weighted-quality-of-service-swqos)
  * [supermajority](/de/docs/terminology#supermajority)
  * [sysvar](/de/docs/terminology#sysvar)
  * [thin client](/de/docs/terminology#thin-client)
  * [tick](/de/docs/terminology#tick)
  * [tick height](/de/docs/terminology#tick-height)
  * [token](/de/docs/terminology#token)
  * [Token Extensions Program](/de/docs/terminology#token-extensions-program)
  * [Token Program](/de/docs/terminology#token-program)
  * [tps](/de/docs/terminology#tps)
  * [tpu](/de/docs/terminology#tpu)
  * [transaction](/de/docs/terminology#transaction)
  * [transaction id](/de/docs/terminology#transaction-id)
  * [transaction confirmations](/de/docs/terminology#transaction-confirmations)
  * [transactions entry](/de/docs/terminology#transactions-entry)
  * [tvu](/de/docs/terminology#tvu)
  * [validator](/de/docs/terminology#validator)
  * [VDF](/de/docs/terminology#vdf)
  * [verifiable delay function (VDF](/de/docs/terminology#verifiable-delay-function-vdf)
  * [vote](/de/docs/terminology#vote)
  * [vote credit](/de/docs/terminology#vote-credit)
  * [wallet](/de/docs/terminology#wallet)
  * [warmup period](/de/docs/terminology#warmup-period)

[Scroll to Top](/de/docs/terminology#)

[Edit Page](https://github.com/solana-foundation/developer-
content/tree/main/docs/terminology.md)

[Home](/de)>[Solana Dokumentation](/de/docs)

# [Terminology](/de/docs/terminology)

The following terms are used throughout the Solana documentation and
development ecosystem.

## account #

A record in the Solana ledger that either holds data or is an executable
program.

Like an account at a traditional bank, a Solana account may hold funds called
[lamports](/de/docs/terminology#lamport). Like a file in Linux, it is
addressable by a key, often referred to as a [public
key](/de/docs/terminology#public-key-pubkey) or pubkey.

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
height](/de/docs/terminology#tick-height). It includes at least the set of all
[accounts](/de/docs/terminology#account) holding nonzero [native
tokens](/de/docs/terminology#native-token).

## block #

A contiguous set of [entries](/de/docs/terminology#entry) on the ledger
covered by a [vote](/de/docs/terminology#ledger-vote). A
[leader](/de/docs/terminology#leader) produces at most one block per
[slot](/de/docs/terminology#slot).

## blockhash #

A unique value ([hash](/de/docs/terminology#hash)) that identifies a record
(block). Solana computes a blockhash from the last [entry
id](/de/docs/terminology#entry-id) of the block.

## block height #

The number of [blocks](/de/docs/terminology#block) beneath the current block.
The first block after the [genesis block](/de/docs/terminology#genesis-block)
has height one.

## bootstrap validator #

The [validator](/de/docs/terminology#validator) that produces the genesis
(first) [block](/de/docs/terminology#block) of a block chain.

## BPF loader #

The Solana program that owns and loads [BPF](/de/docs/programs/faq#berkeley-
packet-filter-bpf) [onchain programs](/de/docs/terminology#onchain-program),
allowing the program to interface with the runtime.

## client #

A computer program that accesses the Solana server network
[cluster](/de/docs/terminology#cluster).

## commitment #

A measure of the network confirmation for the
[block](/de/docs/terminology#block).

## cluster #

A set of [validators](/de/docs/terminology#validator) maintaining a single
[ledger](/de/docs/terminology#ledger).

## compute budget #

The maximum number of [compute units](/de/docs/terminology#compute-units)
consumed per transaction.

## compute units #

The smallest unit of measure for consumption of computational resources of the
blockchain.

## confirmation time #

The wallclock duration between a [leader](/de/docs/terminology#leader)
creating a [tick entry](/de/docs/terminology#tick) and creating a [confirmed
block](/de/docs/terminology#confirmed-block).

## confirmed block #

A [block](/de/docs/terminology#block) that has received a [super
majority](/de/docs/terminology#supermajority) of [ledger
votes](/de/docs/terminology#ledger-vote).

## control plane #

A gossip network connecting all [nodes](/de/docs/terminology#node) of a
[cluster](/de/docs/terminology#cluster).

## cooldown period #

Some number of [epochs](/de/docs/terminology#epoch) after
[stake](/de/docs/terminology#stake) has been deactivated while it
progressively becomes available for withdrawal. During this period, the stake
is considered to be "deactivating". More info about: [warmup and
cooldown](https://docs.solanalabs.com/implemented-proposals/staking-
rewards#stake-warmup-cooldown-withdrawal)

## credit #

See [vote credit](/de/docs/terminology#vote-credit).

## cross-program invocation (CPI) #

A call from one [onchain program](/de/docs/terminology#onchain-program) to
another. For more information, see [calling between
programs](/de/docs/core/cpi).

## data plane #

A multicast network used to efficiently validate
[entries](/de/docs/terminology#entry) and gain consensus.

## drone #

An off-chain service that acts as a custodian for a user's private key. It
typically serves to validate and sign transactions.

## entry #

An entry on the [ledger](/de/docs/terminology#ledger) either a
[tick](/de/docs/terminology#tick) or a [transaction's
entry](/de/docs/terminology#transactions-entry).

## entry id #

A preimage resistant [hash](/de/docs/terminology#hash) over the final contents
of an entry, which acts as the [entry's](/de/docs/terminology#entry) globally
unique identifier. The hash serves as evidence of:

  * The entry being generated after a duration of time
  * The specified [transactions](/de/docs/terminology#transaction) are those included in the entry
  * The entry's position with respect to other entries in [ledger](/de/docs/terminology#ledger)

See [proof of history](/de/docs/terminology#proof-of-history-poh).

## epoch #

The time, i.e. number of [slots](/de/docs/terminology#slot), for which a
[leader schedule](/de/docs/terminology#leader-schedule) is valid.

## fee account #

The fee account in the transaction is the account that pays for the cost of
including the transaction in the ledger. This is the first account in the
transaction. This account must be declared as Read-Write (writable) in the
transaction since paying for the transaction reduces the account balance.

## finality #

When nodes representing 2/3rd of the [stake](/de/docs/terminology#stake) have
a common [root](/de/docs/terminology#root).

## fork #

A [ledger](/de/docs/terminology#ledger) derived from common entries but then
diverged.

## genesis block #

The first [block](/de/docs/terminology#block) in the chain.

## genesis config #

The configuration file that prepares the [ledger](/de/docs/terminology#ledger)
for the [genesis block](/de/docs/terminology#genesis-block).

## hash #

A digital fingerprint of a sequence of bytes.

## inflation #

An increase in token supply over time used to fund rewards for validation and
to fund continued development of Solana.

## inner instruction #

See [cross-program invocation](/de/docs/terminology#cross-program-invocation-
cpi).

## instruction #

A call to invoke a specific [instruction
handler](/de/docs/terminology#instruction-handler) in a
[program](/de/docs/terminology#program). An instruction also specifies which
accounts it wants to read or modify, and additional data that serves as
auxiliary input to the [instruction handler](/de/docs/terminology#instruction-
handler). A [client](/de/docs/terminology#client) must include at least one
instruction in a [transaction](/de/docs/terminology#transaction), and all
instructions must complete for the transaction to be considered successful.

## instruction handler #

Instruction handlers are [program](/de/docs/terminology#program) functions
that process [instructions](/de/docs/terminology#instruction) from
[transactions](/de/docs/terminology#transaction). An instruction handler may
contain one or more [cross-program invocations](/de/docs/terminology#cross-
program-invocation-cpi).

## keypair #

A [public key](/de/docs/terminology#public-key-pubkey) and corresponding
[private key](/de/docs/terminology#private-key) for accessing an account.

## lamport #

A fractional [native token](/de/docs/terminology#native-token) with the value
of 0.000000001 [sol](/de/docs/terminology#sol).

Info

Within the compute budget, a quantity of _[micro-
lamports](https://github.com/solana-
labs/solana/blob/ced8f6a512c61e0dd5308095ae8457add4a39e94/program-
runtime/src/prioritization_fee.rs#L1-L2)_ is used in the calculation of
[prioritization fees](/de/docs/terminology#prioritization-fee).

## leader #

The role of a [validator](/de/docs/terminology#validator) when it is appending
[entries](/de/docs/terminology#entry) to the
[ledger](/de/docs/terminology#ledger).

## leader schedule #

A sequence of [validator](/de/docs/terminology#validator) [public
keys](/de/docs/terminology#public-key-pubkey) mapped to
[slots](/de/docs/terminology#slot). The cluster uses the leader schedule to
determine which validator is the [leader](/de/docs/terminology#leader) at any
moment in time.

## ledger #

A list of [entries](/de/docs/terminology#entry) containing
[transactions](/de/docs/terminology#transaction) signed by
[clients](/de/docs/terminology#client). Conceptually, this can be traced back
to the [genesis block](/de/docs/terminology#genesis-block), but an actual
[validator](/de/docs/terminology#validator)'s ledger may have only newer
[blocks](/de/docs/terminology#block) to reduce storage, as older ones are not
needed for validation of future blocks by design.

## ledger vote #

A [hash](/de/docs/terminology#hash) of the [validator's
state](/de/docs/terminology#bank-state) at a given [tick
height](/de/docs/terminology#tick-height). It comprises a
[validator's](/de/docs/terminology#validator) affirmation that a
[block](/de/docs/terminology#block) it has received has been verified, as well
as a promise not to vote for a conflicting [block](/de/docs/terminology#block)
(i.e. [fork](/de/docs/terminology#fork)) for a specific amount of time, the
[lockout](/de/docs/terminology#lockout) period.

## light client #

A type of [client](/de/docs/terminology#client) that can verify it's pointing
to a valid [cluster](/de/docs/terminology#cluster). It performs more ledger
verification than a [thin client](/de/docs/terminology#thin-client) and less
than a [validator](/de/docs/terminology#validator).

## loader #

A [program](/de/docs/terminology#program) with the ability to interpret the
binary encoding of other on-chain programs.

## lockout #

The duration of time for which a [validator](/de/docs/terminology#validator)
is unable to [vote](/de/docs/terminology#ledger-vote) on another
[fork](/de/docs/terminology#fork).

## message #

The structured contents of a [transaction](/de/docs/terminology#transaction).
Generally containing a header, array of account addresses, recent
[blockhash](/de/docs/terminology#blockhash), and an array of
[instructions](/de/docs/terminology#instruction).

Learn more about the [message formatting inside of
transactions](/de/docs/core/transactions#message-header) here.

## Nakamoto coefficient #

A measure of decentralization, the Nakamoto Coefficient is the smallest number
of independent entities that can act collectively to shut down a blockchain.
The term was coined by Balaji S. Srinivasan and Leland Lee in [Quantifying
Decentralization](https://news.earn.com/quantifying-
decentralization-e39db233c28e).

## native token #

The [token](/de/docs/terminology#token) used to track work done by
[nodes](/de/docs/terminology#node) in a cluster.

## node #

A computer participating in a [cluster](/de/docs/terminology#cluster).

## node count #

The number of [validators](/de/docs/terminology#validator) participating in a
[cluster](/de/docs/terminology#cluster).

## onchain program #

The executable code on Solana blockchain that interprets the
[instructions](/de/docs/terminology#instruction) sent inside of each
[transaction](/de/docs/terminology#transaction) to read and modify accounts
over which it has control. These programs are often referred to as "[_smart
contracts_](/de/docs/core/programs)" on other blockchains.

## PoH #

See [Proof of History](/de/docs/terminology#proof-of-history-poh).

## point #

A weighted [credit](/de/docs/terminology#credit) in a rewards regime. In the
[validator](/de/docs/terminology#validator) [rewards
regime](https://docs.solanalabs.com/consensus/stake-delegation-and-rewards),
the number of points owed to a [stake](/de/docs/terminology#stake) during
redemption is the product of the [vote credits](/de/docs/terminology#vote-
credit) earned and the number of lamports staked.

## private key #

The private key of a [keypair](/de/docs/terminology#keypair).

## program #

See [onchain program](/de/docs/terminology#onchain-program).

## program derived account (PDA) #

An account whose signing authority is a program and thus is not controlled by
a private key like other accounts.

## program id #

The public key of the [account](/de/docs/terminology#account) containing a
[program](/de/docs/terminology#program).

## proof of history (PoH) #

A stack of proofs, each of which proves that some data existed before the
proof was created and that a precise duration of time passed before the
previous proof. Like a [VDF](/de/docs/terminology#verifiable-delay-function-
vdf), a Proof of History can be verified in less time than it took to produce.

## prioritization fee #

An additional fee user can specify in the compute budget
[instruction](/de/docs/terminology#instruction) to prioritize their
[transactions](/de/docs/terminology#transaction).

The prioritization fee is calculated by multiplying the requested maximum
compute units by the compute-unit price (specified in increments of 0.000001
lamports per compute unit) rounded up to the nearest lamport.

Transactions should request the minimum amount of compute units required for
execution to minimize fees.

## public key (pubkey) #

The public key of a [keypair](/de/docs/terminology#keypair).

## rent #

Fee paid by [Accounts](/de/docs/terminology#account) and
[Programs](/de/docs/terminology#program) to store data on the blockchain. When
accounts do not have enough balance to pay rent, they may be Garbage
Collected.

See also [rent exempt](/de/docs/terminology#rent-exempt) below. Learn more
about rent here: [What is rent?](/de/docs/intro/rent).

## rent exempt #

Accounts that maintain a minimum lamport balance that is proportional to the
amount of data stored on the account. All newly created accounts are stored
on-chain permanently until the account is closed. It is not possible to create
an account that falls below the rent exemption threshold.

## root #

A [block](/de/docs/terminology#block) or [slot](/de/docs/terminology#slot)
that has reached maximum [lockout](/de/docs/terminology#lockout) on a
[validator](/de/docs/terminology#validator). The root is the highest block
that is an ancestor of all active forks on a validator. All ancestor blocks of
a root are also transitively a root. Blocks that are not an ancestor and not a
descendant of the root are excluded from consideration for consensus and can
be discarded.

## runtime #

The component of a [validator](/de/docs/terminology#validator) responsible for
[program](/de/docs/terminology#program) execution.

## Sealevel #

Solana's parallel run-time for [onchain
programs](/de/docs/terminology#onchain-program).

## shred #

A fraction of a [block](/de/docs/terminology#block); the smallest unit sent
between [validators](/de/docs/terminology#validator).

## signature #

A 64-byte ed25519 signature of R (32-bytes) and S (32-bytes). With the
requirement that R is a packed Edwards point not of small order and S is a
scalar in the range of `0 <= S < L`. This requirement ensures no signature
malleability. Each transaction must have at least one signature for [fee
account](/de/docs/terminology#fee-account). Thus, the first signature in
transaction can be treated as [transaction
id](/de/docs/terminology#transaction-id)

## skip rate #

The percentage of [skipped slots](/de/docs/terminology#skipped-slot) out of
the total leader slots in the current epoch. This metric can be misleading as
it has high variance after the epoch boundary when the sample size is small,
as well as for validators with a low number of leader slots, however can also
be useful in identifying node misconfigurations at times.

## skipped slot #

A past [slot](/de/docs/terminology#slot) that did not produce a
[block](/de/docs/terminology#block), because the leader was offline or the
[fork](/de/docs/terminology#fork) containing the slot was abandoned for a
better alternative by cluster consensus. A skipped slot will not appear as an
ancestor for blocks at subsequent slots, nor increment the [block
height](/de/docs/terminology#block-height), nor expire the oldest
`recent_blockhash`.

Whether a slot has been skipped can only be determined when it becomes older
than the latest [rooted](/de/docs/terminology#root) (thus not-skipped) slot.

## slot #

The period of time for which each [leader](/de/docs/terminology#leader)
ingests transactions and produces a [block](/de/docs/terminology#block).

Collectively, slots create a logical clock. Slots are ordered sequentially and
non-overlapping, comprising roughly equal real-world time as per
[PoH](/de/docs/terminology#proof-of-history-poh).

## smart contract #

See [onchain program](/de/docs/terminology#onchain-program).

## sol #

The [native token](/de/docs/terminology#native-token) of a Solana
[cluster](/de/docs/terminology#cluster).

## Solana Program Library (SPL) #

A [library of programs](https://spl.solana.com/) on Solana such as spl-token
that facilitates tasks such as creating and using tokens.

## stake #

Tokens forfeit to the [cluster](/de/docs/terminology#cluster) if malicious
[validator](/de/docs/terminology#validator) behavior can be proven.

## stake-weighted quality of service (SWQoS) #

SWQoS allows [preferential treatment for transactions that come from staked
validators](/de/developers/guides/advanced/stake-weighted-qos).

## supermajority #

2/3 of a [cluster](/de/docs/terminology#cluster).

## sysvar #

A system [account](/de/docs/terminology#account).
[Sysvars](https://docs.solanalabs.com/runtime/sysvars) provide cluster state
information such as current tick height, rewards
[points](/de/docs/terminology#point) values, etc. Programs can access Sysvars
via a Sysvar account (pubkey) or by querying via a syscall.

## thin client #

A type of [client](/de/docs/terminology#client) that trusts it is
communicating with a valid [cluster](/de/docs/terminology#cluster).

## tick #

A ledger [entry](/de/docs/terminology#entry) that estimates wallclock
duration.

## tick height #

The Nth [tick](/de/docs/terminology#tick) in the
[ledger](/de/docs/terminology#ledger).

## token #

A digitally transferable asset.

## Token Extensions Program #

The [Token Extensions Program](https://spl.solana.com/token-2022) has the
program ID `TokenzQdBNbLqP5VEhdkAS6EPFLC1PHnBqCXEpPxuEb` and includes all the
same features as the [Token Program](/de/docs/terminology#token-program), but
comes with extensions such as confidential transfers, custom transfer logic,
extended metadata, and much more.

## Token Program #

The [Token Program](https://spl.solana.com/token) has the program ID
`TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA`, and provides the basic
capabilities of transferring, freezing, and minting tokens.

## tps #

[Transactions](/de/docs/terminology#transaction) per second.

## tpu #

[Transaction processing unit](https://docs.solanalabs.com/validator/tpu).

## transaction #

One or more [instructions](/de/docs/terminology#instruction) signed by a
[client](/de/docs/terminology#client) using one or more
[keypairs](/de/docs/terminology#keypair) and executed atomically with only two
possible outcomes: success or failure.

## transaction id #

The first [signature](/de/docs/terminology#signature) in a
[transaction](/de/docs/terminology#transaction), which can be used to uniquely
identify the transaction across the complete
[ledger](/de/docs/terminology#ledger).

## transaction confirmations #

The number of [confirmed blocks](/de/docs/terminology#confirmed-block) since
the transaction was accepted onto the [ledger](/de/docs/terminology#ledger). A
transaction is finalized when its block becomes a
[root](/de/docs/terminology#root).

## transactions entry #

A set of [transactions](/de/docs/terminology#transaction) that may be executed
in parallel.

## tvu #

[Transaction validation unit](https://docs.solanalabs.com/validator/tvu).

## validator #

A full participant in a Solana network [cluster](/de/docs/terminology#cluster)
that produces new [blocks](/de/docs/terminology#block). A validator validates
the transactions added to the [ledger](/de/docs/terminology#ledger)

## VDF #

See [verifiable delay function](/de/docs/terminology#verifiable-delay-
function-vdf).

## verifiable delay function (VDF) #

A function that takes a fixed amount of time to execute that produces a proof
that it ran, which can then be verified in less time than it took to produce.

## vote #

See [ledger vote](/de/docs/terminology#ledger-vote).

## vote credit #

A reward tally for [validators](/de/docs/terminology#validator). A vote credit
is awarded to a validator in its vote account when the validator reaches a
[root](/de/docs/terminology#root).

## wallet #

A collection of [keypairs](/de/docs/terminology#keypair) that allows users to
manage their funds.

## warmup period #

Some number of [epochs](/de/docs/terminology#epoch) after
[stake](/de/docs/terminology#stake) has been delegated while it progressively
becomes effective. During this period, the stake is considered to be
"activating". More info about: [warmup and
cooldown](https://docs.solanalabs.com/consensus/stake-delegation-and-
rewards#stake-warmup-cooldown-withdrawal)

[Previous« JSON RPC Methods](/de/docs/rpc)[NextOverview
»](/de/docs/intro/overview)

  * [Solana Dokumentation](/de/docs)

    * [JSON RPC Methods](/de/docs/rpc)
    * [Terminology](/de/docs/terminology)
  * Introduction

    * [Overview](/de/docs/intro/overview)
    * [Wallets](/de/docs/intro/wallets)
    * [Intro to Development](/de/docs/intro/dev)
  * Core Concepts

    * [Solana Account Model](/de/docs/core/accounts)
    * [Transactions and Instructions](/de/docs/core/transactions)
    * [Fees on Solana](/de/docs/core/fees)
    * [Programs on Solana](/de/docs/core/programs)
    * [Program Derived Address](/de/docs/core/pda)
    * [Cross Program Invocation](/de/docs/core/cpi)
    * [Tokens on Solana](/de/docs/core/tokens)
    * [Clusters & Endpoints](/de/docs/core/clusters)
  * Advanced Concepts

    * [Versioned Transactions](/de/docs/advanced/versions)
    * [Address Lookup Tables](/de/docs/advanced/lookup-tables)
    * [Confirmation & Expiration](/de/docs/advanced/confirmation)
    * [Retrying Transactions](/de/docs/advanced/retry)
    * [State Compression](/de/docs/advanced/state-compression)
  * Solana Clients

    * [Rust](/de/docs/clients/rust)
    * [JavaScript / TypeScript](/de/docs/clients/javascript)
    * [Web3.js API Examples](/de/docs/clients/javascript-reference)
  * [Economics](/de/docs/economics)

    * Inflation
      * [Proposed Inflation Schedule](/de/docs/economics/inflation/inflation-schedule)
      * [Inflation Terminology](/de/docs/economics/inflation/terminology)
    * [Staking](/de/docs/economics/staking)
      * [Stake Accounts](/de/docs/economics/staking/stake-accounts)
      * [Stake Programming](/de/docs/economics/staking/stake-programming)
  * Developing Programs

    * [Overview](/de/docs/programs/overview)
    * [Debugging Programs](/de/docs/programs/debugging)
    * [Deploying Programs](/de/docs/programs/deploying)
    * [Program Examples](/de/docs/programs/examples)
    * [FAQ](/de/docs/programs/faq)
    * [Developing with C](/de/docs/programs/lang-c)
    * [Developing with Rust](/de/docs/programs/lang-rust)
    * [Limitations](/de/docs/programs/limitations)
  * More Information

    * [Add Solana to Your Exchange](/de/docs/more/exchange)

Managed by

[](/de)

[](/youtube)[](/twitter)[](/discord)[](/reddit)[](/github)[](/telegram)

© 2024 Solana Foundation. All rights reserved.

Solana

  * [Fördermittel](https://solana.org/grants)
  * [Break Solana](https://break.solana.com/)
  * [Media Kit](/de/branding)
  * [Karriere](https://jobs.solana.com/)
  * [Haftungsausschluss](/de/tos)
  * [Privacy Policy](/de/privacy-policy)

Get Connected

  * [Ökosystem](/de/ecosystem)
  * [Blog](/de/news)
  * [Newsletter](/de/newsletter)

de

© 2024 Solana Foundation. All rights reserved.

