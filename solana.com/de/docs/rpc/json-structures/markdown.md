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

  * [Transactions](/de/docs/rpc/json-structures#transactions)
  * [Inner Instructions](/de/docs/rpc/json-structures#inner-instructions)
  * [Token Balances](/de/docs/rpc/json-structures#token-balances)

[Scroll to Top](/de/docs/rpc/json-structures#)

[Edit Page](https://github.com/solana-foundation/developer-
content/tree/main/docs/rpc/json-structures.mdx)

[Home](/de)>[Solana Dokumentation](/de/docs)>[Solana RPC
Methods](/de/docs/rpc)

# [Common JSON Data Structures for Solana RPC Methods](/de/docs/rpc/json-
structures)

Various Solana RPC methods will return more complex responses as structured
JSON objects, filled with specific keyed values.

The most common of these JSON data structures include:

  * [transactions](/de/docs/rpc/json-structures#transactions)
  * [inner instructions](/de/docs/rpc/json-structures#inner-instructions)
  * [token balances](/de/docs/rpc/json-structures#token-balances)

## Transactions #

Transactions are quite different from those on other blockchains. Be sure to
review [Anatomy of a Transaction](/de/docs/core/transactions) to learn about
transactions on Solana.

The JSON structure of a transaction is defined as follows:

  * `signatures: <array[string]>` \- A list of base-58 encoded signatures applied to the transaction. The list is always of length `message.header.numRequiredSignatures` and not empty. The signature at index `i` corresponds to the public key at index `i` in `message.accountKeys`. The first one is used as the [transaction id](/de/docs/terminology#transaction-id).
  * `message: <object>` \- Defines the content of the transaction.
    * `accountKeys: <array[string]>` \- List of base-58 encoded public keys used by the transaction, including by the instructions and for signatures. The first `message.header.numRequiredSignatures` public keys must sign the transaction.
    * `header: <object>` \- Details the account types and signatures required by the transaction.
      * `numRequiredSignatures: <number>` \- The total number of signatures required to make the transaction valid. The signatures must match the first `numRequiredSignatures` of `message.accountKeys`.
      * `numReadonlySignedAccounts: <number>` \- The last `numReadonlySignedAccounts` of the signed keys are read-only accounts. Programs may process multiple transactions that load read-only accounts within a single PoH entry, but are not permitted to credit or debit lamports or modify account data. Transactions targeting the same read-write account are evaluated sequentially.
      * `numReadonlyUnsignedAccounts: <number>` \- The last `numReadonlyUnsignedAccounts` of the unsigned keys are read-only accounts.
    * `recentBlockhash: <string>` \- A base-58 encoded hash of a recent block in the ledger used to prevent transaction duplication and to give transactions lifetimes.
    * `instructions: <array[object]>` \- List of program instructions that will be executed in sequence and committed in one atomic transaction if all succeed.
      * `programIdIndex: <number>` \- Index into the `message.accountKeys` array indicating the program account that executes this instruction.
      * `accounts: <array[number]>` \- List of ordered indices into the `message.accountKeys` array indicating which accounts to pass to the program.
      * `data: <string>` \- The program input data encoded in a base-58 string.
    * `addressTableLookups: <array[object]|undefined>` \- List of address table lookups used by a transaction to dynamically load addresses from on-chain address lookup tables. Undefined if `maxSupportedTransactionVersion` is not set.
      * `accountKey: <string>` \- base-58 encoded public key for an address lookup table account.
      * `writableIndexes: <array[number]>` \- List of indices used to load addresses of writable accounts from a lookup table.
      * `readonlyIndexes: <array[number]>` \- List of indices used to load addresses of readonly accounts from a lookup table.

## Inner Instructions #

The Solana runtime records the cross-program instructions that are invoked
during transaction processing and makes these available for greater
transparency of what was executed on-chain per transaction instruction.
Invoked instructions are grouped by the originating transaction instruction
and are listed in order of processing.

The JSON structure of inner instructions is defined as a list of objects in
the following structure:

  * `index: number` \- Index of the transaction instruction from which the inner instruction(s) originated
  * `instructions: <array[object]>` \- Ordered list of inner program instructions that were invoked during a single transaction instruction.
    * `programIdIndex: <number>` \- Index into the `message.accountKeys` array indicating the program account that executes this instruction.
    * `accounts: <array[number]>` \- List of ordered indices into the `message.accountKeys` array indicating which accounts to pass to the program.
    * `data: <string>` \- The program input data encoded in a base-58 string.

## Token Balances #

The JSON structure of token balances is defined as a list of objects in the
following structure:

  * `accountIndex: <number>` \- Index of the account in which the token balance is provided for.
  * `mint: <string>` \- Pubkey of the token's mint.
  * `owner: <string|undefined>` \- Pubkey of token balance's owner.
  * `programId: <string|undefined>` \- Pubkey of the Token program that owns the account.
  * `uiTokenAmount: <object>` -
    * `amount: <string>` \- Raw amount of tokens as a string, ignoring decimals.
    * `decimals: <number>` \- Number of decimals configured for token's mint.
    * `uiAmount: <number|null>` \- Token amount as a float, accounting for decimals. **DEPRECATED**
    * `uiAmountString: <string>` \- Token amount as a string, accounting for decimals.

[Previous« Solana RPC Methods](/de/docs/rpc)[NextHTTP Methods
»](/de/docs/rpc/http)

  * [Solana Dokumentation](/de/docs)

  * [Solana RPC Methods](/de/docs/rpc)

    * [Data Structures as JSON](/de/docs/rpc/json-structures)
    * [HTTP Methods](/de/docs/rpc/http)
      * [getAccountInfo](/de/docs/rpc/http/getaccountinfo)
      * [getBalance](/de/docs/rpc/http/getbalance)
      * [getBlock](/de/docs/rpc/http/getblock)
      * [getBlockCommitment](/de/docs/rpc/http/getblockcommitment)
      * [getBlockHeight](/de/docs/rpc/http/getblockheight)
      * [getBlockProduction](/de/docs/rpc/http/getblockproduction)
      * [getBlockTime](/de/docs/rpc/http/getblocktime)
      * [getBlocks](/de/docs/rpc/http/getblocks)
      * [getBlocksWithLimit](/de/docs/rpc/http/getblockswithlimit)
      * [getClusterNodes](/de/docs/rpc/http/getclusternodes)
      * [getEpochInfo](/de/docs/rpc/http/getepochinfo)
      * [getEpochSchedule](/de/docs/rpc/http/getepochschedule)
      * [getFeeForMessage](/de/docs/rpc/http/getfeeformessage)
      * [getFirstAvailableBlock](/de/docs/rpc/http/getfirstavailableblock)
      * [getGenesisHash](/de/docs/rpc/http/getgenesishash)
      * [getHealth](/de/docs/rpc/http/gethealth)
      * [getHighestSnapshotSlot](/de/docs/rpc/http/gethighestsnapshotslot)
      * [getIdentity](/de/docs/rpc/http/getidentity)
      * [getInflationGovernor](/de/docs/rpc/http/getinflationgovernor)
      * [getInflationRate](/de/docs/rpc/http/getinflationrate)
      * [getInflationReward](/de/docs/rpc/http/getinflationreward)
      * [getLargestAccounts](/de/docs/rpc/http/getlargestaccounts)
      * [getLatestBlockhash](/de/docs/rpc/http/getlatestblockhash)
      * [getLeaderSchedule](/de/docs/rpc/http/getleaderschedule)
      * [getMaxRetransmitSlot](/de/docs/rpc/http/getmaxretransmitslot)
      * [getMaxShredInsertSlot](/de/docs/rpc/http/getmaxshredinsertslot)
      * [getMinimumBalanceForRentExemption](/de/docs/rpc/http/getminimumbalanceforrentexemption)
      * [getMultipleAccounts](/de/docs/rpc/http/getmultipleaccounts)
      * [getProgramAccounts](/de/docs/rpc/http/getprogramaccounts)
      * [getRecentPerformanceSamples](/de/docs/rpc/http/getrecentperformancesamples)
      * [getRecentPrioritizationFees](/de/docs/rpc/http/getrecentprioritizationfees)
      * [getSignatureStatuses](/de/docs/rpc/http/getsignaturestatuses)
      * [getSignaturesForAddress](/de/docs/rpc/http/getsignaturesforaddress)
      * [getSlot](/de/docs/rpc/http/getslot)
      * [getSlotLeader](/de/docs/rpc/http/getslotleader)
      * [getSlotLeaders](/de/docs/rpc/http/getslotleaders)
      * [getStakeActivation](/de/docs/rpc/http/getstakeactivation)
      * [getStakeMinimumDelegation](/de/docs/rpc/http/getstakeminimumdelegation)
      * [getSupply](/de/docs/rpc/http/getsupply)
      * [getTokenAccountBalance](/de/docs/rpc/http/gettokenaccountbalance)
      * [getTokenAccountsByDelegate](/de/docs/rpc/http/gettokenaccountsbydelegate)
      * [getTokenAccountsByOwner](/de/docs/rpc/http/gettokenaccountsbyowner)
      * [getTokenLargestAccounts](/de/docs/rpc/http/gettokenlargestaccounts)
      * [getTokenSupply](/de/docs/rpc/http/gettokensupply)
      * [getTransaction](/de/docs/rpc/http/gettransaction)
      * [getTransactionCount](/de/docs/rpc/http/gettransactioncount)
      * [getVersion](/de/docs/rpc/http/getversion)
      * [getVoteAccounts](/de/docs/rpc/http/getvoteaccounts)
      * [isBlockhashValid](/de/docs/rpc/http/isblockhashvalid)
      * [minimumLedgerSlot](/de/docs/rpc/http/minimumledgerslot)
      * [requestAirdrop](/de/docs/rpc/http/requestairdrop)
      * [sendTransaction](/de/docs/rpc/http/sendtransaction)
      * [simulateTransaction](/de/docs/rpc/http/simulatetransaction)
    * [Websocket Methods](/de/docs/rpc/websocket)
      * [accountSubscribe](/de/docs/rpc/websocket/accountsubscribe)
      * [accountUnsubscribe](/de/docs/rpc/websocket/accountunsubscribe)
      * [blockSubscribe](/de/docs/rpc/websocket/blocksubscribe)
      * [blockUnsubscribe](/de/docs/rpc/websocket/blockunsubscribe)
      * [logsSubscribe](/de/docs/rpc/websocket/logssubscribe)
      * [logsUnsubscribe](/de/docs/rpc/websocket/logsunsubscribe)
      * [programSubscribe](/de/docs/rpc/websocket/programsubscribe)
      * [programUnsubscribe](/de/docs/rpc/websocket/programunsubscribe)
      * [rootSubscribe](/de/docs/rpc/websocket/rootsubscribe)
      * [rootUnsubscribe](/de/docs/rpc/websocket/rootunsubscribe)
      * [signatureSubscribe](/de/docs/rpc/websocket/signaturesubscribe)
      * [signatureUnsubscribe](/de/docs/rpc/websocket/signatureunsubscribe)
      * [slotSubscribe](/de/docs/rpc/websocket/slotsubscribe)
      * [slotUnsubscribe](/de/docs/rpc/websocket/slotunsubscribe)
      * [slotsUpdatesSubscribe](/de/docs/rpc/websocket/slotsupdatessubscribe)
      * [slotsUpdatesUnsubscribe](/de/docs/rpc/websocket/slotsupdatesunsubscribe)
      * [voteSubscribe](/de/docs/rpc/websocket/votesubscribe)
      * [voteUnsubscribe](/de/docs/rpc/websocket/voteunsubscribe)
    * Deprecated Methods
      * [getConfirmedBlock](/de/docs/rpc/deprecated/getconfirmedblock)
      * [getConfirmedBlocks](/de/docs/rpc/deprecated/getconfirmedblocks)
      * [getConfirmedBlocksWithLimit](/de/docs/rpc/deprecated/getconfirmedblockswithlimit)
      * [getConfirmedSignaturesForAddress2](/de/docs/rpc/deprecated/getconfirmedsignaturesforaddress2)
      * [getConfirmedTransaction](/de/docs/rpc/deprecated/getconfirmedtransaction)
      * [getFeeCalculatorForBlockhash](/de/docs/rpc/deprecated/getfeecalculatorforblockhash)
      * [getFeeRateGovernor](/de/docs/rpc/deprecated/getfeerategovernor)
      * [getFees](/de/docs/rpc/deprecated/getfees)
      * [getRecentBlockhash](/de/docs/rpc/deprecated/getrecentblockhash)
      * [getSnapshotSlot](/de/docs/rpc/deprecated/getsnapshotslot)

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

