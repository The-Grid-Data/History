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
Methods](/ru/docs/rpc)>[Websocket Methods](/ru/docs/rpc/websocket)

# [blockSubscribe RPC Method](/ru/docs/rpc/websocket/blocksubscribe)

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

[commitment](/ru/docs/rpc#configuring-state-commitment) `string` optional

Default: `finalized`

  * `processed` is not supported.

[encoding](/ru/docs/rpc#parsed-responses) `string` optional

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
  * `block: <object|null>` \- A block object as seen in the [getBlock](/ru/docs/rpc/http/getblock) RPC HTTP method.

    
    
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
accountUnsubscribe](/ru/docs/rpc/websocket/accountunsubscribe)[NextblockUnsubscribe
»](/ru/docs/rpc/websocket/blockunsubscribe)

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

