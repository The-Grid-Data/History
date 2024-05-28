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

# [blockSubscribe RPC Method](/docs/rpc/websocket/blocksubscribe)

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

[commitment](/docs/rpc#configuring-state-commitment) `string` optional

Default: `finalized`

  * `processed` is not supported.

[encoding](/docs/rpc#parsed-responses) `string` optional

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
  * `block: <object|null>` \- A block object as seen in the [getBlock](/docs/rpc/http/getblock) RPC HTTP method.

    
    
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
accountUnsubscribe](/docs/rpc/websocket/accountunsubscribe)[NextblockUnsubscribe
»](/docs/rpc/websocket/blockunsubscribe)

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

