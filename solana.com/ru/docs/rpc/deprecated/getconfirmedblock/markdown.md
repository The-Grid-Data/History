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
Methods](/ru/docs/rpc)>Deprecated Methods

# [getConfirmedBlock RPC Method](/ru/docs/rpc/deprecated/getconfirmedblock)

[Edit Page](https://github.com/solana-foundation/developer-
content/tree/main/docs/rpc/deprecated/getConfirmedBlock.mdx)

Returns identity and transaction information about a confirmed block in the
ledger

Deprecated Method

This method is expected to be removed in `solana-core` v2.0. Please use
[getBlock](/ru/docs/rpc/http/getblock) instead.

### Parameters #

`u64` required

slot number, as u64 integer

`object` optional

Configuration object containing the following fields:

[commitment](/ru/docs/rpc#configuring-state-commitment) `string` optional

Default: `finalized`

transactionDetails `string` optional

Default: `full`

level of transaction detail to return, either "full", "signatures", or "none"

rewards `bool` optional

Default: `true`

whether to populate the `rewards` array.

[encoding](/ru/docs/rpc#parsed-responses) `string` optional

Default: `json`

Encoding format for Account data

Values: `json``base58``base64``jsonParsed`

  * `jsonParsed` encoding attempts to use program-specific instruction parsers to return more human-readable and explicit data in the `transaction.message.instructions` list.
  * If `jsonParsed` is requested but a parser cannot be found, the instruction falls back to regular JSON encoding (`accounts`, `data`, and `programIdIndex` fields).

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
        * DEPRECATED: `status: <object>` \- Transaction status
          * `"Ok": <null>` \- Transaction was successful
          * `"Err": <ERR>` \- Transaction failed with TransactionError
    * `signatures: <array>` \- present if "signatures" are requested for transaction details; an array of signatures strings, corresponding to the transaction order in the block
    * `rewards: <array>` \- present if rewards are requested; an array of JSON objects containing:
      * `pubkey: <string>` \- The public key, as base-58 encoded string, of the account that received the reward
      * `lamports: <i64>`\- number of reward lamports credited or debited by the account, as a i64
      * `postBalance: <u64>` \- account balance in lamports after the reward was applied
      * `rewardType: <string|undefined>` \- type of reward: "fee", "rent", "voting", "staking"
      * `commission: <u8|undefined>` \- vote account commission when the reward was credited, only present for voting and staking rewards
    * `blockTime: <i64|null>` \- estimated production time, as Unix timestamp (seconds since the Unix epoch). null if not available

#### For more details on returned data: #

  * [Transaction Structure](/ru/docs/rpc/json-structures#transactions)
  * [Inner Instructions Structure](/ru/docs/rpc/json-structures#inner-instructions)
  * [Token Balances Structure](/ru/docs/rpc/json-structures#token-balances)

### Code sample #

    
    
    curl https://api.devnet.solana.com -X POST -H "Content-Type: application/json" -d '
      {
        "jsonrpc": "2.0", "id": 1,
        "method": "getConfirmedBlock",
        "params": [430, "base64"]
      }
    '

### Response #

    
    
    {
      "jsonrpc": "2.0",
      "result": {
        "blockTime": null,
        "blockhash": "3Eq21vXNB5s86c62bVuUfTeaMif1N2kUqRPBmGRJhyTA",
        "parentSlot": 429,
        "previousBlockhash": "mfcyqEXB3DnHXki6KjjmZck6YjmZLvpAByy2fj4nh6B",
        "rewards": [],
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
              "status": {
                "Ok": null
              }
            },
            "transaction": [
              "AVj7dxHlQ9IrvdYVIjuiRFs1jLaDMHixgrv+qtHBwz51L4/ImLZhszwiyEJDIp7xeBSpm/TX5B7mYzxa+fPOMw0BAAMFJMJVqLw+hJYheizSoYlLm53KzgT82cDVmazarqQKG2GQsLgiqktA+a+FDR4/7xnDX7rsusMwryYVUdixfz1B1Qan1RcZLwqvxvJl4/t3zHragsUp0L47E24tAFUgAAAABqfVFxjHdMkoVmOYaR1etoteuKObS21cc1VbIQAAAAAHYUgdNXR0u3xNdiTr072z2DVec9EQQ/wNo1OAAAAAAAtxOUhPBp2WSjUNJEgfvy70BbxI00fZyEPvFHNfxrtEAQQEAQIDADUCAAAAAQAAAAAAAACtAQAAAAAAAAdUE18R96XTJCe+YfRfUp6WP+YKCy/72ucOL8AoBFSpAA==",
              "base64"
            ]
          }
        ]
      },
      "id": 1
    }

[Previous«
voteUnsubscribe](/ru/docs/rpc/websocket/voteunsubscribe)[NextgetConfirmedBlocks
»](/ru/docs/rpc/deprecated/getconfirmedblocks)

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

