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

# [How to CPI in a Solana program](/vi/developers/guides/getstarted/how-to-
cpi)

updated 24 tháng 4, 2024

[beginner](/vi/developers/guides?difficulty=beginner)[rust](/vi/developers/guides?tags=rust)[anchor](/vi/developers/guides?tags=anchor)[cpi](/vi/developers/guides?tags=cpi)

[![How to CPI in a Solana
program](https://solana.com/_next/image?url=%2Fopengraph%2Fdevelopers%2Fguides%2Fgetstarted%2Fhow-
to-cpi&w=3840&q=75)](/vi/developers/guides/getstarted/how-to-cpi)

This guide uses the [Anchor framework](/vi/developers/guides/getstarted/intro-
to-anchor) to demonstrate how to transfer SOL using a [Cross Program
Invocation (CPI)](/vi/docs/core/cpi). Included below are three different, but
functionally equivalent implementations that you may come across when reading
or writing Solana programs. Here is a final reference program on [Solana
Playground](https://beta.solpg.io/github.com/ZYJLiu/doc-
examples/tree/main/cpi).

## Starter Code #

Here is a starter program on [Solana
Playground](https://beta.solpg.io/github.com/ZYJLiu/doc-
examples/tree/main/cpi-sol-transfer). The `lib.rs` file includes the following
program with a single `sol_transfer` instruction.

lib.rs

    
    
    use anchor_lang::prelude::*;
    use anchor_lang::system_program::{transfer, Transfer};
     
    declare_id!("9AvUNHjxscdkiKQ8tUn12QCMXtcnbR9BVGq3ULNzFMRi");
     
    #[program]
    pub mod cpi {
        use super::*;
     
        pub fn sol_transfer(ctx: Context<SolTransfer>, amount: u64) -> Result<()> {
            let from_pubkey = ctx.accounts.sender.to_account_info();
            let to_pubkey = ctx.accounts.recipient.to_account_info();
            let program_id = ctx.accounts.system_program.to_account_info();
     
            let cpi_context = CpiContext::new(
                program_id,
                Transfer {
                    from: from_pubkey,
                    to: to_pubkey,
                },
            );
     
            transfer(cpi_context, amount)?;
            Ok(())
        }
    }
     
    #[derive(Accounts)]
    pub struct SolTransfer<'info> {
        #[account(mut)]
        sender: Signer<'info>,
        #[account(mut)]
        recipient: SystemAccount<'info>,
        system_program: Program<'info, System>,
    }

The `cpi.test.ts` file demonstrates how to invoke the custom `sol_transfer`
instruction and logs a link to the transaction details on SolanaFM.

cpi.test.ts

    
    
    it("SOL Transfer Anchor", async () => {
      const transactionSignature = await program.methods
        .solTransfer(new BN(transferAmount))
        .accounts({
          sender: sender.publicKey,
          recipient: recipient.publicKey,
        })
        .rpc();
     
      console.log(
        `\nTransaction Signature:` +
          `https://solana.fm/tx/${transactionSignature}?cluster=devnet-solana`,
      );
    });

The transaction details will show that the custom program was first invoked
(instruction 1), which then invokes the System Program (instruction 1.1),
resulting in a successful SOL transfer.

![Transaction Details](https://solana-developer-
content.vercel.app/assets/docs/core/cpi/transaction-details.png)Transaction
Details

You can build, deploy, and run the test of this example on Playground to view
the transaction details on the [SolanaFM explorer](https://solana.fm/).

## How to CPI with Anchor #

In the starter code, the `SolTransfer` struct specifies the accounts required
by the transfer instruction.

    
    
    #[derive(Accounts)]
    pub struct SolTransfer<'info> {
        #[account(mut)]
        sender: Signer<'info>,
        #[account(mut)]
        recipient: SystemAccount<'info>,
        system_program: Program<'info, System>,
    }

### Anchor CpiContext #

The `sol_transfer` instruction included in the starter code shows a typical
approach for constructing CPIs using the [Anchor
framework](https://www.anchor-lang.com/).

This approach involves creating a [`CpiContext`](https://docs.rs/anchor-
lang/latest/anchor_lang/context/struct.CpiContext.html), which includes the
`program_id` and accounts required for the instruction being called, followed
by a helper function (`transfer`) to invoke a specific instruction.

    
    
    use anchor_lang::system_program::{transfer, Transfer};
    
    
    pub fn sol_transfer(ctx: Context<SolTransfer>, amount: u64) -> Result<()> {
        let from_pubkey = ctx.accounts.sender.to_account_info();
        let to_pubkey = ctx.accounts.recipient.to_account_info();
        let program_id = ctx.accounts.system_program.to_account_info();
     
        let cpi_context = CpiContext::new(
            program_id,
            Transfer {
                from: from_pubkey,
                to: to_pubkey,
            },
        );
     
        transfer(cpi_context, amount)?;
        Ok(())
    }

The `cpi_context` variable specifies the program ID (System Program) and
accounts (sender and recipient) required by the transfer instruction.

    
    
    let cpi_context = CpiContext::new(
        program_id,
        Transfer {
            from: from_pubkey,
            to: to_pubkey,
        },
    );

The `cpi_context` and `amount` are then passed into the `transfer` function to
execute the CPI.

    
    
    transfer(cpi_context, amount)?;

### Invoke with Crate Helper #

Under the hood, the `CpiContext` example above is a wrapper around the
`solana_program` crate's `invoke` function which uses
[`system_instruction::transfer`](https://github.com/solana-
labs/solana/blob/27eff8408b7223bb3c4ab70523f8a8dca3ca6645/sdk/program/src/system_instruction.rs#L881)
to build the instruction.

The example below demonstrates how to use the `invoke()` function to make a
CPI to the transfer instruction of the System Program using the
`system_instruction::transfer` method.

First, add these imports to the top of `lib.rs`:

    
    
    use anchor_lang::solana_program::{program::invoke, system_instruction};

Next, modify the `sol_transfer` instruction with the following:

    
    
    pub fn sol_transfer(ctx: Context<SolTransfer>, amount: u64) -> Result<()> {
        let from_pubkey = ctx.accounts.sender.to_account_info();
        let to_pubkey = ctx.accounts.recipient.to_account_info();
        let program_id = ctx.accounts.system_program.to_account_info();
     
        let instruction =
            &system_instruction::transfer(&from_pubkey.key(), &to_pubkey.key(), amount);
     
        invoke(instruction, &[from_pubkey, to_pubkey, program_id])?;
        Ok(())
    }

This implementation is functionally equivalent to the previous example.

### Invoke with Instruction #

You can also manually build the instruction to pass into the `invoke()`
function. This is useful when there is not a crate available to help build the
instruction you want to invoke.

This approach requires you to manually specify the `AccountMeta`s required by
the instruction and correctly create the instruction data buffer.

The `sol_transfer` instruction below is a fully expanded equivalent of the
previous two examples.

    
    
    pub fn sol_transfer(ctx: Context<SolTransfer>, amount: u64) -> Result<()> {
        let from_pubkey = ctx.accounts.sender.to_account_info();
        let to_pubkey = ctx.accounts.recipient.to_account_info();
        let program_id = ctx.accounts.system_program.to_account_info();
     
        // Prepare instruction AccountMetas
        let account_metas = vec![
            AccountMeta::new(from_pubkey.key(), true),
            AccountMeta::new(to_pubkey.key(), false),
        ];
     
        // SOL transfer instruction discriminator
        let instruction_discriminator: u32 = 2;
     
        // Prepare instruction data
        let mut instruction_data = Vec::with_capacity(4 + 8);
        instruction_data.extend_from_slice(&instruction_discriminator.to_le_bytes());
        instruction_data.extend_from_slice(&amount.to_le_bytes());
     
        // Create instruction
        let instruction = Instruction {
            program_id: program_id.key(),
            accounts: account_metas,
            data: instruction_data,
        };
     
        // Invoke instruction
        invoke(&instruction, &[from_pubkey, to_pubkey, program_id])?;
        Ok(())
    }

The `sol_transfer` instruction above replicates this
[example](/vi/docs/core/transactions#manual-sol-transfer) of manually building
a SOL transfer instruction. It follows the same pattern as building an
[instruction](/vi/docs/core/transactions#instruction) to add to a transaction.

When building an instruction in Rust, use the following syntax to specify the
`AccountMeta` for each account:

    
    
    AccountMeta::new(account1_pubkey, true),           // writable, signer
    AccountMeta::new(account2_pubkey, false),          // writable, not signer
    AccountMeta::new_readonly(account3_pubkey, false), // not writable, not signer
    AccountMeta::new_readonly(account4_pubkey, true),  // writable, signer

[Previous« How to CPI with a PDA Signer in a Solana
program](/vi/developers/guides/getstarted/how-to-cpi-with-signer)[NextHow to
create a token on Solana »](/vi/developers/guides/getstarted/how-to-create-a-
token)

##### Table of Contents

  * [Starter Code](/vi/developers/guides/getstarted/how-to-cpi#starter-code)
  * [How to CPI with Anchor](/vi/developers/guides/getstarted/how-to-cpi#how-to-cpi-with-anchor)
  * [Anchor CpiContext](/vi/developers/guides/getstarted/how-to-cpi#anchor-cpicontext)
  * [Invoke with Crate Helper](/vi/developers/guides/getstarted/how-to-cpi#invoke-with-crate-helper)
  * [Invoke with Instruction](/vi/developers/guides/getstarted/how-to-cpi#invoke-with-instruction)

[Scroll to Top](/vi/developers/guides/getstarted/how-to-cpi#)

[Edit Page](https://github.com/solana-foundation/developer-
content/tree/main/content/guides/getstarted/how-to-cpi.md)

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

