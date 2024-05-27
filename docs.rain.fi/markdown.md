Skip to main content

[![Rain.fi Documentation](/img/logo.svg)![Rain.fi
Documentation](/img/logo.svg)](/)[Introduction](/)[Classes](/classes/overview)[Utilities](/utils/overview)[About](/about)

[Rain.fi](https://rain.fi)

  * [Introduction](/)
  * [Classes](/category/classes)

  * [Interest](/category/interest)

  * [Utilities](/category/utilities)

  * [](/)
  * Introduction

On this page

# Introduction

![](https://i.ibb.co/fCpnvzQ/rain-simple-logo.png)

# Rain.fi

**Leveraging the liquidity of NFTs like never before.**

[![Tutorials](https://img.shields.io/badge/docs-tutorials-
yellow)](https://docs.rain.fi)[![Discord](https://img.shields.io/badge/chat-
discord-
blueviolet)](https://discord.com/invite/usrMBX5adn)[![Twitter](https://img.shields.io/badge/follow-
twitter-blue)](https://twitter.com/rainfi_)

**This code is given as is and is unaudited. Use at your own risk.**  
**The examples might not be always up to date since the package is in active
development.**

# Table of contents:

  * 💧 Installation
  * 💧 Program IDs
  * 💧 Start
  * 💧 Classes & Functions
  * 💧 Interest
  * 💧 License

## 💧 Installation​

**Yarn:**

    
    
     yarn add @rainfi/sdk  
    

**NPM:**

    
    
     npm i @rainfi/sdk  
    

## 💧 Program IDs​

    
    
     Mainnet = RainEraPU5yDoJmTrHdYynK9739GkEfDsE4ffqce2BR  
     Devnet  = RainEraPU5yDoJmTrHdYynK9739GkEfDsE4ffqce2BR // Not live yet  
    

## 💧 Start​

To start working with Rain SDK, initialize `new Rain()` class using the
snippet below.

Then, go to **[this page](/classes/rain)** and read more about `Rain` class,
it's properties and functions it provides.

    
    
    import { Pool, Rain } from "@rainfi/sdk";  
    import { Connection, LAMPORTS_PER_SOL, Keypair, PublicKey } from "@solana/web3.js";  
      
    const connection = new Connection("https://api.mainnet-beta.solana.com", "confirmed");  
    const { publicKey } = Keypair.generate() // Replace with your pubkey  
      
    // Let you interact with the whole protocol  
    const rain = new Rain(connection, publicKey);  
    

## 💧 Classes & Functions​

To explore all classes and utility functions Rain SDK provides, visit **[Utils
Overview](/utils/overview)** and **[Classes Overview](/classes/overview)**.

It will give you broad view on all you can achieve with the SDK.

## 💧 Interest​

To read more about fees, interest formula and how are fees calculated, visit
**[Interest Page](/interest/overview)**.

## 💧 License​

Unless you explicitly state otherwise, any contribution intentionally
submitted for inclusion by you shall be licensed at the discretion of the
repository maintainers without any additional terms or conditions.

[NextClasses](/category/classes)

  * 💧 Installation
  * 💧 Program IDs
  * 💧 Start
  * 💧 Classes & Functions
  * 💧 Interest
  * 💧 License

Docs

  * [Introduction](/)
  * [Classes](/classes/overview)
  * [Utility Functions](/utils/overview)

Community

  * [Discord](https://discord.gg/547RjHj83b)
  * [Twitter](https://twitter.com/rainfi_)

Copyright © Rain.fi 2023. Built with Docusaurus.

