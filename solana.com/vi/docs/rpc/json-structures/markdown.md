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

  * [Transactions](/vi/docs/rpc/json-structures#transactions)
  * [Inner Instructions](/vi/docs/rpc/json-structures#inner-instructions)
  * [Token Balances](/vi/docs/rpc/json-structures#token-balances)

[Scroll to Top](/vi/docs/rpc/json-structures#)

[Edit Page](https://github.com/solana-foundation/developer-
content/tree/main/docs/rpc/json-structures.mdx)

[Home](/vi)>[Solana Documentation](/vi/docs)>[Solana RPC
Methods](/vi/docs/rpc)

# [Common JSON Data Structures for Solana RPC Methods](/vi/docs/rpc/json-
structures)

Various Solana RPC methods will return more complex responses as structured
JSON objects, filled with specific keyed values.

The most common of these JSON data structures include:

  * [transactions](/vi/docs/rpc/json-structures#transactions)
  * [inner instructions](/vi/docs/rpc/json-structures#inner-instructions)
  * [token balances](/vi/docs/rpc/json-structures#token-balances)

## Transactions #

Transactions are quite different from those on other blockchains. Be sure to
review [Anatomy of a Transaction](/vi/docs/core/transactions) to learn about
transactions on Solana.

The JSON structure of a transaction is defined as follows:

  * `signatures: <array[string]>` \- A list of base-58 encoded signatures applied to the transaction. The list is always of length `message.header.numRequiredSignatures` and not empty. The signature at index `i` corresponds to the public key at index `i` in `message.accountKeys`. The first one is used as the [transaction id](/vi/docs/terminology#transaction-id).
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

[Previous« Solana RPC Methods](/vi/docs/rpc)[NextHTTP Methods
»](/vi/docs/rpc/http)

  * [Solana Documentation](/vi/docs)

  * [Solana RPC Methods](/vi/docs/rpc)

    * [Data Structures as JSON](/vi/docs/rpc/json-structures)
    * [HTTP Methods](/vi/docs/rpc/http)
      * [getAccountInfo](/vi/docs/rpc/http/getaccountinfo)
      * [getBalance](/vi/docs/rpc/http/getbalance)
      * [getBlock](/vi/docs/rpc/http/getblock)
      * [getBlockCommitment](/vi/docs/rpc/http/getblockcommitment)
      * [getBlockHeight](/vi/docs/rpc/http/getblockheight)
      * [getBlockProduction](/vi/docs/rpc/http/getblockproduction)
      * [getBlockTime](/vi/docs/rpc/http/getblocktime)
      * [getBlocks](/vi/docs/rpc/http/getblocks)
      * [getBlocksWithLimit](/vi/docs/rpc/http/getblockswithlimit)
      * [getClusterNodes](/vi/docs/rpc/http/getclusternodes)
      * [getEpochInfo](/vi/docs/rpc/http/getepochinfo)
      * [getEpochSchedule](/vi/docs/rpc/http/getepochschedule)
      * [getFeeForMessage](/vi/docs/rpc/http/getfeeformessage)
      * [getFirstAvailableBlock](/vi/docs/rpc/http/getfirstavailableblock)
      * [getGenesisHash](/vi/docs/rpc/http/getgenesishash)
      * [getHealth](/vi/docs/rpc/http/gethealth)
      * [getHighestSnapshotSlot](/vi/docs/rpc/http/gethighestsnapshotslot)
      * [getIdentity](/vi/docs/rpc/http/getidentity)
      * [getInflationGovernor](/vi/docs/rpc/http/getinflationgovernor)
      * [getInflationRate](/vi/docs/rpc/http/getinflationrate)
      * [getInflationReward](/vi/docs/rpc/http/getinflationreward)
      * [getLargestAccounts](/vi/docs/rpc/http/getlargestaccounts)
      * [getLatestBlockhash](/vi/docs/rpc/http/getlatestblockhash)
      * [getLeaderSchedule](/vi/docs/rpc/http/getleaderschedule)
      * [getMaxRetransmitSlot](/vi/docs/rpc/http/getmaxretransmitslot)
      * [getMaxShredInsertSlot](/vi/docs/rpc/http/getmaxshredinsertslot)
      * [getMinimumBalanceForRentExemption](/vi/docs/rpc/http/getminimumbalanceforrentexemption)
      * [getMultipleAccounts](/vi/docs/rpc/http/getmultipleaccounts)
      * [getProgramAccounts](/vi/docs/rpc/http/getprogramaccounts)
      * [getRecentPerformanceSamples](/vi/docs/rpc/http/getrecentperformancesamples)
      * [getRecentPrioritizationFees](/vi/docs/rpc/http/getrecentprioritizationfees)
      * [getSignatureStatuses](/vi/docs/rpc/http/getsignaturestatuses)
      * [getSignaturesForAddress](/vi/docs/rpc/http/getsignaturesforaddress)
      * [getSlot](/vi/docs/rpc/http/getslot)
      * [getSlotLeader](/vi/docs/rpc/http/getslotleader)
      * [getSlotLeaders](/vi/docs/rpc/http/getslotleaders)
      * [getStakeActivation](/vi/docs/rpc/http/getstakeactivation)
      * [getStakeMinimumDelegation](/vi/docs/rpc/http/getstakeminimumdelegation)
      * [getSupply](/vi/docs/rpc/http/getsupply)
      * [getTokenAccountBalance](/vi/docs/rpc/http/gettokenaccountbalance)
      * [getTokenAccountsByDelegate](/vi/docs/rpc/http/gettokenaccountsbydelegate)
      * [getTokenAccountsByOwner](/vi/docs/rpc/http/gettokenaccountsbyowner)
      * [getTokenLargestAccounts](/vi/docs/rpc/http/gettokenlargestaccounts)
      * [getTokenSupply](/vi/docs/rpc/http/gettokensupply)
      * [getTransaction](/vi/docs/rpc/http/gettransaction)
      * [getTransactionCount](/vi/docs/rpc/http/gettransactioncount)
      * [getVersion](/vi/docs/rpc/http/getversion)
      * [getVoteAccounts](/vi/docs/rpc/http/getvoteaccounts)
      * [isBlockhashValid](/vi/docs/rpc/http/isblockhashvalid)
      * [minimumLedgerSlot](/vi/docs/rpc/http/minimumledgerslot)
      * [requestAirdrop](/vi/docs/rpc/http/requestairdrop)
      * [sendTransaction](/vi/docs/rpc/http/sendtransaction)
      * [simulateTransaction](/vi/docs/rpc/http/simulatetransaction)
    * [Websocket Methods](/vi/docs/rpc/websocket)
      * [accountSubscribe](/vi/docs/rpc/websocket/accountsubscribe)
      * [accountUnsubscribe](/vi/docs/rpc/websocket/accountunsubscribe)
      * [blockSubscribe](/vi/docs/rpc/websocket/blocksubscribe)
      * [blockUnsubscribe](/vi/docs/rpc/websocket/blockunsubscribe)
      * [logsSubscribe](/vi/docs/rpc/websocket/logssubscribe)
      * [logsUnsubscribe](/vi/docs/rpc/websocket/logsunsubscribe)
      * [programSubscribe](/vi/docs/rpc/websocket/programsubscribe)
      * [programUnsubscribe](/vi/docs/rpc/websocket/programunsubscribe)
      * [rootSubscribe](/vi/docs/rpc/websocket/rootsubscribe)
      * [rootUnsubscribe](/vi/docs/rpc/websocket/rootunsubscribe)
      * [signatureSubscribe](/vi/docs/rpc/websocket/signaturesubscribe)
      * [signatureUnsubscribe](/vi/docs/rpc/websocket/signatureunsubscribe)
      * [slotSubscribe](/vi/docs/rpc/websocket/slotsubscribe)
      * [slotUnsubscribe](/vi/docs/rpc/websocket/slotunsubscribe)
      * [slotsUpdatesSubscribe](/vi/docs/rpc/websocket/slotsupdatessubscribe)
      * [slotsUpdatesUnsubscribe](/vi/docs/rpc/websocket/slotsupdatesunsubscribe)
      * [voteSubscribe](/vi/docs/rpc/websocket/votesubscribe)
      * [voteUnsubscribe](/vi/docs/rpc/websocket/voteunsubscribe)
    * Deprecated Methods
      * [getConfirmedBlock](/vi/docs/rpc/deprecated/getconfirmedblock)
      * [getConfirmedBlocks](/vi/docs/rpc/deprecated/getconfirmedblocks)
      * [getConfirmedBlocksWithLimit](/vi/docs/rpc/deprecated/getconfirmedblockswithlimit)
      * [getConfirmedSignaturesForAddress2](/vi/docs/rpc/deprecated/getconfirmedsignaturesforaddress2)
      * [getConfirmedTransaction](/vi/docs/rpc/deprecated/getconfirmedtransaction)
      * [getFeeCalculatorForBlockhash](/vi/docs/rpc/deprecated/getfeecalculatorforblockhash)
      * [getFeeRateGovernor](/vi/docs/rpc/deprecated/getfeerategovernor)
      * [getFees](/vi/docs/rpc/deprecated/getfees)
      * [getRecentBlockhash](/vi/docs/rpc/deprecated/getrecentblockhash)
      * [getSnapshotSlot](/vi/docs/rpc/deprecated/getsnapshotslot)

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

