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

# [getSignaturesForAddress RPC
Method](/de/docs/rpc/http/getsignaturesforaddress)

[Edit Page](https://github.com/solana-foundation/developer-
content/tree/main/docs/rpc/http/getSignaturesForAddress.mdx)

Returns signatures for confirmed transactions that include the given address
in their `accountKeys` list. Returns signatures backwards in time from the
provided signature or most recent confirmed block

### Parameters #

`string` required

Account address as base-58 encoded string

`object` optional

Configuration object containing the following fields:

[commitment](/de/docs/rpc#configuring-state-commitment) `string` optional

minContextSlot `number` optional

The minimum slot that the request can be evaluated at

limit `number` optional

Default: `1000`

maximum transaction signatures to return (between 1 and 1,000).

before `string` optional

start searching backwards from this transaction signature. If not provided the
search starts from the top of the highest max confirmed block.

until `string` optional

search until this transaction signature, if found before limit reached

### Result #

An array of `<object>`, ordered from **newest** to **oldest** transaction,
containing transaction signature information with the following fields:

  * `signature: <string>` \- transaction signature as base-58 encoded string
  * `slot: <u64>` \- The slot that contains the block with the transaction
  * `err: <object|null>` \- Error if transaction failed, null if transaction succeeded. See [TransactionError definitions](https://github.com/solana-labs/solana/blob/c0c60386544ec9a9ec7119229f37386d9f070523/sdk/src/transaction/error.rs#L13) for more info.
  * `memo: <string|null>` \- Memo associated with the transaction, null if no memo is present
  * `blockTime: <i64|null>` \- estimated production time, as Unix timestamp (seconds since the Unix epoch) of when transaction was processed. null if not available.
  * `confirmationStatus: <string|null>` \- The transaction's cluster confirmation status; Either `processed`, `confirmed`, or `finalized`. See [Commitment](/de/docs/rpc#configuring-state-commitment) for more on optimistic confirmation.

### Code sample #

    
    
    curl https://api.devnet.solana.com -X POST -H "Content-Type: application/json" -d '
      {
        "jsonrpc": "2.0",
        "id": 1,
        "method": "getSignaturesForAddress",
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
getSignatureStatuses](/de/docs/rpc/http/getsignaturestatuses)[NextgetSlot
»](/de/docs/rpc/http/getslot)

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

