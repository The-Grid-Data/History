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

  * [Compressing onchain addresses](/docs/advanced/lookup-tables#compressing-onchain-addresses)
  * [Versioned Transactions](/docs/advanced/lookup-tables#versioned-transactions)
  * [How to create an address lookup table](/docs/advanced/lookup-tables#how-to-create-an-address-lookup-table)
  * [Add addresses to a lookup table](/docs/advanced/lookup-tables#add-addresses-to-a-lookup-table)
  * [Fetch an Address Lookup Table](/docs/advanced/lookup-tables#fetch-an-address-lookup-table)
  * [How to use an address lookup table in a transaction](/docs/advanced/lookup-tables#how-to-use-an-address-lookup-table-in-a-transaction)
  * [More Resources](/docs/advanced/lookup-tables#more-resources)

[Scroll to Top](/docs/advanced/lookup-tables#)

[Edit Page](https://github.com/solana-foundation/developer-
content/tree/main/docs/advanced/lookup-tables.md)

[Home](/)>[Solana Documentation](/docs)>Advanced Concepts

# [Address Lookup Tables](/docs/advanced/lookup-tables)

Address Lookup Tables, commonly referred to as "_lookup tables_ " or "_ALTs_ "
for short, allow developers to create a collection of related addresses to
efficiently load more addresses in a single transaction.

Since each transaction on the Solana blockchain requires a listing of every
address that is interacted with as part of the transaction, this listing would
effectively be capped at 32 addresses per transaction. With the help of
[Address Lookup Tables](/docs/advanced/lookup-tables), a transaction would now
be able to raise that limit to 256 addresses per transaction.

## Compressing onchain addresses #

After all the desired addresses have been stored onchain in an Address Lookup
Table, each address can be referenced inside a transaction by its 1-byte index
within the table (instead of their full 32-byte address). This lookup method
effectively "_compresses_ " a 32-byte address into a 1-byte index value.

This "_compression_ " enables storing up to 256 addresses in a single lookup
table for use inside any given transaction.

## Versioned Transactions #

To utilize an Address Lookup Table inside a transaction, developers must use
v0 transactions that were introduced with the new [Versioned Transaction
format](/docs/advanced/versions).

## How to create an address lookup table #

Creating a new lookup table with the `@solana/web3.js` library is similar to
the older `legacy` transactions, but with some differences.

Using the `@solana/web3.js` library, you can use the
[`createLookupTable`](https://solana-labs.github.io/solana-
web3.js/classes/AddressLookupTableProgram.html#createLookupTable) function to
construct the instruction needed to create a new lookup table, as well as
determine its address:

    
    
    const web3 = require("@solana/web3.js");
     
    // connect to a cluster and get the current `slot`
    const connection = new web3.Connection(web3.clusterApiUrl("devnet"));
    const slot = await connection.getSlot();
     
    // Assumption:
    // `payer` is a valid `Keypair` with enough SOL to pay for the execution
     
    const [lookupTableInst, lookupTableAddress] =
      web3.AddressLookupTableProgram.createLookupTable({
        authority: payer.publicKey,
        payer: payer.publicKey,
        recentSlot: slot,
      });
     
    console.log("lookup table address:", lookupTableAddress.toBase58());
     
    // To create the Address Lookup Table onchain:
    // send the `lookupTableInst` instruction in a transaction

Info

NOTE: Address lookup tables can be **created** with either a `v0` transaction
or a `legacy` transaction. But the Solana runtime can only retrieve and handle
the additional addresses within a lookup table while using [v0 Versioned
Transactions](/docs/advanced/versions#current-transaction-versions).

## Add addresses to a lookup table #

Adding addresses to a lookup table is known as "_extending_ ". Using the
`@solana/web3.js` library, you can create a new _extend_ instruction using the
[`extendLookupTable`](https://solana-labs.github.io/solana-
web3.js/classes/AddressLookupTableProgram.html#extendLookupTable) method:

    
    
    // add addresses to the `lookupTableAddress` table via an `extend` instruction
    const extendInstruction = web3.AddressLookupTableProgram.extendLookupTable({
      payer: payer.publicKey,
      authority: payer.publicKey,
      lookupTable: lookupTableAddress,
      addresses: [
        payer.publicKey,
        web3.SystemProgram.programId,
        // list more `publicKey` addresses here
      ],
    });
     
    // Send this `extendInstruction` in a transaction to the cluster
    // to insert the listing of `addresses` into your lookup table with address `lookupTableAddress`

Info

NOTE: Due to the same memory limits of `legacy` transactions, any transaction
used to _extend_ an Address Lookup Table is also limited in how many addresses
can be added at a time. Because of this, you will need to use multiple
transactions to _extend_ any table with more addresses (~20) that can fit
within a single transaction's memory limits.

Once these addresses have been inserted into the table, and stored onchain,
you will be able to utilize the Address Lookup Table in future transactions.
Enabling up to 256 addresses in those future transactions.

## Fetch an Address Lookup Table #

Similar to requesting another account (or PDA) from the cluster, you can fetch
a complete Address Lookup Table with the
[`getAddressLookupTable`](https://solana-labs.github.io/solana-
web3.js/classes/Connection.html#getAddressLookupTable) method:

    
    
    // define the `PublicKey` of the lookup table to fetch
    const lookupTableAddress = new web3.PublicKey("");
     
    // get the table from the cluster
    const lookupTableAccount = (
      await connection.getAddressLookupTable(lookupTableAddress)
    ).value;
     
    // `lookupTableAccount` will now be a `AddressLookupTableAccount` object
     
    console.log("Table address from cluster:", lookupTableAccount.key.toBase58());

Our `lookupTableAccount` variable will now be a `AddressLookupTableAccount`
object which we can parse to read the listing of all the addresses stored on
chain in the lookup table:

    
    
    // loop through and parse all the addresses stored in the table
    for (let i = 0; i < lookupTableAccount.state.addresses.length; i++) {
      const address = lookupTableAccount.state.addresses[i];
      console.log(i, address.toBase58());
    }

## How to use an address lookup table in a transaction #

After you have created your lookup table, and stored your needed address on
chain (via extending the lookup table), you can create a `v0` transaction to
utilize the onchain lookup capabilities.

Just like older `legacy` transactions, you can create all the
[instructions](/docs/terminology#instruction) your transaction will execute
onchain. You can then provide an array of these instructions to the
[Message](/docs/terminology#message) used in the `v0 transaction.

Info

NOTE: The instructions used inside a `v0` transaction can be constructed using
the same methods and functions used to create the instructions in the past.
There is no required change to the instructions used involving an Address
Lookup Table.

    
    
    // Assumptions:
    // - `arrayOfInstructions` has been created as an `array` of `TransactionInstruction`
    // - we are using the `lookupTableAccount` obtained above
     
    // construct a v0 compatible transaction `Message`
    const messageV0 = new web3.TransactionMessage({
      payerKey: payer.publicKey,
      recentBlockhash: blockhash,
      instructions: arrayOfInstructions, // note this is an array of instructions
    }).compileToV0Message([lookupTableAccount]);
     
    // create a v0 transaction from the v0 message
    const transactionV0 = new web3.VersionedTransaction(messageV0);
     
    // sign the v0 transaction using the file system wallet we created named `payer`
    transactionV0.sign([payer]);
     
    // send and confirm the transaction
    // (NOTE: There is NOT an array of Signers here; see the note below...)
    const txid = await web3.sendAndConfirmTransaction(connection, transactionV0);
     
    console.log(
      `Transaction: https://explorer.solana.com/tx/${txid}?cluster=devnet`,
    );

Info

NOTE: When sending a `VersionedTransaction` to the cluster, it must be signed
BEFORE calling the `sendAndConfirmTransaction` method. If you pass an array of
`Signer` (like with `legacy` transactions) the method will trigger an error!

## More Resources #

  * Read the [proposal](https://docs.solanalabs.com/proposals/versioned-transactions) for Address Lookup Tables and Versioned transactions
  * [Example Rust program using Address Lookup Tables](https://github.com/TeamRaccoons/address-lookup-table-multi-swap)

[Previous« Versioned Transactions](/docs/advanced/versions)[NextConfirmation &
Expiration »](/docs/advanced/confirmation)

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

![](https://t.co/1/i/adsct?bci=4&eci=3&event=%7B%7D&event_id=d0d5a3c3-369a-4988-ba6e-4b1311c2d208&integration=gtm&p_id=Twitter&p_user_id=0&pl_id=35cf0ff7-adb7-431e-b6c4-b2b91f513ed7&tw_document_href=https%3A%2F%2Fsolana.com%2Fdocs%2Fadvanced%2Flookup-
tables&tw_iframe_status=0&txn_id=o6jgu&type=javascript&version=2.3.30)![](https://analytics.twitter.com/1/i/adsct?bci=4&eci=3&event=%7B%7D&event_id=d0d5a3c3-369a-4988-ba6e-4b1311c2d208&integration=gtm&p_id=Twitter&p_user_id=0&pl_id=35cf0ff7-adb7-431e-b6c4-b2b91f513ed7&tw_document_href=https%3A%2F%2Fsolana.com%2Fdocs%2Fadvanced%2Flookup-
tables&tw_iframe_status=0&txn_id=o6jgu&type=javascript&version=2.3.30)
