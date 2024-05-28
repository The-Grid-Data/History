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

# [How to Request Optimal Compute Budget](/developers/guides/advanced/how-to-
request-optimal-compute)

updated March 19, 2024

[intermediate](/developers/guides?difficulty=intermediate)[compute](/developers/guides?tags=compute)

[![How to Request Optimal Compute
Budget](https://solana.com/_next/image?url=%2Fopengraph%2Fdevelopers%2Fguides%2Fadvanced%2Fhow-
to-request-optimal-compute&w=3840&q=75)](/developers/guides/advanced/how-to-
request-optimal-compute)

All transactions on Solana use [Compute Units (CU)](/docs/terminology#compute-
units), which measure the computational resources your transaction uses on the
network. When you pay [priority fees](/developers/guides/advanced/how-to-use-
priority-fees) on your transactions, you must specify the exact amount of
compute units you expect to use; otherwise, you will overpay for your
transaction. This guide will provide step-by-step instructions on optimizing
the compute units for your transaction requests.

## How to Request Compute Budget #

For precise control over your transaction's computational resources, use the
`setComputeUnitLimit` instruction from the Compute Budget program. This
instruction allocates a specific number of compute units for your transaction,
ensuring you only pay for what you need.

    
    
    // import { ComputeBudgetProgram } from "@solana/web3.js"
     
    const modifyComputeUnits = ComputeBudgetProgram.setComputeUnitLimit({
      units: 300,
    });

This instruction will allocate a specific amount of compute units for your
transaction. How do we come up with the number to use?

The [simulateTransaction RPC method](/docs/rpc/http/simulatetransaction) will
return the estimated compute units consumed given a transaction.

The [Solana helpers npm package](https://www.npmjs.com/package/@solana-
developers/helpers) includes
[`getSimulationComputeUnits`](https://github.com/solana-
developers/helpers?tab=readme-ov-file#get-simulated-compute-units-cus-for-
transaction-instructions), a small function that uses `simulateTransaction` to
calculate the compute units. You can then set the compute units in your new
transaction, and send the new transaction for an optimal result.

    
    
    npm i @solana-developers/helpers

The syntax is simply:

    
    
    getSimulationComputeUnits(
      connection: Connection,
      instructions: Array<TransactionInstruction>,
      payer: PublicKey,
      lookupTables: Array<AddressLookupTableAccount>
    );

For example:

    
    
    const units = await getSimulationComputeUnits(
      connection,
      transactions,
      payer.publicKey,
    );

Using `getSimulationComputeUnits`, you can build an optimal transaction that
use an appropriate amount of compute units for what the transaction consumes:

    
    
    // import { ... } from "@solana/web3.js"
     
    async function buildOptimalTransaction(
      connection: Connection,
      instructions: Array<TransactionInstruction>,
      signer: Signer,
      lookupTables: Array<AddressLookupTableAccount>,
    ) {
      const [microLamports, units, recentBlockhash] = await Promise.all([
        100 /* Get optimal priority fees - https://solana.com/developers/guides/advanced/how-to-use-priority-fees*/,
        getSimulationComputeUnits(
          connection,
          instructions,
          signer.publicKey,
          lookupTables,
        ),
        connection.getLatestBlockhash(),
      ]);
     
      instructions.unshift(
        ComputeBudgetProgram.setComputeUnitPrice({ microLamports }),
      );
      if (units) {
        // probably should add some margin of error to units
        instructions.unshift(ComputeBudgetProgram.setComputeUnitLimit({ units }));
      }
      return {
        transaction: new VersionedTransaction(
          new TransactionMessage({
            instructions,
            recentBlockhash: recentBlockhash.blockhash,
            payerKey: signer.publicKey,
          }).compileToV0Message(lookupTables),
        ),
        recentBlockhash,
      };
    }

Credit for this example code

Credit to Sammmmmy, aka [@stegaBOB](https://twitter.com/stegaBOB), for the
source code of these two functions.

## Special Considerations #

Compute units for transactions are not always stable. For example, the compute
usage can change if the transaction you are executing has a call to
`find_program_address`, such as when finding a program derived address.

If you have a variable compute usage on your transactions, you can do one of
two things:

  1. Run a test over your transactions over some time to find out the ceiling compute unit usage and use that number.

  2. Take the compute units returned from `simulateTransaction` and add a percentage to the total. For example, if you chose to add 10% more CU and the result you received from `simulateTransaction` was 1000 CU, you would set 1100 CU on your transaction.

## Conclusion #

Requesting the optimal compute units for your transaction is essential to help
you pay less for your transaction and to help schedule your transaction better
on the network. Wallets, dApps, and other services should ensure their compute
unit requests are optimal to provide the best experience possible for their
users.

## More Resources #

You can learn more about the Compute Budget and related topics with these
resources:

  * documentation for the [Compute Budget](/docs/core/runtime#compute-budget)
  * Guide on [how to use priority fees](/developers/guides/advanced/how-to-use-priority-fees)
  * Guide on [how to optimize compute units in programs](/developers/guides/advanced/how-to-optimize-compute)

[Previous« How to Optimize Compute Usage on
Solana](/developers/guides/advanced/how-to-optimize-compute)[NextHow to use
Priority Fees on Solana »](/developers/guides/advanced/how-to-use-priority-
fees)

##### Table of Contents

  * [How to Request Compute Budget](/developers/guides/advanced/how-to-request-optimal-compute#how-to-request-compute-budget)
  * [Special Considerations](/developers/guides/advanced/how-to-request-optimal-compute#special-considerations)
  * [Conclusion](/developers/guides/advanced/how-to-request-optimal-compute#conclusion)
  * [More Resources](/developers/guides/advanced/how-to-request-optimal-compute#more-resources)

[Scroll to Top](/developers/guides/advanced/how-to-request-optimal-compute#)

[Edit Page](https://github.com/solana-foundation/developer-
content/tree/main/content/guides/advanced/how-to-request-optimal-compute.md)

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
