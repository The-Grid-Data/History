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

[Home](/)>[Developers](/developers)>[Guides](/developers/guides)

# [How to use Priority Fees on Solana](/developers/guides/advanced/how-to-use-
priority-fees)

updated March 7, 2024

[intermediate](/developers/guides?difficulty=intermediate)[web3js](/developers/guides?tags=web3js)

[![How to use Priority Fees on
Solana](https://solana.com/_next/image?url=%2Fopengraph%2Fdevelopers%2Fguides%2Fadvanced%2Fhow-
to-use-priority-fees&w=3840&q=75)](/developers/guides/advanced/how-to-use-
priority-fees)

This guide is meant to be a reference for developers who want to add priority
fees to their transactions on Solana. We will cover priority fees, how to use
them, special considerations, and best practices to estimate them.

## What are Priority Fees? #

Prioritization Fees are an optional fee, priced in [micro-
lamports](/docs/terminology#lamport) per [Compute
Unit](/docs/terminology#compute-units) (e.g. small amounts of SOL), appended
to transactions to make them economically compelling for validator nodes to
include in blocks on the network. This additional fee will be on top of the
base [Transaction Fee](/docs/core/fees) already set, which is 5000 lamports
per signature in your transaction.

## Why Should I Use Priority Fees? #

When a transaction journeys through a validator, one of the critical stages of
the validator is scheduling the transaction. A validator is economically
incentivized to schedule transactions with the highest fee per compute unit
associated, guaranteeing users use resources optimally. A user can still have
their transaction executed with no priority fee attached but with a lesser
guarantee. When blocks are saturated with transactions with priority fees,
validators will drop transactions without priority fees.

## How do I Implement Priority Fees? #

When adding priority fees to a transaction, keep in mind the amount of compute
units (CU) used for your transaction. The higher the CU required for the
transaction, the more fees you will pay when adding priority fees.

Using the [Compute Budget Program](/docs/core/runtime#compute-budget), you can
change the CU requested for your transaction and add any additional priority
fee required. Do note that your CU request must be equal to or greater than
the CU needed for the transaction; otherwise, the transaction will fail.

Let's take a simple transfer SOL transaction and add priority fees. A
[transfer SOL transaction takes 300
CU](https://explorer.solana.com/tx/5scDyuiiEbLxjLUww3APE9X7i8LE3H63unzonUwMG7s2htpoAGG17sgRsNAhR1zVs6NQAnZeRVemVbkAct5myi17).
To best optimize our transaction, request exactly 300 CU with the Compute
Budget Program when adding additional priority fees.

    
    
    // import { ... } from "@solana/web3.js"
     
    const modifyComputeUnits = ComputeBudgetProgram.setComputeUnitLimit({
      units: 300,
    });
     
    const addPriorityFee = ComputeBudgetProgram.setComputeUnitPrice({
      microLamports: 20000,
    });
     
    const transaction = new Transaction()
      .add(modifyComputeUnits)
      .add(addPriorityFee)
      .add(
        SystemProgram.transfer({
          fromPubkey: payer.publicKey,
          toPubkey: toAccount,
          lamports: 10000000,
        }),
      );

Viewing [this
transaction](https://explorer.solana.com/tx/5scDyuiiEbLxjLUww3APE9X7i8LE3H63unzonUwMG7s2htpoAGG17sgRsNAhR1zVs6NQAnZeRVemVbkAct5myi17)
on the Solana Explorer, see that we used
`ComputeBudgetProgram.setComputeUnitLimit` to set the Compute Unit Limit to
300 CUs while also adding a priority fee of 20000 micro-lamports with
`ComputeBudgetProgram.setComputeUnitPrice`.

## How Do I Estimate Priority Fees? #

The best way to estimate priority fees for a given transaction is to query the
historical priority fees required to land a transaction given the correct
accounts. The
[getRecentPrioritizationFees](/docs/rpc/http/getrecentprioritizationfees) JSON
RPC API method will retrieve the lowest priority fees used recently to land a
transaction in a block.

When using `getRecentPrioritizationFees`, provide the accounts used in your
transaction; otherwise, you'll find the lowest fee to land a transaction
overall. Account contention within a block decides priority, and validators
will schedule accordingly.

This RPC method will return the highest fee associated with the provided
accounts, which then becomes the base fee to consider when adding priority
fees.

    
    
    curl https://api.devnet.solana.com -X POST -H "Content-Type: application/json" -d '
      {
        "jsonrpc":"2.0", "id":1,
        "method": "getRecentPrioritizationFees",
        "params": [
          ["CxELquR1gPP8wHe33gZ4QxqGB3sZ9RSwsJ2KshVewkFY"]
        ]
      }
    '

Different approaches to setting Priority Fees exist, and some [third-party
APIs](https://docs.helius.dev/solana-rpc-nodes/alpha-priority-fee-api) are
available to determine the best fee to apply. Given the dynamic nature of the
network, there will not be a "perfect" way to set priority fees, and careful
analysis should be used before choosing a path forward.

## Special Considerations #

If you use priority fees with a [Durable
Nonce](/developers/guides/advanced/introduction-to-durable-nonces)
Transaction, you must ensure the `AdvanceNonce` instruction is your
transaction's first instruction. This is critical to ensure your transaction
is successful; otherwise, it will fail.

    
    
    const advanceNonce = SystemProgram.nonceAdvance({
      noncePubkey: nonceAccountPubkey,
      authorizedPubkey: nonceAccountAuth.publicKey,
    });
     
    const modifyComputeUnits = ComputeBudgetProgram.setComputeUnitLimit({
      units: 300,
    });
     
    const addPriorityFee = ComputeBudgetProgram.setComputeUnitPrice({
      microLamports: 20000,
    });
     
    const transaction = new Transaction()
      .add(advanceNonce)
      .add(modifyComputeUnits)
      .add(addPriorityFee)
      .add(
        SystemProgram.transfer({
          fromPubkey: payer.publicKey,
          toPubkey: toAccount,
          lamports: 10000000,
        }),
      );

[Previous« How to Request Optimal Compute
Budget](/developers/guides/advanced/how-to-request-optimal-
compute)[NextDurable & Offline Transaction Signing using Nonces
»](/developers/guides/advanced/introduction-to-durable-nonces)

##### Table of Contents

  * [What are Priority Fees](/developers/guides/advanced/how-to-use-priority-fees#what-are-priority-fees)
  * [Why Should I Use Priority Fees](/developers/guides/advanced/how-to-use-priority-fees#why-should-i-use-priority-fees)
  * [How do I Implement Priority Fees](/developers/guides/advanced/how-to-use-priority-fees#how-do-i-implement-priority-fees)
  * [How Do I Estimate Priority Fees](/developers/guides/advanced/how-to-use-priority-fees#how-do-i-estimate-priority-fees)
  * [Special Considerations](/developers/guides/advanced/how-to-use-priority-fees#special-considerations)

[Scroll to Top](/developers/guides/advanced/how-to-use-priority-fees#)

[Edit Page](https://github.com/solana-foundation/developer-
content/tree/main/content/guides/advanced/how-to-use-priority-fees.md)

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

