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

# [How to CPI with a PDA Signer in a Solana
program](/developers/guides/getstarted/how-to-cpi-with-signer)

updated April 24, 2024

[beginner](/developers/guides?difficulty=beginner)[rust](/developers/guides?tags=rust)[anchor](/developers/guides?tags=anchor)[cpi](/developers/guides?tags=cpi)[pda](/developers/guides?tags=pda)

[![How to CPI with a PDA Signer in a Solana
program](https://solana.com/_next/image?url=%2Fopengraph%2Fdevelopers%2Fguides%2Fgetstarted%2Fhow-
to-cpi-with-signer&w=3840&q=75)](/developers/guides/getstarted/how-to-cpi-
with-signer)

This guide uses the [Anchor framework](/developers/guides/getstarted/intro-to-
anchor) to demonstrate how to transfer SOL using a [Cross-Program Invocation
(CPI)](/docs/core/cpi) where the sender is a PDA that the program must sign
for.

A typical use case for this scenario is a program that manages [token
accounts](/docs/core/tokens#token-account) on behalf of users. For instance,
consider a scenario where a DeFi protocol pools user funds into a single
account. The protocol needs to include security checks to automatically handle
withdrawal requests. In such cases, the control over these pooled funds is not
with a single user but rather with the program itself. This requires the [use
of PDAs](/docs/core/pda) as the owner of the protocol's token accounts to
programmatically sign for withdrawals.

Included below are two different, but functionally equivalent implementations
that you may come across when reading or writing Solana programs. Here is the
final reference program on [Solana
Playground](https://beta.solpg.io/github.com/ZYJLiu/doc-
examples/tree/main/cpi-pda).

## Starter Code #

Here is a starter program on [Solana
Playground](https://beta.solpg.io/github.com/ZYJLiu/doc-
examples/tree/main/cpi-sol-transfer-pda-signer). The `lib.rs` file includes
the following program with a single `sol_transfer` instruction.

lib.rs

    
    
    use anchor_lang::prelude::*;
    use anchor_lang::system_program::{transfer, Transfer};
     
    declare_id!("3455LkCS85a4aYmSeNbRrJsduNQfYRY82A7eCD3yQfyR");
     
    #[program]
    pub mod cpi {
        use super::*;
     
        pub fn sol_transfer(ctx: Context<SolTransfer>, amount: u64) -> Result<()> {
            let from_pubkey = ctx.accounts.pda_account.to_account_info();
            let to_pubkey = ctx.accounts.recipient.to_account_info();
            let program_id = ctx.accounts.system_program.to_account_info();
     
            let seed = to_pubkey.key();
            let bump_seed = ctx.bumps.pda_account;
            let signer_seeds: &[&[&[u8]]] = &[&[b"pda", seed.as_ref(), &[bump_seed]]];
     
            let cpi_context = CpiContext::new(
                program_id,
                Transfer {
                    from: from_pubkey,
                    to: to_pubkey,
                },
            )
            .with_signer(signer_seeds);
     
            transfer(cpi_context, amount)?;
            Ok(())
        }
    }
     
    #[derive(Accounts)]
    pub struct SolTransfer<'info> {
        #[account(
            mut,
            seeds = [b"pda", recipient.key().as_ref()],
            bump,
        )]
        pda_account: SystemAccount<'info>,
        #[account(mut)]
        recipient: SystemAccount<'info>,
        system_program: Program<'info, System>,
    }

The `cpi.test.ts` file demonstrates how to invoke the custom `sol_transfer`
instruction and logs a link to the transaction details on SolanaFM.

It shows how to derive the PDA using the seeds specified in the program:

    
    
    const [PDA] = PublicKey.findProgramAddressSync(
      [Buffer.from("pda"), wallet.publicKey.toBuffer()],
      program.programId,
    );

The first step in this example is to fund the PDA account with a basic SOL
transfer from the Playground wallet.

cpi.test.ts

    
    
    it("Fund PDA with SOL", async () => {
      const transferInstruction = SystemProgram.transfer({
        fromPubkey: wallet.publicKey,
        toPubkey: PDA,
        lamports: transferAmount,
      });
     
      const transaction = new Transaction().add(transferInstruction);
     
      const transactionSignature = await sendAndConfirmTransaction(
        connection,
        transaction,
        [wallet.payer], // signer
      );
     
      console.log(
        `\nTransaction Signature:` +
          `https://solana.fm/tx/${transactionSignature}?cluster=devnet-solana`,
      );
    });

Once the PDA is funded with SOL, invoke the `sol_transfer` instruction. This
instruction transfers SOL from the PDA back to the `wallet` account via a CPI
to the System Program, which is "signed" for by the custom program.

    
    
    it("SOL Transfer with PDA signer", async () => {
      const transactionSignature = await program.methods
        .solTransfer(new BN(transferAmount))
        .accounts({
          pdaAccount: PDA,
          recipient: wallet.publicKey,
        })
        .rpc();
     
      console.log(
        `\nTransaction Signature: https://solana.fm/tx/${transactionSignature}?cluster=devnet-solana`,
      );
    });

The transaction details will show that the custom program was first invoked
(instruction 1), which then invokes the System Program (instruction 1.1),
resulting in a successful SOL transfer.

![Transaction Details](https://solana-developer-
content.vercel.app/assets/docs/core/cpi/transaction-details-
pda.png)Transaction Details

You can build, deploy, and run the test to view the transaction details on the
[SolanaFM explorer](https://solana.fm/).

## How to CPI with signers using Anchor #

In the starter code, the `SolTransfer` struct specifies the accounts required
by the transfer instruction.

    
    
    #[derive(Accounts)]
    pub struct SolTransfer<'info> {
        #[account(
            mut,
            seeds = [b"pda", recipient.key().as_ref()],
            bump,
        )]
        pda_account: SystemAccount<'info>,
        #[account(mut)]
        recipient: SystemAccount<'info>,
        system_program: Program<'info, System>,
    }

The `seeds` to derive the address for the `pda_account` include the hardcoded
string "pda" and the address of the `recipient` account. This means the
address for the `pda_account` is unique for each `recipient`.

The Javascript equivalent to derive the PDA is included in the test file.

    
    
    const [PDA] = PublicKey.findProgramAddressSync(
      [Buffer.from("pda"), wallet.publicKey.toBuffer()],
      program.programId,
    );

### Anchor CpiContext #

The `sol_transfer` instruction included in the starter code shows a typical
approach for constructing CPIs using the Anchor framework.

This approach involves creating a [`CpiContext`](https://docs.rs/anchor-
lang/latest/anchor_lang/context/struct.CpiContext.html), which includes the
`program_id` and accounts required for the instruction being called, followed
by a helper function (`transfer`) to invoke a specific instruction.

    
    
    pub fn sol_transfer(ctx: Context<SolTransfer>, amount: u64) -> Result<()> {
        let from_pubkey = ctx.accounts.pda_account.to_account_info();
        let to_pubkey = ctx.accounts.recipient.to_account_info();
        let program_id = ctx.accounts.system_program.to_account_info();
     
        let seed = to_pubkey.key();
        let bump_seed = ctx.bumps.pda_account;
        let signer_seeds: &[&[&[u8]]] = &[&[b"pda", seed.as_ref(), &[bump_seed]]];
     
        let cpi_context = CpiContext::new(
            program_id,
            Transfer {
                from: from_pubkey,
                to: to_pubkey,
            },
        )
        .with_signer(signer_seeds);
     
        transfer(cpi_context, amount)?;
        Ok(())
    }

When signing with PDAs, the optional seeds and bump seed are included in the
`cpi_context` as `signer_seeds` using `with_signer()`.

    
    
    let seed = to_pubkey.key();
    let bump_seed = ctx.bumps.pda_account;
    let signer_seeds: &[&[&[u8]]] = &[&[b"pda", seed.as_ref(), &[bump_seed]]];
     
    let cpi_context = CpiContext::new(
        program_id,
        Transfer {
            from: from_pubkey,
            to: to_pubkey,
        },
    )
    .with_signer(signer_seeds);

The `cpi_context` and `amount` are then passed into the `transfer` function to
execute the CPI.

    
    
    transfer(cpi_context, amount)?;

When the CPI is processed, the Solana runtime will validate that the provided
seeds and caller program ID derive a valid PDA. The PDA is then added as a
signer on the invocation. This mechanism allows for programs to
programmatically sign for PDAs that are derived from their program ID.

### Invoke with Crate Helper #

Under the hood, the example above is a wrapper around the `invoke_signed()`
function which uses
[`system_instruction::transfer`](https://github.com/solana-
labs/solana/blob/27eff8408b7223bb3c4ab70523f8a8dca3ca6645/sdk/program/src/system_instruction.rs#L881)
to build the instruction.

The example below demonstrates how to use the `invoke_signed()` function to
make a CPI to the transfer instruction of the System Program using the
`system_instruction::transfer` method and signed for by a PDA.

First, add these imports to the top of `lib.rs`:

    
    
    use anchor_lang::solana_program::{program::invoke_signed, system_instruction};

Next, modify the `sol_transfer` instruction with the following:

    
    
    pub fn sol_transfer(ctx: Context<SolTransfer>, amount: u64) -> Result<()> {
        let from_pubkey = ctx.accounts.pda_account.to_account_info();
        let to_pubkey = ctx.accounts.recipient.to_account_info();
        let program_id = ctx.accounts.system_program.to_account_info();
     
        let seed = to_pubkey.key();
        let bump_seed = ctx.bumps.pda_account;
        let signer_seeds: &[&[&[u8]]] = &[&[b"pda", seed.as_ref(), &[bump_seed]]];
     
        let instruction =
            &system_instruction::transfer(&from_pubkey.key(), &to_pubkey.key(), amount);
     
        invoke_signed(instruction, &[from_pubkey, to_pubkey, program_id], signer_seeds)?;
        Ok(())
    }

This implementation is functionally equivalent to the previous example. The
`signer_seeds` are passed into the `invoke_signed` function.

[Previous« Intro to Solana development (using only your
browser)](/developers/guides/getstarted/hello-world-in-your-browser)[NextHow
to CPI in a Solana program »](/developers/guides/getstarted/how-to-cpi)

##### Table of Contents

  * [Starter Code](/developers/guides/getstarted/how-to-cpi-with-signer#starter-code)
  * [How to CPI with signers using Anchor](/developers/guides/getstarted/how-to-cpi-with-signer#how-to-cpi-with-signers-using-anchor)
  * [Anchor CpiContext](/developers/guides/getstarted/how-to-cpi-with-signer#anchor-cpicontext)
  * [Invoke with Crate Helper](/developers/guides/getstarted/how-to-cpi-with-signer#invoke-with-crate-helper)

[Scroll to Top](/developers/guides/getstarted/how-to-cpi-with-signer#)

[Edit Page](https://github.com/solana-foundation/developer-
content/tree/main/content/guides/getstarted/how-to-cpi-with-signer.md)

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

