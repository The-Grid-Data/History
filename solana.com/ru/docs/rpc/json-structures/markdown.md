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

  * [Transactions](/ru/docs/rpc/json-structures#transactions)
  * [Inner Instructions](/ru/docs/rpc/json-structures#inner-instructions)
  * [Token Balances](/ru/docs/rpc/json-structures#token-balances)

[Scroll to Top](/ru/docs/rpc/json-structures#)

[Edit Page](https://github.com/solana-foundation/developer-
content/tree/main/docs/rpc/json-structures.mdx)

[Home](/ru)>[Solana Documentation](/ru/docs)>[Solana RPC
Methods](/ru/docs/rpc)

# [Common JSON Data Structures for Solana RPC Methods](/ru/docs/rpc/json-
structures)

Various Solana RPC methods will return more complex responses as structured
JSON objects, filled with specific keyed values.

The most common of these JSON data structures include:

  * [transactions](/ru/docs/rpc/json-structures#transactions)
  * [inner instructions](/ru/docs/rpc/json-structures#inner-instructions)
  * [token balances](/ru/docs/rpc/json-structures#token-balances)

## Transactions #

Transactions are quite different from those on other blockchains. Be sure to
review [Anatomy of a Transaction](/ru/docs/core/transactions) to learn about
transactions on Solana.

The JSON structure of a transaction is defined as follows:

  * `signatures: <array[string]>` \- A list of base-58 encoded signatures applied to the transaction. The list is always of length `message.header.numRequiredSignatures` and not empty. The signature at index `i` corresponds to the public key at index `i` in `message.accountKeys`. The first one is used as the [transaction id](/ru/docs/terminology#transaction-id).
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

[Previous« Solana RPC Methods](/ru/docs/rpc)[NextHTTP Methods
»](/ru/docs/rpc/http)

  * [Solana Documentation](/ru/docs)

  * [Solana RPC Methods](/ru/docs/rpc)

    * [Data Structures as JSON](/ru/docs/rpc/json-structures)
    * [HTTP Methods](/ru/docs/rpc/http)
      * [getAccountInfo](/ru/docs/rpc/http/getaccountinfo)
      * [getBalance](/ru/docs/rpc/http/getbalance)
      * [getBlock](/ru/docs/rpc/http/getblock)
      * [getBlockCommitment](/ru/docs/rpc/http/getblockcommitment)
      * [getBlockHeight](/ru/docs/rpc/http/getblockheight)
      * [getBlockProduction](/ru/docs/rpc/http/getblockproduction)
      * [getBlockTime](/ru/docs/rpc/http/getblocktime)
      * [getBlocks](/ru/docs/rpc/http/getblocks)
      * [getBlocksWithLimit](/ru/docs/rpc/http/getblockswithlimit)
      * [getClusterNodes](/ru/docs/rpc/http/getclusternodes)
      * [getEpochInfo](/ru/docs/rpc/http/getepochinfo)
      * [getEpochSchedule](/ru/docs/rpc/http/getepochschedule)
      * [getFeeForMessage](/ru/docs/rpc/http/getfeeformessage)
      * [getFirstAvailableBlock](/ru/docs/rpc/http/getfirstavailableblock)
      * [getGenesisHash](/ru/docs/rpc/http/getgenesishash)
      * [getHealth](/ru/docs/rpc/http/gethealth)
      * [getHighestSnapshotSlot](/ru/docs/rpc/http/gethighestsnapshotslot)
      * [getIdentity](/ru/docs/rpc/http/getidentity)
      * [getInflationGovernor](/ru/docs/rpc/http/getinflationgovernor)
      * [getInflationRate](/ru/docs/rpc/http/getinflationrate)
      * [getInflationReward](/ru/docs/rpc/http/getinflationreward)
      * [getLargestAccounts](/ru/docs/rpc/http/getlargestaccounts)
      * [getLatestBlockhash](/ru/docs/rpc/http/getlatestblockhash)
      * [getLeaderSchedule](/ru/docs/rpc/http/getleaderschedule)
      * [getMaxRetransmitSlot](/ru/docs/rpc/http/getmaxretransmitslot)
      * [getMaxShredInsertSlot](/ru/docs/rpc/http/getmaxshredinsertslot)
      * [getMinimumBalanceForRentExemption](/ru/docs/rpc/http/getminimumbalanceforrentexemption)
      * [getMultipleAccounts](/ru/docs/rpc/http/getmultipleaccounts)
      * [getProgramAccounts](/ru/docs/rpc/http/getprogramaccounts)
      * [getRecentPerformanceSamples](/ru/docs/rpc/http/getrecentperformancesamples)
      * [getRecentPrioritizationFees](/ru/docs/rpc/http/getrecentprioritizationfees)
      * [getSignatureStatuses](/ru/docs/rpc/http/getsignaturestatuses)
      * [getSignaturesForAddress](/ru/docs/rpc/http/getsignaturesforaddress)
      * [getSlot](/ru/docs/rpc/http/getslot)
      * [getSlotLeader](/ru/docs/rpc/http/getslotleader)
      * [getSlotLeaders](/ru/docs/rpc/http/getslotleaders)
      * [getStakeActivation](/ru/docs/rpc/http/getstakeactivation)
      * [getStakeMinimumDelegation](/ru/docs/rpc/http/getstakeminimumdelegation)
      * [getSupply](/ru/docs/rpc/http/getsupply)
      * [getTokenAccountBalance](/ru/docs/rpc/http/gettokenaccountbalance)
      * [getTokenAccountsByDelegate](/ru/docs/rpc/http/gettokenaccountsbydelegate)
      * [getTokenAccountsByOwner](/ru/docs/rpc/http/gettokenaccountsbyowner)
      * [getTokenLargestAccounts](/ru/docs/rpc/http/gettokenlargestaccounts)
      * [getTokenSupply](/ru/docs/rpc/http/gettokensupply)
      * [getTransaction](/ru/docs/rpc/http/gettransaction)
      * [getTransactionCount](/ru/docs/rpc/http/gettransactioncount)
      * [getVersion](/ru/docs/rpc/http/getversion)
      * [getVoteAccounts](/ru/docs/rpc/http/getvoteaccounts)
      * [isBlockhashValid](/ru/docs/rpc/http/isblockhashvalid)
      * [minimumLedgerSlot](/ru/docs/rpc/http/minimumledgerslot)
      * [requestAirdrop](/ru/docs/rpc/http/requestairdrop)
      * [sendTransaction](/ru/docs/rpc/http/sendtransaction)
      * [simulateTransaction](/ru/docs/rpc/http/simulatetransaction)
    * [Websocket Methods](/ru/docs/rpc/websocket)
      * [accountSubscribe](/ru/docs/rpc/websocket/accountsubscribe)
      * [accountUnsubscribe](/ru/docs/rpc/websocket/accountunsubscribe)
      * [blockSubscribe](/ru/docs/rpc/websocket/blocksubscribe)
      * [blockUnsubscribe](/ru/docs/rpc/websocket/blockunsubscribe)
      * [logsSubscribe](/ru/docs/rpc/websocket/logssubscribe)
      * [logsUnsubscribe](/ru/docs/rpc/websocket/logsunsubscribe)
      * [programSubscribe](/ru/docs/rpc/websocket/programsubscribe)
      * [programUnsubscribe](/ru/docs/rpc/websocket/programunsubscribe)
      * [rootSubscribe](/ru/docs/rpc/websocket/rootsubscribe)
      * [rootUnsubscribe](/ru/docs/rpc/websocket/rootunsubscribe)
      * [signatureSubscribe](/ru/docs/rpc/websocket/signaturesubscribe)
      * [signatureUnsubscribe](/ru/docs/rpc/websocket/signatureunsubscribe)
      * [slotSubscribe](/ru/docs/rpc/websocket/slotsubscribe)
      * [slotUnsubscribe](/ru/docs/rpc/websocket/slotunsubscribe)
      * [slotsUpdatesSubscribe](/ru/docs/rpc/websocket/slotsupdatessubscribe)
      * [slotsUpdatesUnsubscribe](/ru/docs/rpc/websocket/slotsupdatesunsubscribe)
      * [voteSubscribe](/ru/docs/rpc/websocket/votesubscribe)
      * [voteUnsubscribe](/ru/docs/rpc/websocket/voteunsubscribe)
    * Deprecated Methods
      * [getConfirmedBlock](/ru/docs/rpc/deprecated/getconfirmedblock)
      * [getConfirmedBlocks](/ru/docs/rpc/deprecated/getconfirmedblocks)
      * [getConfirmedBlocksWithLimit](/ru/docs/rpc/deprecated/getconfirmedblockswithlimit)
      * [getConfirmedSignaturesForAddress2](/ru/docs/rpc/deprecated/getconfirmedsignaturesforaddress2)
      * [getConfirmedTransaction](/ru/docs/rpc/deprecated/getconfirmedtransaction)
      * [getFeeCalculatorForBlockhash](/ru/docs/rpc/deprecated/getfeecalculatorforblockhash)
      * [getFeeRateGovernor](/ru/docs/rpc/deprecated/getfeerategovernor)
      * [getFees](/ru/docs/rpc/deprecated/getfees)
      * [getRecentBlockhash](/ru/docs/rpc/deprecated/getrecentblockhash)
      * [getSnapshotSlot](/ru/docs/rpc/deprecated/getsnapshotslot)

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

