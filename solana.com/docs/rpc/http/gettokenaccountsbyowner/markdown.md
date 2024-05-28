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

# [getTokenAccountsByOwner RPC Method](/docs/rpc/http/gettokenaccountsbyowner)

[Edit Page](https://github.com/solana-foundation/developer-
content/tree/main/docs/rpc/http/getTokenAccountsByOwner.mdx)

Returns all SPL Token accounts by token owner.

### Parameters #

`string` required

Pubkey of account delegate to query, as base-58 encoded string

`object` optional

A JSON object with one of the following fields:

  * `mint: <string>` \- Pubkey of the specific token Mint to limit accounts to, as base-58 encoded string; or
  * `programId: <string>` \- Pubkey of the Token program that owns the accounts, as base-58 encoded string

`object` optional

Configuration object containing the following fields:

[commitment](/docs/rpc#configuring-state-commitment) `string` optional

minContextSlot `number` optional

The minimum slot that the request can be evaluated at

dataSlice `object` optional

Request a slice of the account's data.

  * `length: <usize>` \- number of bytes to return
  * `offset: <usize>` \- byte offset from which to start reading

Info

Data slicing is only available for `base58`, `base64`, or `base64+zstd`
encodings.

[encoding](/docs/rpc#parsed-responses) `string` optional

Encoding format for Account data

Values: `base58``base64``base64+zstd``jsonParsed`

  * `base58` is slow and limited to less than 129 bytes of Account data.
  * `base64` will return base64 encoded data for Account data of any size.
  * `base64+zstd` compresses the Account data using [Zstandard](https://facebook.github.io/zstd/) and base64-encodes the result.
  * `jsonParsed` encoding attempts to use program-specific state parsers to return more human-readable and explicit account state data.
  * If `jsonParsed` is requested but a parser cannot be found, the field falls back to `base64` encoding, detectable when the `data` field is type `string`.

### Result #

The result will be an RpcResponse JSON object with `value` equal to an array
of JSON objects, which will contain:

  * `pubkey: <string>` \- the account Pubkey as base-58 encoded string
  * `account: <object>` \- a JSON object, with the following sub fields:
    * `lamports: <u64>` \- number of lamports assigned to this account, as a u64
    * `owner: <string>` \- base-58 encoded Pubkey of the program this account has been assigned to
    * `data: <object>` \- Token state data associated with the account, either as encoded binary data or in JSON format `{<program>: <state>}`
    * `executable: <bool>` \- boolean indicating if the account contains a program (and is strictly read-only)
    * `rentEpoch: <u64>` \- the epoch at which this account will next owe rent, as u64
    * `size: <u64>` \- the data size of the account

When the data is requested with the `jsonParsed` encoding a format similar to
that of the [Token Balances Structure](/docs/rpc/json-structures#token-
balances) can be expected inside the structure, both for the `tokenAmount` and
the `delegatedAmount` \- with the latter being an optional object.

### Code sample #

    
    
    curl https://api.devnet.solana.com -X POST -H "Content-Type: application/json" -d '
      {
        "jsonrpc": "2.0",
        "id": 1,
        "method": "getTokenAccountsByOwner",
        "params": [
          "4Qkev8aNZcqFNSRhQzwyLMFSsi94jHqE8WNVTJzTP99F",
          {
            "mint": "3wyAj7Rt1TWVPZVteFJPLa26JmLvdb1CAKEFZm3NY75E"
          },
          {
            "encoding": "jsonParsed"
          }
        ]
      }
    '

### Response #

    
    
    {
      "jsonrpc": "2.0",
      "result": {
        "context": {
          "slot": 1114
        },
        "value": [
          {
            "account": {
              "data": {
                "program": "spl-token",
                "parsed": {
                  "accountType": "account",
                  "info": {
                    "tokenAmount": {
                      "amount": "1",
                      "decimals": 1,
                      "uiAmount": 0.1,
                      "uiAmountString": "0.1"
                    },
                    "delegate": "4Nd1mBQtrMJVYVfKf2PJy9NZUZdTAsp7D4xWLs4gDB4T",
                    "delegatedAmount": {
                      "amount": "1",
                      "decimals": 1,
                      "uiAmount": 0.1,
                      "uiAmountString": "0.1"
                    },
                    "state": "initialized",
                    "isNative": false,
                    "mint": "3wyAj7Rt1TWVPZVteFJPLa26JmLvdb1CAKEFZm3NY75E",
                    "owner": "4Qkev8aNZcqFNSRhQzwyLMFSsi94jHqE8WNVTJzTP99F"
                  },
                  "type": "account"
                },
                "space": 165
              },
              "executable": false,
              "lamports": 1726080,
              "owner": "TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA",
              "rentEpoch": 4,
              "space": 165
            },
            "pubkey": "C2gJg6tKpQs41PRS1nC8aw3ZKNZK3HQQZGVrDFDup5nx"
          }
        ]
      },
      "id": 1
    }

[Previous«
getTokenAccountsByDelegate](/docs/rpc/http/gettokenaccountsbydelegate)[NextgetTokenLargestAccounts
»](/docs/rpc/http/gettokenlargestaccounts)

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

