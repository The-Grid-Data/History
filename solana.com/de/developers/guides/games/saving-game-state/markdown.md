This website uses cookies to offer you a better browsing experience. Find out
more on how we use cookies.

Opt-out[Details](/de/privacy-policy#collection-of-information)

Accept

[![Solana](/_next/static/media/logotype-dark.f79d530d.svg)](/de)

  * Learn
  * Developers
  * Solutions
  * Network
  * Community

Search```K`

[Documentation](/de/docs)[RPC
API](/de/docs/rpc)[Cookbook](/de/developers/cookbook)[Guides](/de/developers/guides)[Terminology](/de/docs/terminology)

[Home](/de)>[Developers](/de/developers)>[Guides](/de/developers/guides)

# [Saving game state](/de/developers/guides/games/saving-game-state)

updated 25\. April 2024

[beginner](/de/developers/guides?difficulty=beginner)[games](/de/developers/guides?tags=games)[anchor](/de/developers/guides?tags=anchor)[program](/de/developers/guides?tags=program)[solana
playground](/de/developers/guides?tags=solana%20playground)[web3js](/de/developers/guides?tags=web3js)[native](/de/developers/guides?tags=native)[rust](/de/developers/guides?tags=rust)

[![Saving game
state](https://solana.com/_next/image?url=%2Fopengraph%2Fdevelopers%2Fguides%2Fgames%2Fsaving-
game-state&w=3840&q=75)](/de/developers/guides/games/saving-game-state)

You can use Solana blockchain to save the state of your game in program
accounts. These are accounts that are owned by your program and they are
derived from the program ID and some seeds. These can be thought of as
database entries. We can for example create a PlayerData account and use the
players public key as a seed. This means every player can have one player
account per wallet. These accounts can be up to 10Kb by default. If you need a
bigger account look into [how to handle big
accounts](https://github.com/solana-developers/anchor-zero-copy-example) This
can be done in a program like this:

    
    
    pub fn init_player(ctx: Context<InitPlayer>) -> Result<()> {
        ctx.accounts.player.energy = MAX_ENERGY;
        ctx.accounts.player.health = MAX_HEALTH;
        ctx.accounts.player.last_login = Clock::get()?.unix_timestamp;
        Ok(())
    }
     
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
        pub health: u64,
        pub log: u64,
        pub energy: u64,
        pub last_login: i64
    }
     

You can then interact with this player data via transaction instructions. Lets
say we want the player to get experience for killing a monster for example:

    
    
        pub fn kill_enemy(mut ctx: Context<KillEnemy>, enemyId: u8) -> Result<()> {
            let account = &mut ctx.accounts;
     
            ... handle energy
     
            if ctx.accounts.player.energy == 0 {
                return err!(ErrorCode::NotEnoughEnergy);
            }
     
            ... get enemy values by id and calculate battle
     
            ctx.accounts.player.xp = ctx.accounts.player.xp + 1;
            ctx.accounts.player.energy = ctx.accounts.player.energy - 1;
     
            ... handle level up
     
            msg!("You killed enemy and got 1 xp. You have {} xp and {} energy left.", ctx.accounts.player.xp, ctx.accounts.player.energy);
            Ok(())
        }

This is how this would look like from a JavaScript client:

    
    
    const wallet = useAnchorWallet();
    const provider = new AnchorProvider(connection, wallet, {});
    setProvider(provider);
    const program = new Program(IDL, PROGRAM_ID, provider);
     
    const [pda] = PublicKey.findProgramAddressSync(
      [Buffer.from("player", "utf8"),
      publicKey.toBuffer()],
      new PublicKey(PROGRAM_ID)
    );
     
    try {
      const transaction = program.methods
        .initPlayer()
        .accounts({
          player: pda,
          signer: publicKey,
          systemProgram: SystemProgram.programId,
        })
        .transaction();
     
      const tx = await transaction;
      const txSig = await sendTransaction(tx, connection);
      await connection.confirmTransaction(txSig, "confirmed");

How to actually build this energy system you can learn here: [Building an
Energy system](/de/developers/guides/games/energy-system)

[Previous« Port Anchor to Unity](/de/developers/guides/games/porting-anchor-
to-unity)[NextStoring SOL in a PDA »](/de/developers/guides/games/store-sol-
in-pda)

##### Table of Contents

[Scroll to Top](/de/developers/guides/games/saving-game-state#)

[Edit Page](https://github.com/solana-foundation/developer-
content/tree/main/content/guides/games/saving-game-state.md)

Managed by

[](/de)

[](/youtube)[](/twitter)[](/discord)[](/reddit)[](/github)[](/telegram)

© 2024 Solana Foundation. All rights reserved.

Solana

  * [Fördermittel](https://solana.org/grants)
  * [Break Solana](https://break.solana.com/)
  * [Media Kit](/de/branding)
  * [Karriere](https://jobs.solana.com/)
  * [Haftungsausschluss](/de/tos)
  * [Privacy Policy](/de/privacy-policy)

Get Connected

  * [Ökosystem](/de/ecosystem)
  * [Blog](/de/news)
  * [Newsletter](/de/newsletter)

de

© 2024 Solana Foundation. All rights reserved.
