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
Methods](/docs/rpc)>[Websocket Methods](/docs/rpc/websocket)

# [voteSubscribe RPC Method](/docs/rpc/websocket/votesubscribe)

[Edit Page](https://github.com/solana-foundation/developer-
content/tree/main/docs/rpc/websocket/voteSubscribe.mdx)

Subscribe to receive notification anytime a new vote is observed in gossip.
These votes are pre-consensus therefore there is no guarantee these votes will
enter the ledger.

Unstable Method

This subscription is unstable and only available if the validator was started
with the `--rpc-pubsub-enable-vote-subscription` flag. The format of this
subscription may change in the future.

### Parameters #

**None**

### Result #

`<integer>` \- subscription id (needed to unsubscribe)

### Code sample #

    
    
    { "jsonrpc": "2.0", "id": 1, "method": "voteSubscribe" }

### Response #

    
    
    { "jsonrpc": "2.0", "result": 0, "id": 1 }

#### Notification Format: #

The notification will be an object with the following fields:

  * `hash: <string>` \- The vote hash
  * `slots: <array>` \- The slots covered by the vote, as an array of u64 integers
  * `timestamp: <i64|null>` \- The timestamp of the vote
  * `signature: <string>` \- The signature of the transaction that contained this vote
  * `votePubkey: <string>` \- The public key of the vote account, as base-58 encoded string

    
    
    {
      "jsonrpc": "2.0",
      "method": "voteNotification",
      "params": {
        "result": {
          "hash": "8Rshv2oMkPu5E4opXTRyuyBeZBqQ4S477VG26wUTFxUM",
          "slots": [1, 2],
          "timestamp": null
        },
        "subscription": 0
      }
    }

[Previous«
slotsUpdatesUnsubscribe](/docs/rpc/websocket/slotsupdatesunsubscribe)[NextvoteUnsubscribe
»](/docs/rpc/websocket/voteunsubscribe)

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

