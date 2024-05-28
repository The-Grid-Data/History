This website uses cookies to offer you a better browsing experience. Find out
more on how we use cookies.

Opt-out[Details](/privacy-policy#collection-of-information)

Accept

[![Solana](/_next/static/media/logotype.e4df684f.svg)](/)

  * Learn
  * Developers
  * Solutions
  * Network
  * Community

Search```K`

[Documentation](/docs)[RPC
API](/docs/rpc)[Cookbook](/developers/cookbook)[Guides](/developers/guides)[Terminology](/docs/terminology)

# EVM vs. SVM: Client Differences

Learn about the differences between clients on Solana and Ethereum.

**Table of Contents**

  

Types of validator clients

Number of nodes in Ethereum and Solana

Types of node

List of RPC services

Summary

Ethereum and Solana are unique blockchains that have multiple diverse
validator clients for validating transactions. Having various validator
clients helps prevent network disruptions in case a specific client encounters
issues. In this chapter, we will introduce validator clients in the Ethereum
and Solana ecosystems and discuss the types of nodes that exist.

## **Types of validator clients**

As Ethereum transitioned from PoW (Proof of Work) to PoS (Proof of Stake), it
adopted two types of validator clients: Execution Layer (EL) and Consensus
Layer (CL) clients. Execution clients are responsible for receiving new
transactions broadcasted on the network, executing them on the EVM, and
maintaining the current state and database of all Ethereum data. Consensus
clients, on the other hand, implement the consensus algorithm of PoS and
achieve consensus on the network based on verified data from execution
clients. These two types of clients serve different roles, which is why
Ethereum validator nodes typically run both execution and consensus clients.
In contrast, Solana combines both functionalities in a single client.

Here are the list of execution clients for Ethereum:

Client | Language  
---|---  
Geth | Golang  
Besu | Java  
Nethermind | C# .NET  
Erigon | Go  
Reth | Rust  
  
And here are the list of consensus clients for Ethereum:

Client | Language  
---|---  
Lighthouse | Rust  
Lodestar | TypeScript  
Nimbus | Nim  
Prysm | Go  
Teku | Java  
  
Now, let's take a look at Solana's validator clients list:

Client | Language  
---|---  
Solana Labs | Rust  
Jito-Solana | Rust  
Firedancer | C++  
sig | Zig  
Agave | Rust  
  
## **Number of nodes in Ethereum and Solana**

For Ethereum, you can check the number of nodes operated for each validator
client by visiting
[clientdiversity](https://clientdiversity.org/#distribution). For Solana, you
can find this information from the [Validator Health Report](/news/validator-
health-report-october-2023).

## **Types of node**

Nodes come in various forms depending on their use cases and required
conditions. They can range from heavyweight nodes that store all data to
lightweight nodes focused solely on processing transactions.

**Ethereum classifies nodes into three types based on _the scope of data
storage and participation in consensus:_**

  * **Full Node** : Full nodes validate the blockchain block by block, downloading and verifying the data for each block. There are various types of full nodes, with some starting from the genesis block and validating all blocks in the entire blockchain history. Others begin validation from recent trusted blocks, typically maintaining a local copy of the most recent 128 blocks and periodically deleting older data to save disk space. Older data can be regenerated when needed.
  * **Archive Node** : Archive nodes verify and preserve all blocks from the genesis block onward, never deleting any data. They are essential for services like block explorers, wallet providers, and chain analysis, as well as for querying test sets without mining them reliably.
  * **Light Node** : Light nodes download only block headers instead of the entire blockchain. Additional information required by light nodes is requested from full nodes. Light nodes can independently verify data received against the state root of block headers. They do not require high bandwidth or powerful hardware, making it possible to participate in the Ethereum network from mobile phones or embedded devices. Light nodes do not participate in consensus, meaning they cannot become miners or validators, but they provide the same functionality and security guarantees as full nodes, allowing access to the Ethereum blockchain.

**For Solana, nodes are divided into two types _based on their participation
in consensus:_**

  * **Consensus Nodes** : Consensus nodes play a vital role in the network by creating and proposing new blocks to the network and voting on the validity of new blocks proposed by other nodes. They are central to the network's functioning.
  * **RPC Nodes (Remote Procedure Call Nodes)** : RPC nodes are essential for dApps built on top of the Solana blockchain, serving as gateways for blockchain data. Like consensus nodes, they independently verify all new blocks and network changes but do not participate in voting.

Solana distinguishes RPC nodes from consensus nodes from the start. However,
RPC nodes do not participate in voting. Ethereum's RPC nodes are typically
based on full nodes or archive nodes.

**Why does Solana categorize nodes this way?** Unlike Ethereum, Solana
generates a high number of transactions per second, and storing the entire
blockchain on every node is impractical due to the high transaction volume.
Currently, Solana stores data using Google Bigtable, and RPC nodes access data
from there. Therefore, Solana focuses less on storing a large amount of data
locally, which differs from Ethereum's node categorization criteria.

In summary, here's a comparison:

**Node storing all data and participating in consensus**

  * **Ethereum:** Archive Node
  * **Solana:** [n/a]

**Node storing some data and participating in consensus**

  * **Ethereum:** Full Node
  * **Solana:** Consensus Node

**Node storing some data and not participating in consensus**

  * **Ethereum:** Light Node
  * **Solana:** RPC Node

Node Type | Ethereum | Solana  
---|---|---  
Node storing all data and participating in consensus. | Archive Node | [n/a]  
Node storing some data and participating in consensus. | Full Node | Consensus Node  
Node storing some data and not participating in consensus. | Light Node | RPC Node  
  
## **List of RPC services**

There are RPC services that support both Ethereum and Solana simultaneously,
as well as those that support a single chain. Services like Alchemy and
Quicknode support both Ethereum and Solana. You can check Solana’s [various
RPC services here](/rpc).

## **Summary**

  * Like Ethereum, Solana also has various types of validator clients.
  * While the types of nodes may appear different for each chain, they fundamentally provide users with the same functionalities.

EVM TO SVM

[Home](/developers/evm-to-svm)

## Start building on Solana

[![](/_next/image?url=https%3A%2F%2Fcdn.builder.io%2Fapi%2Fv1%2Fimage%2Fassets%252Fce0c7323a97a4d91bd0baa7490ec9139%252Fdfb1773873354d118d134beca2334288&w=3840&q=75)![](/_next/image?url=https%3A%2F%2Fcdn.builder.io%2Fapi%2Fv1%2Fimage%2Fassets%252Fce0c7323a97a4d91bd0baa7490ec9139%252Fdfb1773873354d118d134beca2334288&w=3840&q=75)Intro
to Solana Development](/developers/guides/getstarted/hello-world-in-your-
browser)

[![](/_next/image?url=https%3A%2F%2Fcdn.builder.io%2Fapi%2Fv1%2Fimage%2Fassets%252Fce0c7323a97a4d91bd0baa7490ec9139%252Fdfb1773873354d118d134beca2334288&w=3840&q=75)![](/_next/image?url=https%3A%2F%2Fcdn.builder.io%2Fapi%2Fv1%2Fimage%2Fassets%252Fce0c7323a97a4d91bd0baa7490ec9139%252Fdfb1773873354d118d134beca2334288&w=3840&q=75)
Intro to Solana Development](/developers/guides/getstarted/hello-world-in-
your-
browser)[![](/_next/image?url=https%3A%2F%2Fcdn.builder.io%2Fapi%2Fv1%2Fimage%2Fassets%252Fce0c7323a97a4d91bd0baa7490ec9139%252Fdfb1773873354d118d134beca2334288&w=3840&q=75)![](/_next/image?url=https%3A%2F%2Fcdn.builder.io%2Fapi%2Fv1%2Fimage%2Fassets%252Fce0c7323a97a4d91bd0baa7490ec9139%252Fdfb1773873354d118d134beca2334288&w=3840&q=75)
Solana Development
Course](https://www.soldev.app/course)[![](/_next/image?url=https%3A%2F%2Fcdn.builder.io%2Fapi%2Fv1%2Fimage%2Fassets%252Fce0c7323a97a4d91bd0baa7490ec9139%252Fdfb1773873354d118d134beca2334288&w=3840&q=75)![](/_next/image?url=https%3A%2F%2Fcdn.builder.io%2Fapi%2Fv1%2Fimage%2Fassets%252Fce0c7323a97a4d91bd0baa7490ec9139%252Fdfb1773873354d118d134beca2334288&w=3840&q=75)
Solana
Bootcamp](https://youtu.be/0P8JeL3TURU?feature=shared)[![](/_next/image?url=https%3A%2F%2Fcdn.builder.io%2Fapi%2Fv1%2Fimage%2Fassets%252Fce0c7323a97a4d91bd0baa7490ec9139%252Fdfb1773873354d118d134beca2334288&w=3840&q=75)![](/_next/image?url=https%3A%2F%2Fcdn.builder.io%2Fapi%2Fv1%2Fimage%2Fassets%252Fce0c7323a97a4d91bd0baa7490ec9139%252Fdfb1773873354d118d134beca2334288&w=3840&q=75)
More Solana Developer Tools](/developers)

![](https://cdn.builder.io/api/v1/pixel?apiKey=ce0c7323a97a4d91bd0baa7490ec9139)

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

