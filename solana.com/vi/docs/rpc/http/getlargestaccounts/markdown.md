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

[Home](/vi)>[Solana Documentation](/vi/docs)>[Solana RPC
Methods](/vi/docs/rpc)>[HTTP Methods](/vi/docs/rpc/http)

# [getLargestAccounts RPC Method](/vi/docs/rpc/http/getlargestaccounts)

[Edit Page](https://github.com/solana-foundation/developer-
content/tree/main/docs/rpc/http/getLargestAccounts.mdx)

Returns the 20 largest accounts, by lamport balance (results may be cached up
to two hours)

### Parameters #

`object` optional

Configuration object containing the following fields:

[commitment](/vi/docs/rpc#configuring-state-commitment) `string` optional

filter `string` optional

filter results by account type

Values: `circulating``nonCirculating`

### Result #

The result will be an RpcResponse JSON object with `value` equal to an array
of `<object>` containing:

  * `address: <string>` \- base-58 encoded address of the account
  * `lamports: <u64>` \- number of lamports in the account, as a u64

### Code sample #

    
    
    curl https://api.devnet.solana.com -X POST -H "Content-Type: application/json" -d '
      {"jsonrpc":"2.0","id":1, "method":"getLargestAccounts"}
    '

### Response #

    
    
    {
      "jsonrpc": "2.0",
      "result": {
        "context": {
          "slot": 54
        },
        "value": [
          {
            "lamports": 999974,
            "address": "99P8ZgtJYe1buSK8JXkvpLh8xPsCFuLYhz9hQFNw93WJ"
          },
          {
            "lamports": 42,
            "address": "uPwWLo16MVehpyWqsLkK3Ka8nLowWvAHbBChqv2FZeL"
          },
          {
            "lamports": 42,
            "address": "aYJCgU7REfu3XF8b3QhkqgqQvLizx8zxuLBHA25PzDS"
          },
          {
            "lamports": 42,
            "address": "CTvHVtQ4gd4gUcw3bdVgZJJqApXE9nCbbbP4VTS5wE1D"
          },
          {
            "lamports": 20,
            "address": "4fq3xJ6kfrh9RkJQsmVd5gNMvJbuSHfErywvEjNQDPxu"
          },
          {
            "lamports": 4,
            "address": "AXJADheGVp9cruP8WYu46oNkRbeASngN5fPCMVGQqNHa"
          },
          {
            "lamports": 2,
            "address": "8NT8yS6LiwNprgW4yM1jPPow7CwRUotddBVkrkWgYp24"
          },
          {
            "lamports": 1,
            "address": "SysvarEpochSchedu1e111111111111111111111111"
          },
          {
            "lamports": 1,
            "address": "11111111111111111111111111111111"
          },
          {
            "lamports": 1,
            "address": "Stake11111111111111111111111111111111111111"
          },
          {
            "lamports": 1,
            "address": "SysvarC1ock11111111111111111111111111111111"
          },
          {
            "lamports": 1,
            "address": "StakeConfig11111111111111111111111111111111"
          },
          {
            "lamports": 1,
            "address": "SysvarRent111111111111111111111111111111111"
          },
          {
            "lamports": 1,
            "address": "Config1111111111111111111111111111111111111"
          },
          {
            "lamports": 1,
            "address": "SysvarStakeHistory1111111111111111111111111"
          },
          {
            "lamports": 1,
            "address": "SysvarRecentB1ockHashes11111111111111111111"
          },
          {
            "lamports": 1,
            "address": "SysvarFees111111111111111111111111111111111"
          },
          {
            "lamports": 1,
            "address": "Vote111111111111111111111111111111111111111"
          }
        ]
      },
      "id": 1
    }

[Previous«
getInflationReward](/vi/docs/rpc/http/getinflationreward)[NextgetLatestBlockhash
»](/vi/docs/rpc/http/getlatestblockhash)

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

