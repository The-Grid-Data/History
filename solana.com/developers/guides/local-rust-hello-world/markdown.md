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

# [Setup, build, and deploy a Solana program locally in
Rust](/developers/guides/getstarted/local-rust-hello-world)

updated March 28, 2023

[intro](/developers/guides?difficulty=intro)[quickstart](/developers/guides?tags=quickstart)[local](/developers/guides?tags=local)[rust](/developers/guides?tags=rust)[native](/developers/guides?tags=native)

[![Setup, build, and deploy a Solana program locally in
Rust](https://solana.com/_next/image?url=%2Fopengraph%2Fdevelopers%2Fguides%2Fgetstarted%2Flocal-
rust-hello-world&w=3840&q=75)](/developers/guides/getstarted/local-rust-hello-
world)

Rust is the most common programming language to write Solana programs with.
This quickstart guide will demonstrate how to quickly setup, build, and deploy
your first Rust based Solana program to the blockchain.

Do you have the Solana CLI installed?

This guide uses the Solana CLI and assumes you have setup your local
development environment. Checkout our [local development quickstart
guide](/developers/guides/setup-local-development) here to quickly get setup.

## What you will learn #

  * how to install the Rust language locally
  * how to initialize a new Solana Rust program
  * how to code a basic Solana program in Rust
  * how to build and deploy your Rust program

## Install Rust and Cargo #

To be able to compile Rust based Solana programs, install the Rust language
and Cargo (the Rust package manager) using [Rustup](https://rustup.rs/):

    
    
    curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh

## Run your localhost validator #

The Solana CLI comes with the [test
validator](https://docs.solana.com/developing/test-validator) built in. This
command line tool will allow you to run a full blockchain cluster on your
machine.

    
    
    solana-test-validator

PRO TIP

Run the Solana test validator in a new/separate terminal window that will
remain open. This command line program must remain running for your localhost
validator to remain online and ready for action.

Configure your Solana CLI to use your localhost validator for all your future
terminal commands and Solana program deployment:

    
    
    solana config set --url localhost

## Create a new Rust library with Cargo #

Solana programs written in Rust are _libraries_ which are compiled to [BPF
bytecode](https://docs.solana.com/developing/on-chain-programs/faq#berkeley-
packet-filter-bpf) and saved in the `.so` format.

Initialize a new Rust library named `hello_world` via the Cargo command line:

    
    
    cargo init hello_world --lib
    cd hello_world

Add the `solana-program` crate to your new Rust library:

    
    
    cargo add solana-program

Pro Tip

It is highly recommended to keep your `solana-program` and other Solana Rust
dependencies in-line with your installed version of the Solana CLI. For
example, if you are running Solana CLI `1.17.17`, you can instead run:

    
    
    cargo add solana-program@"=1.17.17"

This will ensure your crate uses only `1.17.17` and nothing else. If you
experience compatibility issues with Solana dependencies, check out the
[Solana Stack Exchange](https://solana.stackexchange.com/questions/9798/error-
building-program-with-solana-program-v1-18-and-cli-v1-17/9799)

Open your `Cargo.toml` file and add these required Rust library configuration
settings, updating your project name as appropriate:

    
    
    [lib]
    name = "hello_world"
    crate-type = ["cdylib", "lib"]

## Create your first Solana program #

The code for your Rust based Solana program will live in your `src/lib.rs`
file. Inside `src/lib.rs` you will be able to import your Rust crates and
define your logic. Open your `src/lib.rs` file in your favorite editor.

At the top of `lib.rs`, import the `solana-program` crate and bring our needed
items into the local namespace:

    
    
    use solana_program::{
        account_info::AccountInfo,
        entrypoint,
        entrypoint::ProgramResult,
        pubkey::Pubkey,
        msg,
    };

Every Solana program must define an `entrypoint` that tells the Solana runtime
where to start executing your onchain code. Your program's
[entrypoint](https://docs.solana.com/developing/on-chain-programs/developing-
rust#program-entrypoint) should provide a public function named
`process_instruction`:

    
    
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

This program above will simply [log a
message](https://docs.solana.com/developing/on-chain-
programs/debugging#logging) of "_Hello, world!_ " to the blockchain cluster,
then gracefully exit with `Ok(())`.

## Build your Rust program #

Inside a terminal window, you can build your Solana Rust program by running in
the root of your project (i.e. the directory with your `Cargo.toml` file):

    
    
    cargo build-bpf

Info

After each time you build your Solana program, the above command will output
the build path of your compiled program's `.so` file and the default keyfile
that will be used for the program's address. `cargo build-bpf` installs the
toolchain from the currently installed solana CLI tools. You may need to
upgrade those tools if you encounter any version incompatibilities.

## Deploy your Solana program #

Using the Solana CLI, you can deploy your program to your currently selected
cluster:

    
    
    solana program deploy ./target/deploy/hello_world.so

Once your Solana program has been deployed (and the transaction
[finalized](https://docs.solana.com/cluster/commitments)), the above command
will output your program's public address (aka its "program id").

    
    
    # example output
    Program Id: EFH95fWg49vkFNbAdw9vy75tM7sWZ2hQbTTUmuACGip3

#### Congratulations! #

You have successfully setup, built, and deployed a Solana program using the
Rust language.

Check your wallet balance!

Check your Solana wallet's balance again after you deployed. See how much SOL
it cost to deploy your simple program?

## Next steps #

See the links below to learn more about writing Rust based Solana programs:

  * [Overview of writing Solana programs](https://docs.solana.com/developing/on-chain-programs/overview)
  * [Learn more about developing Solana programs with Rust](https://docs.solana.com/developing/on-chain-programs/developing-rust)
  * [Debugging onchain programs](https://docs.solana.com/developing/on-chain-programs/debugging)

[Previous« How to write a Native Rust
Program](/developers/guides/getstarted/intro-to-native-rust)[NextGetting
started with Solana with Rust Experience
»](/developers/guides/getstarted/rust-to-solana)

##### Table of Contents

  * [What you will learn](/developers/guides/getstarted/local-rust-hello-world#what-you-will-learn)
  * [Install Rust and Cargo](/developers/guides/getstarted/local-rust-hello-world#install-rust-and-cargo)
  * [Run your localhost validator](/developers/guides/getstarted/local-rust-hello-world#run-your-localhost-validator)
  * [Create a new Rust library with Cargo](/developers/guides/getstarted/local-rust-hello-world#create-a-new-rust-library-with-cargo)
  * [Create your first Solana program](/developers/guides/getstarted/local-rust-hello-world#create-your-first-solana-program)
  * [Build your Rust program](/developers/guides/getstarted/local-rust-hello-world#build-your-rust-program)
  * [Deploy your Solana program](/developers/guides/getstarted/local-rust-hello-world#deploy-your-solana-program)
  * [Next steps](/developers/guides/getstarted/local-rust-hello-world#next-steps)

[Scroll to Top](/developers/guides/getstarted/local-rust-hello-world#)

[Edit Page](https://github.com/solana-foundation/developer-
content/tree/main/content/guides/getstarted/local-rust-hello-world.md)

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

