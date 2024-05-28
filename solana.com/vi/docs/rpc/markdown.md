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

##### Table of Contents

  * [Configuring State Commitment](/vi/docs/rpc#configuring-state-commitment)
  * [Default Commitment](/vi/docs/rpc#default-commitment)
  * [RpcResponse Structure](/vi/docs/rpc#rpcresponse-structure)
  * [Parsed Responses](/vi/docs/rpc#parsed-responses)
  * [Filter criteria](/vi/docs/rpc#filter-criteria)

[Scroll to Top](/vi/docs/rpc#)

[Edit Page](https://github.com/solana-foundation/developer-
content/tree/main/docs/rpc/index.mdx)

[Home](/vi)>[Solana Documentation](/vi/docs)

# [Solana RPC Methods & Documentation](/vi/docs/rpc)

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

[Previous« Solana Documentation](/vi/docs)[NextData Structures as JSON
»](/vi/docs/rpc/json-structures)

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

