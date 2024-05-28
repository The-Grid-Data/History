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

[Home](/)>[Solana Cookbook](/developers/cookbook)>Accounts

[Edit Page](https://github.com/solana-foundation/developer-
content/tree/main/content/cookbook/accounts/sign-with-pda.md)

# [How to Sign with a PDA's Account](/developers/cookbook/accounts/sign-with-
pda)

Program derived addresses (PDA) can be used to have accounts owned by programs
that can sign. This is useful if you want a program to own a token account and
you want the program to transfer tokens from one account to another.

sign-with-pda.rs

    
    
    use solana_program::{
        account_info::next_account_info, account_info::AccountInfo, entrypoint,
        entrypoint::ProgramResult, program::invoke_signed, pubkey::Pubkey, system_instruction,
    };
     
    entrypoint!(process_instruction);
     
    fn process_instruction(
        _program_id: &Pubkey,
        accounts: &[AccountInfo],
        instruction_data: &[u8],
    ) -> ProgramResult {
        let account_info_iter = &mut accounts.iter();
     
        let pda_account_info = next_account_info(account_info_iter)?;
        let to_account_info = next_account_info(account_info_iter)?;
        let system_program_account_info = next_account_info(account_info_iter)?;
     
        // pass bump seed for saving compute budget
        let bump_seed = instruction_data[0];
     
        invoke_signed(
            &system_instruction::transfer(
                &pda_account_info.key,
                &to_account_info.key,
                100_000_000, // 0.1 SOL
            ),
            &[
                pda_account_info.clone(),
                to_account_info.clone(),
                system_program_account_info.clone(),
            ],
            &[&[b"escrow", &[bump_seed]]],
        )?;
     
        Ok(())
    }
     

[Previous« How to Create a PDA's
Account](/developers/cookbook/accounts/create-pda-account)[NextHow to Close an
Account »](/developers/cookbook/accounts/close-account)

  * [Solana Cookbook](/developers/cookbook)

    * Wallets
      * [How to Create a Keypair](/developers/cookbook/wallets/create-keypair)
      * [How to Restore a Keypair](/developers/cookbook/wallets/restore-keypair)
      * [How to Verify a Keypair](/developers/cookbook/wallets/verify-keypair)
      * [How to Validate a Public Key](/developers/cookbook/wallets/check-publickey)
      * [How to Generate Mnemonics for Keypairs](/developers/cookbook/wallets/generate-mnemonic)
      * [How to Restore a Keypair from a Mnemonic](/developers/cookbook/wallets/restore-from-mnemonic)
      * [How to Generate a Vanity Address](/developers/cookbook/wallets/generate-vanity-address)
      * [How to Sign and Verify a Message](/developers/cookbook/wallets/sign-message)
      * [How to Connect a Wallet with React](/developers/cookbook/wallets/connect-wallet-react)
    * Transactions
      * [How to Send SOL](/developers/cookbook/transactions/send-sol)
      * [How to Send Tokens](/developers/cookbook/transactions/send-tokens)
      * [How to Calculate Transaction Cost](/developers/cookbook/transactions/calculate-cost)
      * [How to Add a Memo to a Transaction](/developers/cookbook/transactions/add-memo)
      * [How to Add Priority Fees to a Transaction](/developers/cookbook/transactions/add-priority-fees)
      * [How to Optimize Compute Requested](/developers/cookbook/transactions/optimize-compute)
    * Accounts
      * [How to Create an Account](/developers/cookbook/accounts/create-account)
      * [How to Calculate Account Creation Cost](/developers/cookbook/accounts/calculate-rent)
      * [How to Create a PDA's Account](/developers/cookbook/accounts/create-pda-account)
      * [How to Sign with a PDA's Account](/developers/cookbook/accounts/sign-with-pda)
      * [How to Close an Account](/developers/cookbook/accounts/close-account)
      * [How to Get Account Balance](/developers/cookbook/accounts/get-account-balance)

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

