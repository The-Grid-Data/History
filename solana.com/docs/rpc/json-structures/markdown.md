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

  * [Transactions](/docs/rpc/json-structures#transactions)
  * [Inner Instructions](/docs/rpc/json-structures#inner-instructions)
  * [Token Balances](/docs/rpc/json-structures#token-balances)

[Scroll to Top](/docs/rpc/json-structures#)

[Edit Page](https://github.com/solana-foundation/developer-
content/tree/main/docs/rpc/json-structures.mdx)

[Home](/)>[Solana Documentation](/docs)>[Solana RPC Methods](/docs/rpc)

# [Common JSON Data Structures for Solana RPC Methods](/docs/rpc/json-
structures)

Various Solana RPC methods will return more complex responses as structured
JSON objects, filled with specific keyed values.

The most common of these JSON data structures include:

  * [transactions](/docs/rpc/json-structures#transactions)
  * [inner instructions](/docs/rpc/json-structures#inner-instructions)
  * [token balances](/docs/rpc/json-structures#token-balances)

## Transactions #

Transactions are quite different from those on other blockchains. Be sure to
review [Anatomy of a Transaction](/docs/core/transactions) to learn about
transactions on Solana.

The JSON structure of a transaction is defined as follows:

  * `signatures: <array[string]>` \- A list of base-58 encoded signatures applied to the transaction. The list is always of length `message.header.numRequiredSignatures` and not empty. The signature at index `i` corresponds to the public key at index `i` in `message.accountKeys`. The first one is used as the [transaction id](/docs/terminology#transaction-id).
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

[Previous« Solana RPC Methods](/docs/rpc)[NextHTTP Methods »](/docs/rpc/http)

  * [Solana Documentation](/docs)

  * [Solana RPC Methods](/docs/rpc)

    * [Data Structures as JSON](/docs/rpc/json-structures)
    * [HTTP Methods](/docs/rpc/http)
      * [getAccountInfo](/docs/rpc/http/getaccountinfo)
      * [getBalance](/docs/rpc/http/getbalance)
      * [getBlock](/docs/rpc/http/getblock)
      * [getBlockCommitment](/docs/rpc/http/getblockcommitment)
      * [getBlockHeight](/docs/rpc/http/getblockheight)
      * [getBlockProduction](/docs/rpc/http/getblockproduction)
      * [getBlockTime](/docs/rpc/http/getblocktime)
      * [getBlocks](/docs/rpc/http/getblocks)
      * [getBlocksWithLimit](/docs/rpc/http/getblockswithlimit)
      * [getClusterNodes](/docs/rpc/http/getclusternodes)
      * [getEpochInfo](/docs/rpc/http/getepochinfo)
      * [getEpochSchedule](/docs/rpc/http/getepochschedule)
      * [getFeeForMessage](/docs/rpc/http/getfeeformessage)
      * [getFirstAvailableBlock](/docs/rpc/http/getfirstavailableblock)
      * [getGenesisHash](/docs/rpc/http/getgenesishash)
      * [getHealth](/docs/rpc/http/gethealth)
      * [getHighestSnapshotSlot](/docs/rpc/http/gethighestsnapshotslot)
      * [getIdentity](/docs/rpc/http/getidentity)
      * [getInflationGovernor](/docs/rpc/http/getinflationgovernor)
      * [getInflationRate](/docs/rpc/http/getinflationrate)
      * [getInflationReward](/docs/rpc/http/getinflationreward)
      * [getLargestAccounts](/docs/rpc/http/getlargestaccounts)
      * [getLatestBlockhash](/docs/rpc/http/getlatestblockhash)
      * [getLeaderSchedule](/docs/rpc/http/getleaderschedule)
      * [getMaxRetransmitSlot](/docs/rpc/http/getmaxretransmitslot)
      * [getMaxShredInsertSlot](/docs/rpc/http/getmaxshredinsertslot)
      * [getMinimumBalanceForRentExemption](/docs/rpc/http/getminimumbalanceforrentexemption)
      * [getMultipleAccounts](/docs/rpc/http/getmultipleaccounts)
      * [getProgramAccounts](/docs/rpc/http/getprogramaccounts)
      * [getRecentPerformanceSamples](/docs/rpc/http/getrecentperformancesamples)
      * [getRecentPrioritizationFees](/docs/rpc/http/getrecentprioritizationfees)
      * [getSignatureStatuses](/docs/rpc/http/getsignaturestatuses)
      * [getSignaturesForAddress](/docs/rpc/http/getsignaturesforaddress)
      * [getSlot](/docs/rpc/http/getslot)
      * [getSlotLeader](/docs/rpc/http/getslotleader)
      * [getSlotLeaders](/docs/rpc/http/getslotleaders)
      * [getStakeActivation](/docs/rpc/http/getstakeactivation)
      * [getStakeMinimumDelegation](/docs/rpc/http/getstakeminimumdelegation)
      * [getSupply](/docs/rpc/http/getsupply)
      * [getTokenAccountBalance](/docs/rpc/http/gettokenaccountbalance)
      * [getTokenAccountsByDelegate](/docs/rpc/http/gettokenaccountsbydelegate)
      * [getTokenAccountsByOwner](/docs/rpc/http/gettokenaccountsbyowner)
      * [getTokenLargestAccounts](/docs/rpc/http/gettokenlargestaccounts)
      * [getTokenSupply](/docs/rpc/http/gettokensupply)
      * [getTransaction](/docs/rpc/http/gettransaction)
      * [getTransactionCount](/docs/rpc/http/gettransactioncount)
      * [getVersion](/docs/rpc/http/getversion)
      * [getVoteAccounts](/docs/rpc/http/getvoteaccounts)
      * [isBlockhashValid](/docs/rpc/http/isblockhashvalid)
      * [minimumLedgerSlot](/docs/rpc/http/minimumledgerslot)
      * [requestAirdrop](/docs/rpc/http/requestairdrop)
      * [sendTransaction](/docs/rpc/http/sendtransaction)
      * [simulateTransaction](/docs/rpc/http/simulatetransaction)
    * [Websocket Methods](/docs/rpc/websocket)
      * [accountSubscribe](/docs/rpc/websocket/accountsubscribe)
      * [accountUnsubscribe](/docs/rpc/websocket/accountunsubscribe)
      * [blockSubscribe](/docs/rpc/websocket/blocksubscribe)
      * [blockUnsubscribe](/docs/rpc/websocket/blockunsubscribe)
      * [logsSubscribe](/docs/rpc/websocket/logssubscribe)
      * [logsUnsubscribe](/docs/rpc/websocket/logsunsubscribe)
      * [programSubscribe](/docs/rpc/websocket/programsubscribe)
      * [programUnsubscribe](/docs/rpc/websocket/programunsubscribe)
      * [rootSubscribe](/docs/rpc/websocket/rootsubscribe)
      * [rootUnsubscribe](/docs/rpc/websocket/rootunsubscribe)
      * [signatureSubscribe](/docs/rpc/websocket/signaturesubscribe)
      * [signatureUnsubscribe](/docs/rpc/websocket/signatureunsubscribe)
      * [slotSubscribe](/docs/rpc/websocket/slotsubscribe)
      * [slotUnsubscribe](/docs/rpc/websocket/slotunsubscribe)
      * [slotsUpdatesSubscribe](/docs/rpc/websocket/slotsupdatessubscribe)
      * [slotsUpdatesUnsubscribe](/docs/rpc/websocket/slotsupdatesunsubscribe)
      * [voteSubscribe](/docs/rpc/websocket/votesubscribe)
      * [voteUnsubscribe](/docs/rpc/websocket/voteunsubscribe)
    * Deprecated Methods
      * [getConfirmedBlock](/docs/rpc/deprecated/getconfirmedblock)
      * [getConfirmedBlocks](/docs/rpc/deprecated/getconfirmedblocks)
      * [getConfirmedBlocksWithLimit](/docs/rpc/deprecated/getconfirmedblockswithlimit)
      * [getConfirmedSignaturesForAddress2](/docs/rpc/deprecated/getconfirmedsignaturesforaddress2)
      * [getConfirmedTransaction](/docs/rpc/deprecated/getconfirmedtransaction)
      * [getFeeCalculatorForBlockhash](/docs/rpc/deprecated/getfeecalculatorforblockhash)
      * [getFeeRateGovernor](/docs/rpc/deprecated/getfeerategovernor)
      * [getFees](/docs/rpc/deprecated/getfees)
      * [getRecentBlockhash](/docs/rpc/deprecated/getrecentblockhash)
      * [getSnapshotSlot](/docs/rpc/deprecated/getsnapshotslot)

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

