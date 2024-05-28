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

# [Build an Energy System for Casual Games on
Solana](/developers/guides/games/energy-system)

updated April 25, 2024

[intermediate](/developers/guides?difficulty=intermediate)[games](/developers/guides?tags=games)[anchor](/developers/guides?tags=anchor)[program](/developers/guides?tags=program)[react](/developers/guides?tags=react)[web3js](/developers/guides?tags=web3js)[unity](/developers/guides?tags=unity)[rust](/developers/guides?tags=rust)

[![Build an Energy System for Casual Games on
Solana](https://solana.com/_next/image?url=%2Fopengraph%2Fdevelopers%2Fguides%2Fgames%2Fenergy-
system&w=3840&q=75)](/developers/guides/games/energy-system)

Casual games commonly use energy systems, meaning that actions in the game
cost energy which refills over time. In this guide we will walk through how to
build one on Solana. If you don't have any prior Solana knowledge, start with
the [Hello World Example](/developers/guides/games/hello-world) instead.

You can easily set up a new game with an energy system and a React client
using [Create Solana Game](https://github.com/solana-developers/solana-game-
preset). Just run the command:

    
    
    npx create-solana-game your-game-name

Info

You can find a tutorial on [how to use `create-solana-
game`](https://youtu.be/fnhivg_pemI?si=6xIubFFYPOGiEjKY). and also a [video
walkthrough](https://youtu.be/YYQtRCXJBgs?si=fIZRFkIYJ9wYjEcI) of the example
being explained in this guide below.

## Anchor program #

For starters, we will guide you through creating an Anchor program that
gradually replenishes the player's energy reserves over time. The energy will
enable them to execute various actions within the game. In our example, a
lumberjack will chop trees with every tree rewarding one wood and costing one
energy point.

### Creating the player account #

First the player needs to create an account which saves the state of our
player. We will also save the Unix time stamp of the player's last interaction
with the program in the `last_login` value. With this state, we will be able
to calculate how much energy the player has at a certain point in time. We
also have a value for how much wood the lumberjack cuts in the game.

    
    
    pub fn init_player(ctx: Context<InitPlayer>) -> Result<()> {
        ctx.accounts.player.energy = MAX_ENERGY;
        ctx.accounts.player.last_login = Clock::get()?.unix_timestamp;
        Ok(())
    }
     
    ...
     
    #[derive(Accounts)]
    pub struct InitPlayer <'info> {
        #[account(
            init,
            payer = signer,
            space = 1000,
            seeds = [b"player".as_ref(), signer.key().as_ref()],
            bump,
        )]
        pub player: Account<'info, PlayerData>,
        #[account(mut)]
        pub signer: Signer<'info>,
        pub system_program: Program<'info, System>,
    }
     
    #[account]
    pub struct PlayerData {
        pub name: String,
        pub level: u8,
        pub xp: u64,
        pub wood: u64,
        pub energy: u64,
        pub last_login: i64
    }

### Chopping trees #

Then whenever the player calls the `chop_tree` instruction we will check if
the player has enough energy and reward them with one wood (by incrementing
the player's wood count).

    
    
    #[error_code]
    pub enum ErrorCode {
        #[msg("Not enough energy")]
        NotEnoughEnergy,
    }
     
    pub fn chop_tree(mut ctx: Context<ChopTree>) -> Result<()> {
        let account = &mut ctx.accounts;
        update_energy(account)?;
     
        if ctx.accounts.player.energy == 0 {
            return err!(ErrorCode::NotEnoughEnergy);
        }
     
        ctx.accounts.player.wood = ctx.accounts.player.wood + 1;
        ctx.accounts.player.energy = ctx.accounts.player.energy - 1;
        msg!("You chopped a tree and got 1 wood. You have {} wood and {} energy left.", ctx.accounts.player.wood, ctx.accounts.player.energy);
        Ok(())
    }

### Calculating the energy #

The interesting part happens in the `update_energy` function. We check how
much time has passed and calculate the energy that the player will have at the
given time. We will do the same in the client. We lazily update the energy
instead of polling it all the time. This is a common technique in game
development.

    
    
    const TIME_TO_REFILL_ENERGY: i64 = 60;
    const MAX_ENERGY: u64 = 10;
     
    pub fn update_energy(ctx: &mut ChopTree) -> Result<()> {
        let mut time_passed: i64 = &Clock::get()?.unix_timestamp - &ctx.player.last_login;
        let mut time_spent: i64 = 0;
        while time_passed > TIME_TO_REFILL_ENERGY {
            ctx.player.energy = ctx.player.energy + 1;
            time_passed -= TIME_TO_REFILL_ENERGY;
            time_spent += TIME_TO_REFILL_ENERGY;
            if ctx.player.energy == MAX_ENERGY {
                break;
            }
        }
     
        if ctx.player.energy >= MAX_ENERGY {
            ctx.player.last_login = Clock::get()?.unix_timestamp;
        } else {
            ctx.player.last_login += time_spent;
        }
     
        Ok(())
    }

## JavaScript client #

Here is a [complete example](https://github.com/solana-developers/solana-game-
starter-kits/tree/main/lumberjack) using `create-solana-game`, with a React
client.

### Create connection #

In the Anchor.ts file we create a connection to the Solana blockchain (in this
case, devnet):

    
    
    export const connection = new Connection(
      "https://api.devnet.solana.com",
      "confirmed",
    );

Notice that the confirmation parameter is set to `confirmed`. This means that
we wait until the transactions are `confirmed` instead of `finalized`. This
means that we wait until the super majority of the network said that the
transaction is valid. This takes around 400ms and there was never a confirmed
transaction which did not get finalized. Generally for games, `confirmed` is
the perfect transaction commitment level.

### Initialize player data #

First, we will find the program address for the player account using the seed
string `player` and the player's public key ([deriving the
PDA](/docs/core/pda)). Then we call `initPlayer` to create the account.

    
    
    const [pda] = PublicKey.findProgramAddressSync(
      [Buffer.from("player", "utf8"), publicKey.toBuffer()],
      new PublicKey(LUMBERJACK_PROGRAM_ID),
    );
     
    const transaction = program.methods
      .initPlayer()
      .accounts({
        player: pda,
        signer: publicKey,
        systemProgram: SystemProgram.programId,
      })
      .transaction();
     
    const tx = await transaction;
    const txSig = await sendTransaction(tx, connection, {
      skipPreflight: true,
    });
     
    await connection.confirmTransaction(txSig, "confirmed");

### Subscribe to account updates #

Next we will use websockets within the JavaScript client to subscribe and
listen for changes on the player's account. We use websockets here (over
manually polling the RPC) because it is a faster way to get the changes.

`connection.onAccountChange` creates a socket connection to the RPC node which
will push any changes that happen to the account to the client. We can then
use the `program.coder` to decode the account data into the TypeScript types
and directly use it in the game.

    
    
    useEffect(() => {
      if (!publicKey) {
        return;
      }
      const [pda] = PublicKey.findProgramAddressSync(
        [Buffer.from("player", "utf8"), publicKey.toBuffer()],
        new PublicKey(LUMBERJACK_PROGRAM_ID),
      );
      try {
        program.account.playerData.fetch(pda).then(data => {
          setGameState(data);
        });
      } catch (e) {
        window.alert("No player data found, please init!");
      }
     
      connection.onAccountChange(pda, account => {
        setGameState(program.coder.accounts.decode("playerData", account.data));
      });
    }, [publicKey]);

### Calculate energy and show count down #

In the JavaScript client, we can now perform the same logic as in the program
to precalculate how much energy the player would have at this point in time
and show a countdown timer for the player so that he knows when the next
energy will be available:

    
    
    useEffect(() => {
        const interval = setInterval(async () => {
            if (gameState == null || gameState.lastLogin == undefined || gameState.energy >= 10) {return;}
            const lastLoginTime = gameState.lastLogin * 1000;
            let timePassed = ((Date.now() - lastLoginTime) / 1000);
            while (timePassed > TIME_TO_REFILL_ENERGY && gameState.energy < MAX_ENERGY) {
                gameState.energy = (parseInt(gameState.energy) + 1);
                gameState.lastLogin = parseInt(gameState.lastLogin) + TIME_TO_REFILL_ENERGY;
                timePassed -= TIME_TO_REFILL_ENERGY;
            }
            setTimePassed(timePassed);
            let nextEnergyIn = Math.floor(TIME_TO_REFILL_ENERGY - timePassed);
            if (nextEnergyIn < TIME_TO_REFILL_ENERGY && nextEnergyIn > 0) {
                setEnergyNextIn(nextEnergyIn);
            } else {
                setEnergyNextIn(0);
            }
     
        }, 1000);
     
        return () => clearInterval(interval);
    }, [gameState, timePassed]);
     
    ...
     
    {(gameState && <div className="flex flex-col items-center">
        {("Wood: " + gameState.wood + " Energy: " + gameState.energy + " Next energy in: " + nextEnergyIn )}
    </div>)}
     

With this you can now build any energy based game and even if someone builds a
bot for the game the most they can do is play optimally, which may be even
easier to achieve when playing normally depending on the logic of your game.

This game becomes even better when you add the ability to [use tokens in
games](/developers/guides/games/interact-with-tokens). For example, rewarding
players with some SPL tokens for their actions in game..

[Previous« How to create a CRUD dApp on
Solana](/developers/guides/dapps/journal)[NextSolana Game Development Examples
»](/developers/guides/games/game-examples)

##### Table of Contents

  * [Anchor program](/developers/guides/games/energy-system#anchor-program)
  * [Creating the player account](/developers/guides/games/energy-system#creating-the-player-account)
  * [Chopping trees](/developers/guides/games/energy-system#chopping-trees)
  * [Calculating the energy](/developers/guides/games/energy-system#calculating-the-energy)
  * [JavaScript client](/developers/guides/games/energy-system#javascript-client)
  * [Create connection](/developers/guides/games/energy-system#create-connection)
  * [Initialize player data](/developers/guides/games/energy-system#initialize-player-data)
  * [Subscribe to account updates](/developers/guides/games/energy-system#subscribe-to-account-updates)
  * [Calculate energy and show count down](/developers/guides/games/energy-system#calculate-energy-and-show-count-down)

[Scroll to Top](/developers/guides/games/energy-system#)

[Edit Page](https://github.com/solana-foundation/developer-
content/tree/main/content/guides/games/energy-system.md)

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

