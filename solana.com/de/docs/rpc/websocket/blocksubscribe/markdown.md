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
Methods](/de/docs/rpc)>[Websocket Methods](/de/docs/rpc/websocket)

# [blockSubscribe RPC Method](/de/docs/rpc/websocket/blocksubscribe)

[Edit Page](https://github.com/solana-foundation/developer-
content/tree/main/docs/rpc/websocket/blockSubscribe.mdx)

Subscribe to receive notification anytime a new block is `confirmed` or
`finalized`.

Unstable Method

This subscription is considered **unstable** and is only available if the
validator was started with the `--rpc-pubsub-enable-block-subscription` flag.
The format of this subscription may change in the future.

### Parameters #

filter `string | object` required

filter criteria for the logs to receive results by account type; currently
supported:

`string`

`all` \- include all transactions in block

`object`

A JSON object with the following field:

  * `mentionsAccountOrProgram: <string>` \- return only transactions that mention the provided public key (as base-58 encoded string). If no mentions in a given block, then no notification will be sent.

`object` optional

Configuration object containing the following fields:

[commitment](/de/docs/rpc#configuring-state-commitment) `string` optional

Default: `finalized`

  * `processed` is not supported.

[encoding](/de/docs/rpc#parsed-responses) `string` optional

Default: `json`

encoding format for each returned Transaction

Values: `json``jsonParsed``base58``base64`

  * `jsonParsed` attempts to use program-specific instruction parsers to return more human-readable and explicit data in the `transaction.message.instructions` list.
  * If `jsonParsed` is requested but a parser cannot be found, the instruction falls back to regular JSON encoding (`accounts`, `data`, and `programIdIndex` fields).

transactionDetails `string` optional

Default: `full`

level of transaction detail to return

Values: `full``accounts``signatures``none`

  * If `accounts` are requested, transaction details only include signatures and an annotated list of accounts in each transaction.
  * Transaction metadata is limited to only: fee, err, pre_balances, post_balances, pre_token_balances, and post_token_balances.

maxSupportedTransactionVersion `number` optional

the max transaction version to return in responses.

  * If the requested block contains a transaction with a higher version, an error will be returned.
  * If this parameter is omitted, only legacy transactions will be returned, and a block containing any versioned transaction will prompt the error.

showRewards `bool` optional

whether to populate the `rewards` array. If parameter not provided, the
default includes rewards.

### Result #

`integer` \- subscription id (needed to unsubscribe)

### Code sample #

    
    
    {
      "jsonrpc": "2.0",
      "id": "1",
      "method": "blockSubscribe",
      "params": ["all"]
    }
    
    
    {
      "jsonrpc": "2.0",
      "id": "1",
      "method": "blockSubscribe",
      "params": [
        {
          "mentionsAccountOrProgram": "LieKvPRE8XeX3Y2xVNHjKlpAScD12lYySBVQ4HqoJ5op"
        },
        {
          "commitment": "confirmed",
          "encoding": "base64",
          "showRewards": true,
          "transactionDetails": "full"
        }
      ]
    }

### Response #

    
    
    { "jsonrpc": "2.0", "result": 0, "id": 1 }

#### Notification Format: #

The notification will be an object with the following fields:

  * `slot: <u64>` \- The corresponding slot.
  * `err: <object|null>` \- Error if something went wrong publishing the notification otherwise null.
  * `block: <object|null>` \- A block object as seen in the [getBlock](/de/docs/rpc/http/getblock) RPC HTTP method.

    
    
    {
      "jsonrpc": "2.0",
      "method": "blockNotification",
      "params": {
        "result": {
          "context": {
            "slot": 112301554
          },
          "value": {
            "slot": 112301554,
            "block": {
              "previousBlockhash": "GJp125YAN4ufCSUvZJVdCyWQJ7RPWMmwxoyUQySydZA",
              "blockhash": "6ojMHjctdqfB55JDpEpqfHnP96fiaHEcvzEQ2NNcxzHP",
              "parentSlot": 112301553,
              "transactions": [
                {
                  "transaction": [
                    "OpltwoUvWxYi1P2U8vbIdE/aPntjYo5Aa0VQ2JJyeJE2g9Vvxk8dDGgFMruYfDu8/IfUWb0REppTe7IpAuuLRgIBAAkWnj4KHRpEWWW7gvO1c0BHy06wZi2g7/DLqpEtkRsThAXIdBbhXCLvltw50ZnjDx2hzw74NVn49kmpYj2VZHQJoeJoYJqaKcvuxCi/2i4yywedcVNDWkM84Iuw+cEn9/ROCrXY4qBFI9dveEERQ1c4kdU46xjxj9Vi+QXkb2Kx45QFVkG4Y7HHsoS6WNUiw2m4ffnMNnOVdF9tJht7oeuEfDMuUEaO7l9JeUxppCvrGk3CP45saO51gkwVYEgKzhpKjCx3rgsYxNR81fY4hnUQXSbbc2Y55FkwgRBpVvQK7/+clR4Gjhd3L4y+OtPl7QF93Akg1LaU9wRMs5nvfDFlggqI9PqJl+IvVWrNRdBbPS8LIIhcwbRTkSbqlJQWxYg3Bo2CTVbw7rt1ZubuHWWp0mD/UJpLXGm2JprWTePNULzHu67sfqaWF99LwmwjTyYEkqkRt1T0Je5VzHgJs0N5jY4iIU9K3lMqvrKOIn/2zEMZ+ol2gdgjshx+sphIyhw65F3J/Dbzk04LLkK+CULmN571Y+hFlXF2ke0BIuUG6AUF+4214Cu7FXnqo3rkxEHDZAk0lRrAJ8X/Z+iwuwI5cgbd9uHXZaGT2cvhRs7reawctIXtX1s3kTqM9YV+/wCpDLAp8axcEkaQkLDKRoWxqp8XLNZSKial7Rk+ELAVVKWoWLRXRZ+OIggu0OzMExvVLE5VHqy71FNHq4gGitkiKYNFWSLIE4qGfdFLZXy/6hwS+wq9ewjikCpd//C9BcCL7Wl0iQdUslxNVCBZHnCoPYih9JXvGefOb9WWnjGy14sG9j70+RSVx6BlkFELWwFvIlWR/tHn3EhHAuL0inS2pwX7ZQTAU6gDVaoqbR2EiJ47cKoPycBNvHLoKxoY9AZaBjPl6q8SKQJSFyFd9n44opAgI6zMTjYF/8Ok4VpXEESp3QaoUyTI9sOJ6oFP6f4dwnvQelgXS+AEfAsHsKXxGAIUDQENAgMEBQAGBwgIDg8IBJCER3QXl1AVDBADCQoOAAQLERITDAjb7ugh3gOuTy==",
                    "base64"
                  ],
                  "meta": {
                    "err": null,
                    "status": {
                      "Ok": null
                    },
                    "fee": 5000,
                    "preBalances": [
                      1758510880, 2067120, 1566000, 1461600, 2039280, 2039280,
                      1900080, 1865280, 0, 3680844220, 2039280
                    ],
                    "postBalances": [
                      1758505880, 2067120, 1566000, 1461600, 2039280, 2039280,
                      1900080, 1865280, 0, 3680844220, 2039280
                    ],
                    "innerInstructions": [
                      {
                        "index": 0,
                        "instructions": [
                          {
                            "programIdIndex": 13,
                            "accounts": [1, 15, 3, 4, 2, 14],
                            "data": "21TeLgZXNbtHXVBzCaiRmH"
                          },
                          {
                            "programIdIndex": 14,
                            "accounts": [3, 4, 1],
                            "data": "6qfC8ic7Aq99"
                          },
                          {
                            "programIdIndex": 13,
                            "accounts": [1, 15, 3, 5, 2, 14],
                            "data": "21TeLgZXNbsn4QEpaSEr3q"
                          },
                          {
                            "programIdIndex": 14,
                            "accounts": [3, 5, 1],
                            "data": "6LC7BYyxhFRh"
                          }
                        ]
                      },
                      {
                        "index": 1,
                        "instructions": [
                          {
                            "programIdIndex": 14,
                            "accounts": [4, 3, 0],
                            "data": "7aUiLHFjSVdZ"
                          },
                          {
                            "programIdIndex": 19,
                            "accounts": [17, 18, 16, 9, 11, 12, 14],
                            "data": "8kvZyjATKQWYxaKR1qD53V"
                          },
                          {
                            "programIdIndex": 14,
                            "accounts": [9, 11, 18],
                            "data": "6qfC8ic7Aq99"
                          }
                        ]
                      }
                    ],
                    "logMessages": [
                      "Program QMNeHCGYnLVDn1icRAfQZpjPLBNkfGbSKRB83G5d8KB invoke [1]",
                      "Program QMWoBmAyJLAsA1Lh9ugMTw2gciTihncciphzdNzdZYV invoke [2]"
                    ],
                    "preTokenBalances": [
                      {
                        "accountIndex": 4,
                        "mint": "iouQcQBAiEXe6cKLS85zmZxUqaCqBdeHFpqKoSz615u",
                        "uiTokenAmount": {
                          "uiAmount": null,
                          "decimals": 6,
                          "amount": "0",
                          "uiAmountString": "0"
                        },
                        "owner": "LieKvPRE8XeX3Y2xVNHjKlpAScD12lYySBVQ4HqoJ5op",
                        "programId": "TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA"
                      },
                      {
                        "accountIndex": 5,
                        "mint": "iouQcQBAiEXe6cKLS85zmZxUqaCqBdeHFpqKoSz615u",
                        "uiTokenAmount": {
                          "uiAmount": 11513.0679,
                          "decimals": 6,
                          "amount": "11513067900",
                          "uiAmountString": "11513.0679"
                        },
                        "owner": "rXhAofQCT7NN9TUqigyEAUzV1uLL4boeD8CRkNBSkYk",
                        "programId": "TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA"
                      },
                      {
                        "accountIndex": 10,
                        "mint": "Saber2gLauYim4Mvftnrasomsv6NvAuncvMEZwcLpD1",
                        "uiTokenAmount": {
                          "uiAmount": null,
                          "decimals": 6,
                          "amount": "0",
                          "uiAmountString": "0"
                        },
                        "owner": "CL9wkGFT3SZRRNa9dgaovuRV7jrVVigBUZ6DjcgySsCU",
                        "programId": "TokenzQdBNbLqP5VEhdkAS6EPFLC1PHnBqCXEpPxuEb"
                      },
                      {
                        "accountIndex": 11,
                        "mint": "Saber2gLauYim4Mvftnrasomsv6NvAuncvMEZwcLpD1",
                        "uiTokenAmount": {
                          "uiAmount": 15138.514093,
                          "decimals": 6,
                          "amount": "15138514093",
                          "uiAmountString": "15138.514093"
                        },
                        "owner": "LieKvPRE8XeX3Y2xVNHjKlpAScD12lYySBVQ4HqoJ5op",
                        "programId": "TokenzQdBNbLqP5VEhdkAS6EPFLC1PHnBqCXEpPxuEb"
                      }
                    ],
                    "postTokenBalances": [
                      {
                        "accountIndex": 4,
                        "mint": "iouQcQBAiEXe6cKLS85zmZxUqaCqBdeHFpqKoSz615u",
                        "uiTokenAmount": {
                          "uiAmount": null,
                          "decimals": 6,
                          "amount": "0",
                          "uiAmountString": "0"
                        },
                        "owner": "LieKvPRE8XeX3Y2xVNHjKlpAScD12lYySBVQ4HqoJ5op",
                        "programId": "TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA"
                      },
                      {
                        "accountIndex": 5,
                        "mint": "iouQcQBAiEXe6cKLS85zmZxUqaCqBdeHFpqKoSz615u",
                        "uiTokenAmount": {
                          "uiAmount": 11513.103028,
                          "decimals": 6,
                          "amount": "11513103028",
                          "uiAmountString": "11513.103028"
                        },
                        "owner": "rXhAofQCT7NN9TUqigyEAUzV1uLL4boeD8CRkNBSkYk",
                        "programId": "TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA"
                      },
                      {
                        "accountIndex": 10,
                        "mint": "Saber2gLauYim4Mvftnrasomsv6NvAuncvMEZwcLpD1",
                        "uiTokenAmount": {
                          "uiAmount": null,
                          "decimals": 6,
                          "amount": "0",
                          "uiAmountString": "0"
                        },
                        "owner": "CL9wkGFT3SZRRNa9dgaovuRV7jrVVigBUZ6DjcgySsCU",
                        "programId": "TokenzQdBNbLqP5VEhdkAS6EPFLC1PHnBqCXEpPxuEb"
                      },
                      {
                        "accountIndex": 11,
                        "mint": "Saber2gLauYim4Mvftnrasomsv6NvAuncvMEZwcLpD1",
                        "uiTokenAmount": {
                          "uiAmount": 15489.767829,
                          "decimals": 6,
                          "amount": "15489767829",
                          "uiAmountString": "15489.767829"
                        },
                        "owner": "BeiHVPRE8XeX3Y2xVNrSsTpAScH94nYySBVQ4HqgN9at",
                        "programId": "TokenzQdBNbLqP5VEhdkAS6EPFLC1PHnBqCXEpPxuEb"
                      }
                    ],
                    "rewards": []
                  }
                }
              ],
              "blockTime": 1639926816,
              "blockHeight": 101210751
            },
            "err": null
          }
        },
        "subscription": 14
      }
    }

[Previous«
accountUnsubscribe](/de/docs/rpc/websocket/accountunsubscribe)[NextblockUnsubscribe
»](/de/docs/rpc/websocket/blockunsubscribe)

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
