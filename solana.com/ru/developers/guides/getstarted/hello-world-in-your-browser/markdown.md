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

[Home](/ru)>[Developers](/ru/developers)>[Guides](/ru/developers/guides)

# [Intro to Solana development (using only your
browser)](/ru/developers/guides/getstarted/hello-world-in-your-browser)

updated 18 января 2023 г.

[intro](/ru/developers/guides?difficulty=intro)[quickstart](/ru/developers/guides?tags=quickstart)[Solana
Playground](/ru/developers/guides?tags=Solana%20Playground)[native](/ru/developers/guides?tags=native)[rust](/ru/developers/guides?tags=rust)[web3js](/ru/developers/guides?tags=web3js)

[![Intro to Solana development \(using only your
browser\)](https://solana.com/_next/image?url=%2Fopengraph%2Fdevelopers%2Fguides%2Fgetstarted%2Fhello-
world-in-your-browser&w=3840&q=75)](/ru/developers/guides/getstarted/hello-
world-in-your-browser)

For this "hello world" quickstart guide, we will use [Solana
Playground](https://beta.solpg.io), a browser based IDE to develop and deploy
our Solana program. To use it, you do **NOT** have to install any software on
your computer. Simply open Solana Playground in your browser of choice, and
you are ready to write and deploy Solana programs.

## What you will learn #

  * how to get started with Solana Playground
  * how to create a Solana wallet on Playground
  * how to program a basic Solana program in Rust
  * how to build and deploy a Solana Rust program
  * how to interact with your onchain program using JavaScript

## Using Solana Playground #

[Solana Playground](https://beta.solpg.io) is browser based application that
will let you write, build, and deploy onchain Solana programs. All from your
browser. No installation needed.

It is a great developer resource for getting started with Solana development,
especially on Windows.

### Import our example project #

In a new tab in your browser, open our example "_Hello World_ " [project on
Solana Playground](https://beta.solpg.io/6314a69688a7fca897ad7d1d)

Next, import the project into your local workspace by clicking the "**Import**
" icon and naming your project `hello_world`.

Info

If you do **not** import the program into **your** Solana Playground, then you
will **not** be able to make changes to the code. But you **will** still be
able to build and deploy the code to a Solana cluster.

### Create a Playground wallet #

Normally with [local development](/ru/developers/guides/getstarted/setup-
local-development), you will need to create a file system wallet for use with
the Solana CLI. But with the Solana Playground, you only need to click a few
buttons to create a browser based wallet.

Info

Your _Playground Wallet_ will be saved in your browser's local storage.
Clearing your browser cache will remove your saved wallet. When creating a new
wallet, you will have the option to save a local copy of your wallet's keypair
file.

Click on the red status indicator button at the bottom left of the screen,
(optionally) save your wallet's keypair file to your computer for backup, then
click "**Continue** ".

After your Playground Wallet is created, you will notice the bottom of the
window now states your wallet's address, your SOL balance, and the Solana
cluster you are connected to (Devnet is usually the default/recommended, but a
"localhost" [test validator](/ru/developers/guides/getstarted/setup-local-
development) is also acceptable).

## Create a Solana program #

The code for your Rust based Solana program will live in your `src/lib.rs`
file. Inside `src/lib.rs` you will be able to import your Rust crates and
define your logic. Open your `src/lib.rs` file within Solana Playground.

### Import the `solana_program` crate #

At the top of `lib.rs`, we import the `solana-program` crate and bring our
needed items into the local namespace:

    
    
    use solana_program::{
        account_info::AccountInfo,
        entrypoint,
        entrypoint::ProgramResult,
        pubkey::Pubkey,
        msg,
    };

### Write your program logic #

Every Solana program must define an `entrypoint` that tells the Solana runtime
where to start executing your onchain code. Your program's
[entrypoint](/ru/docs/programs/lang-rust#program-entrypoint) should provide a
public function named `process_instruction`:

    
    
    // declare and export the program's entrypoint
    entrypoint!(process_instruction);
     
    // program entrypoint's implementation
    pub fn process_instruction(
        program_id: &Pubkey,
        accounts: &[AccountInfo],
        instruction_data: &[u8]
    ) -> ProgramResult {
        // log a message to the blockchain
        msg!("Hello, world!");
     
        // gracefully exit the program
        Ok(())
    }

Every onchain program should return the `Ok` [result enum](https://doc.rust-
lang.org/std/result/) with a value of `()`. This tells the Solana runtime that
your program executed successfully without errors.

Our program above will simply [log a
message](/ru/docs/programs/debugging#logging) of "_Hello, world!_ " to the
blockchain cluster, then gracefully exit with `Ok(())`.

### Build your program #

On the left sidebar, select the "**Build & Deploy**" tab. Next, click the
"Build" button.

If you look at the Playground's terminal, you should see your Solana program
begin to compile. Once complete, you will see a success message.

Info

You may receive _warning_ when your program is compiled due to unused
variables. Don't worry, these warning will not affect your build. They are due
to our very simple program not using all the variables we declared in the
`process_instruction` function.

### Deploy your program #

You can click the "Deploy" button to deploy your first program to the Solana
blockchain. Specifically to your selected cluster (e.g. Devnet, Testnet, etc).

After each deployment, you will see your Playground Wallet balance change. By
default, Solana Playground will automatically request SOL airdrops on your
behalf to ensure your wallet has enough SOL to cover the cost of deployment.

Info

Note: If you need more SOL, you can airdrop more by typing airdrop command in
the playground terminal:

    
    
    solana airdrop 2

### Find your program id #

When executing a program using [web3.js](/ru/docs/clients/javascript-
reference) or from [another Solana program](/ru/docs/core/cpi), you will need
to provide the `program id` (aka public address of your program).

Inside Solana Playground's **Build & Deploy** sidebar, you can find your
`program id` under the **Program Credentials** dropdown.

#### Congratulations! #

You have successfully setup, built, and deployed a Solana program using the
Rust language directly in your browser. Next, we will demonstrate how to
interact with your onchain program.

## Interact with your onchain program #

Once you have successfully deployed a Solana program to the blockchain, you
will want to be able to interact with that program.

Like most developers creating dApps and websites, we will interact with our on
chain program using JavaScript. Specifically, will use the open source [NPM
package](https://www.npmjs.com/package/@solana/web3.js) `@solana/web3.js` to
aid in our client application.

Info

This web3.js package is an abstraction layer on top of the [JSON RPC
API](/ru/docs/rpc) that reduced the need for rewriting common boilerplate,
helping to simplify your client side application code.

### Initialize client #

We will be using Solana Playground for the client generation. Create a client
folder by running `run` command in the playground terminal:

    
    
    run

We have created `client` folder and a default `client.ts`. This is where we
will work for the rest of our `hello world` program.

### Playground globals #

In playground, there are many utilities that are globally available for us to
use without installing or setting up anything. Most important ones for our
`hello world` program are `web3` for `@solana/web3.js` and `pg` for Solana
Playground utilities.

Info

You can go over all of the available globals by pressing `CTRL+SPACE` (or
`CMD+SPACE` on macOS) inside the editor.

### Call the program #

To execute your onchain program, you must send a
[transaction](/ru/docs/core/transactions) to it. Each transaction submitted to
the Solana blockchain contains a listing of instructions (and the program's
that instruction will interact with).

Here we create a new transaction and add a single `instruction` to it:

    
    
    // create an empty transaction
    const transaction = new web3.Transaction();
     
    // add a hello world program instruction to the transaction
    transaction.add(
      new web3.TransactionInstruction({
        keys: [],
        programId: new web3.PublicKey(pg.PROGRAM_ID),
      }),
    );

Each `instruction` must include all the keys involved in the operation and the
program ID we want to execute. In this example `keys` is empty because our
program only logs `hello world` and doesn't need any accounts.

With our transaction created, we can submit it to the cluster:

    
    
    // send the transaction to the Solana cluster
    console.log("Sending transaction...");
    const txHash = await web3.sendAndConfirmTransaction(
      pg.connection,
      transaction,
      [pg.wallet.keypair],
    );
    console.log("Transaction sent with hash:", txHash);

Info

The first signer in the signers array is the transaction fee payer by default.
We are signing with our keypair `pg.wallet.keypair`.

### Run the application #

With the client application written, you can run the code via the same `run`
command.

Once your application completes, you will see output similar to this:

    
    
    Running client...
      client.ts:
        My address: GkxZRRNPfaUfL9XdYVfKF3rWjMcj5md6b6mpRoWpURwP
        My balance: 5.7254472 SOL
        Sending transaction...
        Transaction sent with hash: 2Ra7D9JoqeNsax9HmNq6MB4qWtKPGcLwoqQ27mPYsPFh3h8wignvKB2mWZVvdzCyTnp7CEZhfg2cEpbavib9mCcq

### Get transaction logs #

We will be using `solana-cli` directly in playground to get the information
about any transaction:

    
    
    solana confirm -v <TRANSACTION_HASH>

Change `<TRANSACTION_HASH>` with the hash you received from calling `hello
world` program.

You should see `Hello, world!` in the **Log Messages** section of the output.
🎉

#### Congratulations!!! #

You have now written a client application for your onchain program. You are
now a Solana developer!

PS: Try to update your program's message then re-build, re-deploy, and re-
execute your program.

## Next steps #

See the links below to learn more about writing Solana programs, and setting
up your local development environment:

  * [Setup your local development environment](/ru/developers/guides/getstarted/setup-local-development)
  * [Overview of writing Solana programs](/ru/docs/programs)
  * [Learn more about developing Solana programs with Rust](/ru/docs/programs/lang-rust)
  * [Debugging onchain programs](/ru/docs/programs/debugging)

[Previous« Full-stack Solana development with React and
Anchor](/ru/developers/guides/getstarted/full-stack-solana-
development)[NextHow to CPI with a PDA Signer in a Solana program
»](/ru/developers/guides/getstarted/how-to-cpi-with-signer)

##### Table of Contents

  * [What you will learn](/ru/developers/guides/getstarted/hello-world-in-your-browser#what-you-will-learn)
  * [Using Solana Playground](/ru/developers/guides/getstarted/hello-world-in-your-browser#using-solana-playground)
  * [Import our example project](/ru/developers/guides/getstarted/hello-world-in-your-browser#import-our-example-project)
  * [Create a Playground wallet](/ru/developers/guides/getstarted/hello-world-in-your-browser#create-a-playground-wallet)
  * [Create a Solana program](/ru/developers/guides/getstarted/hello-world-in-your-browser#create-a-solana-program)
  * [Import the `solana_program` crate](/ru/developers/guides/getstarted/hello-world-in-your-browser#import-the-solana_program-crate)
  * [Write your program logic](/ru/developers/guides/getstarted/hello-world-in-your-browser#write-your-program-logic)
  * [Build your program](/ru/developers/guides/getstarted/hello-world-in-your-browser#build-your-program)
  * [Deploy your program](/ru/developers/guides/getstarted/hello-world-in-your-browser#deploy-your-program)
  * [Find your program id](/ru/developers/guides/getstarted/hello-world-in-your-browser#find-your-program-id)
  * [Interact with your onchain program](/ru/developers/guides/getstarted/hello-world-in-your-browser#interact-with-your-onchain-program)
  * [Initialize client](/ru/developers/guides/getstarted/hello-world-in-your-browser#initialize-client)
  * [Playground globals](/ru/developers/guides/getstarted/hello-world-in-your-browser#playground-globals)
  * [Call the program](/ru/developers/guides/getstarted/hello-world-in-your-browser#call-the-program)
  * [Run the application](/ru/developers/guides/getstarted/hello-world-in-your-browser#run-the-application)
  * [Get transaction logs](/ru/developers/guides/getstarted/hello-world-in-your-browser#get-transaction-logs)
  * [Next steps](/ru/developers/guides/getstarted/hello-world-in-your-browser#next-steps)

[Scroll to Top](/ru/developers/guides/getstarted/hello-world-in-your-browser#)

[Edit Page](https://github.com/solana-foundation/developer-
content/tree/main/content/guides/getstarted/hello-world-in-your-browser.md)

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

