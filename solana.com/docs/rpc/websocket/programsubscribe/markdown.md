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

# [programSubscribe RPC Method](/docs/rpc/websocket/programsubscribe)

[Edit Page](https://github.com/solana-foundation/developer-
content/tree/main/docs/rpc/websocket/programSubscribe.mdx)

Subscribe to a program to receive notifications when the lamports or data for
an account owned by the given program changes

### Parameters #

`string` required

Pubkey of the `program_id`, as base-58 encoded string

`object` optional

Configuration object containing the following fields:

[commitment](/docs/rpc#configuring-state-commitment) `string` optional

[filters](/docs/rpc#filter-criteria) `array` optional

filter results using various filter objects

Info

The resultant account must meet **ALL** filter criteria to be included in the
returned results

[encoding](/docs/rpc#parsed-responses) `string` optional

Encoding format for Account data

Values: `base58``base64``base64+zstd``jsonParsed`

  * `base58` is slow.
  * `jsonParsed` encoding attempts to use program-specific state parsers to return more human-readable and explicit account state data.
  * If `jsonParsed` is requested but a parser cannot be found, the field falls back to `base64` encoding, detectable when the `data` field is type `string`.

### Result #

`<integer>` \- Subscription id (needed to unsubscribe)

### Code sample #

    
    
    {
      "jsonrpc": "2.0",
      "id": 1,
      "method": "programSubscribe",
      "params": [
        "11111111111111111111111111111111",
        {
          "encoding": "base64",
          "commitment": "finalized"
        }
      ]
    }
    {
      "jsonrpc": "2.0",
      "id": 1,
      "method": "programSubscribe",
      "params": [
        "11111111111111111111111111111111",
        {
          "encoding": "jsonParsed"
        }
      ]
    }
    {
      "jsonrpc": "2.0",
      "id": 1,
      "method": "programSubscribe",
      "params": [
        "11111111111111111111111111111111",
        {
          "encoding": "base64",
          "filters": [
            {
              "dataSize": 80
            }
          ]
        }
      ]
    }

### Response #

    
    
    { "jsonrpc": "2.0", "result": 24040, "id": 1 }

#### Notification format #

The notification format is a **single** program account object as seen in the
[getProgramAccounts](/docs/rpc/http/getprogramaccounts) RPC HTTP method.

Base58 encoding:

    
    
    {
      "jsonrpc": "2.0",
      "method": "programNotification",
      "params": {
        "result": {
          "context": {
            "slot": 5208469
          },
          "value": {
            "pubkey": "H4vnBqifaSACnKa7acsxstsY1iV1bvJNxsCY7enrd1hq",
            "account": {
              "data": [
                "11116bv5nS2h3y12kD1yUKeMZvGcKLSjQgX6BeV7u1FrjeJcKfsHPXHRDEHrBesJhZyqnnq9qJeUuF7WHxiuLuL5twc38w2TXNLxnDbjmuR",
                "base58"
              ],
              "executable": false,
              "lamports": 33594,
              "owner": "11111111111111111111111111111111",
              "rentEpoch": 636,
              "space": 80
            }
          }
        },
        "subscription": 24040
      }
    }

Parsed-JSON encoding:

    
    
    {
      "jsonrpc": "2.0",
      "method": "programNotification",
      "params": {
        "result": {
          "context": {
            "slot": 5208469
          },
          "value": {
            "pubkey": "H4vnBqifaSACnKa7acsxstsY1iV1bvJNxsCY7enrd1hq",
            "account": {
              "data": {
                "program": "nonce",
                "parsed": {
                  "type": "initialized",
                  "info": {
                    "authority": "Bbqg1M4YVVfbhEzwA9SpC9FhsaG83YMTYoR4a8oTDLX",
                    "blockhash": "LUaQTmM7WbMRiATdMMHaRGakPtCkc2GHtH57STKXs6k",
                    "feeCalculator": {
                      "lamportsPerSignature": 5000
                    }
                  }
                }
              },
              "executable": false,
              "lamports": 33594,
              "owner": "11111111111111111111111111111111",
              "rentEpoch": 636,
              "space": 80
            }
          }
        },
        "subscription": 24040
      }
    }

[Previous«
logsUnsubscribe](/docs/rpc/websocket/logsunsubscribe)[NextprogramUnsubscribe
»](/docs/rpc/websocket/programunsubscribe)

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

