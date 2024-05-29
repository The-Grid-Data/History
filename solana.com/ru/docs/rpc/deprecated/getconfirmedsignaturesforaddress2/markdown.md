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

# [getConfirmedSignaturesForAddress2 RPC
Method](/ru/docs/rpc/deprecated/getconfirmedsignaturesforaddress2)

[Edit Page](https://github.com/solana-foundation/developer-
content/tree/main/docs/rpc/deprecated/getConfirmedSignaturesForAddress2.mdx)

Returns signatures for confirmed transactions that include the given address
in their `accountKeys` list. Returns signatures backwards in time from the
provided signature or most recent confirmed block

Deprecated Method

This method is expected to be removed in `solana-core` v2.0. Please use
[getSignaturesForAddress](/ru/docs/rpc/http/getsignaturesforaddress) instead.

### Parameters #

`string` required

account address, as base-58 encoded string

`object` optional

Configuration object containing the following fields:

[commitment](/ru/docs/rpc#configuring-state-commitment) `string` optional

Default: `finalized`

limit `number` optional

maximum transaction signatures to return (between 1 and 1,000, default:
1,000).

before `string` optional

start searching backwards from this transaction signature. (If not provided
the search starts from the top of the highest max confirmed block.)

until `string` optional

search until this transaction signature, if found before limit reached.

### Result #

The result field will be an array of `<object>`, ordered from newest to oldest
transaction, containing transaction signature information with the following
fields:

  * `signature: <string>` \- transaction signature as base-58 encoded string
  * `slot: <u64>` \- The slot that contains the block with the transaction
  * `err: <object|null>` \- Error if transaction failed, null if transaction succeeded. [TransactionError definitions](https://github.com/solana-labs/solana/blob/c0c60386544ec9a9ec7119229f37386d9f070523/sdk/src/transaction/error.rs#L13)
  * `memo: <string|null>` \- Memo associated with the transaction, null if no memo is present
  * `blockTime: <i64|null>` \- estimated production time, as Unix timestamp (seconds since the Unix epoch) of when transaction was processed. null if not available.

### Code sample #

    
    
    curl https://api.devnet.solana.com -X POST -H "Content-Type: application/json" -d '
      {
        "jsonrpc": "2.0",
        "id": 1,
        "method": "getConfirmedSignaturesForAddress2",
        "params": [
          "Vote111111111111111111111111111111111111111",
          {
            "limit": 1
          }
        ]
      }
    '

### Response #

    
    
    {
      "jsonrpc": "2.0",
      "result": [
        {
          "err": null,
          "memo": null,
          "signature": "5h6xBEauJ3PK6SWCZ1PGjBvj8vDdWG3KpwATGy1ARAXFSDwt8GFXM7W5Ncn16wmqokgpiKRLuS83KUxyZyv2sUYv",
          "slot": 114,
          "blockTime": null
        }
      ],
      "id": 1
    }

[Previous«
getConfirmedBlocksWithLimit](/ru/docs/rpc/deprecated/getconfirmedblockswithlimit)[NextgetConfirmedTransaction
»](/ru/docs/rpc/deprecated/getconfirmedtransaction)

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
