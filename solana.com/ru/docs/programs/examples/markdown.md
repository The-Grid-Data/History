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

##### Table of Contents

  * [Basics](/ru/docs/programs/examples#basics)
  * [Compression](/ru/docs/programs/examples#compression)
  * [Oracles](/ru/docs/programs/examples#oracles)
  * [Tokens](/ru/docs/programs/examples#tokens)
  * [Token 2022 (Token Extensions](/ru/docs/programs/examples#token-2022-token-extensions)
  * [Break](/ru/docs/programs/examples#break)
  * [Build and Run](/ru/docs/programs/examples#build-and-run)

[Scroll to Top](/ru/docs/programs/examples#)

[Edit Page](https://github.com/solana-foundation/developer-
content/tree/main/docs/programs/examples.md)

[Home](/ru)>[Solana Documentation](/ru/docs)>Developing Programs

# [Program Examples](/ru/docs/programs/examples)

The "[Solana Program Examples](https://github.com/solana-developers/program-
examples)" repository on GitHub offers several subfolders, each containing
code examples for different Solana programming paradigms and languages,
designed to help developers learn and experiment with Solana blockchain
development.

You can find the examples in the `solana-developers/program-examples` together
with README files that explain you how to run the different examples. Most
examples are self-contained and are available in native Rust (ie, with no
framework), [Anchor](https://www.anchor-lang.com/docs/installation),
[Seahorse](https://seahorse-lang.org/) and it also contains a list of examples
that we would love to [see as contributions](https://github.com/solana-
developers/program-examples?tab=readme-ov-file#examples-wed-love-to-see).  
Within the repo you will find the following subfolder, each with assorted
example programs within them:

  * [Basics](/ru/docs/programs/examples#basics)
  * [Compression](/ru/docs/programs/examples#compression)
  * [Oracles](/ru/docs/programs/examples#oracles)
  * [Tokens](/ru/docs/programs/examples#tokens)
  * [Token 2022 (Token Extensions)](/ru/docs/programs/examples#token-2022-token-extensions)
  * [Break](/ru/docs/programs/examples#break)
    * [Build and Run](/ru/docs/programs/examples#build-and-run)

## Basics #

Contains a series of examples that demonstrate the foundational steps for
building Solana programs using native Rust libraries. These examples are
designed to help developers understand the core concepts of Solana
programming.

Example Name| Description| Language  
---|---|---  
[Create Account](https://github.com/solana-developers/program-
examples/tree/main/basics/account-data)| Saving an address with name, house
number, street and city in an account.| Native, Anchor  
[Checking Accounts](https://github.com/solana-developers/program-
examples/tree/main/basics/checking-accounts)| Security lessons that shows how
to do account checks| Native, Anchor  
[Close Account](https://github.com/solana-developers/program-
examples/tree/main/basics/close-account)| Show you how to close accounts to
get its rent back.| Native, Anchor  
[Counter](https://github.com/solana-developers/program-
examples/tree/main/basics/counter)| A simple counter program in all the
different architectures.| Native, Anchor, Seahorse, mpl-stack  
[Create Account](https://github.com/solana-developers/program-
examples/tree/main/basics/create-account)| How to create a system account
within a program.| Native, Anchor  
[Cross Program Invocation](https://github.com/solana-developers/program-
examples/tree/main/basics/cross-program-invocation)| Using a hand and lever
analogy this shows you how to call another program from within a program.|
Native, Anchor  
[hello solana](https://github.com/solana-developers/program-
examples/tree/main/basics/hello-solana)| Hello world example which just prints
hello world in the transaction logs.| Native, Anchor  
[Pda Rent payer](https://github.com/solana-developers/program-
examples/tree/main/basics/pda-rent-payer)| Shows you how you can use the
lamports from a PDA to pay for a new account.| Native, Anchor  
[Processing Instructions](https://github.com/solana-developers/program-
examples/tree/main/basics/processing-instructions)| Shows you how to handle
instruction data string and u32.| Native, Anchor  
[Program Derived Addresses](https://github.com/solana-developers/program-
examples/tree/main/basics/program-derived-addresses)| Shows how to use seeds
to refer to a PDA and save data in it.| Native, Anchor  
[Realloc](https://github.com/solana-developers/program-
examples/tree/main/basics/realloc)| Shows you how to increase and decrease the
size of an existing account.| Native, Anchor  
[Rent](https://github.com/solana-developers/program-
examples/tree/main/basics/rent)| Here you will learn how to calculate rent
requirements within a program.| Native, Anchor  
[Repository Layout](https://github.com/solana-developers/program-
examples/tree/main/basics/repository-layout)| Recommendations on how to
structure your program layout.| Native, Anchor  
[Transfer SOL](https://github.com/solana-developers/program-
examples/tree/main/basics/transfer-sol)| Different methods of transferring SOL
for system accounts and PDAs.| Native, Anchor, Seahorse  
  
## Compression #

Contains a series of examples that demonstrate how to use [state
compression](/ru/docs/advanced/state-compression) on Solana. Mainly focused on
compressed NFTs (cNFTs).

Example Name| Description| Language  
---|---|---  
[cNFT-burn](https://github.com/solana-developers/program-
examples/tree/main/compression/cnft-burn)| To destroy a cNFT it can be burnt.
This examples shows how to do that in a program.| Anchor  
[cNFT-Vault](https://github.com/solana-developers/program-
examples/tree/main/compression/cnft-vault/anchor)| How to custody a cNFT in a
program and send it out again.| Anchor  
[cutils](https://github.com/solana-developers/program-
examples/tree/main/compression/cutils)| A suite utils to for example mint and
verify cNFTs in a program.| Anchor  
  
## Oracles #

Oracles allow to use off chain data in programs.

Example Name| Description| Language  
---|---|---  
[Pyth](https://github.com/solana-developers/program-
examples/tree/main/oracles/pyth)| Pyth makes price data of tokens available in
on chain programs.| Anchor, Seahorse  
  
## Tokens #

Most tokens on Solana use the Solana Program Library (SPL) token standard.
Here you can find many examples on how to mint, transfer, burn tokens and even
how to interact with them in programs.

Example Name| Description| Language  
---|---|---  
[Create Token](https://github.com/solana-developers/program-
examples/tree/main/tokens/create-token)| How to create a token and add
metaplex metadata to it.| Anchor, Native  
[NFT Minter](https://github.com/solana-developers/program-
examples/tree/main/tokens/nft-minter)| Minting only one amount of a token and
then removing the mint authority.| Anchor, Native  
[PDA Mint Authority](https://github.com/solana-developers/program-
examples/tree/main/tokens/pda-mint-authority)| Shows you how to change the
mint authority of a mint, to mint tokens from within a program.| Anchor,
Native  
[SPL Token Minter](https://github.com/solana-developers/program-
examples/tree/main/tokens/spl-token-minter)| Explains how to use Associated
Token Accounts to be able to keep track of token accounts.| Anchor, Native  
[Token Swap](https://github.com/solana-developers/program-
examples/tree/main/tokens/token-swap)| Extensive example that shows you how to
build a AMM (automated market maker) pool for SPL tokens.| Anchor  
[Transfer Tokens](https://github.com/solana-developers/program-
examples/tree/main/tokens/transfer-tokens)| Shows how to transfer SPL token
using CPIs into the token program.| Anchor, Native, Seahorse  
[Token-2022](https://github.com/solana-developers/program-
examples/tree/main/tokens/token-2022)| See Token 2022 (Token extensions).|
Anchor, Native  
  
## Token 2022 (Token Extensions) #

Token 2022 is a new standard for tokens on Solana. It is a more flexible and
lets you add 16 different extensions to a token mint to add more functionality
to it. A full list of the extensions can be found in the [Getting Started
Guide](/ru/developers/guides/token-extensions/getting-started)

Example Name| Description| Language  
---|---|---  
[Basics](https://github.com/solana-developers/program-
examples/tree/main/tokens/token-2022/basics/anchor)| How to create a token,
mint and transfer it.| Anchor  
[Default account state](https://github.com/solana-developers/program-
examples/tree/main/tokens/token-2022/default-account-state/native)| This
extension lets you create token accounts with a certain state, for example
frozen.| Native  
[Mint Close Authority](https://github.com/solana-developers/program-
examples/tree/main/tokens/token-2022/mint-close-authority)| With the old token
program it was not possible to close a mint. Now it is.| Native  
[Multiple Extensions](https://github.com/solana-developers/program-
examples/tree/main/tokens/token-2022/multiple-extensions)| Shows you how you
can add multiple extensions to a single mint| Native  
[NFT Metadata pointer](https://github.com/solana-developers/program-
examples/tree/main/tokens/token-2022/nft-meta-data-pointer)| It is possible to
use the metadata extension to create NFTs and add dynamic on chain metadata.|
Anchor  
[Not Transferable](https://github.com/solana-developers/program-
examples/tree/main/tokens/token-2022/non-transferable/native)| Useful for
example for achievements, referral programs or any soul bound tokens.| Native  
[Transfer fee](https://github.com/solana-developers/program-
examples/tree/main/tokens/token-2022/transfer-fees)| Every transfer of the
tokens hold some tokens back in the token account which can then be
collected.| Native  
[Transfer Hook](https://github.com/solana-developers/program-
examples/tree/main/tokens/token-2022/transfer-hook)| Four examples to add
additional functionality to your token using a CPI from the token program into
your program.| Anchor  
  
## Break #

[Break](https://break.solana.com/) is a React app that gives users a visceral
feeling for just how fast and high-performance the Solana network really is.
Can you _break_ the Solana blockchain? During a 15 second play-through, each
click of a button or keystroke sends a new transaction to the cluster. Smash
the keyboard as fast as you can and watch your transactions get finalized in
real-time while the network takes it all in stride!

Break can be played on our Devnet, Testnet and Mainnet Beta networks. Plays
are free on Devnet and Testnet, where the session is funded by a network
faucet. On Mainnet Beta, users pay to play 0.08 SOL per game. The session
account can be funded by a local keystore wallet or by scanning a QR code from
Trust Wallet to transfer the tokens.

[Click here to play Break](https://break.solana.com/)

### Build and Run #

First fetch the latest version of the example code:

    
    
    git clone https://github.com/solana-labs/break.git
    cd break

Next, follow the steps in the git repository's
[README](https://github.com/solana-labs/break/blob/main/README.md).

[Previous« Deploying Programs](/ru/docs/programs/deploying)[NextFAQ
»](/ru/docs/programs/faq)

  * [Solana Documentation](/ru/docs)

    * [JSON RPC Methods](/ru/docs/rpc)
    * [Terminology](/ru/docs/terminology)
  * Introduction

    * [Overview](/ru/docs/intro/overview)
    * [Wallets](/ru/docs/intro/wallets)
    * [Intro to Development](/ru/docs/intro/dev)
  * Core Concepts

    * [Solana Account Model](/ru/docs/core/accounts)
    * [Transactions and Instructions](/ru/docs/core/transactions)
    * [Fees on Solana](/ru/docs/core/fees)
    * [Programs on Solana](/ru/docs/core/programs)
    * [Program Derived Address](/ru/docs/core/pda)
    * [Cross Program Invocation](/ru/docs/core/cpi)
    * [Tokens on Solana](/ru/docs/core/tokens)
    * [Clusters & Endpoints](/ru/docs/core/clusters)
  * Advanced Concepts

    * [Versioned Transactions](/ru/docs/advanced/versions)
    * [Address Lookup Tables](/ru/docs/advanced/lookup-tables)
    * [Confirmation & Expiration](/ru/docs/advanced/confirmation)
    * [Retrying Transactions](/ru/docs/advanced/retry)
    * [State Compression](/ru/docs/advanced/state-compression)
  * Solana Clients

    * [Rust](/ru/docs/clients/rust)
    * [JavaScript / TypeScript](/ru/docs/clients/javascript)
    * [Web3.js API Examples](/ru/docs/clients/javascript-reference)
  * [Economics](/ru/docs/economics)

    * Inflation
      * [Proposed Inflation Schedule](/ru/docs/economics/inflation/inflation-schedule)
      * [Inflation Terminology](/ru/docs/economics/inflation/terminology)
    * [Staking](/ru/docs/economics/staking)
      * [Stake Accounts](/ru/docs/economics/staking/stake-accounts)
      * [Stake Programming](/ru/docs/economics/staking/stake-programming)
  * Developing Programs

    * [Overview](/ru/docs/programs/overview)
    * [Debugging Programs](/ru/docs/programs/debugging)
    * [Deploying Programs](/ru/docs/programs/deploying)
    * [Program Examples](/ru/docs/programs/examples)
    * [FAQ](/ru/docs/programs/faq)
    * [Developing with C](/ru/docs/programs/lang-c)
    * [Developing with Rust](/ru/docs/programs/lang-rust)
    * [Limitations](/ru/docs/programs/limitations)
  * More Information

    * [Add Solana to Your Exchange](/ru/docs/more/exchange)

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

