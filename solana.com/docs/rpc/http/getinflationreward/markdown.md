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

[Home](/)>[Solana Documentation](/docs)>[Solana RPC Methods](/docs/rpc)>[HTTP
Methods](/docs/rpc/http)

# [getInflationReward RPC Method](/docs/rpc/http/getinflationreward)

[Edit Page](https://github.com/solana-foundation/developer-
content/tree/main/docs/rpc/http/getInflationReward.mdx)

Returns the inflation / staking reward for a list of addresses for an epoch

### Parameters #

`array` optional

An array of addresses to query, as base-58 encoded strings

`object` optional

Configuration object containing the following fields:

[commitment](/docs/rpc#configuring-state-commitment) `string` optional

epoch `u64` optional

An epoch for which the reward occurs. If omitted, the previous epoch will be
used

minContextSlot `number` optional

The minimum slot that the request can be evaluated at

### Result #

The result field will be a JSON array with the following fields:

  * `epoch: <u64>` \- epoch for which reward occured
  * `effectiveSlot: <u64>` \- the slot in which the rewards are effective
  * `amount: <u64>` \- reward amount in lamports
  * `postBalance: <u64>` \- post balance of the account in lamports
  * `commission: <u8|undefined>` \- vote account commission when the reward was credited

### Code sample #

    
    
    curl https://api.devnet.solana.com -X POST -H "Content-Type: application/json" -d '
      {
        "jsonrpc": "2.0",
        "id": 1,
        "method": "getInflationReward",
        "params": [
          [
            "6dmNQ5jwLeLk5REvio1JcMshcbvkYMwy26sJ8pbkvStu",
            "BGsqMegLpV6n6Ve146sSX2dTjUMj3M92HnU8BbNRMhF2"
          ],
          {"epoch": 2}
        ]
      }
    '

### Response #

    
    
    {
      "jsonrpc": "2.0",
      "result": [
        {
          "amount": 2500,
          "effectiveSlot": 224,
          "epoch": 2,
          "postBalance": 499999442500
        },
        null
      ],
      "id": 1
    }

[Previous«
getInflationRate](/docs/rpc/http/getinflationrate)[NextgetLargestAccounts
»](/docs/rpc/http/getlargestaccounts)

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

