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

[Home](/de)>[Solana Dokumentation](/de/docs)>[Solana RPC
Methods](/de/docs/rpc)>[HTTP Methods](/de/docs/rpc/http)

# [getTransaction RPC Method](/de/docs/rpc/http/gettransaction)

[Edit Page](https://github.com/solana-foundation/developer-
content/tree/main/docs/rpc/http/getTransaction.mdx)

Returns transaction details for a confirmed transaction

### Parameters #

`string` required

Transaction signature, as base-58 encoded string

`object` optional

Configuration object containing the following fields:

[commitment](/de/docs/rpc#configuring-state-commitment) `string` optional

  * `processed` is not supported.

maxSupportedTransactionVersion `number` optional

Set the max transaction version to return in responses. If the requested
transaction is a higher version, an error will be returned. If this parameter
is omitted, only legacy transactions will be returned, and any versioned
transaction will prompt the error.

[encoding](/de/docs/rpc#parsed-responses) `string` optional

Default: `json`

Encoding for the returned Transaction

Values: `json``jsonParsed``base64``base58`

  * `jsonParsed` encoding attempts to use program-specific state parsers to return more human-readable and explicit data in the `transaction.message.instructions` list.
  * If `jsonParsed` is requested but a parser cannot be found, the instruction falls back to regular JSON encoding (`accounts`, `data`, and `programIdIndex` fields).

### Result #

  * `<null>` \- if transaction is not found or not confirmed
  * `<object>` \- if transaction is confirmed, an object with the following fields:
    * `slot: <u64>` \- the slot this transaction was processed in
    * `transaction: <object|[string,encoding]>` \- [Transaction](/de/docs/rpc/json-structures#transactions) object, either in JSON format or encoded binary data, depending on encoding parameter
    * `blockTime: <i64|null>` \- estimated production time, as Unix timestamp (seconds since the Unix epoch) of when the transaction was processed. null if not available
    * `meta: <object|null>` \- transaction status metadata object:
      * `err: <object|null>` \- Error if transaction failed, null if transaction succeeded. [TransactionError definitions](https://docs.rs/solana-sdk/latest/solana_sdk/transaction/enum.TransactionError.html)
      * `fee: <u64>` \- fee this transaction was charged, as u64 integer
      * `preBalances: <array>` \- array of u64 account balances from before the transaction was processed
      * `postBalances: <array>` \- array of u64 account balances after the transaction was processed
      * `innerInstructions: <array|null>` \- List of [inner instructions](/de/docs/rpc/json-structures#inner-instructions) or `null` if inner instruction recording was not enabled during this transaction
      * `preTokenBalances: <array|undefined>` \- List of [token balances](/de/docs/rpc/json-structures#token-balances) from before the transaction was processed or omitted if token balance recording was not yet enabled during this transaction
      * `postTokenBalances: <array|undefined>` \- List of [token balances](/de/docs/rpc/json-structures#token-balances) from after the transaction was processed or omitted if token balance recording was not yet enabled during this transaction
      * `logMessages: <array|null>` \- array of string log messages or `null` if log message recording was not enabled during this transaction
      * DEPRECATED: `status: <object>` \- Transaction status
        * `"Ok": <null>` \- Transaction was successful
        * `"Err": <ERR>` \- Transaction failed with TransactionError
      * `rewards: <array|null>` \- transaction-level rewards, populated if rewards are requested; an array of JSON objects containing:
        * `pubkey: <string>` \- The public key, as base-58 encoded string, of the account that received the reward
        * `lamports: <i64>`\- number of reward lamports credited or debited by the account, as a i64
        * `postBalance: <u64>` \- account balance in lamports after the reward was applied
        * `rewardType: <string>` \- type of reward: currently only "rent", other types may be added in the future
        * `commission: <u8|undefined>` \- vote account commission when the reward was credited, only present for voting and staking rewards
      * `loadedAddresses: <object|undefined>` \- Transaction addresses loaded from address lookup tables. Undefined if `maxSupportedTransactionVersion` is not set in request params, or if `jsonParsed` encoding is set in request params.
        * `writable: <array[string]>` \- Ordered list of base-58 encoded addresses for writable loaded accounts
        * `readonly: <array[string]>` \- Ordered list of base-58 encoded addresses for readonly loaded accounts
      * `returnData: <object|undefined>` \- the most-recent return data generated by an instruction in the transaction, with the following fields:
        * `programId: <string>` \- the program that generated the return data, as base-58 encoded Pubkey
        * `data: <[string, encoding]>` \- the return data itself, as base-64 encoded binary data
      * `computeUnitsConsumed: <u64|undefined>` \- number of [compute units](/de/docs/core/fees#compute-budget) consumed by the transaction
    * `version: <"legacy"|number|undefined>` \- Transaction version. Undefined if `maxSupportedTransactionVersion` is not set in request params.

### Code sample #

    
    
    curl https://api.devnet.solana.com -X POST -H "Content-Type: application/json" -d '
      {
        "jsonrpc": "2.0",
        "id": 1,
        "method": "getTransaction",
        "params": [
          "2nBhEBYYvfaAe16UMNqRHre4YNSskvuYgx3M6E4JP1oDYvZEJHvoPzyUidNgNX5r9sTyN1J9UxtbCXy2rqYcuyuv",
          "json"
        ]
      }
    '

### Response #

    
    
    {
      "jsonrpc": "2.0",
      "result": {
        "meta": {
          "err": null,
          "fee": 5000,
          "innerInstructions": [],
          "postBalances": [499998932500, 26858640, 1, 1, 1],
          "postTokenBalances": [],
          "preBalances": [499998937500, 26858640, 1, 1, 1],
          "preTokenBalances": [],
          "rewards": [],
          "status": {
            "Ok": null
          }
        },
        "slot": 430,
        "transaction": {
          "message": {
            "accountKeys": [
              "3UVYmECPPMZSCqWKfENfuoTv51fTDTWicX9xmBD2euKe",
              "AjozzgE83A3x1sHNUR64hfH7zaEBWeMaFuAN9kQgujrc",
              "SysvarS1otHashes111111111111111111111111111",
              "SysvarC1ock11111111111111111111111111111111",
              "Vote111111111111111111111111111111111111111"
            ],
            "header": {
              "numReadonlySignedAccounts": 0,
              "numReadonlyUnsignedAccounts": 3,
              "numRequiredSignatures": 1
            },
            "instructions": [
              {
                "accounts": [1, 2, 3, 0],
                "data": "37u9WtQpcm6ULa3WRQHmj49EPs4if7o9f1jSRVZpm2dvihR9C8jY4NqEwXUbLwx15HBSNcP1",
                "programIdIndex": 4
              }
            ],
            "recentBlockhash": "mfcyqEXB3DnHXki6KjjmZck6YjmZLvpAByy2fj4nh6B"
          },
          "signatures": [
            "2nBhEBYYvfaAe16UMNqRHre4YNSskvuYgx3M6E4JP1oDYvZEJHvoPzyUidNgNX5r9sTyN1J9UxtbCXy2rqYcuyuv"
          ]
        }
      },
      "blockTime": null,
      "id": 1
    }

[Previous«
getTokenSupply](/de/docs/rpc/http/gettokensupply)[NextgetTransactionCount
»](/de/docs/rpc/http/gettransactioncount)

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

