Skip to main content

[](/en/)

  * Learn
  * Use
  * Build
  * Participate
  * Research

Search```K`

Languages EN

# Learn Foundational Ethereum Topics with SQL

SQLQueryingTransactions

Beginner

![✍️](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/270d.svg)Paul
Apivat

![📚](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4da.svg)[paulapivat.com(opens
in a new tab)](https://paulapivat.com/post/query_ethereum/)

![📆](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4c6.svg)
May 11, 2021

![⏱️](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/23f1.svg)8
minute read minute read

On this page

  * Transactions
    * Etherscan
    * Dune Analytics
  * Breaking Down Transactions
  * Blocks
  * Gas
  * Summary

Many Ethereum tutorials target developers, but there’s a lack of educational
resources for data analysts or for people who wish to see on-chain data
without running a client or node.

This tutorial helps readers understand fundamental Ethereum concepts including
transactions, blocks and gas by querying on-chain data with structured query
language (SQL) through an interface provided by [Dune Analytics(opens in a new
tab)](https://dune.xyz/home).

On-chain data can help us understand Ethereum, the network, and as an economy
for computing power and should serve as a base for understanding challenges
facing Ethereum today (i.e., rising gas prices) and, more importantly,
discussions around scaling solutions.

### Transactions

A user’s journey on Ethereum starts with initializing a user-controlled
account or an entity with an ETH balance. There are two account types - user-
controlled or a smart contract (see
[ethereum.org](/en/developers/docs/accounts/)).

Any account can be viewed on a block explorer like [Etherscan(opens in a new
tab)](https://etherscan.io/). Block explorers are a portal to Ethereum’s data.
They display, in real-time, data on blocks, transactions, miners, accounts and
other on-chain activity (see [here](/en/developers/docs/data-and-
analytics/block-explorers/)).

However, a user may wish to query the data directly to reconcile the
information provided by external block explorers. [Dune Analytics(opens in a
new tab)](https://duneanalytics.com/) provides this capability to anyone with
some knowledge of SQL.

For reference, the smart contract account for the Ethereum Foundation (EF) can
be viewed on [Etherscan(opens in a new
tab)](https://etherscan.io/address/0xde0b295669a9fd93d5f28d9ec85e40f4cb697bae).

One thing to note is that all accounts, including the EF’s, have a public
address that can be used to send and receive transactions.

The account balance on Etherscan comprises regular transactions and internal
transactions. Internal transactions, despite the name, are not _actual_
transactions that change the state of the chain. They are value transfers
initiated by executing a contract ([source(opens in a new
tab)](https://ethereum.stackexchange.com/questions/3417/how-to-get-contract-
internal-transactions)). Since internal transactions have no signature, they
are **not** included on the blockchain and cannot be queried with Dune
Analytics.

Therefore, this tutorial will focus on regular transactions. This can be
queried as such:

    
    
    1WITH temp_table AS (
    
    2SELECT
    
    3    hash,
    
    4    block_number,
    
    5    block_time,
    
    6    "from",
    
    7    "to",
    
    8    value / 1e18 AS ether,
    
    9    gas_used,
    
    10    gas_price / 1e9 AS gas_price_gwei
    
    11FROM ethereum."transactions"
    
    12WHERE "to" = '\xde0B295669a9FD93d5F28D9Ec85E40f4cb697BAe'
    
    13ORDER BY block_time DESC
    
    14)
    
    15SELECT
    
    16    hash,
    
    17    block_number,
    
    18    block_time,
    
    19    "from",
    
    20    "to",
    
    21    ether,
    
    22    (gas_used * gas_price_gwei) / 1e9 AS txn_fee
    
    23FROM temp_table
    
    Show all

This will yield the same information as provided on Etherscan's transaction
page. For comparison, here are the two sources:

#### Etherscan

[![](/_next/image/?url=%2Fcontent%2Fdevelopers%2Ftutorials%2Flearn-
foundational-ethereum-topics-with-
sql%2Fetherscan_view.png&w=1920&q=75)](/content/developers/tutorials/learn-
foundational-ethereum-topics-with-sql/etherscan_view.png)

[EF's contract page on Etherscan.(opens in a new
tab)](https://etherscan.io/address/0xde0B295669a9FD93d5F28D9Ec85E40f4cb697BAe)

#### Dune Analytics

[![](/_next/image/?url=%2Fcontent%2Fdevelopers%2Ftutorials%2Flearn-
foundational-ethereum-topics-with-
sql%2Fdune_view.png&w=1920&q=75)](/content/developers/tutorials/learn-
foundational-ethereum-topics-with-sql/dune_view.png)

You can find dashboard [here(opens in a new
tab)](https://duneanalytics.com/paulapivat/Learn-Ethereum). Click on the table
to see the query (also see above).

### Breaking Down Transactions

A submitted transaction includes several pieces of information including
([source](/en/developers/docs/transactions/)):

  * **Recipient** : The receiving address (queried as "to")
  * **Signature** : While a sender's private keys signs a transaction, what we can query with SQL is a sender's public address ("from").
  * **Value** : This is the amount of ETH transferred (see `ether` column).
  * **Data** : This is arbitrary data that's been hashed (see `data` column)
  * **gasLimit** – the maximum amount of gas units that can be consumed by the transaction. Units of gas represent computational steps
  * **maxPriorityFeePerGas** \- the maximum amount of gas to be included as a tip to the miner
  * **maxFeePerGas** \- the maximum amount of gas willing to be paid for the transaction (inclusive of baseFeePerGas and maxPriorityFeePerGas)

We can query these specific pieces of information for transactions to the
Ethereum Foundation public address:

    
    
    1SELECT
    
    2    "to",
    
    3    "from",
    
    4    value / 1e18 AS ether,
    
    5    data,
    
    6    gas_limit,
    
    7    gas_price / 1e9 AS gas_price_gwei,
    
    8    gas_used,
    
    9    ROUND(((gas_used / gas_limit) * 100),2) AS gas_used_pct
    
    10FROM ethereum."transactions"
    
    11WHERE "to" = '\xde0B295669a9FD93d5F28D9Ec85E40f4cb697BAe'
    
    12ORDER BY block_time DESC
    
    Show all

### Blocks

Each transaction will change the state of the Ethereum virtual machine
([EVM](/en/developers/docs/evm/))
([source](/en/developers/docs/transactions/)). Transactions are broadcasted to
the network to be verified and included in a block. Each transaction is
associated with a block number. To see the data, we could query a specific
block number: 12396854 (the most recent block among Ethereum Foundation
transactions as of this writing, 11/5/21).

Moreover, when we query the next two blocks, we can see that each block
contains the hash of the previous block (i.e., parent hash), illustrating how
the blockchain is formed.

Each block contains a reference to it parent block. This is shown below
between the `hash` and `parent_hash` columns
([source](/en/developers/docs/blocks/)):

[![parent_hash](/_next/image/?url=%2Fcontent%2Fdevelopers%2Ftutorials%2Flearn-
foundational-ethereum-topics-with-
sql%2Fparent_hash.png&w=1920&q=75)](/content/developers/tutorials/learn-
foundational-ethereum-topics-with-sql/parent_hash.png)

Here is the [query(opens in a new
tab)](https://duneanalytics.com/queries/44856/88292) on Dune Analytics:

    
    
    1SELECT
    
    2   time,
    
    3   number,
    
    4   hash,
    
    5   parent_hash,
    
    6   nonce
    
    7FROM ethereum."blocks"
    
    8WHERE "number" = 12396854 OR "number" = 12396855 OR "number" = 12396856
    
    9LIMIT 10
    
    Show all

We can examine a block by querying time, block number, difficulty, hash,
parent hash, and nonce.

The only thing this query does not cover is _list of transaction_ which
requires a separate query below and _state root_. A full or archival node will
store all transactions and state transitions, allowing for clients to query
the state of the chain at any time. Because this requires large storage space,
we can separate chain data from state data:

  * Chain data (list of blocks, transactions)
  * State data (result of each transaction’s state transition)

State root falls in the latter and is _implicit_ data (not stored on-chain),
while chain data is explicit and stored on the chain itself ([source(opens in
a new tab)](https://ethereum.stackexchange.com/questions/359/where-is-the-
state-data-stored)).

For this tutorial, we'll be focusing on on-chain data that _can_ be queried
with SQL via Dune Analytics.

As stated above, each block contains a list of transactions, we can query this
by filtering for a specific block. We'll try the most recent block, 12396854:

    
    
    1SELECT * FROM ethereum."transactions"
    
    2WHERE block_number = 12396854
    
    3ORDER BY block_time DESC`

Here's the SQL output on Dune:

[![](/_next/image/?url=%2Fcontent%2Fdevelopers%2Ftutorials%2Flearn-
foundational-ethereum-topics-with-
sql%2Flist_of_txn.png&w=1920&q=75)](/content/developers/tutorials/learn-
foundational-ethereum-topics-with-sql/list_of_txn.png)

This single block being added to the chain changes the state of the Ethereum
virtual machine ([EVM](/en/developers/docs/evm/)). Dozens sometimes, hundreds
of transactions are verified at once. In this specific case, 222 transactions
were included.

To see how many were actually successful, we would add another filter to count
successful transactions:

    
    
    1WITH temp_table AS (
    
    2    SELECT * FROM ethereum."transactions"
    
    3    WHERE block_number = 12396854 AND success = true
    
    4    ORDER BY block_time DESC
    
    5)
    
    6SELECT
    
    7    COUNT(success) AS num_successful_txn
    
    8FROM temp_table

For block 12396854, out of 222 total transactions, 204 were successfully
verified:

[![](/_next/image/?url=%2Fcontent%2Fdevelopers%2Ftutorials%2Flearn-
foundational-ethereum-topics-with-
sql%2Fsuccessful_txn.png&w=1504&q=75)](/content/developers/tutorials/learn-
foundational-ethereum-topics-with-sql/successful_txn.png)

Transactions requests occur dozens of times per second, but blocks are
committed approximately once every 15 seconds
([source](/en/developers/docs/blocks/)).

To see that there is one block produced approximately every 15 seconds, we
could take the number of seconds in a day (86400) divided by 15 to get an
estimated average number of blocks per day (~ 5760).

The chart for Ethereum blocks produced per day (2016 - present) is:

[![](/_next/image/?url=%2Fcontent%2Fdevelopers%2Ftutorials%2Flearn-
foundational-ethereum-topics-with-
sql%2Fdaily_blocks.png&w=1504&q=75)](/content/developers/tutorials/learn-
foundational-ethereum-topics-with-sql/daily_blocks.png)

The average number of blocks produced daily over this time period is ~5,874:

[![](/_next/image/?url=%2Fcontent%2Fdevelopers%2Ftutorials%2Flearn-
foundational-ethereum-topics-with-
sql%2Favg_daily_blocks.png&w=750&q=75)](/content/developers/tutorials/learn-
foundational-ethereum-topics-with-sql/avg_daily_blocks.png)

The queries are:

    
    
    1# query to visualize number of blocks produced daily since 2016
    
    2
    
    3SELECT
    
    4    DATE_TRUNC('day', time) AS dt,
    
    5    COUNT(*) AS block_count
    
    6FROM ethereum."blocks"
    
    7GROUP BY dt
    
    8OFFSET 1
    
    9
    
    10# average number of blocks produced per day
    
    11
    
    12WITH temp_table AS (
    
    13SELECT
    
    14    DATE_TRUNC('day', time) AS dt,
    
    15    COUNT(*) AS block_count
    
    16FROM ethereum."blocks"
    
    17GROUP BY dt
    
    18OFFSET 1
    
    19)
    
    20SELECT
    
    21    AVG(block_count) AS avg_block_count
    
    22FROM temp_table
    
    Show all

The average number of blocks produced per day since 2016 is slightly above
that number at 5,874. Alternatively, dividing 86400 seconds by 5874 average
blocks comes out to 14.7 seconds or approximately one block every 15 seconds.

### Gas

Blocks are bounded in size. The maximum block size is dynamic and varies
according to network demand between 12,500,000 and 25,000,000 units. Limits
are required to prevent arbitrarily large block sizes putting strain on full
nodes in terms of disk space and speed requirements
([source](/en/developers/docs/blocks/)).

One way to conceptualize block gas limit is to think of it as the **supply**
of available block space in which to batch transactions. The block gas limit
can be queried and visualized from 2016 to present day:

[![](/_next/image/?url=%2Fcontent%2Fdevelopers%2Ftutorials%2Flearn-
foundational-ethereum-topics-with-
sql%2Favg_gas_limit.png&w=1920&q=75)](/content/developers/tutorials/learn-
foundational-ethereum-topics-with-sql/avg_gas_limit.png)

    
    
    1SELECT
    
    2    DATE_TRUNC('day', time) AS dt,
    
    3    AVG(gas_limit) AS avg_block_gas_limit
    
    4FROM ethereum."blocks"
    
    5GROUP BY dt
    
    6OFFSET 1

Then there is the actual gas used daily to pay for computing done on the
Ethereum chain (i.e., sending transaction, calling a smart contract, minting
an NFT). This is the **demand** for available Ethereum block space:

[![](/_next/image/?url=%2Fcontent%2Fdevelopers%2Ftutorials%2Flearn-
foundational-ethereum-topics-with-
sql%2Fdaily_gas_used.png&w=1920&q=75)](/content/developers/tutorials/learn-
foundational-ethereum-topics-with-sql/daily_gas_used.png)

    
    
    1SELECT
    
    2    DATE_TRUNC('day', time) AS dt,
    
    3    AVG(gas_used) AS avg_block_gas_used
    
    4FROM ethereum."blocks"
    
    5GROUP BY dt
    
    6OFFSET 1

We can also juxtapose these two charts together to see how **demand and
supply** line up:

[![gas_demand_supply](/_next/image/?url=%2Fcontent%2Fdevelopers%2Ftutorials%2Flearn-
foundational-ethereum-topics-with-
sql%2Fgas_demand_supply.png&w=1920&q=75)](/content/developers/tutorials/learn-
foundational-ethereum-topics-with-sql/gas_demand_supply.png)

Therefore we can understand gas prices as a function of demand for Ethereum
block space, given available supply.

Finally, we may want to query average daily gas prices for the Ethereum chain,
however, doing so will result in an especially long query time, so we’ll
filter our query to the average amount of gas paid per transaction by the
Ethereum Foundation.

[![](/_next/image/?url=%2Fcontent%2Fdevelopers%2Ftutorials%2Flearn-
foundational-ethereum-topics-with-
sql%2Fef_daily_gas.png&w=1920&q=75)](/content/developers/tutorials/learn-
foundational-ethereum-topics-with-sql/ef_daily_gas.png)

We can see gas prices paid for all transactions made to the Ethereum
Foundation address over the years. Here is the query:

    
    
    1SELECT
    
    2    block_time,
    
    3    gas_price / 1e9 AS gas_price_gwei,
    
    4    value / 1e18 AS eth_sent
    
    5FROM ethereum."transactions"
    
    6WHERE "to" = '\xde0B295669a9FD93d5F28D9Ec85E40f4cb697BAe'
    
    7ORDER BY block_time DESC

### Summary

With this tutorial, we understand foundational Ethereum concepts and how the
Ethereum blockchain works by querying and getting a feel for on-chain data.

The dashboard that holds all code used in this tutorial can be found
[here(opens in a new tab)](https://duneanalytics.com/paulapivat/Learn-
Ethereum).

For more use of data to explore web3 [find me on Twitter(opens in a new
tab)](https://twitter.com/paulapivat).

p

Last edit: [@pettinarip(opens in a new tab)](https://github.com/pettinarip),
December 4, 2023

See contributors

### Was this tutorial helpful?

YesNo

  * [Edit page(opens in a new tab)](https://github.com/ethereum/ethereum-org-website/tree/dev/public/content/developers/tutorials/learn-foundational-ethereum-topics-with-sql/index.md)
  * On this page

    * Transactions
      * Etherscan
      * Dune Analytics
    * Breaking Down Transactions
    * Blocks
    * Gas
    * Summary

Website last updated: May 22, 2024

[(opens in a new tab)](https://github.com/ethereum/ethereum-org-
website)[(opens in a new tab)](https://twitter.com/ethdotorg)[(opens in a new
tab)](https://discord.gg/ethereum-org)

### Learn

  * [Learn Hub](/en/learn/)
  * [What is Ethereum?](/en/what-is-ethereum/)
  * [What is ether (ETH)?](/en/eth/)
  * [Ethereum wallets](/en/wallets/)
  * [What is Web3?](/en/web3/)
  * [Smart contracts](/en/smart-contracts/)
  * [Gas fees](/en/gas/)
  * [Run a node](/en/run-a-node/)
  * [Ethereum security and scam prevention](/en/security/)
  * [Quiz Hub](/en/quizzes/)
  * [Ethereum glossary](/en/glossary/)

### Use

  * [Guides](/en/guides/)
  * [Choose your wallet](/en/wallets/find-wallet/)
  * [Get ETH](/en/get-eth/)
  * [Dapps - Decentralized applications](/en/dapps/)
  * [Stablecoins](/en/stablecoins/)
  * [NFTs - Non-fungible tokens](/en/nft/)
  * [DeFi - Decentralized finance](/en/defi/)
  * [DAOs - Decentralized autonomous organizations](/en/dao/)
  * [Decentralized identity](/en/decentralized-identity/)
  * [Stake ETH](/en/staking/)
  * [Layer 2](/en/layer-2/)

### Build

  * [Builder's home](/en/developers/)
  * [Tutorials](/en/developers/tutorials/)
  * [Documentation](/en/developers/docs/)
  * [Learn by coding](/en/developers/learning-tools/)
  * [Set up local environment](/en/developers/local-environment/)
  * [Grants](/en/community/grants/)
  * [Foundational topics](/en/developers/docs/intro-to-ethereum/)
  * [UX/UI design fundamentals](/en/developers/docs/design-and-ux/)
  * [Enterprise - Mainnet Ethereum](/en/enterprise/)
  * [Enterprise - Private Ethereum](/en/enterprise/private-ethereum/)

### Participate

  * [Community hub](/en/community/)
  * [Online communities](/en/community/online/)
  * [Ethereum events](/en/community/events/)
  * [Contributing to ethereum.org](/en/contributing/)
  * [Translation Program](/en/contributing/translation-program/)
  * [Ethereum bug bounty program](/en/bug-bounty/)
  * [Ethereum Foundation](/en/foundation/)
  * [Ethereum Foundation Blog(opens in a new tab)](https://blog.ethereum.org/)
  * [Ecosystem Support Program(opens in a new tab)](https://esp.ethereum.foundation)
  * [Devcon(opens in a new tab)](https://devcon.org/)

### Research

  * [Ethereum Whitepaper](/en/whitepaper/)
  * [Ethereum roadmap](/en/roadmap/)
  * [Improved security](/en/roadmap/security/)
  * [Technical history of Ethereum](/en/history/)
  * [Open research](/en/community/research/)
  * [Ethereum Improvement Proposals](/en/eips/)
  * [Ethereum governance](/en/governance/)

  * [About us](/en/about/)
  * [Ethereum brand assets](/en/assets/)
  * [Code of conduct](/en/community/code-of-conduct/)
  * [Jobs](/en/about/#open-jobs)
  * [Privacy policy](/en/privacy-policy/)
  * [Terms of use](/en/terms-of-use/)
  * [Cookie policy](/en/cookie-policy/)
  * [Press Contact(opens in a new tab)](mailto:press@ethereum.org)

Is this page helpful?

