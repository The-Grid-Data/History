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

# [getBlockTime RPC Method](/ru/docs/rpc/http/getblocktime)

[Edit Page](https://github.com/solana-foundation/developer-
content/tree/main/docs/rpc/http/getBlockTime.mdx)

Returns the estimated production time of a block.

Info

Each validator reports their UTC time to the ledger on a regular interval by
intermittently adding a timestamp to a Vote for a particular block. A
requested block's time is calculated from the stake-weighted mean of the Vote
timestamps in a set of recent blocks recorded on the ledger.

### Parameters #

`u64` required

block number, identified by Slot

### Result #

  * `<i64>` \- estimated production time, as Unix timestamp (seconds since the Unix epoch)

### Code sample #

    
    
    curl https://api.devnet.solana.com -X POST -H "Content-Type: application/json" -d '
      {
        "jsonrpc":"2.0", "id":1,
        "method": "getBlockTime",
        "params":[5]
      }
    '

### Response #

When a block time is available:

    
    
    {
      "jsonrpc": "2.0",
      "result": 1574721591,
      "id": 1
    }

When a block time is not available:

    
    
    {
      "jsonrpc": "2.0",
      "error": {
        "code": -32004,
        "message": "Block not available for slot 150"
      },
      "id": 1
    }

[Previous«
getBlockProduction](/ru/docs/rpc/http/getblockproduction)[NextgetBlocks
»](/ru/docs/rpc/http/getblocks)

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

