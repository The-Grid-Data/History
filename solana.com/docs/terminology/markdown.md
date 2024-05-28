This website uses cookies to offer you a better browsing experience. Find out
more on how we use cookies.

Opt-out[Details](/privacy-policy#collection-of-information)

Accept

[![Solana](/_next/static/media/logotype-dark.f79d530d.svg)](/)

  * Learn
  * Developers
  * Solutions
  * Network
  * Community

Search```K`

[Documentation](/docs)[RPC
API](/docs/rpc)[Cookbook](/developers/cookbook)[Guides](/developers/guides)[Terminology](/docs/terminology)

##### Table of Contents

  * [account](/docs/terminology#account)
  * [account owner](/docs/terminology#account-owner)
  * [app](/docs/terminology#app)
  * [bank state](/docs/terminology#bank-state)
  * [block](/docs/terminology#block)
  * [blockhash](/docs/terminology#blockhash)
  * [block height](/docs/terminology#block-height)
  * [bootstrap validator](/docs/terminology#bootstrap-validator)
  * [BPF loader](/docs/terminology#bpf-loader)
  * [client](/docs/terminology#client)
  * [commitment](/docs/terminology#commitment)
  * [cluster](/docs/terminology#cluster)
  * [compute budget](/docs/terminology#compute-budget)
  * [compute units](/docs/terminology#compute-units)
  * [confirmation time](/docs/terminology#confirmation-time)
  * [confirmed block](/docs/terminology#confirmed-block)
  * [control plane](/docs/terminology#control-plane)
  * [cooldown period](/docs/terminology#cooldown-period)
  * [credit](/docs/terminology#credit)
  * [cross-program invocation (CPI](/docs/terminology#cross-program-invocation-cpi)
  * [data plane](/docs/terminology#data-plane)
  * [drone](/docs/terminology#drone)
  * [entry](/docs/terminology#entry)
  * [entry id](/docs/terminology#entry-id)
  * [epoch](/docs/terminology#epoch)
  * [fee account](/docs/terminology#fee-account)
  * [finality](/docs/terminology#finality)
  * [fork](/docs/terminology#fork)
  * [genesis block](/docs/terminology#genesis-block)
  * [genesis config](/docs/terminology#genesis-config)
  * [hash](/docs/terminology#hash)
  * [inflation](/docs/terminology#inflation)
  * [inner instruction](/docs/terminology#inner-instruction)
  * [instruction](/docs/terminology#instruction)
  * [instruction handler](/docs/terminology#instruction-handler)
  * [keypair](/docs/terminology#keypair)
  * [lamport](/docs/terminology#lamport)
  * [leader](/docs/terminology#leader)
  * [leader schedule](/docs/terminology#leader-schedule)
  * [ledger](/docs/terminology#ledger)
  * [ledger vote](/docs/terminology#ledger-vote)
  * [light client](/docs/terminology#light-client)
  * [loader](/docs/terminology#loader)
  * [lockout](/docs/terminology#lockout)
  * [message](/docs/terminology#message)
  * [Nakamoto coefficient](/docs/terminology#nakamoto-coefficient)
  * [native token](/docs/terminology#native-token)
  * [node](/docs/terminology#node)
  * [node count](/docs/terminology#node-count)
  * [onchain program](/docs/terminology#onchain-program)
  * [PoH](/docs/terminology#poh)
  * [point](/docs/terminology#point)
  * [private key](/docs/terminology#private-key)
  * [program](/docs/terminology#program)
  * [program derived account (PDA](/docs/terminology#program-derived-account-pda)
  * [program id](/docs/terminology#program-id)
  * [proof of history (PoH](/docs/terminology#proof-of-history-poh)
  * [prioritization fee](/docs/terminology#prioritization-fee)
  * [public key (pubkey](/docs/terminology#public-key-pubkey)
  * [rent](/docs/terminology#rent)
  * [rent exempt](/docs/terminology#rent-exempt)
  * [root](/docs/terminology#root)
  * [runtime](/docs/terminology#runtime)
  * [Sealevel](/docs/terminology#sealevel)
  * [shred](/docs/terminology#shred)
  * [signature](/docs/terminology#signature)
  * [skip rate](/docs/terminology#skip-rate)
  * [skipped slot](/docs/terminology#skipped-slot)
  * [slot](/docs/terminology#slot)
  * [smart contract](/docs/terminology#smart-contract)
  * [sol](/docs/terminology#sol)
  * [Solana Program Library (SPL](/docs/terminology#solana-program-library-spl)
  * [stake](/docs/terminology#stake)
  * [stake-weighted quality of service (SWQoS](/docs/terminology#stake-weighted-quality-of-service-swqos)
  * [supermajority](/docs/terminology#supermajority)
  * [sysvar](/docs/terminology#sysvar)
  * [thin client](/docs/terminology#thin-client)
  * [tick](/docs/terminology#tick)
  * [tick height](/docs/terminology#tick-height)
  * [token](/docs/terminology#token)
  * [Token Extensions Program](/docs/terminology#token-extensions-program)
  * [Token Program](/docs/terminology#token-program)
  * [tps](/docs/terminology#tps)
  * [tpu](/docs/terminology#tpu)
  * [transaction](/docs/terminology#transaction)
  * [transaction id](/docs/terminology#transaction-id)
  * [transaction confirmations](/docs/terminology#transaction-confirmations)
  * [transactions entry](/docs/terminology#transactions-entry)
  * [tvu](/docs/terminology#tvu)
  * [validator](/docs/terminology#validator)
  * [VDF](/docs/terminology#vdf)
  * [verifiable delay function (VDF](/docs/terminology#verifiable-delay-function-vdf)
  * [vote](/docs/terminology#vote)
  * [vote credit](/docs/terminology#vote-credit)
  * [wallet](/docs/terminology#wallet)
  * [warmup period](/docs/terminology#warmup-period)

[Scroll to Top](/docs/terminology#)

[Edit Page](https://github.com/solana-foundation/developer-
content/tree/main/docs/terminology.md)

[Home](/)>[Solana Documentation](/docs)

# [Terminology](/docs/terminology)

The following terms are used throughout the Solana documentation and
development ecosystem.

## account #

A record in the Solana ledger that either holds data or is an executable
program.

Like an account at a traditional bank, a Solana account may hold funds called
[lamports](/docs/terminology#lamport). Like a file in Linux, it is addressable
by a key, often referred to as a [public key](/docs/terminology#public-key-
pubkey) or pubkey.

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
height](/docs/terminology#tick-height). It includes at least the set of all
[accounts](/docs/terminology#account) holding nonzero [native
tokens](/docs/terminology#native-token).

## block #

A contiguous set of [entries](/docs/terminology#entry) on the ledger covered
by a [vote](/docs/terminology#ledger-vote). A
[leader](/docs/terminology#leader) produces at most one block per
[slot](/docs/terminology#slot).

## blockhash #

A unique value ([hash](/docs/terminology#hash)) that identifies a record
(block). Solana computes a blockhash from the last [entry
id](/docs/terminology#entry-id) of the block.

## block height #

The number of [blocks](/docs/terminology#block) beneath the current block. The
first block after the [genesis block](/docs/terminology#genesis-block) has
height one.

## bootstrap validator #

The [validator](/docs/terminology#validator) that produces the genesis (first)
[block](/docs/terminology#block) of a block chain.

## BPF loader #

The Solana program that owns and loads [BPF](/docs/programs/faq#berkeley-
packet-filter-bpf) [onchain programs](/docs/terminology#onchain-program),
allowing the program to interface with the runtime.

## client #

A computer program that accesses the Solana server network
[cluster](/docs/terminology#cluster).

## commitment #

A measure of the network confirmation for the
[block](/docs/terminology#block).

## cluster #

A set of [validators](/docs/terminology#validator) maintaining a single
[ledger](/docs/terminology#ledger).

## compute budget #

The maximum number of [compute units](/docs/terminology#compute-units)
consumed per transaction.

## compute units #

The smallest unit of measure for consumption of computational resources of the
blockchain.

## confirmation time #

The wallclock duration between a [leader](/docs/terminology#leader) creating a
[tick entry](/docs/terminology#tick) and creating a [confirmed
block](/docs/terminology#confirmed-block).

## confirmed block #

A [block](/docs/terminology#block) that has received a [super
majority](/docs/terminology#supermajority) of [ledger
votes](/docs/terminology#ledger-vote).

## control plane #

A gossip network connecting all [nodes](/docs/terminology#node) of a
[cluster](/docs/terminology#cluster).

## cooldown period #

Some number of [epochs](/docs/terminology#epoch) after
[stake](/docs/terminology#stake) has been deactivated while it progressively
becomes available for withdrawal. During this period, the stake is considered
to be "deactivating". More info about: [warmup and
cooldown](https://docs.solanalabs.com/implemented-proposals/staking-
rewards#stake-warmup-cooldown-withdrawal)

## credit #

See [vote credit](/docs/terminology#vote-credit).

## cross-program invocation (CPI) #

A call from one [onchain program](/docs/terminology#onchain-program) to
another. For more information, see [calling between programs](/docs/core/cpi).

## data plane #

A multicast network used to efficiently validate
[entries](/docs/terminology#entry) and gain consensus.

## drone #

An off-chain service that acts as a custodian for a user's private key. It
typically serves to validate and sign transactions.

## entry #

An entry on the [ledger](/docs/terminology#ledger) either a
[tick](/docs/terminology#tick) or a [transaction's
entry](/docs/terminology#transactions-entry).

## entry id #

A preimage resistant [hash](/docs/terminology#hash) over the final contents of
an entry, which acts as the [entry's](/docs/terminology#entry) globally unique
identifier. The hash serves as evidence of:

  * The entry being generated after a duration of time
  * The specified [transactions](/docs/terminology#transaction) are those included in the entry
  * The entry's position with respect to other entries in [ledger](/docs/terminology#ledger)

See [proof of history](/docs/terminology#proof-of-history-poh).

## epoch #

The time, i.e. number of [slots](/docs/terminology#slot), for which a [leader
schedule](/docs/terminology#leader-schedule) is valid.

## fee account #

The fee account in the transaction is the account that pays for the cost of
including the transaction in the ledger. This is the first account in the
transaction. This account must be declared as Read-Write (writable) in the
transaction since paying for the transaction reduces the account balance.

## finality #

When nodes representing 2/3rd of the [stake](/docs/terminology#stake) have a
common [root](/docs/terminology#root).

## fork #

A [ledger](/docs/terminology#ledger) derived from common entries but then
diverged.

## genesis block #

The first [block](/docs/terminology#block) in the chain.

## genesis config #

The configuration file that prepares the [ledger](/docs/terminology#ledger)
for the [genesis block](/docs/terminology#genesis-block).

## hash #

A digital fingerprint of a sequence of bytes.

## inflation #

An increase in token supply over time used to fund rewards for validation and
to fund continued development of Solana.

## inner instruction #

See [cross-program invocation](/docs/terminology#cross-program-invocation-
cpi).

## instruction #

A call to invoke a specific [instruction
handler](/docs/terminology#instruction-handler) in a
[program](/docs/terminology#program). An instruction also specifies which
accounts it wants to read or modify, and additional data that serves as
auxiliary input to the [instruction handler](/docs/terminology#instruction-
handler). A [client](/docs/terminology#client) must include at least one
instruction in a [transaction](/docs/terminology#transaction), and all
instructions must complete for the transaction to be considered successful.

## instruction handler #

Instruction handlers are [program](/docs/terminology#program) functions that
process [instructions](/docs/terminology#instruction) from
[transactions](/docs/terminology#transaction). An instruction handler may
contain one or more [cross-program invocations](/docs/terminology#cross-
program-invocation-cpi).

## keypair #

A [public key](/docs/terminology#public-key-pubkey) and corresponding [private
key](/docs/terminology#private-key) for accessing an account.

## lamport #

A fractional [native token](/docs/terminology#native-token) with the value of
0.000000001 [sol](/docs/terminology#sol).

Info

Within the compute budget, a quantity of _[micro-
lamports](https://github.com/solana-
labs/solana/blob/ced8f6a512c61e0dd5308095ae8457add4a39e94/program-
runtime/src/prioritization_fee.rs#L1-L2)_ is used in the calculation of
[prioritization fees](/docs/terminology#prioritization-fee).

## leader #

The role of a [validator](/docs/terminology#validator) when it is appending
[entries](/docs/terminology#entry) to the [ledger](/docs/terminology#ledger).

## leader schedule #

A sequence of [validator](/docs/terminology#validator) [public
keys](/docs/terminology#public-key-pubkey) mapped to
[slots](/docs/terminology#slot). The cluster uses the leader schedule to
determine which validator is the [leader](/docs/terminology#leader) at any
moment in time.

## ledger #

A list of [entries](/docs/terminology#entry) containing
[transactions](/docs/terminology#transaction) signed by
[clients](/docs/terminology#client). Conceptually, this can be traced back to
the [genesis block](/docs/terminology#genesis-block), but an actual
[validator](/docs/terminology#validator)'s ledger may have only newer
[blocks](/docs/terminology#block) to reduce storage, as older ones are not
needed for validation of future blocks by design.

## ledger vote #

A [hash](/docs/terminology#hash) of the [validator's
state](/docs/terminology#bank-state) at a given [tick
height](/docs/terminology#tick-height). It comprises a
[validator's](/docs/terminology#validator) affirmation that a
[block](/docs/terminology#block) it has received has been verified, as well as
a promise not to vote for a conflicting [block](/docs/terminology#block) (i.e.
[fork](/docs/terminology#fork)) for a specific amount of time, the
[lockout](/docs/terminology#lockout) period.

## light client #

A type of [client](/docs/terminology#client) that can verify it's pointing to
a valid [cluster](/docs/terminology#cluster). It performs more ledger
verification than a [thin client](/docs/terminology#thin-client) and less than
a [validator](/docs/terminology#validator).

## loader #

A [program](/docs/terminology#program) with the ability to interpret the
binary encoding of other on-chain programs.

## lockout #

The duration of time for which a [validator](/docs/terminology#validator) is
unable to [vote](/docs/terminology#ledger-vote) on another
[fork](/docs/terminology#fork).

## message #

The structured contents of a [transaction](/docs/terminology#transaction).
Generally containing a header, array of account addresses, recent
[blockhash](/docs/terminology#blockhash), and an array of
[instructions](/docs/terminology#instruction).

Learn more about the [message formatting inside of
transactions](/docs/core/transactions#message-header) here.

## Nakamoto coefficient #

A measure of decentralization, the Nakamoto Coefficient is the smallest number
of independent entities that can act collectively to shut down a blockchain.
The term was coined by Balaji S. Srinivasan and Leland Lee in [Quantifying
Decentralization](https://news.earn.com/quantifying-
decentralization-e39db233c28e).

## native token #

The [token](/docs/terminology#token) used to track work done by
[nodes](/docs/terminology#node) in a cluster.

## node #

A computer participating in a [cluster](/docs/terminology#cluster).

## node count #

The number of [validators](/docs/terminology#validator) participating in a
[cluster](/docs/terminology#cluster).

## onchain program #

The executable code on Solana blockchain that interprets the
[instructions](/docs/terminology#instruction) sent inside of each
[transaction](/docs/terminology#transaction) to read and modify accounts over
which it has control. These programs are often referred to as "[_smart
contracts_](/docs/core/programs)" on other blockchains.

## PoH #

See [Proof of History](/docs/terminology#proof-of-history-poh).

## point #

A weighted [credit](/docs/terminology#credit) in a rewards regime. In the
[validator](/docs/terminology#validator) [rewards
regime](https://docs.solanalabs.com/consensus/stake-delegation-and-rewards),
the number of points owed to a [stake](/docs/terminology#stake) during
redemption is the product of the [vote credits](/docs/terminology#vote-credit)
earned and the number of lamports staked.

## private key #

The private key of a [keypair](/docs/terminology#keypair).

## program #

See [onchain program](/docs/terminology#onchain-program).

## program derived account (PDA) #

An account whose signing authority is a program and thus is not controlled by
a private key like other accounts.

## program id #

The public key of the [account](/docs/terminology#account) containing a
[program](/docs/terminology#program).

## proof of history (PoH) #

A stack of proofs, each of which proves that some data existed before the
proof was created and that a precise duration of time passed before the
previous proof. Like a [VDF](/docs/terminology#verifiable-delay-function-vdf),
a Proof of History can be verified in less time than it took to produce.

## prioritization fee #

An additional fee user can specify in the compute budget
[instruction](/docs/terminology#instruction) to prioritize their
[transactions](/docs/terminology#transaction).

The prioritization fee is calculated by multiplying the requested maximum
compute units by the compute-unit price (specified in increments of 0.000001
lamports per compute unit) rounded up to the nearest lamport.

Transactions should request the minimum amount of compute units required for
execution to minimize fees.

## public key (pubkey) #

The public key of a [keypair](/docs/terminology#keypair).

## rent #

Fee paid by [Accounts](/docs/terminology#account) and
[Programs](/docs/terminology#program) to store data on the blockchain. When
accounts do not have enough balance to pay rent, they may be Garbage
Collected.

See also [rent exempt](/docs/terminology#rent-exempt) below. Learn more about
rent here: [What is rent?](/docs/intro/rent).

## rent exempt #

Accounts that maintain a minimum lamport balance that is proportional to the
amount of data stored on the account. All newly created accounts are stored
on-chain permanently until the account is closed. It is not possible to create
an account that falls below the rent exemption threshold.

## root #

A [block](/docs/terminology#block) or [slot](/docs/terminology#slot) that has
reached maximum [lockout](/docs/terminology#lockout) on a
[validator](/docs/terminology#validator). The root is the highest block that
is an ancestor of all active forks on a validator. All ancestor blocks of a
root are also transitively a root. Blocks that are not an ancestor and not a
descendant of the root are excluded from consideration for consensus and can
be discarded.

## runtime #

The component of a [validator](/docs/terminology#validator) responsible for
[program](/docs/terminology#program) execution.

## Sealevel #

Solana's parallel run-time for [onchain programs](/docs/terminology#onchain-
program).

## shred #

A fraction of a [block](/docs/terminology#block); the smallest unit sent
between [validators](/docs/terminology#validator).

## signature #

A 64-byte ed25519 signature of R (32-bytes) and S (32-bytes). With the
requirement that R is a packed Edwards point not of small order and S is a
scalar in the range of `0 <= S < L`. This requirement ensures no signature
malleability. Each transaction must have at least one signature for [fee
account](/docs/terminology#fee-account). Thus, the first signature in
transaction can be treated as [transaction id](/docs/terminology#transaction-
id)

## skip rate #

The percentage of [skipped slots](/docs/terminology#skipped-slot) out of the
total leader slots in the current epoch. This metric can be misleading as it
has high variance after the epoch boundary when the sample size is small, as
well as for validators with a low number of leader slots, however can also be
useful in identifying node misconfigurations at times.

## skipped slot #

A past [slot](/docs/terminology#slot) that did not produce a
[block](/docs/terminology#block), because the leader was offline or the
[fork](/docs/terminology#fork) containing the slot was abandoned for a better
alternative by cluster consensus. A skipped slot will not appear as an
ancestor for blocks at subsequent slots, nor increment the [block
height](/docs/terminology#block-height), nor expire the oldest
`recent_blockhash`.

Whether a slot has been skipped can only be determined when it becomes older
than the latest [rooted](/docs/terminology#root) (thus not-skipped) slot.

## slot #

The period of time for which each [leader](/docs/terminology#leader) ingests
transactions and produces a [block](/docs/terminology#block).

Collectively, slots create a logical clock. Slots are ordered sequentially and
non-overlapping, comprising roughly equal real-world time as per
[PoH](/docs/terminology#proof-of-history-poh).

## smart contract #

See [onchain program](/docs/terminology#onchain-program).

## sol #

The [native token](/docs/terminology#native-token) of a Solana
[cluster](/docs/terminology#cluster).

## Solana Program Library (SPL) #

A [library of programs](https://spl.solana.com/) on Solana such as spl-token
that facilitates tasks such as creating and using tokens.

## stake #

Tokens forfeit to the [cluster](/docs/terminology#cluster) if malicious
[validator](/docs/terminology#validator) behavior can be proven.

## stake-weighted quality of service (SWQoS) #

SWQoS allows [preferential treatment for transactions that come from staked
validators](/developers/guides/advanced/stake-weighted-qos).

## supermajority #

2/3 of a [cluster](/docs/terminology#cluster).

## sysvar #

A system [account](/docs/terminology#account).
[Sysvars](https://docs.solanalabs.com/runtime/sysvars) provide cluster state
information such as current tick height, rewards
[points](/docs/terminology#point) values, etc. Programs can access Sysvars via
a Sysvar account (pubkey) or by querying via a syscall.

## thin client #

A type of [client](/docs/terminology#client) that trusts it is communicating
with a valid [cluster](/docs/terminology#cluster).

## tick #

A ledger [entry](/docs/terminology#entry) that estimates wallclock duration.

## tick height #

The Nth [tick](/docs/terminology#tick) in the
[ledger](/docs/terminology#ledger).

## token #

A digitally transferable asset.

## Token Extensions Program #

The [Token Extensions Program](https://spl.solana.com/token-2022) has the
program ID `TokenzQdBNbLqP5VEhdkAS6EPFLC1PHnBqCXEpPxuEb` and includes all the
same features as the [Token Program](/docs/terminology#token-program), but
comes with extensions such as confidential transfers, custom transfer logic,
extended metadata, and much more.

## Token Program #

The [Token Program](https://spl.solana.com/token) has the program ID
`TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA`, and provides the basic
capabilities of transferring, freezing, and minting tokens.

## tps #

[Transactions](/docs/terminology#transaction) per second.

## tpu #

[Transaction processing unit](https://docs.solanalabs.com/validator/tpu).

## transaction #

One or more [instructions](/docs/terminology#instruction) signed by a
[client](/docs/terminology#client) using one or more
[keypairs](/docs/terminology#keypair) and executed atomically with only two
possible outcomes: success or failure.

## transaction id #

The first [signature](/docs/terminology#signature) in a
[transaction](/docs/terminology#transaction), which can be used to uniquely
identify the transaction across the complete
[ledger](/docs/terminology#ledger).

## transaction confirmations #

The number of [confirmed blocks](/docs/terminology#confirmed-block) since the
transaction was accepted onto the [ledger](/docs/terminology#ledger). A
transaction is finalized when its block becomes a
[root](/docs/terminology#root).

## transactions entry #

A set of [transactions](/docs/terminology#transaction) that may be executed in
parallel.

## tvu #

[Transaction validation unit](https://docs.solanalabs.com/validator/tvu).

## validator #

A full participant in a Solana network [cluster](/docs/terminology#cluster)
that produces new [blocks](/docs/terminology#block). A validator validates the
transactions added to the [ledger](/docs/terminology#ledger)

## VDF #

See [verifiable delay function](/docs/terminology#verifiable-delay-function-
vdf).

## verifiable delay function (VDF) #

A function that takes a fixed amount of time to execute that produces a proof
that it ran, which can then be verified in less time than it took to produce.

## vote #

See [ledger vote](/docs/terminology#ledger-vote).

## vote credit #

A reward tally for [validators](/docs/terminology#validator). A vote credit is
awarded to a validator in its vote account when the validator reaches a
[root](/docs/terminology#root).

## wallet #

A collection of [keypairs](/docs/terminology#keypair) that allows users to
manage their funds.

## warmup period #

Some number of [epochs](/docs/terminology#epoch) after
[stake](/docs/terminology#stake) has been delegated while it progressively
becomes effective. During this period, the stake is considered to be
"activating". More info about: [warmup and
cooldown](https://docs.solanalabs.com/consensus/stake-delegation-and-
rewards#stake-warmup-cooldown-withdrawal)

[Previous« JSON RPC Methods](/docs/rpc)[NextOverview »](/docs/intro/overview)

  * [Solana Documentation](/docs)

    * [JSON RPC Methods](/docs/rpc)
    * [Terminology](/docs/terminology)
  * Introduction

    * [Overview](/docs/intro/overview)
    * [Wallets](/docs/intro/wallets)
    * [Intro to Development](/docs/intro/dev)
  * Core Concepts

    * [Solana Account Model](/docs/core/accounts)
    * [Transactions and Instructions](/docs/core/transactions)
    * [Fees on Solana](/docs/core/fees)
    * [Programs on Solana](/docs/core/programs)
    * [Program Derived Address](/docs/core/pda)
    * [Cross Program Invocation](/docs/core/cpi)
    * [Tokens on Solana](/docs/core/tokens)
    * [Clusters & Endpoints](/docs/core/clusters)
  * Advanced Concepts

    * [Versioned Transactions](/docs/advanced/versions)
    * [Address Lookup Tables](/docs/advanced/lookup-tables)
    * [Confirmation & Expiration](/docs/advanced/confirmation)
    * [Retrying Transactions](/docs/advanced/retry)
    * [State Compression](/docs/advanced/state-compression)
  * Solana Clients

    * [Rust](/docs/clients/rust)
    * [JavaScript / TypeScript](/docs/clients/javascript)
    * [Web3.js API Examples](/docs/clients/javascript-reference)
  * [Economics](/docs/economics)

    * Inflation
      * [Proposed Inflation Schedule](/docs/economics/inflation/inflation-schedule)
      * [Inflation Terminology](/docs/economics/inflation/terminology)
    * [Staking](/docs/economics/staking)
      * [Stake Accounts](/docs/economics/staking/stake-accounts)
      * [Stake Programming](/docs/economics/staking/stake-programming)
  * Developing Programs

    * [Overview](/docs/programs/overview)
    * [Debugging Programs](/docs/programs/debugging)
    * [Deploying Programs](/docs/programs/deploying)
    * [Program Examples](/docs/programs/examples)
    * [FAQ](/docs/programs/faq)
    * [Developing with C](/docs/programs/lang-c)
    * [Developing with Rust](/docs/programs/lang-rust)
    * [Limitations](/docs/programs/limitations)
  * More Information

    * [Add Solana to Your Exchange](/docs/more/exchange)

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

