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

# EVM vs. SVM: Consensus

Learn the differences in how Ethereum and Solana achieve consensus.

**Table of Contents**

  

Ethereum's original consensus

Ethereum's current consensus

Solana's consensus

Summary

Both Ethereum and Solana are known to use PoS (Proof of Stake) for their
consensus mechanisms. They both generate blocks through validators based on
staking. Although they fundamentally use the same consensus, Ethereum
currently records about 30 TPS (transactions per second), while Solana boasts
4000 TPS. This difference indirectly shows how consensus can significantly
impact block generation speed. This chapter will delve into the differences
between the two chains.

### **Ethereum's original consensus**

Originally, Ethereum adopted the Proof of Work(PoW) method, which is still
used by Bitcoin. After the Merge upgrade in August 2022, Ethereum transitioned
from Proof of Work to Proof of Stake, and now employs PoS as mentioned above.

### **Ethereum's current consensus**

At its core, Ethereum uses PoS, but it specifically employs a consensus
algorithm called Gasper. Gasper is a combination of Casper the Friendly
Finality Gadget (Casper-FFG) and the LMD-GHOST fork choice algorithm. Before
delving into Gasper, it's important to note that Ethereum initially generates
blocks based on the PoW-based Nakamoto consensus. The Nakamoto consensus
follows the Longest Chain Rule, selecting the longest chain in the blockchain
during a fork. Therefore, Ethereum hasn't completely abandoned PoW; it retains
basic block generation under PoW while integrating PoS elements on top.

Casper (Casper-FFG), a part of Gasper, upgrades certain blocks to a
"finalized" state, ensuring network participants are synchronized with the
regular chain. It was initially proposed for the transitional phase from a
PoW-based chain to PoS during the Merge upgrade and now contributes partially
to the larger Gasper algorithm. LMD-GHOST (Latest Message Driven Greediest
Heaviest Observed SubTree) is a fork choice algorithm used to select the most
valid and trustworthy chain among various forks. In case of a fork generating
multiple new blocks, validators vote through attestation messages to determine
which block to append to the existing chain. These attestations follow a path
from the genesis block to the latest block (leaf block), selecting the block
backed by the most recent attestations.

### **Solana's consensus**

What are the corresponding technological components in Solana for each of
Ethereum's consensus algorithms? The answer lies in Tower BFT, which supports
PoS.

First, let's understand BFT and PBFT. BFT is a method for achieving reliable
consensus among nodes in a distributed system, stemming from the 'Byzantine
Generals Problem.' It ensures the system operates correctly even if some nodes
are malicious or unreliable. PBFT is a practical implementation of BFT that
guarantees system finality and consistency by securing agreement on all
transactions among all nodes.

Tower BFT adopts a variant of PBFT, with one fundamental difference: Proof of
History (PoH) acts as a global clock before consensus. In Solana's
implementation, PoH is used as the network clock, arranging the order of
blocks, transactions, and data.

Ethereum often inefficiently updates its entire network state for specific
transactions, and transactions may not be processed sequentially. In contrast,
Solana utilizes PoH (Proof of History) to support PoS. To determine the
cryptographic time between two events, a series of computational steps are
required. For example, consider two photos: one of an apple and another of the
photo being taken. We can infer that the photo of the apple was taken first.
Solana tracks their sequence by adding timestamps to data, ensuring no mix-up
in its structures.

Using PoH, Tower BFT effectively determines the order of blocks, transactions,
and data through timestamp verification. Therefore, validators can
conclusively decide on forks, opting for the chain most trusted by votes.
Ethereum lacks a timestamp concept like PoH for overall state synchronization,
forcing validators to calculate from previous hashes to select a fork.
Conversely, Solana's Tower BFT, based on PoH, effortlessly achieves consensus
without needing full block verification.

Therefore, the comparison can be summarized as follows:

Ethereum | Solana  
---|---  
Proof of Work » Proof of Stake  | Proof of Stake>  
Casper the Friendly Finality Gadget (Casper-FFG)  | Tower BFT + PoH  
LMD-GHOST Fork Choice Rule  |  Tower BFT  
  
### Summary

  * **Ethereum’s Consensus:** PoS based Gasper = Casper the Friendly Finality Gadget (Casper-FFG) + LMD-GHOST Fork Choice Rule
  * **Solana’s Consensus:** PoS based Tower BFT + PoH

EVM TO SVM

[Home](/developers/evm-to-svm)[Next: Accounts](/developers/evm-to-
svm/accounts)

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

