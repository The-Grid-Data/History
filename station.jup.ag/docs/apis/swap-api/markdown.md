Skip to main content

[![Jupiter Logo](/img/jupiter-logo.svg)![Jupiter Logo](/img/jupiter-
logo.svg)**Jupiter Station**](/)[Guides](/guides)[Docs](/docs)[API
Playground](/api-v6)[Partners](/partners)[Stats](/stats)

Search

[ Launch App  ](https://jup.ag/)

  * [Welcome](/docs/)
  * [Jupiter APIs](/docs/api)

    * [V6 Swap API](/docs/apis/swap-api)
    * [Payments API](/docs/apis/payments-api)
    * [Adding Fees](/docs/apis/adding-fees)
    * [Price API](/docs/apis/price-api)
    * [Flash Fill](/docs/apis/flash-fill)
    * [CPI / Smart Contract Integration](/docs/apis/cpi)
    * [Game Dev (C#)](/docs/apis/c-sharp-example)
    * [Self-hosted V6 Swap API](/docs/apis/self-hosted)
    * [Troubleshooting](/docs/apis/troubleshooting)
  * [Limit Order](/docs/limit-order)

  * [DCA](/docs/dca)

  * [Jupiter Terminal](/docs/jup-terminal)

  * [Projects and Dexes](/docs/projects-and-dexes)

  * [Token List](/docs/token-list)

  * [Additional Topics](/docs/additional-topics/)

  * [Legacy](/docs/apis)

  * [Legal](/docs/legal)

  * [](/)
  * [Jupiter APIs](/docs/api)
  * V6 Swap API

On this page

# V6 Swap API

Jupiter API is the easiest way for developers to access liquidity on Solana.
Simply pass in the desired pairs, amount, and slippage, and the API will
return the serialized transactions needed to execute the swap, which can then
be passed into the Solana blockchain with the required signatures.

### Try it out!​

Click to play video

Your browser does not support the video tag.

    
    
    # Copy and paste this into your terminal!  
    curl -s 'https://quote-api.jup.ag/v6/quote?inputMint=So11111111111111111111111111111111111111112&outputMint=EPjFWdd5AufqSSqeM2qN1xzybapC8G4wEGGkZwyTDt1v&amount=1000000&slippageBps=1' | jq '.outAmount'  
    

## V6 API Reference​

All Jupiter swaps are using versioned transactions and address lookup tables.
But not all wallets support Versioned Transactions yet, so if you detect a
wallet that does not support versioned transactions, you will need to use the
`asLegacyTransaction` parameter.

Learn more about the Jupiter API Documentation at the [OpenAPI
documentation](/api-v6). This documentation has a REST request list and a
built in API Playground. Use the API Playground to try API calls now!

API Documentation

[OpenAPI Documentation](/api-v6)

### Guide for V6 Swap API​

#### 1\. Install required libraries​

Running this example requires a minimum of [NodeJS
16](https://nodejs.org/en/). In your command line terminal, install the
libraries.

    
    
    npm i @solana/web3.js  
    npm i cross-fetch  
    npm i @project-serum/anchor  
    npm i bs58  
    

#### 2\. Import from libraries and setup connection​

Next you can copy the following code snippets to a javascript file jupiter-
api-example.js. And when you are ready to run the code, just type: _node
jupiter-api-example.js_

    
    
     import { Connection, Keypair, VersionedTransaction } from '@solana/web3.js';  
    import fetch from 'cross-fetch';  
    import { Wallet } from '@project-serum/anchor';  
    import bs58 from 'bs58';  
      
    // It is recommended that you use your own RPC endpoint.  
    // This RPC endpoint is only for demonstration purposes so that this example will run.  
    const connection = new Connection('https://neat-hidden-sanctuary.solana-mainnet.discover.quiknode.pro/2af5315d336f9ae920028bbb90a73b724dc1bbed/');  
    

tip

Always make sure that you are using your own RPC endpoint. The RPC endpoint
used by the connection object in the above example may not work anymore. For
more information about RPC endpoints see the [official Solana
Documentation](https://solana.com/docs/core/clusters) to learn more about
their public RPC endpoints.

#### 3\. Setup your wallet​

You can paste in your private key for testing purposes but this is not
recommended for production applications.

    
    
    const wallet = new Wallet(Keypair.fromSecretKey(bs58.decode(process.env.PRIVATE_KEY || '')));  
    

#### 4\. Get the route for a swap​

Here, we are getting a quote to swap from SOL to USDC.

    
    
    // Swapping SOL to USDC with input 0.1 SOL and 0.5% slippage  
    const quoteResponse = await (  
      await fetch('https://quote-api.jup.ag/v6/quote?inputMint=So11111111111111111111111111111111111111112\  
    &outputMint=EPjFWdd5AufqSSqeM2qN1xzybapC8G4wEGGkZwyTDt1v\  
    &amount=100000000\  
    &slippageBps=50'  
      )  
    ).json();  
    // console.log({ quoteResponse })  
    

### Get the best swap routes for a token trade pair sorted by largest output
token amount​

GET

https://quote-api.jup.ag/v6/quote

### Request Parameters​

Parameter| Type| Required| Description  
---|---|---|---  
`inputMint`| String| Yes| Input token mint address  
`outputMint`| String| Yes| Output token mint address  
`amount`| Integer| Yes| The API takes in _amount_ in integer and you have to
factor in the decimals for each token by looking up the decimals for that
token. For example, USDC has 6 decimals and 1 USDC is 1000000 in integer when
passing it in into the API.  
`slippageBps`| Integer| No| The slippage % in BPS. If the output token amount
exceeds the slippage then the swap transaction will fail.  
`swapMode`| String| No| (ExactIn or ExactOut) Defaults to ExactIn. ExactOut is
for supporting use cases where you need an exact token amount, like payments.
In this case the slippage is on the input token.  
`platformFeeBps`| Integer| No| If you want to charge the user a fee, you can
specify the fee in BPS. Fee % is taken out of the output token.  
`onlyDirectRoutes`| Boolean| No| Default is false. Direct Routes limits
Jupiter routing to single hop routes only.  
`asLegacyTransaction`| Boolean| No| Default is false. Instead of using
versioned transaction, this will use the legacy transaction.  
`excludeDexes`| Array| No| Default is that all DEXes are included. You can
pass in the DEXes that you want to exclude and separate them by `,`. For
example, `Aldrin,Saber`.  
`maxAccounts`| Integer| No| Find a route given a maximum number of accounts
involved, this might dangerously limit routing ending up giving a bad price.
The max is an estimation and not the exact count.  
  
Platform Fee

If you'd like to charge a fee, pass in `platformFeeBps` as a parameter in the
quote.

Amount

The API takes in amount in integer and you have to factor in the decimals for
each token by looking up the decimals for that token. For example, USDC has 6
decimals and 1 USDC is 1000000 in integer when passing it in into the API.

#### 5\. Get the serialized transactions to perform the swap​

Once we have the quote, we need to serialize the quote into a swap transaction
that can be submitted on chain.

    
    
    // get serialized transactions for the swap  
    const { swapTransaction } = await (  
      await fetch('https://quote-api.jup.ag/v6/swap', {  
        method: 'POST',  
        headers: {  
          'Content-Type': 'application/json'  
        },  
        body: JSON.stringify({  
          // quoteResponse from /quote api  
          quoteResponse,  
          // user public key to be used for the swap  
          userPublicKey: wallet.publicKey.toString(),  
          // auto wrap and unwrap SOL. default is true  
          wrapAndUnwrapSol: true,  
          // feeAccount is optional. Use if you want to charge a fee.  feeBps must have been passed in /quote API.  
          // feeAccount: "fee_account_public_key"  
        })  
      })  
    ).json();  
    

POST

https://quote-api.jup.ag/v6/swap

### Request Parameters​

Parameter| Type| Required| Description  
---|---|---|---  
`userPublicKey`| String| Yes| The user public key.  
`quoteResponse`| Quote Response| Yes| The object that is returned from the
Quote API.  
`wrapAndUnwrapSol`| Boolean| No| Default is true. If true, will automatically
wrap/unwrap SOL. If false, it will use wSOL token account.  
`useSharedAccounts`| Boolean| No| Default is true. This enables the usage of
shared program accounts. That means no intermediate token accounts or open
orders accounts need to be created for the users. But it also means that the
likelihood of hot accounts is higher.  
`feeAccount`| String| No| Fee token account for the output token, it is
derived using the seeds = ["referral_ata", referral_account, mint] and the
`REFER4ZgmyYx9c6He5XfaTMiGfdLwRnkV4RPp9t9iF3` referral contract (only pass in
if you set a `platformFeeBps` in `/quote` and make sure that the feeAccount
has been created)  
`computeUnitPriceMicroLamports`| Integer| No| The compute unit price to
prioritize the transaction, the additional fee will be `computeUnitSet
(1400000) * computeUnitPriceMicroLamports`.  
`asLegacyTransaction`| Boolean| No| Default is false. Request a legacy
transaction rather than the default versioned transaction, needs to be paired
with a quote using asLegacyTransaction otherwise the transaction might be too
large.  
`useTokenLedger`| Boolean| No| Default is false. This is useful when the
instruction before the swap has a transfer that increases the input token
amount. Then, the swap will just use the difference between the token ledger
token amount and post token amount.  
`destinationTokenAccount`| String| No| Public key of the token account that
will be used to receive the token out of the swap. If not provided, the user's
ATA will be used. If provided, we assume that the token account is already
initialized.  
  
#### 6\. Deserialize and sign the transaction​

    
    
    // deserialize the transaction  
    const swapTransactionBuf = Buffer.from(swapTransaction, 'base64');  
    var transaction = VersionedTransaction.deserialize(swapTransactionBuf);  
    console.log(transaction);  
      
    // sign the transaction  
    transaction.sign([wallet.payer]);  
    

#### 7\. Execute the transaction​

    
    
    // Execute the transaction  
    const rawTransaction = transaction.serialize()  
    const txid = await connection.sendRawTransaction(rawTransaction, {  
      skipPreflight: true,  
      maxRetries: 2  
    });  
    await connection.confirmTransaction(txid);  
    console.log(`https://solscan.io/tx/${txid}`);  
    

Solana Network Congestion

Due to the network congestion on Solana, the `sendRawTransaction` method may
not be able to help you to land your transaction. You should check out this
[`transactionSender`](https://github.com/jup-ag/jupiter-quote-api-
node/blob/main/example/utils/transactionSender.ts) file to send transaction.

## Advanced error handling to disable certain AMM from the API​

Sometimes an AMM will throw an error when swapping. To prevent getting a quote
from the failed AMM, you can use the `excludeDexes` parameter when getting
`/quote`.

Example JS, with the help of `@mercurial-finance/optimist` package:

    
    
    import { parseErrorForTransaction } from '@mercurial-finance/optimist';  
      
    // TX ID from last step if the transaction failed.  
    const transaction = connection.getTransaction(txid, {  
      maxSupportedTransactionVersion: 0,  
      commitment: 'confirmed'  
    });  
      
    const programIdToLabelHash = await (  
      await fetch('https://quote-api.jup.ag/v6/program-id-to-label')  
    ).json();  
    const { programIds } = parseErrorForTransaction(transaction);  
      
    let excludeDexes = new Set();  
    if (programIds) {  
      for (let programId of programIds) {  
        let foundLabel = programIdToLabelHash[programId];  
        if(foundLabel) {  
          excludeDexes.add(foundLabel);  
        }  
      }  
    }  
      
    // Request another quote with `excludeDexes`.  
    const { data } = await (  
      await fetch(`https://quote-api.jup.ag/v6/quote?inputMint=So11111111111111111111111111111111111111112  
    &outputMint=EPjFWdd5AufqSSqeM2qN1xzybapC8G4wEGGkZwyTDt1v  
    &amount=100000000&excludeDexes=${Array.from(excludeDexes).join(',')}  
    &slippageBps=50`  
      )  
    ).json();  
    

## Instructions Instead of Transaction​

Sometimes you may prefer to compose using instructions instead of one
transaction that is returned from the `/swap` endpoint. You can post to
`/swap-instructions` instead, it takes the same parameters as the `/swap`
endpoint.

    
    
    const instructions = await (  
      await fetch('https://quote-api.jup.ag/v6/swap-instructions', {  
        method: 'POST',  
        headers: {  
          'Content-Type': 'application/json'  
        },  
        body: JSON.stringify({  
          // quoteResponse from /quote api  
          quoteResponse,  
          userPublicKey: swapUserKeypair.publicKey.toBase58(),  
        })  
      })  
    ).json();  
      
    if (instructions.error) {  
      throw new Error("Failed to get swap instructions: " + instructions.error);  
    }  
      
    const {  
      tokenLedgerInstruction, // If you are using `useTokenLedger = true`.  
      computeBudgetInstructions, // The necessary instructions to setup the compute budget.  
      setupInstructions, // Setup missing ATA for the users.  
      swapInstruction: swapInstructionPayload, // The actual swap instruction.  
      cleanupInstruction, // Unwrap the SOL if `wrapAndUnwrapSol = true`.  
      addressLookupTableAddresses, // The lookup table addresses that you can use if you are using versioned transaction.  
    } = instructions;  
      
    const deserializeInstruction = (instruction) => {  
      return new TransactionInstruction({  
        programId: new PublicKey(instruction.programId),  
        keys: instruction.accounts.map((key) => ({  
          pubkey: new PublicKey(key.pubkey),  
          isSigner: key.isSigner,  
          isWritable: key.isWritable,  
        })),  
        data: Buffer.from(instruction.data, "base64"),  
      });  
    };  
      
    const getAddressLookupTableAccounts = async (  
      keys: string[]  
    ): Promise<AddressLookupTableAccount[]> => {  
      const addressLookupTableAccountInfos =  
        await connection.getMultipleAccountsInfo(  
          keys.map((key) => new PublicKey(key))  
        );  
      
      return addressLookupTableAccountInfos.reduce((acc, accountInfo, index) => {  
        const addressLookupTableAddress = keys[index];  
        if (accountInfo) {  
          const addressLookupTableAccount = new AddressLookupTableAccount({  
            key: new PublicKey(addressLookupTableAddress),  
            state: AddressLookupTableAccount.deserialize(accountInfo.data),  
          });  
          acc.push(addressLookupTableAccount);  
        }  
      
        return acc;  
      }, new Array<AddressLookupTableAccount>());  
    };  
      
    const addressLookupTableAccounts: AddressLookupTableAccount[] = [];  
      
    addressLookupTableAccounts.push(  
      ...(await getAddressLookupTableAccounts(addressLookupTableAddresses))  
    );  
      
    const blockhash = (await connection.getLatestBlockhash()).blockhash;  
    const messageV0 = new TransactionMessage({  
      payerKey: payerPublicKey,  
      recentBlockhash: blockhash,  
      instructions: [  
        // uncomment if needed: ...setupInstructions.map(deserializeInstruction),  
        deserializeInstruction(swapInstructionPayload),  
        // uncomment if needed: deserializeInstruction(cleanupInstruction),  
      ],  
    }).compileToV0Message(addressLookupTableAccounts);  
    const transaction = new VersionedTransaction(messageV0);  
    

## Using `maxAccounts`​

Sometimes, if you are composing with Jupiter Swap instruction, you may want to
spare some accounts (64 max in 1 Solana transaction) for your own program
instruction, you can use `maxAccounts`.

    
    
    // If you know that your instruction will take up 10 accounts, you  
    // can pass in 54 as `maxAccounts` when quoting.  
    const { data } = await (  
      await fetch('https://quote-api.jup.ag/v6/quote?inputMint=So11111111111111111111111111111111111111112\  
    &outputMint=EPjFWdd5AufqSSqeM2qN1xzybapC8G4wEGGkZwyTDt1v\  
    &amount=100000000\  
    &slippageBps=50\  
    &maxAccounts=54'  
      )  
    ).json();  
    const quoteResponse = data;  
    // console.log(quoteResponse)  
    

The `maxAccounts` is an estimation since it doesn't consider account
overlapping but it is a good start to control how many accounts you want per
transaction.

## Using Token Ledger Instruction​

Sometimes you may not know the exact input amount for the Jupiter swap until
an instruction before the swap happens.

For example:

    
    
    const instructions = await (  
      await fetch('https://quote-api.jup.ag/v6/swap-instructions', {  
        method: 'POST',  
        headers: {  
          'Content-Type': 'application/json'  
        },  
        body: JSON.stringify({  
          // quoteResponse from /quote api  
          quoteResponse,  
          useTokenLedger: true,  
      })  
    ).json();  
      
    const {  
      tokenLedgerInstruction: tokenLedgerPayload, // If you are using `useTokenLedger = true`.  
      swapInstruction: swapInstructionPayload, // The actual swap instruction.  
      addressLookupTableAddresses, // The lookup table addresses that you can use if you are using versioned transaction.  
    } = instructions;  
      
    // A withdraw instruction that will increase the user input token account amount.  
    const withdrawInstruction = ...;  
      
    // Coupled with the tokenLedgerInstruction, the swap instruction will use the  
    // user increased amount of the input token account after the withdrawal as input amount.  
    const tokenLedgerInstruction = new TransactionInstruction({  
      programId: new PublicKey(tokenLedgerPayload.programId),  
      keys: tokenLedgerPayload.accounts.map((key) => ({  
        pubkey: new PublicKey(key.pubkey),  
          isSigner: key.isSigner,  
          isWritable: key.isWritable,  
        })),  
      data: Buffer.from(tokenLedgerPayload.data, "base64"),  
    });  
      
    const swapInstruction = new TransactionInstruction({  
      programId: new PublicKey(swapInstructionPayload.programId),  
      keys: swapInstructionPayload.accounts.map((key) => ({  
        pubkey: new PublicKey(key.pubkey),  
          isSigner: key.isSigner,  
          isWritable: key.isWritable,  
        })),  
      data: Buffer.from(swapInstructionPayload.data, "base64"),  
    });  
      
    const getAdressLookupTableAccounts = async (  
      keys: string[]  
    ): Promise<AddressLookupTableAccount[]> => {  
      const addressLookupTableAccountInfos =  
        await connection.getMultipleAccountsInfo(  
          keys.map((key) => new PublicKey(key))  
        );  
      
      return addressLookupTableAccountInfos.reduce((acc, accountInfo, index) => {  
        const addressLookupTableAddress = keys[index];  
        if (accountInfo) {  
          const addressLookupTableAccount = new AddressLookupTableAccount({  
            key: new PublicKey(addressLookupTableAddress),  
            state: AddressLookupTableAccount.deserialize(accountInfo.data),  
          });  
          acc.push(addressLookupTableAccount);  
        }  
      
        return acc;  
      }, new Array<AddressLookupTableAccount>());  
    };  
      
    const addressLookupTableAccounts: AddressLookupTableAccount[] = [];  
      
    addressLookupTableAccounts.push(  
      ...(await getAdressLookupTableAccounts(addressLookupTableAddresses))  
    );  
      
    const messageV0 = new TransactionMessage({  
      payerKey: payerPublicKey,  
      recentBlockhash: blockhash,  
      instructions: [tokenLedgerInstruction, withdrawInstruction, swapInstruction],  
    }).compileToV0Message(addressLookupTableAccounts);  
    const transaction = new VersionedTransaction(messageV0);  
    

This can be useful if you want to withdraw from Solend and immediately convert
your withdrawal token into another token with Jupiter.

## Setting Priority Fee for Your Transaction​

If transactions are expiring without confirmation on-chain, this might mean
that you have to pay additional fees to prioritize your transaction. To do so,
you can set the `computeUnitPriceMicroLamports` parameter.

    
    
    const transaction = await (  
      await fetch('https://quote-api.jup.ag/v6/swap', {  
        method: 'POST',  
        headers: {  
          'Content-Type': 'application/json'  
        },  
        body: JSON.stringify({  
          // quoteResponse from /quote api  
          quoteResponse,  
          // user public key to be used for the swap  
          userPublicKey: wallet.publicKey.toString(),  
          dynamicComputeUnitLimit: true, // allow dynamic compute limit instead of max 1,400,000  
          // custom priority fee  
          prioritizationFeeLamports: 'auto' // or custom lamports: 1000  
        })  
      })  
    ).json();  
    

If 'auto' is used, Jupiter will automatically set a priority fee for the
transaction, it will be capped at 5,000,000 lamports / 0.005 SOL.

## Examples​

For more example scripts please visit the [jupiter-quote-api-node public Git
repository](https://github.com/jup-ag/jupiter-quote-api-node). The repository
has some further scripts and instructions for you to explore!

  * Javascript/Typescript: <https://github.com/jup-ag/jupiter-quote-api-node>
  * Rust: <https://github.com/jup-ag/jupiter-api-rust-example>

Having issues? Head to the [Troubleshooting](/docs/apis/troubleshooting)
section for some help.

[Edit this page](https://github.com/jup-ag/space-
station/tree/main/docs/2-apis/1-swap-api.md)

[PreviousJupiter APIs](/docs/api)[NextPayments API](/docs/apis/payments-api)

  * Try it out!
  * V6 API Reference
    * Guide for V6 Swap API
    * Get the best swap routes for a token trade pair sorted by largest output token amount
    * Request Parameters
    * Request Parameters
  * Advanced error handling to disable certain AMM from the API
  * Instructions Instead of Transaction
  * Using `maxAccounts`
  * Using Token Ledger Instruction
  * Setting Priority Fee for Your Transaction
  * Examples

