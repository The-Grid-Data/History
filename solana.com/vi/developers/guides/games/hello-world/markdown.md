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

[Home](/vi)>[Developers](/vi/developers)>[Guides](/vi/developers/guides)

# [Hello World for Solana Game Development](/vi/developers/guides/games/hello-
world)

updated 25 tháng 4, 2024

[beginner](/vi/developers/guides?difficulty=beginner)[games](/vi/developers/guides?tags=games)[anchor](/vi/developers/guides?tags=anchor)[program](/vi/developers/guides?tags=program)[web3js](/vi/developers/guides?tags=web3js)[quickstart](/vi/developers/guides?tags=quickstart)[rust](/vi/developers/guides?tags=rust)

[![Hello World for Solana Game
Development](https://solana.com/_next/image?url=%2Fopengraph%2Fdevelopers%2Fguides%2Fgames%2Fhello-
world&w=3840&q=75)](/vi/developers/guides/games/hello-world)

In this development guide, we will walkthrough a simple on-chain game using
the Solana blockchain. This game, lovingly called _Tiny Adventure_ , is a
beginner-friendly Solana program created using the [Anchor
framework](/vi/developers/guides/getstarted/intro-to-anchor). The goal of this
program is to show you how to create a simple game that allows players to
track their position and move left or right.

Info

You can find the complete source code, available to deploy from your browser,
in this [Solana Playground example](https://beta.solpg.io/tutorials/tiny-
adventure).

If need to familiarize yourself with the Anchor framework, feel free to check
out the Anchor module of the [Solana Course](https://www.soldev.app/course) to
get started.

## Video Walkthrough #

## Getting Started #

To help make our initial Solana development faster, we will use the Solana
Playground (web based IDE) to code, build, and deploy our on-chain program.
This will make it so we do not have to setup or install anything locally to
get started with Solana development.

### Solana Playground #

Visit the [Solana Playground](https://beta.solpg.io/) and create a new Anchor
project. If you're new to Solana Playground, you'll also need to create a
Playground Wallet. Here is an example of how to use Solana Playground:

![Setting up the Solana Playground](https://solana-developer-
content.vercel.app/assets/guides/hello-world/solpg.gif)Setting up the Solana
Playground

### Initial Program Code #

After creating a new Playground project, replace the default starter code in
`lib.rs` with the code below:

lib.rs

    
    
    use anchor_lang::prelude::*;
     
    declare_id!("11111111111111111111111111111111");
     
    #[program]
    mod tiny_adventure {
        use super::*;
     
        // instruction handlers will go here
    }
     
    // structs will go here
     
    fn print_player(player_position: u8) {
        if player_position == 0 {
            msg!("A Journey Begins!");
            msg!("o.......");
        } else if player_position == 1 {
            msg!("..o.....");
        } else if player_position == 2 {
            msg!("....o...");
        } else if player_position == 3 {
            msg!("........\\o/");
            msg!("You have reached the end! Super!");
        }
    }

In this game, the player starts at position 0 and can move left or right. To
show the player's progress throughout the game, we'll use message logs to
display their journey.

## Defining the Game Data Account #

The first step in building the game is to define a structure for the on-chain
account that will store the player's position.

The `GameDataAccount` struct contains a single field, `player_position`, which
stores the player's current position as an unsigned 8-bit integer.

lib.rs

    
    
    use anchor_lang::prelude::*;
     
    declare_id!("11111111111111111111111111111111");
     
    #[program]
    mod tiny_adventure {
        use super::*;
     
        ...
    }
     
    // Define the Game Data Account structure
    #[account]
    pub struct GameDataAccount {
        player_position: u8,
    }
     
    ...

## Program Instructions #

Our Tiny Adventure program consists of only 3 [instruction
handlers](/vi/docs/core/transactions#instruction):

  * `initialize` \- sets up an on-chain account to store the player's position
  * `move_left` \- lets the player move their position to the left
  * `move_right` \- lets the player move their position to the right

### Initialize Instruction #

Our `initialize` instruction initializes the `GameDataAccount` if it does not
already exist, sets the `player_position` to 0, and print some message logs.

The `initialize` instruction requires 3 accounts:

  * `new_game_data_account` \- the `GameDataAccount` we are initializing
  * `signer` \- the player paying for the initialization of the `GameDataAccount`
  * `system_program` \- a required account when creating a new account

lib.rs

    
    
    #[program]
    pub mod tiny_adventure {
        use super::*;
     
        // Instruction to initialize GameDataAccount and set position to 0
        pub fn initialize(ctx: Context<Initialize>) -> Result<()> {
            ctx.accounts.new_game_data_account.player_position = 0;
            msg!("A Journey Begins!");
            msg!("o.......");
            Ok(())
        }
    }
     
    // Specify the accounts required by the initialize instruction
    #[derive(Accounts)]
    pub struct Initialize<'info> {
        #[account(
            init_if_needed,
            seeds = [b"level1"],
            bump,
            payer = signer,
            space = 8 + 1
        )]
        pub new_game_data_account: Account<'info, GameDataAccount>,
        #[account(mut)]
        pub signer: Signer<'info>,
        pub system_program: Program<'info, System>,
    }
     
    ...

In this example, a [Program Derived Address (PDA)](/vi/docs/core/pda) is used
for the `GameDataAccount` address. This enables us to deterministically locate
the address later on. It is important to note that the PDA in this example is
generated with a single fixed value as the seed (`level1`), limiting our
program to creating only one `GameDataAccount`. The `init_if_needed`
constraint then ensures that the `GameDataAccount` is initialized only if it
doesn't already exist.

It is worth noting that the current implementation does not have any
restrictions on who can modify the `GameDataAccount`. This effectively
transforms the game into a multiplayer experience where everyone can control
the player's movement.

Alternatively, you can use the signer's address as an extra seed in the
`initialize` instruction, which would enable each player to create their own
`GameDataAccount`.

### Move Left Instruction #

Now that we can initialize a `GameDataAccount` account, let’s implement the
`move_left` instruction which allows a player update their `player_position`.

In this example, moving left simply means decrementing the `player_position`
by 1. We'll also set the minimum position to 0. The only account needed for
this instruction is the `GameDataAccount`.

lib.rs

    
    
    #[program]
    pub mod tiny_adventure {
        use super::*;
        ...
     
        // Instruction to move left
        pub fn move_left(ctx: Context<MoveLeft>) -> Result<()> {
            let game_data_account = &mut ctx.accounts.game_data_account;
            if game_data_account.player_position == 0 {
                msg!("You are back at the start.");
            } else {
                game_data_account.player_position -= 1;
                print_player(game_data_account.player_position);
            }
            Ok(())
        }
    }
     
    // Specify the account required by the move_left instruction
    #[derive(Accounts)]
    pub struct MoveLeft<'info> {
        #[account(mut)]
        pub game_data_account: Account<'info, GameDataAccount>,
    }
     
    ...

### Move Right Instruction #

Lastly, let’s implement the `move_right` instruction. Similarly, moving right
will simply mean incrementing the `player_position` by 1. We’ll also limit the
maximum position to 3.

Just like before, the only account needed for this instruction is the
`GameDataAccount`.

lib.rs

    
    
    #[program]
    pub mod tiny_adventure {
        use super::*;
    		...
     
    		// Instruction to move right
    		pub fn move_right(ctx: Context<MoveRight>) -> Result<()> {
    		    let game_data_account = &mut ctx.accounts.game_data_account;
    		    if game_data_account.player_position == 3 {
    		        msg!("You have reached the end! Super!");
    		    } else {
    		        game_data_account.player_position = game_data_account.player_position + 1;
    		        print_player(game_data_account.player_position);
    		    }
    		    Ok(())
    		}
    }
     
    // Specify the account required by the move_right instruction
    #[derive(Accounts)]
    pub struct MoveRight<'info> {
        #[account(mut)]
        pub game_data_account: Account<'info, GameDataAccount>,
    }
     
    ...

## Build and Deploy #

We've now completed the Tiny Adventure program! Your final program should
resemble the following:

lib.rs

    
    
    use anchor_lang::prelude::*;
     
    // This is your program's public key and it will update
    // automatically when you build the project.
    declare_id!("BouPBVWkdVHbxsdzqeMwkjqd5X67RX5nwMEwxn8MDpor");
     
    #[program]
    mod tiny_adventure {
        use super::*;
     
        pub fn initialize(ctx: Context<Initialize>) -> Result<()> {
            ctx.accounts.new_game_data_account.player_position = 0;
            msg!("A Journey Begins!");
            msg!("o.......");
            Ok(())
        }
     
        pub fn move_left(ctx: Context<MoveLeft>) -> Result<()> {
            let game_data_account = &mut ctx.accounts.game_data_account;
            if game_data_account.player_position == 0 {
                msg!("You are back at the start.");
            } else {
                game_data_account.player_position -= 1;
                print_player(game_data_account.player_position);
            }
            Ok(())
        }
     
        pub fn move_right(ctx: Context<MoveRight>) -> Result<()> {
            let game_data_account = &mut ctx.accounts.game_data_account;
            if game_data_account.player_position == 3 {
                msg!("You have reached the end! Super!");
            } else {
                game_data_account.player_position = game_data_account.player_position + 1;
                print_player(game_data_account.player_position);
            }
            Ok(())
        }
    }
     
    fn print_player(player_position: u8) {
        if player_position == 0 {
            msg!("A Journey Begins!");
            msg!("o.......");
        } else if player_position == 1 {
            msg!("..o.....");
        } else if player_position == 2 {
            msg!("....o...");
        } else if player_position == 3 {
            msg!("........\\o/");
            msg!("You have reached the end! Super!");
        }
    }
     
    #[derive(Accounts)]
    pub struct Initialize<'info> {
        #[account(
            init_if_needed,
            seeds = [b"level1"],
            bump,
            payer = signer,
            space = 8 + 1
        )]
        pub new_game_data_account: Account<'info, GameDataAccount>,
        #[account(mut)]
        pub signer: Signer<'info>,
        pub system_program: Program<'info, System>,
    }
     
    #[derive(Accounts)]
    pub struct MoveLeft<'info> {
        #[account(mut)]
        pub game_data_account: Account<'info, GameDataAccount>,
    }
     
    #[derive(Accounts)]
    pub struct MoveRight<'info> {
        #[account(mut)]
        pub game_data_account: Account<'info, GameDataAccount>,
    }
     
    #[account]
    pub struct GameDataAccount {
        player_position: u8,
    }

With the program completed, it's time to build and deploy it on Solana
Playground!

If this is your first time using Solana Playground, create a Playground Wallet
first and ensure that you're connected to a Devnet endpoint. Then, run `solana
airdrop 5`. Once you have enough SOL, build and deploy the program. If the
command fails you there are other ways on [how to get devnet
SOL](/vi/developers/guides/getstarted/solana-token-airdrop-and-faucets) here.

## Get Started with the Client #

This next section will guide you through a simple client-side implementation
for interacting with the game. We'll break down the code and provide detailed
explanations for each step. In Solana Playground, navigate to the `client.ts`
file and add the code snippets from the following sections.

### Derive the GameDataAccount Account Address #

First, let’s derive the PDA for the `GameDataAccount` using the
`findProgramAddress` function.

Info

A [Program Derived Address (PDA)](/vi/docs/core/pda) is unique address in the
format of a public key, derived using the program's ID and additional seeds.

client.ts

    
    
    // The PDA address everyone will be able to control the character if the interact with your program
    const [globalLevel1GameDataAccount, bump] =
      await anchor.web3.PublicKey.findProgramAddress(
        [Buffer.from("level1", "utf8")],
        pg.program.programId,
      );

### Initialize the Game State #

Next, let’s try to fetch the game data account using the PDA from the previous
step. If the account doesn't exist, we'll create it by invoking the
`initialize` instruction from our program.

client.ts

    
    
    let txHash;
    let gameDateAccount;
     
    try {
      gameDateAccount = await pg.program.account.gameDataAccount.fetch(
        globalLevel1GameDataAccount,
      );
    } catch {
      // Check if the account is already initialized, other wise initialize it
      txHash = await pg.program.methods
        .initialize()
        .accounts({
          newGameDataAccount: globalLevel1GameDataAccount,
          signer: pg.wallet.publicKey,
          systemProgram: web3.SystemProgram.programId,
        })
        .signers([pg.wallet.keypair])
        .rpc();
     
      console.log(`Use 'solana confirm -v ${txHash}' to see the logs`);
      await pg.connection.confirmTransaction(txHash);
      console.log("A journey begins...");
      console.log("o........");
    }

### Move Left and Right #

Now we are ready to interact with the game by moving left or right. This is
done by invoking the `moveLeft` or `moveRight` instructions from the program
by submitting a transaction to the Solana network.

You can repeat this step as many times as you like, each will execute the move
logic on-chain, updating the player's state.

client.ts

    
    
    // Here you can play around now, move left and right
    txHash = await pg.program.methods
      //.moveLeft()
      .moveRight()
      .accounts({
        gameDataAccount: globalLevel1GameDataAccount,
      })
      .signers([pg.wallet.keypair])
      .rpc();
    console.log(`Use 'solana confirm -v ${txHash}' to see the logs`);
    await pg.connection.confirmTransaction(txHash);
     
    gameDateAccount = await pg.program.account.gameDataAccount.fetch(
      globalLevel1GameDataAccount,
    );
     
    console.log("Player position is:", gameDateAccount.playerPosition.toString());

### Logging the Player's Position #

Lastly, let’s use a `switch` statement to log the character's position based
on the `playerPosition` value stored in the `gameDateAccount`. We’ll use this
as a visual representation of the character's movement in the game.

client.ts

    
    
    switch (gameDateAccount.playerPosition) {
      case 0:
        console.log("A journey begins...");
        console.log("o........");
        break;
      case 1:
        console.log("....o....");
        break;
      case 2:
        console.log("......o..");
        break;
      case 3:
        console.log(".........\\o/");
        break;
    }

### Run the Client Program #

Finally, run the client by clicking the “Run” button in Solana Playground. The
output should be similar to the following:

    
    
    Running client...
      client.ts:
        My address: 8ujtDmwpkQ4Bp4GU4zUWmzf65sc21utdcxFAELESca22
        My balance: 4.649749614 SOL
        Use 'solana confirm -v 4MRXEWfGqvmro1KsKb94Zz8qTZsPa9x99oMFbLBz2WicLnr8vdYYsQwT5u3pK5Vt1i9BDrVH5qqTXwtif6sCRJCy' to see the logs
        Player position is: 1
        ....o....

Congratulations! You have successfully built, deployed, and invoked the Tiny
Adventure game from the client.

Info

To further illustrate the possibilities, check out this [frontend
demo](https://nextjs-tiny-adventure.vercel.app/) that demonstrates how to
interact with the Tiny Adventure program through a Next.js frontend. You can
also view this Next.js project's [source code](https://github.com/solana-
developers/solana-game-examples/tree/main/tiny-adventure) here.

## What's Next? #

With the basic game complete, unleash your creativity and practice building
independently by implementing your own ideas to enrich the game experience.
Here are a few suggestions:

  1. Modify the in-game texts to create an intriguing story. Invite a friend to play through your custom narrative and observe the on-chain transactions as they unfold!
  2. Add a chest that rewards players with [SOL Rewards](/vi/developers/guides/games/store-sol-in-pda) or let the player collect coins and [interact with tokens](/vi/developers/guides/games/interact-with-tokens) as they progress through the game.
  3. Create a grid that allows the player to move up, down, left, and right, and introduce multiple players for a more dynamic experience.

### Part Two #

You can continue the guided development of our Tiny Adventure game, with this
guide [Tiny Adventure - Part Two](/vi/developers/guides/games/store-sol-in-
pda), where we will demonstrate how to store SOL in the program and distribute
it to players as rewards.

### More Resources #

You can also discover more Solana game development resources here:

  * [Getting Started Guide](/vi/developers/guides/games/getting-started-with-game-development)
  * [Solana Gaming SDKs](/vi/developers/guides/games/game-sdks)
  * [Learn by example](/vi/developers/guides/games/game-examples)
  * [Energy System](/vi/developers/guides/games/energy-system)
  * [NFTs in games](/vi/developers/guides/games/nfts-in-games)
  * [Token in games](/vi/developers/guides/games/interact-with-tokens)

[Previous« Getting started with game development on
Solana](/vi/developers/guides/games/getting-started-with-game-
development)[NextHow interact with tokens in programs
»](/vi/developers/guides/games/interact-with-tokens)

##### Table of Contents

  * [Video Walkthrough](/vi/developers/guides/games/hello-world#video-walkthrough)
  * [Getting Started](/vi/developers/guides/games/hello-world#getting-started)
  * [Solana Playground](/vi/developers/guides/games/hello-world#solana-playground)
  * [Initial Program Code](/vi/developers/guides/games/hello-world#initial-program-code)
  * [Defining the Game Data Account](/vi/developers/guides/games/hello-world#defining-the-game-data-account)
  * [Program Instructions](/vi/developers/guides/games/hello-world#program-instructions)
  * [Initialize Instruction](/vi/developers/guides/games/hello-world#initialize-instruction)
  * [Move Left Instruction](/vi/developers/guides/games/hello-world#move-left-instruction)
  * [Move Right Instruction](/vi/developers/guides/games/hello-world#move-right-instruction)
  * [Build and Deploy](/vi/developers/guides/games/hello-world#build-and-deploy)
  * [Get Started with the Client](/vi/developers/guides/games/hello-world#get-started-with-the-client)
  * [Derive the GameDataAccount Account Address](/vi/developers/guides/games/hello-world#derive-the-gamedataaccount-account-address)
  * [Initialize the Game State](/vi/developers/guides/games/hello-world#initialize-the-game-state)
  * [Move Left and Right](/vi/developers/guides/games/hello-world#move-left-and-right)
  * [Logging the Player's Position](/vi/developers/guides/games/hello-world#logging-the-player-s-position)
  * [Run the Client Program](/vi/developers/guides/games/hello-world#run-the-client-program)
  * [What's Next](/vi/developers/guides/games/hello-world#what-s-next)
  * [Part Two](/vi/developers/guides/games/hello-world#part-two)
  * [More Resources](/vi/developers/guides/games/hello-world#more-resources)

[Scroll to Top](/vi/developers/guides/games/hello-world#)

[Edit Page](https://github.com/solana-foundation/developer-
content/tree/main/content/guides/games/hello-world.md)

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

Sol Play

449 subscribers

[Let's build a Solana Game! - Part 1 - Anchor +
Playground](https://www.youtube.com/watch?v=_vQ3bSs3svs)

[]()

Sol Play

Search

Info

Shopping

Tap to unmute

If playback doesn't begin shortly, try restarting your device.

Share

Include playlist

An error occurred while retrieving sharing information. Please try again
later.

Watch later

Share

Copy link

Watch on

0:00

0:00 / 34:19•Live

•

[](https://www.youtube.com/watch?v=_vQ3bSs3svs "Watch on YouTube")

# An error occurred.

[Try watching this video on
www.youtube.com](https://www.youtube.com/watch?v=_vQ3bSs3svs), or enable
JavaScript if it is disabled in your browser.

