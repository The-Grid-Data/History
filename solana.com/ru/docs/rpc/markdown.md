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

##### Table of Contents

  * [Configuring State Commitment](/ru/docs/rpc#configuring-state-commitment)
  * [Default Commitment](/ru/docs/rpc#default-commitment)
  * [RpcResponse Structure](/ru/docs/rpc#rpcresponse-structure)
  * [Parsed Responses](/ru/docs/rpc#parsed-responses)
  * [Filter criteria](/ru/docs/rpc#filter-criteria)

[Scroll to Top](/ru/docs/rpc#)

[Edit Page](https://github.com/solana-foundation/developer-
content/tree/main/docs/rpc/index.mdx)

[Home](/ru)>[Solana Documentation](/ru/docs)

# [Solana RPC Methods & Documentation](/ru/docs/rpc)

Interact with Solana nodes directly with the JSON RPC API via the HTTP and
Websocket methods.

## Configuring State Commitment #

For preflight checks and transaction processing, Solana nodes choose which
bank state to query based on a commitment requirement set by the client. The
commitment describes how finalized a block is at that point in time. When
querying the ledger state, it's recommended to use lower levels of commitment
to report progress and higher levels to ensure the state will not be rolled
back.

In descending order of commitment (most finalized to least finalized), clients
may specify:

  * `finalized` \- the node will query the most recent block confirmed by supermajority of the cluster as having reached maximum lockout, meaning the cluster has recognized this block as finalized
  * `confirmed` \- the node will query the most recent block that has been voted on by supermajority of the cluster.
    * It incorporates votes from gossip and replay.
    * It does not count votes on descendants of a block, only direct votes on that block.
    * This confirmation level also upholds "optimistic confirmation" guarantees in release 1.3 and onwards.
  * `processed` \- the node will query its most recent block. Note that the block may still be skipped by the cluster.

For processing many dependent transactions in series, it's recommended to use
`confirmed` commitment, which balances speed with rollback safety. For total
safety, it's recommended to use `finalized` commitment.

### Default Commitment #

If commitment configuration is not provided, the node will [default to
`finalized` commitment](https://github.com/anza-
xyz/agave/blob/aa0922d6845e119ba466f88497e8209d1c82febc/sdk/src/commitment_config.rs#L199-L203)

Only methods that query bank state accept the commitment parameter. They are
indicated in the API Reference below.

## RpcResponse Structure #

Many methods that take a commitment parameter return an RpcResponse JSON
object comprised of two parts:

  * `context` : An RpcResponseContext JSON structure including a `slot` field at which the operation was evaluated.
  * `value` : The value returned by the operation itself.

## Parsed Responses #

Some methods support an `encoding` parameter, and can return account or
instruction data in parsed JSON format if `"encoding":"jsonParsed"` is
requested and the node has a parser for the owning program. Solana nodes
currently support JSON parsing for the following native and SPL programs:

Program| Account State| Instructions  
---|---|---  
Address Lookup| v1.15.0| v1.15.0  
BPF Loader| n/a| stable  
BPF Upgradeable Loader| stable| stable  
Config| stable|  
SPL Associated Token Account| n/a| stable  
SPL Memo| n/a| stable  
SPL Token| stable| stable  
SPL Token 2022| stable| stable  
Stake| stable| stable  
Vote| stable| stable  
  
The list of account parsers can be found [here](https://github.com/solana-
labs/solana/blob/master/account-decoder/src/parse_account_data.rs), and
instruction parsers [here](https://github.com/solana-
labs/solana/blob/master/transaction-status/src/parse_instruction.rs).

## Filter criteria #

Some methods support providing a `filters` object to enable pre-filtering the
data returned within the RpcResponse JSON object. The following filters exist:

  * `memcmp: object` \- compares a provided series of bytes with program account data at a particular offset. Fields:

    * `offset: usize` \- offset into program account data to start comparison
    * `bytes: string` \- data to match, as encoded string
    * `encoding: string` \- encoding for filter `bytes` data, either "base58" or "base64". Data is limited in size to 128 or fewer decoded bytes.  
**NEW: This field, and base64 support generally, is only available in solana-
core v1.14.0 or newer. Please omit when querying nodes on earlier versions**

  * `dataSize: u64` \- compares the program account data length with the provided data size

[Previous« Solana Documentation](/ru/docs)[NextData Structures as JSON
»](/ru/docs/rpc/json-structures)

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

