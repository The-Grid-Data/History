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

##### Table of Contents

  * [Current Transaction Versions](/docs/advanced/versions#current-transaction-versions)
  * [Max supported transaction version](/docs/advanced/versions#max-supported-transaction-version)
  * [How to set max supported version](/docs/advanced/versions#how-to-set-max-supported-version)
  * [Using web3.js](/docs/advanced/versions#using-web3-js)
  * [JSON requests to the RPC](/docs/advanced/versions#json-requests-to-the-rpc)
  * [How to create a Versioned Transaction](/docs/advanced/versions#how-to-create-a-versioned-transaction)
  * [More Resources](/docs/advanced/versions#more-resources)

[Scroll to Top](/docs/advanced/versions#)

[Edit Page](https://github.com/solana-foundation/developer-
content/tree/main/docs/advanced/versions.md)

[Home](/)>[Solana Documentation](/docs)>Advanced Concepts

# [Versioned Transactions](/docs/advanced/versions)

Versioned Transactions are the new transaction format that allow for
additional functionality in the Solana runtime, including [Address Lookup
Tables](/docs/advanced/lookup-tables).

While changes to [onchain](/docs/programs) programs are **NOT** required to
support the new functionality of versioned transactions (or for backwards
compatibility), developers **WILL** need update their client side code to
prevent [errors due to different transaction
versions](/docs/advanced/versions#max-supported-transaction-version).

## Current Transaction Versions #

The Solana runtime supports two transaction versions:

  * `legacy` \- older transaction format with no additional benefit
  * `0` \- added support for [Address Lookup Tables](/docs/advanced/lookup-tables)

## Max supported transaction version #

All RPC requests that return a transaction **_should_** specify the highest
version of transactions they will support in their application using the
`maxSupportedTransactionVersion` option, including
[`getBlock`](/docs/rpc/http/getblock) and
[`getTransaction`](/docs/rpc/http/gettransaction).

An RPC request will fail if a Versioned Transaction is returned that is higher
than the set `maxSupportedTransactionVersion`. (i.e. if a version `0`
transaction is returned when `legacy` is selected)

Info

WARNING: If no `maxSupportedTransactionVersion` value is set, then only
`legacy` transactions will be allowed in the RPC response. Therefore, your RPC
requests **WILL** fail if any version `0` transactions are returned.

## How to set max supported version #

You can set the `maxSupportedTransactionVersion` using both the
[`@solana/web3.js`](https://solana-labs.github.io/solana-web3.js/) library and
JSON formatted requests directly to an RPC endpoint.

### Using web3.js #

Using the [`@solana/web3.js`](https://solana-labs.github.io/solana-web3.js/)
library, you can retrieve the most recent block or get a specific transaction:

    
    
    // connect to the `devnet` cluster and get the current `slot`
    const connection = new web3.Connection(web3.clusterApiUrl("devnet"));
    const slot = await connection.getSlot();
     
    // get the latest block (allowing for v0 transactions)
    const block = await connection.getBlock(slot, {
      maxSupportedTransactionVersion: 0,
    });
     
    // get a specific transaction (allowing for v0 transactions)
    const getTx = await connection.getTransaction(
      "3jpoANiFeVGisWRY5UP648xRXs3iQasCHABPWRWnoEjeA93nc79WrnGgpgazjq4K9m8g2NJoyKoWBV1Kx5VmtwHQ",
      {
        maxSupportedTransactionVersion: 0,
      },
    );

### JSON requests to the RPC #

Using a standard JSON formatted POST request, you can set the
`maxSupportedTransactionVersion` when retrieving a specific block:

    
    
    curl https://api.devnet.solana.com -X POST -H "Content-Type: application/json" -d \
    '{"jsonrpc": "2.0", "id":1, "method": "getBlock", "params": [430, {
      "encoding":"json",
      "maxSupportedTransactionVersion":0,
      "transactionDetails":"full",
      "rewards":false
    }]}'

## How to create a Versioned Transaction #

Versioned transactions can be created similar to the older method of creating
transactions. There are differences in using certain libraries that should be
noted.

Below is an example of how to create a Versioned Transaction, using the
`@solana/web3.js` library, to send perform a SOL transfer between two
accounts.

#### Notes: #

  * `payer` is a valid `Keypair` wallet, funded with SOL
  * `toAccount` a valid `Keypair`

Firstly, import the web3.js library and create a `connection` to your desired
cluster.

We then define the recent `blockhash` and `minRent` we will need for our
transaction and the account:

    
    
    const web3 = require("@solana/web3.js");
     
    // connect to the cluster and get the minimum rent for rent exempt status
    const connection = new web3.Connection(web3.clusterApiUrl("devnet"));
    let minRent = await connection.getMinimumBalanceForRentExemption(0);
    let blockhash = await connection
      .getLatestBlockhash()
      .then(res => res.blockhash);

Create an `array` of all the `instructions` you desire to send in your
transaction. In this example below, we are creating a simple SOL transfer
instruction:

    
    
    // create an array with your desired `instructions`
    const instructions = [
      web3.SystemProgram.transfer({
        fromPubkey: payer.publicKey,
        toPubkey: toAccount.publicKey,
        lamports: minRent,
      }),
    ];

Next, construct a `MessageV0` formatted transaction message with your desired
`instructions`:

    
    
    // create v0 compatible message
    const messageV0 = new web3.TransactionMessage({
      payerKey: payer.publicKey,
      recentBlockhash: blockhash,
      instructions,
    }).compileToV0Message();

Then, create a new `VersionedTransaction`, passing in our v0 compatible
message:

    
    
    const transaction = new web3.VersionedTransaction(messageV0);
     
    // sign your transaction with the required `Signers`
    transaction.sign([payer]);

You can sign the transaction by either:

  * passing an array of `signatures` into the `VersionedTransaction` method, or
  * call the `transaction.sign()` method, passing an array of the required `Signers`

Info

NOTE: After calling the `transaction.sign()` method, all the previous
transaction `signatures` will be fully replaced by new signatures created from
the provided in `Signers`.

After your `VersionedTransaction` has been signed by all required accounts,
you can send it to the cluster and `await` the response:

    
    
    // send our v0 transaction to the cluster
    const txId = await connection.sendTransaction(transaction);
    console.log(`https://explorer.solana.com/tx/${txId}?cluster=devnet`);

Info

NOTE: Unlike `legacy` transactions, sending a `VersionedTransaction` via
`sendTransaction` does **NOT** support transaction signing via passing in an
array of `Signers` as the second parameter. You will need to sign the
transaction before calling `connection.sendTransaction()`.

## More Resources #

  * using [Versioned Transactions for Address Lookup Tables](/docs/advanced/lookup-tables#how-to-create-an-address-lookup-table)
  * view an [example of a v0 transaction](https://explorer.solana.com/tx/h9WQsqSUYhFvrbJWKFPaXximJpLf6Z568NW1j6PBn3f7GPzQXe9PYMYbmWSUFHwgnUmycDNbEX9cr6WjUWkUFKx/?cluster=devnet) on Solana Explorer
  * read the [accepted proposal](https://docs.solanalabs.com/proposals/versioned-transactions) for Versioned Transaction and Address Lookup Tables

[Previous« Clusters & Endpoints](/docs/core/clusters)[NextAddress Lookup
Tables »](/docs/advanced/lookup-tables)

  * [Solana Documentation](/docs)

    * [JSON RPC Methods](/docs/rpc)
    * [Terminology](/docs/terminology)
  * Introduction

    * [Overview](/docs/intro/overview)
    * [Wallets](/docs/intro/wallets)
    * [Intro to Development](/docs/intro/dev)
  * Core Concepts

    * [Solana Account Model](/docs/core/accounts)
    * [Transactions and Instructions](/docs/core/transactions)
    * [Fees on Solana](/docs/core/fees)
    * [Programs on Solana](/docs/core/programs)
    * [Program Derived Address](/docs/core/pda)
    * [Cross Program Invocation](/docs/core/cpi)
    * [Tokens on Solana](/docs/core/tokens)
    * [Clusters & Endpoints](/docs/core/clusters)
  * Advanced Concepts

    * [Versioned Transactions](/docs/advanced/versions)
    * [Address Lookup Tables](/docs/advanced/lookup-tables)
    * [Confirmation & Expiration](/docs/advanced/confirmation)
    * [Retrying Transactions](/docs/advanced/retry)
    * [State Compression](/docs/advanced/state-compression)
  * Solana Clients

    * [Rust](/docs/clients/rust)
    * [JavaScript / TypeScript](/docs/clients/javascript)
    * [Web3.js API Examples](/docs/clients/javascript-reference)
  * [Economics](/docs/economics)

    * Inflation
      * [Proposed Inflation Schedule](/docs/economics/inflation/inflation-schedule)
      * [Inflation Terminology](/docs/economics/inflation/terminology)
    * [Staking](/docs/economics/staking)
      * [Stake Accounts](/docs/economics/staking/stake-accounts)
      * [Stake Programming](/docs/economics/staking/stake-programming)
  * Developing Programs

    * [Overview](/docs/programs/overview)
    * [Debugging Programs](/docs/programs/debugging)
    * [Deploying Programs](/docs/programs/deploying)
    * [Program Examples](/docs/programs/examples)
    * [FAQ](/docs/programs/faq)
    * [Developing with C](/docs/programs/lang-c)
    * [Developing with Rust](/docs/programs/lang-rust)
    * [Limitations](/docs/programs/limitations)
  * More Information

    * [Add Solana to Your Exchange](/docs/more/exchange)

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

