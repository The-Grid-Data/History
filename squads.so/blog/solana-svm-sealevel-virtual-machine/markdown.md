s m a r t

w a l l e t s

a t

l i g h t s p e e d

[Squads](../)

[Protocol](../protocol)

[Extension](../extension)

[Use Cases](../use-cases)

[About](https://www.sqds.io/)

[Blog](../blog)

[](../)

Get started

# What Is SVM - The Solana Virtual Machine

Apr 18, 2023

![what-is-svm-solana-svm-virtual-machine-sealevel-solana-vm-svm-vs-evm-
ethereum-virtual-machine-solana-parallel-
processing](https://framerusercontent.com/images/ctTEgbXLDin7A7Ew6CEpVy7LRd4.png)

Solana has gained significant attention as a next-generation, highly scalable
blockchain, largely due to its exceptional performance capabilities that can
handle thousands of transactions per second with almost no fees. One of the
key elements of Solana's advanced technology is its execution environment,
SVM, which includes the Sealevel parallelization engine.

This article covers the Solana Virtual Machine (SVM) and how this innovative
infrastructure enables the Solana blockchain to deliver enhanced performances
compared to traditional EVM blockchains like Ethereum. While EVM has for a
long time been the dominant virtual machine standard in crypto, we'll also
explore how SVM is gradually expanding through rollup solutions such as Nitro
and Eclipse.

## The Solana Virtual Machine (SVM) and Sealevel Explained

The Solana Virtual Machine, SVM in short, is the execution environment that
processes transactions and smart contracts/programs on the Solana network. In
order to better comprehend SVM, we first need to understand how a virtual
machine works within a crypto network.

In the context of blockchains, a virtual machine (VM) is a piece of software
that runs programs, more often referred to as a runtime environment to execute
smart contracts for a crypto network. When a transaction is submitted, the
virtual machine of the network is responsible for processing it and managing
the state of the blockchain (the current status of the entire network)
impacted by the execution of this transaction. The specific rules for changing
the state of the network are defined by the VM.

When processing a transaction, the VM converts the smart contract code into a
format that can be carried out by the validators' hardware. On Solana, the
main languages for writing smart contract are Rust, C, and C++, which are
compiled into BPF bytecode by the Solana Virtual Machine (SVM), enabling
transactions to be executed efficiently by the nodes of the network
(validators).  
  

![solana-deploy-smart-contract-program-deployment-svm-solana-virtual-machine-
bpf-bytecode-solana-
nodes](https://framerusercontent.com/images/ZTxRhVDrv6FdwTdEKJhS9ja7FUA.png)

The nodes of the Solana network, known as validators, each run their own
isolated environment of the Solana Virtual Machine (SVM) to maintain consensus
across the blockchain. When a smart contract is deployed (modifying the
network's state), it communicates the required state changes to the runtime.
The Solana runtime then forwards these state changes to the SVM instances
operating within each validator's system, where all validator nodes receive a
copy and translate it, updating the blockchain. This distribution of SVM
instances across validators results in a decentralized network, reducing the
risk of DDoS attacks or shutdowns. Moreover, this isolation ensures that
potential bugs or vulnerabilities in a smart contract do not compromise the
security or stability of the entire Solana network.

In summary, these SVM instances can be viewed as âmini-computersâ that
execute the necessary operations to update the state of the Solana network
based on the provided instructions by transactions. While many blockchains
today rely on the Ethereum Virtual Machine (EVM), Solana has developed its own
VM, featuring unique capabilities that deliver improved performance.  
  

![solana-sealevel-parallel-processing-blockchain-virtual-machine-multiple-
transactions-executed-evm-svm-solana-vm-
sealevel](https://framerusercontent.com/images/WQ3GqQbX2oKdsU3k8wXyeojmR0.png)

The key component of SVM is [Sealevel](https://medium.com/solana-
labs/sealevel-parallel-processing-thousands-of-smart-
contracts-d814b378192)**.** This engine enables âhorizontalâ scaling
within the Solana execution environment by allowing multiple smart contracts
to run simultaneously without impacting each other's performance, a concept
known as [parallel processing](https://docs.neonfoundation.io/docs/faq/how-
does-neon-work#how-does-the-neon-evm-enable-the-parallel-execution-of-
transactions). This is possible due to Solana smart contracts describing which
data (state) will be read or written while executing in the runtime. This lets
transactions without conflicts to run at the same time, as well as those just
reading the same information. Sealevel makes it thus possible for the SVM to
handle tens of thousands of transactions simultaneously, as opposed to
processing them one by one like the Ethereum Virtual Machine (EVM).

## SVM vs EVM (Ethereum Virtual Machine)

While both EVM and SVM perform similar functions, the Solana VM is much more
efficient and faster. On EVM, when a smart contract transfers a dollar from a
userâs balance, this transaction is stored within the specific contract's
storage. This design creates potential issues if the Ethereum Virtual Machine
attempts to process multiple transactions in parallel. For example, two
different smart contracts might simultaneously attempt to spend the userâs
balance, or another contract might read this same userâs balance while it is
in the process of being updated, leading to inconsistencies and conflicts.  
  

![evm-processing-vs-svm-virtual-machine-ethereum-single-threaded-runtime-
ethereum-
congestion](https://framerusercontent.com/images/wM6JMqpBEKltqoNXFc54UHdLnwY.png)

In contrast, the Solana account model separates data, such as userâs
balance, for better organization and efficiency. Transactions on Solana also
require explicit specification of the data they will read and modify before
execution in the SVM. As said earlier, this allows programs that do not
interact with the same data to run concurrently, which helps to alleviate
congestion and reduce high fees. For example, the Solana VM can process Toly
sending one dollar to Raj simultaneously with Armani sending three dollars to
Chase.  
  

![solana-deploy-smart-contract-program-deployment-svm-solana-virtual-machine-
bpf-bytecode-solana-
nodes](https://framerusercontent.com/images/ezYMkGFzDz14s8eq1vntq4qYc.png)

The reason EVM struggles with processing multiple transactions simultaneously
is partly due to it being a "single-threaded" runtime environment, which can
only process one contract at a time. Due to this, the EVM design does not take
advantage of multi-core hardware, which means only one core of the
validatorâs hardware is actively processing transactions, while the other
cores remain underutilized. This often results in network congestion and
higher transaction fees. _However, it is important to note that other factors
than its multi-threaded runtime also contribute to EVM limitations, such as
the desire to maintain low hardware requirements for running nodes._

On the other hand, Sealevel optimizes the performance of the Solana runtime by
enabling efficient use of the available hardware resources. SVM is a multi-
threaded runtime environment, designed to process multiple transactions in
parallel by using all the cores available of the validator machine. This makes
Solana able to scale more effectively as the hardware of its validators
improves over time. The Solana Virtual Machine can also manage transaction
fees in a better way thanks to its architecture. This has led to the
development of [localized fee
markets](https://twitter.com/7LayerMagik/status/1615569374647287808?s=20),
which enable fees to be assigned per smart contract. In contrast, EVM chains
rely on global fee markets, meaning that an NFT mint can affect a swap or DeFi
transaction, even though the transactions are unrelated.  
  

![evm-vs-svm-single-threaded-runtime-ethereum-execution-environment-multi-
threaded-runtime-sealevel-solana-vm-virtual-machine-
crypto](https://framerusercontent.com/images/aad2phZyFLLFgEkZs4R32CKZTYU.png)

For all these reasons, SVM's parallel processing capabilities allow Solana to
achieve significantly higher TPS, resulting in faster transaction speeds, and
with almost invisible fees compared to the EVM architecture. This positions
SVM as a next-generation blockchain environment, far more efficient and
performant. As more developers recognize this, we are starting to see greater
adoption of the SVM as an execution environment for smart contracts, with an
emerging ecosystem of SVM rollups taking shape.

## The Emerging Ecosystem of SVM Rollups

A rollup is a type of blockchain scaling solution that processes transactions
outside of a Layer 1 blockchain (e.g., Solana) and later posts the data to a
Layer 1 retroactively. Rollups aim to reduce network congestion and
transaction fees by bundling multiple transactions together into a single
"proof" that is then submitted to the main chain. The greatest advantage of
building a rollup is the ability to fully customize the chain. This
customization allows for various use cases, such as tailored orderbooks,
encrypted mempools for minimizing MEV (Miner Extractable Value), or
permissioned applications designed to meet specific requirements.

A virtual machine can also be used to simplify the deployment process for
developers on other chains that use the same VM. This network effect has
greatly benefited Ethereum and its VM, since it was the first runtime
environment for crypto smart contracts. As a result, EVM has been the primary
execution environment used for building rollup blockchains. Among the two
types of rollups, Optimistic and Zk, [Optimistic
rollups](https://www.eclipse.builders/documentation/glossary#optimistic-
rollup) such as Arbitrum are the most widespread. Recently, SVM has seen
numerous advancements aimed at bringing the rollup technology to Solana
developers. The main projects building rollups for Solana are
[Nitro](https://www.nitro.technology/) and
[Eclipse](https://www.eclipse.builders/).  
  

![](https://framerusercontent.com/images/Orj1f0PiCDrFtSYqtZkeI0f8Y.png)

Nitro is an Optimistic rollup solution, similar to Arbitrum or Optimism, that
utilizes the Solana Virtual Machine (SVM) to enable Solana developers to port
their dApps to various ecosystems. Nitro plans to launch on Sei first, a
sector-specific trading chain built on Cosmos, before expanding to other
chains. It uses SVM to execute transactions with parallelization, which means
users will be able to perform as they would on Solana, while Nitro using Sei
for settlement and consensus. Furthermore, with Sei being part of the Cosmos
ecosystem, Nitroâs projects and its users will be able to benefit from the
IBC interoperability technology, accessing Cosmos assets and liquidity.

Another SVM rollup solution in development is Eclipse, which aims to
facilitate the deployment of customizable rollups. Eclipse's optimistic
rollups enable projects to create their own distinct app chains while
benefiting from the security of established networks (e.g., Cosmos app-chains,
Polygon, Ethereum) and leveraging the Solana Virtual Machine (SVM). SVM serves
as the execution environment, with Eclipse handling settlement, and consensus
and data availability (DA) managed by the developer's chosen Layer 1 network.
Currently, Eclipse offers Optimistic rollup solutions but is working on
launching zk-rollups as well.  
  

![](https://framerusercontent.com/images/XzKgY1tEkKj3MrmIIqYch6995ds.png)

Eclipse has already announced two rollup solutions built on top of SVM:

  * **Polygon SVM** : With this rollup, any project built on Solana can easily deploy onto the Polygon network;

  * **Cascade** : Introduced by Injective and Eclipse, Cascade is an SVM rollup optimized for the IBC ecosystem. It will allow Solana projects to effortlessly deploy to Cascade and access the assets and liquidity of the Cosmos app-chains. Moreover, projects on Injective can now utilize Cascade's parallelized SVM.

All those solutions are simplifying the usage of the Solana VM and expanding
its reach. Users from other chains will also be able to âtasteâ the Solana
parallelization experience without friction, which could lead to more
realization of the SVM superiority and thus to more projects moving their
dApps to Solana to benefit from its architecture and onboard more users.

## SVM Is A Next-Generation Blockchain Environment for Developers

Despite being only three years old, Solana has already demonstrated impressive
performance, and the development of scaling solutions like Nitro and Eclipse
on top of its VM highlights the success of its innovative execution
architecture. Solana has been able to learn from the challenges faced by older
networks like Bitcoin and Ethereum. Bitcoin wasn't designed for smart
contracts, which led to the emergence of Ethereum. Similarly, Ethereum wasn't
prepared for mass adoption and high-speed transactions, paving the way for
Solana and parallel processing. Moreover, access to the SVM environment is
becoming easier for developers, with Neon Labs bringing in Solidity
compatibility with the Solana runtime, as well as the upcoming [Runtime v2
upgrade](https://twitter.com/0xEdgar/status/1617347877000413184?s=20), which
should enable developers to build SVM-compatible dApps using a plethora of
programming languages such as Move.

It is evident that the Solana VM offers a more advanced environment for
building next-generation applications. The parallel processing of transactions
enables higher throughput, akin to what is possible in traditional finance,
enabling developers to build any kind of product without worrying about speed
limits or fees. Building on a chain with TPS as high as 15 will not bring
crypto to mass adoption. Thanks to SVM and Sealevel, Solana can (already)
handle thousands of transactions without congestion nor noticeable gas fees,
making it a perfect environment for building those new applications. And as
the hardware of validators improves, Solanaâs Sealevel runtime will be able
to process even more transactions in parallel, widening the gap between SVM
and EVM while onboarding more users.

Squads will support the expansion of the Solana Virtual Machine (SVM) and
bring multi-signature (multisig) functionality to the whole SVM ecosystem,
enabling anyone to use the best blockchain execution environment with the best
self-custody experience to manage on-chain assets.  
  

_Acknowledgments: Thanks to Jarry Xiao
(_[_Ellipsis_](https://ellipsislabs.xyz/) _) and Neal Somani
(_[_Eclipse_](https://www.eclipse.builders/) _) for feedback on earlier drafts
of this post._

  

### About Squads

Squads is a crypto company operations platform that simplifies management of
developer, creator, and treasury assets for teams building on Solana and SVM.
Open source, formally verified, immutable, Squads enables teams to secure
their on-chain assets in a multisig and jointly manage them.

**Learn more**

 _Squads:_[_https://squads.so/blog/what-is-
squads_](https://squads.so/blog/what-is-squads) _  
Squads Protocol:_[_https://squads.so/blog/solana-svm-smart-contract-wallet-
infrastructure_](https://squads.so/blog/solana-svm-smart-contract-wallet-
infrastructure) _  
Code:_[_https://github.com/Squads-Protocol/squads-
mpl_](https://github.com/Squads-Protocol/squads-mpl)

  

Continue reading

[![solana-treasury-stablecoins-landscape-solutions-usdc-usdt-usdy-ybx-
diversify-stable-treasury-euroe-vchf-maple-credix-stablecoin-yield-
solana](https://framerusercontent.com/images/0bRVstnkv4oB5BpXjXmmQiSc.png)The
Current Stablecoin Landscape on Solana for Enterprise TreasuryMarch 13,
2024](./stablecoins-overview-solana)[![pyth-token-airdrop-solana-squads-
multisig-pyth-allocation-grant-team-pyth-staking-token-governance-squads-app-
squads-
protocol](https://framerusercontent.com/images/owWa2e8vUVngZkQfEWqZ8xinX0.png)Squads
Receives Allocation of $PYTH TokensFebruary 8, 2024](./pyth-airdrop-
allocation)[![marginfi-solana-lending-protocol-borrow-lend-mrgnlend-solana-
interest-rate-apy-lending-sol-jitosol-
msol](https://framerusercontent.com/images/Mpc9bwmMGA7OcH76Is4QDFyyQg.png)Project
Spotlight: marginfi - A New Borrow/Lend ProtocolAugust 22, 2023](./marginfi-
lending-protocol-solana)

[](../)

All rights reserved

Â© Squads Protocol 2024

Product

[Squads](../)

[Protocol](../protocol)

[Extension](../extension)

[Use Cases](../use-cases)

[Why Multisig](https://squads.so/blog/what-are-multisig-wallets)

Resources

[Github](https://github.com/Squads-Protocol)

[SDK](https://www.npmjs.com/package/@sqds/multisig)

[Documentation](https://docs.squads.so/main/basics/welcome-to-squads)

[Blog](../blog)

[Multisig vs MPC](https://squads.so/blog/mpc-wallets-risks-vs-multisig)

Company

[About](../about)

[Brand assets](../brand-assets)

[Twitter](https://twitter.com/squadsprotocol)

[Discord](https://discord.com/invite/YPXz64TrKs)

[Farcaster](https://warpcast.com/squads)

Legal

[Terms of Service](../legal/terms-of-service)

[Privacy Policy](../legal/privacy-policy)

[Contact us](https://discord.com/invite/YPXz64TrKs)

