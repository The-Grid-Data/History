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

[Home](/ru)>[Solana Documentation](/ru/docs)>[Solana RPC
Methods](/ru/docs/rpc)>[HTTP Methods](/ru/docs/rpc/http)

# [getBlock RPC Method](/ru/docs/rpc/http/getblock)

[Edit Page](https://github.com/solana-foundation/developer-
content/tree/main/docs/rpc/http/getBlock.mdx)

Returns identity and transaction information about a confirmed block in the
ledger

### Parameters #

`u64` required

slot number, as `u64` integer

`object` optional

Configuration object containing the following fields:

[commitment](/ru/docs/rpc#configuring-state-commitment) `string` optional

Default: `finalized`

  * `processed` is not supported.

[encoding](/ru/docs/rpc#parsed-responses) `string` optional

Default: `json`

encoding format for each returned Transaction

Values: `json``jsonParsed``base58``base64`

  * `jsonParsed` attempts to use program-specific instruction parsers to return more human-readable and explicit data in the `transaction.message.instructions` list.
  * If `jsonParsed` is requested but a parser cannot be found, the instruction falls back to regular JSON encoding (`accounts`, `data`, and `programIdIndex` fields).

transactionDetails `string` optional

Default: `full`

level of transaction detail to return

Values: `full``accounts``signatures``none`

  * If `accounts` are requested, transaction details only include signatures and an annotated list of accounts in each transaction.
  * Transaction metadata is limited to only: fee, err, pre_balances, post_balances, pre_token_balances, and post_token_balances.

maxSupportedTransactionVersion `number` optional

the max transaction version to return in responses.

  * If the requested block contains a transaction with a higher version, an error will be returned.
  * If this parameter is omitted, only legacy transactions will be returned, and a block containing any versioned transaction will prompt the error.

rewards `bool` optional

whether to populate the `rewards` array. If parameter not provided, the
default includes rewards.

### Result #

The result field will be an object with the following fields:

  * `<null>` \- if specified block is not confirmed
  * `<object>` \- if block is confirmed, an object with the following fields:
    * `blockhash: <string>` \- the blockhash of this block, as base-58 encoded string
    * `previousBlockhash: <string>` \- the blockhash of this block's parent, as base-58 encoded string; if the parent block is not available due to ledger cleanup, this field will return "11111111111111111111111111111111"
    * `parentSlot: <u64>` \- the slot index of this block's parent
    * `transactions: <array>` \- present if "full" transaction details are requested; an array of JSON objects containing:
      * `transaction: <object|[string,encoding]>` \- [Transaction](/ru/docs/rpc/json-structures#transactions) object, either in JSON format or encoded binary data, depending on encoding parameter
      * `meta: <object>` \- transaction status metadata object, containing `null` or:
        * `err: <object|null>` \- Error if transaction failed, null if transaction succeeded. [TransactionError definitions](https://github.com/solana-labs/solana/blob/c0c60386544ec9a9ec7119229f37386d9f070523/sdk/src/transaction/error.rs#L13)
        * `fee: <u64>` \- fee this transaction was charged, as u64 integer
        * `preBalances: <array>` \- array of u64 account balances from before the transaction was processed
        * `postBalances: <array>` \- array of u64 account balances after the transaction was processed
        * `innerInstructions: <array|null>` \- List of [inner instructions](/ru/docs/rpc/json-structures#inner-instructions) or `null` if inner instruction recording was not enabled during this transaction
        * `preTokenBalances: <array|undefined>` \- List of [token balances](/ru/docs/rpc/json-structures#token-balances) from before the transaction was processed or omitted if token balance recording was not yet enabled during this transaction
        * `postTokenBalances: <array|undefined>` \- List of [token balances](/ru/docs/rpc/json-structures#token-balances) from after the transaction was processed or omitted if token balance recording was not yet enabled during this transaction
        * `logMessages: <array|null>` \- array of string log messages or `null` if log message recording was not enabled during this transaction
        * `rewards: <array|null>` \- transaction-level rewards, populated if rewards are requested; an array of JSON objects containing:
          * `pubkey: <string>` \- The public key, as base-58 encoded string, of the account that received the reward
          * `lamports: <i64>`\- number of reward lamports credited or debited by the account, as a i64
          * `postBalance: <u64>` \- account balance in lamports after the reward was applied
          * `rewardType: <string|undefined>` \- type of reward: "fee", "rent", "voting", "staking"
          * `commission: <u8|undefined>` \- vote account commission when the reward was credited, only present for voting and staking rewards
        * DEPRECATED: `status: <object>` \- Transaction status
          * `"Ok": <null>` \- Transaction was successful
          * `"Err": <ERR>` \- Transaction failed with TransactionError
        * `loadedAddresses: <object|undefined>` \- Transaction addresses loaded from address lookup tables. Undefined if `maxSupportedTransactionVersion` is not set in request params, or if `jsonParsed` encoding is set in request params.
          * `writable: <array[string]>` \- Ordered list of base-58 encoded addresses for writable loaded accounts
          * `readonly: <array[string]>` \- Ordered list of base-58 encoded addresses for readonly loaded accounts
        * `returnData: <object|undefined>` \- the most-recent return data generated by an instruction in the transaction, with the following fields:
          * `programId: <string>` \- the program that generated the return data, as base-58 encoded Pubkey
          * `data: <[string, encoding]>` \- the return data itself, as base-64 encoded binary data
        * `computeUnitsConsumed: <u64|undefined>` \- number of [compute units](/ru/docs/core/fees#compute-budget) consumed by the transaction
      * `version: <"legacy"|number|undefined>` \- Transaction version. Undefined if `maxSupportedTransactionVersion` is not set in request params.
    * `signatures: <array>` \- present if "signatures" are requested for transaction details; an array of signatures strings, corresponding to the transaction order in the block
    * `rewards: <array|undefined>` \- block-level rewards, present if rewards are requested; an array of JSON objects containing:
      * `pubkey: <string>` \- The public key, as base-58 encoded string, of the account that received the reward
      * `lamports: <i64>`\- number of reward lamports credited or debited by the account, as a i64
      * `postBalance: <u64>` \- account balance in lamports after the reward was applied
      * `rewardType: <string|undefined>` \- type of reward: "fee", "rent", "voting", "staking"
      * `commission: <u8|undefined>` \- vote account commission when the reward was credited, only present for voting and staking rewards
    * `blockTime: <i64|null>` \- estimated production time, as Unix timestamp (seconds since the Unix epoch). null if not available
    * `blockHeight: <u64|null>` \- the number of blocks beneath this block

### Code sample #

    
    
    curl https://api.devnet.solana.com -X POST -H "Content-Type: application/json" -d '
      {
        "jsonrpc": "2.0","id":1,
        "method":"getBlock",
        "params": [
          430,
          {
            "encoding": "json",
            "maxSupportedTransactionVersion":0,
            "transactionDetails":"full",
            "rewards":false
          }
        ]
      }
    '

### Response #

    
    
    {
      "jsonrpc": "2.0",
      "result": {
        "blockHeight": 428,
        "blockTime": null,
        "blockhash": "3Eq21vXNB5s86c62bVuUfTeaMif1N2kUqRPBmGRJhyTA",
        "parentSlot": 429,
        "previousBlockhash": "mfcyqEXB3DnHXki6KjjmZck6YjmZLvpAByy2fj4nh6B",
        "transactions": [
          {
            "meta": {
              "err": null,
              "fee": 5000,
              "innerInstructions": [],
              "logMessages": [],
              "postBalances": [499998932500, 26858640, 1, 1, 1],
              "postTokenBalances": [],
              "preBalances": [499998937500, 26858640, 1, 1, 1],
              "preTokenBalances": [],
              "rewards": null,
              "status": {
                "Ok": null
              }
            },
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
          }
        ]
      },
      "id": 1
    }

[Previous« getBalance](/ru/docs/rpc/http/getbalance)[NextgetBlockCommitment
»](/ru/docs/rpc/http/getblockcommitment)

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

