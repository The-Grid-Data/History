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

[Home](/)>[Solana Documentation](/docs)>[Solana RPC
Methods](/docs/rpc)>Deprecated Methods

# [getConfirmedBlock RPC Method](/docs/rpc/deprecated/getconfirmedblock)

[Edit Page](https://github.com/solana-foundation/developer-
content/tree/main/docs/rpc/deprecated/getConfirmedBlock.mdx)

Returns identity and transaction information about a confirmed block in the
ledger

Deprecated Method

This method is expected to be removed in `solana-core` v2.0. Please use
[getBlock](/docs/rpc/http/getblock) instead.

### Parameters #

`u64` required

slot number, as u64 integer

`object` optional

Configuration object containing the following fields:

[commitment](/docs/rpc#configuring-state-commitment) `string` optional

Default: `finalized`

transactionDetails `string` optional

Default: `full`

level of transaction detail to return, either "full", "signatures", or "none"

rewards `bool` optional

Default: `true`

whether to populate the `rewards` array.

[encoding](/docs/rpc#parsed-responses) `string` optional

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
      * `transaction: <object|[string,encoding]>` \- [Transaction](/docs/rpc/json-structures#transactions) object, either in JSON format or encoded binary data, depending on encoding parameter
      * `meta: <object>` \- transaction status metadata object, containing `null` or:
        * `err: <object|null>` \- Error if transaction failed, null if transaction succeeded. [TransactionError definitions](https://github.com/solana-labs/solana/blob/c0c60386544ec9a9ec7119229f37386d9f070523/sdk/src/transaction/error.rs#L13)
        * `fee: <u64>` \- fee this transaction was charged, as u64 integer
        * `preBalances: <array>` \- array of u64 account balances from before the transaction was processed
        * `postBalances: <array>` \- array of u64 account balances after the transaction was processed
        * `innerInstructions: <array|null>` \- List of [inner instructions](/docs/rpc/json-structures#inner-instructions) or `null` if inner instruction recording was not enabled during this transaction
        * `preTokenBalances: <array|undefined>` \- List of [token balances](/docs/rpc/json-structures#token-balances) from before the transaction was processed or omitted if token balance recording was not yet enabled during this transaction
        * `postTokenBalances: <array|undefined>` \- List of [token balances](/docs/rpc/json-structures#token-balances) from after the transaction was processed or omitted if token balance recording was not yet enabled during this transaction
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

  * [Transaction Structure](/docs/rpc/json-structures#transactions)
  * [Inner Instructions Structure](/docs/rpc/json-structures#inner-instructions)
  * [Token Balances Structure](/docs/rpc/json-structures#token-balances)

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
voteUnsubscribe](/docs/rpc/websocket/voteunsubscribe)[NextgetConfirmedBlocks
»](/docs/rpc/deprecated/getconfirmedblocks)

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

