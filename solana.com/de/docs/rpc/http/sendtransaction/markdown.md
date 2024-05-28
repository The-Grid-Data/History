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

# [sendTransaction RPC Method](/de/docs/rpc/http/sendtransaction)

[Edit Page](https://github.com/solana-foundation/developer-
content/tree/main/docs/rpc/http/sendTransaction.mdx)

Submits a signed transaction to the cluster for processing.

This method does not alter the transaction in any way; it relays the
transaction created by clients to the node as-is.

If the node's rpc service receives the transaction, this method immediately
succeeds, without waiting for any confirmations. A successful response from
this method does not guarantee the transaction is processed or confirmed by
the cluster.

While the rpc service will reasonably retry to submit it, the transaction
could be rejected if transaction's `recent_blockhash` expires before it lands.

Use
[`getSignatureStatuses`](/de/docs/rpc/http/sendtransaction#getsignaturestatuses)
to ensure a transaction is processed and confirmed.

Before submitting, the following preflight checks are performed:

  1. The transaction signatures are verified
  2. The transaction is simulated against the bank slot specified by the preflight commitment. On failure an error will be returned. Preflight checks may be disabled if desired. It is recommended to specify the same commitment and preflight commitment to avoid confusing behavior.

The returned signature is the first signature in the transaction, which is
used to identify the transaction ([transaction
id](/de/docs/terminology#transaction-id)). This identifier can be easily
extracted from the transaction data before submission.

### Parameters #

`string` required

Fully-signed Transaction, as encoded string.

`object` optional

Configuration object containing the following optional fields:

[encoding](/de/docs/rpc#parsed-responses) `string`

Default: `base58`

Encoding used for the transaction data.

Values: `base58` (_slow_ , **DEPRECATED**), or `base64`.

skipPreflight `bool`

Default: `false`

when `true`, skip the preflight transaction checks

[preflightCommitment](/de/docs/rpc#configuring-state-commitment) `string`

Default: `finalized`

Commitment level to use for preflight.

maxRetries `usize`

Maximum number of times for the RPC node to retry sending the transaction to
the leader. If this parameter not provided, the RPC node will retry the
transaction until it is finalized or until the blockhash expires.

minContextSlot `number`

set the minimum slot at which to perform preflight transaction checks

### Result #

`<string>` \- First Transaction Signature embedded in the transaction, as
base-58 encoded string ([transaction id](/de/docs/terminology#transaction-id))

### Code sample #

    
    
    curl https://api.devnet.solana.com -X POST -H "Content-Type: application/json" -d '
      {
        "jsonrpc": "2.0",
        "id": 1,
        "method": "sendTransaction",
        "params": [
          "4hXTCkRzt9WyecNzV1XPgCDfGAZzQKNxLXgynz5QDuWWPSAZBZSHptvWRL3BjCvzUXRdKvHL2b7yGrRQcWyaqsaBCncVG7BFggS8w9snUts67BSh3EqKpXLUm5UMHfD7ZBe9GhARjbNQMLJ1QD3Spr6oMTBU6EhdB4RD8CP2xUxr2u3d6fos36PD98XS6oX8TQjLpsMwncs5DAMiD4nNnR8NBfyghGCWvCVifVwvA8B8TJxE1aiyiv2L429BCWfyzAme5sZW8rDb14NeCQHhZbtNqfXhcp2tAnaAT"
        ]
      }
    '

### Response #

    
    
    {
      "jsonrpc": "2.0",
      "result": "2id3YC2jK9G5Wo2phDx4gJVAew8DcY5NAojnVuao8rkxwPYPe8cSwE5GzhEgJA2y8fVjDEo6iR6ykBvDxrTQrtpb",
      "id": 1
    }

[Previous«
requestAirdrop](/de/docs/rpc/http/requestairdrop)[NextsimulateTransaction
»](/de/docs/rpc/http/simulatetransaction)

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

