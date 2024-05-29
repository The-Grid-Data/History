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

[Home](/vi)>[Solana Cookbook](/vi/developers/cookbook)>Accounts

[Edit Page](https://github.com/solana-foundation/developer-
content/tree/main/content/cookbook/accounts/create-pda-account.md)

# [How to Create a PDA's Account](/vi/developers/cookbook/accounts/create-pda-
account)

Accounts found at Program Derived Addresses (PDAs) can only be created on-
chain. The accounts have addresses that have an associated off-curve public
key, but no secret key.

To generate a PDA, use `findProgramAddressSync` with your required seeds.
Generating with the same seeds will always generate the same PDA.

## Generating a PDA #

generate-pda.ts

    
    
    import { PublicKey } from "@solana/web3.js";
     
    const programId = new PublicKey("G1DCNUQTSGHehwdLCAmRyAG8hf51eCHrLNUqkgGKYASj");
     
    let [pda, bump] = PublicKey.findProgramAddressSync(
      [Buffer.from("test")],
      programId,
    );
    console.log(`bump: ${bump}, pubkey: ${pda.toBase58()}`);
    // you will find the result is different from `createProgramAddress`.
    // It is expected because the real seed we used to calculate is ["test" + bump]

## Create an Account at a PDA #

### Program #

create-pda.rs

    
    
    use solana_program::{
        account_info::next_account_info, account_info::AccountInfo, entrypoint,
        entrypoint::ProgramResult, program::invoke_signed, pubkey::Pubkey, system_instruction, sysvar::{rent::Rent, Sysvar}
    };
     
    entrypoint!(process_instruction);
     
    fn process_instruction(
        program_id: &Pubkey,
        accounts: &[AccountInfo],
        instruction_data: &[u8],
    ) -> ProgramResult {
        let account_info_iter = &mut accounts.iter();
     
        let payer_account_info = next_account_info(account_info_iter)?;
        let pda_account_info = next_account_info(account_info_iter)?;
        let rent_sysvar_account_info = &Rent::from_account_info(next_account_info(account_info_iter)?)?;
     
        // find space and minimum rent required for account
        let space = instruction_data[0];
        let bump = instruction_data[1];
        let rent_lamports = rent_sysvar_account_info.minimum_balance(space.into());
     
        invoke_signed(
            &system_instruction::create_account(
                &payer_account_info.key,
                &pda_account_info.key,
                rent_lamports,
                space.into(),
                program_id
            ),
            &[
                payer_account_info.clone(),
                pda_account_info.clone()
            ],
            &[&[&payer_account_info.key.as_ref(), &[bump]]]
        )?;
     
        Ok(())
    }

## Client #

create-pda.ts

    
    
    import {
      clusterApiUrl,
      Connection,
      Keypair,
      Transaction,
      SystemProgram,
      PublicKey,
      TransactionInstruction,
      LAMPORTS_PER_SOL,
      SYSVAR_RENT_PUBKEY,
    } from "@solana/web3.js";
     
    (async () => {
      // program id
      const programId = new PublicKey(
        "7ZP42kRwUQ2zgbqXoaXzAFaiQnDyp6swNktTSv8mNQGN",
      );
     
      // connection
      const connection = new Connection(clusterApiUrl("devnet"), "confirmed");
     
      // setup fee payer
      const feePayer = Keypair.generate();
      const feePayerAirdropSignature = await connection.requestAirdrop(
        feePayer.publicKey,
        LAMPORTS_PER_SOL,
      );
      await connection.confirmTransaction(feePayerAirdropSignature);
     
      // setup pda
      let [pda, bump] = await PublicKey.findProgramAddress(
        [feePayer.publicKey.toBuffer()],
        programId,
      );
      console.log(`bump: ${bump}, pubkey: ${pda.toBase58()}`);
     
      const data_size = 0;
     
      let tx = new Transaction().add(
        new TransactionInstruction({
          keys: [
            {
              pubkey: feePayer.publicKey,
              isSigner: true,
              isWritable: true,
            },
            {
              pubkey: pda,
              isSigner: false,
              isWritable: true,
            },
            {
              pubkey: SYSVAR_RENT_PUBKEY,
              isSigner: false,
              isWritable: false,
            },
            {
              pubkey: SystemProgram.programId,
              isSigner: false,
              isWritable: false,
            },
          ],
          data: Buffer.from(new Uint8Array([data_size, bump])),
          programId: programId,
        }),
      );
     
      console.log(`txhash: ${await connection.sendTransaction(tx, [feePayer])}`);
    })();

[Previous« How to Calculate Account Creation
Cost](/vi/developers/cookbook/accounts/calculate-rent)[NextHow to Sign with a
PDA's Account »](/vi/developers/cookbook/accounts/sign-with-pda)

  * [Solana Cookbook](/vi/developers/cookbook)

    * Wallets
      * [How to Create a Keypair](/vi/developers/cookbook/wallets/create-keypair)
      * [How to Restore a Keypair](/vi/developers/cookbook/wallets/restore-keypair)
      * [How to Verify a Keypair](/vi/developers/cookbook/wallets/verify-keypair)
      * [How to Validate a Public Key](/vi/developers/cookbook/wallets/check-publickey)
      * [How to Generate Mnemonics for Keypairs](/vi/developers/cookbook/wallets/generate-mnemonic)
      * [How to Restore a Keypair from a Mnemonic](/vi/developers/cookbook/wallets/restore-from-mnemonic)
      * [How to Generate a Vanity Address](/vi/developers/cookbook/wallets/generate-vanity-address)
      * [How to Sign and Verify a Message](/vi/developers/cookbook/wallets/sign-message)
      * [How to Connect a Wallet with React](/vi/developers/cookbook/wallets/connect-wallet-react)
    * Transactions
      * [How to Send SOL](/vi/developers/cookbook/transactions/send-sol)
      * [How to Send Tokens](/vi/developers/cookbook/transactions/send-tokens)
      * [How to Calculate Transaction Cost](/vi/developers/cookbook/transactions/calculate-cost)
      * [How to Add a Memo to a Transaction](/vi/developers/cookbook/transactions/add-memo)
      * [How to Add Priority Fees to a Transaction](/vi/developers/cookbook/transactions/add-priority-fees)
      * [How to Optimize Compute Requested](/vi/developers/cookbook/transactions/optimize-compute)
    * Accounts
      * [How to Create an Account](/vi/developers/cookbook/accounts/create-account)
      * [How to Calculate Account Creation Cost](/vi/developers/cookbook/accounts/calculate-rent)
      * [How to Create a PDA's Account](/vi/developers/cookbook/accounts/create-pda-account)
      * [How to Sign with a PDA's Account](/vi/developers/cookbook/accounts/sign-with-pda)
      * [How to Close an Account](/vi/developers/cookbook/accounts/close-account)
      * [How to Get Account Balance](/vi/developers/cookbook/accounts/get-account-balance)

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

