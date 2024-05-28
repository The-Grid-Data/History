Skip to main content

[](/en/)

  * Learn
  * Use
  * Build
  * Participate
  * Research

Search```K`

Languages EN

  1. [Home](/en/)/
  2. [Community](/en/community/)/
  3. [Research](/en/community/research/)

Page last updated: March 14, 2024

On this page

  * How Ethereum research works
  * General research resources
  * Sources of Funding
  * Protocol research
    * Consensus
      * Background reading
      * Recent research
    * Execution
      * Background reading
      * Recent research
  * Client Development
    * Execution Clients
    * Consensus Clients
  * Scaling and performance
    * Layer 2
      * Background reading
      * Recent research
    * Bridges
      * Background reading
      * Recent research
    * Sharding
      * Background reading
      * Recent research
    * Hardware
      * Background reading
      * Recent research
  * Security
    * Cryptography & ZKP
      * Background reading
      * Recent research
    * Wallets
      * Background reading
      * Recent research
  * Community, education and outreach
    * UX/UI
      * Background reading
      * Recent research
    * Economics
      * Background reading
      * Recent research
    * Blockspace and fee markets
      * Background reading
      * Recent research
    * Proof-of-stake incentives
      * Background reading
      * Recent research
    * Liquid staking and derivatives
      * Background reading
      * Recent research
  * Testing
    * Formal verification
      * Background reading
      * Recent research
  * Data science and analytics
    * Background reading
      * Recent research
  * Apps and tooling
    * DeFi
      * Background reading
      * Recent research
    * DAOs
      * Background reading
      * Recent research
    * Developer tools
      * Background reading
      * Recent research
    * Oracles
      * Background reading
      * Recent Research
    * App security
      * Background reading
      * Recent research
    * Technology stack
      * Background reading
      * Recent research

# Active areas of Ethereum research

One of the primary strengths of Ethereum is that an active research and
engineering community are constantly improving it. Many enthusiastic, skilled
people worldwide would like to apply themselves to outstanding issues in
Ethereum, but it is not always easy to find out what those issues are. This
page outlines key active research areas as a rough guide to Ethereum's cutting
edge.

## How Ethereum research works

Ethereum research is open and transparent, embodying principles of
[Decentralized Science (DeSci)(opens in a new
tab)](https://hackernoon.com/desci-decentralized-science-as-our-chance-to-
recover-the-real-science). The culture is to make research tools and outputs
as open and interactive as possible, for example, through executable
notebooks. Ethereum research moves quickly, with new findings posted and
discussed in the open on forums such as [ethresear.ch(opens in a new
tab)](https://ethresear.ch/) rather than reaching the community through
traditional publications after rounds of peer review.

## General research resources

Regardless of the specific topic, there is a wealth of information on Ethereum
research to be found at [ethresear.ch(opens in a new
tab)](https://ethresear.ch) and the [Eth R&D Discord channel(opens in a new
tab)](https://discord.gg/qGpsxSA). These are the primary places where Ethereum
researchers discuss the latest ideas and development opportunities.

This report published in May 2022 by [DelphiDigital(opens in a new
tab)](https://members.delphidigital.io/reports/the-hitchhikers-guide-to-
ethereum) provides a good overview of the Ethereum roadmap.

## Sources of Funding

You can get involved with Ethereum research and get paid for it! For example,
[the Ethereum Foundation](/en/foundation/) recently ran an [Academic Grants
funding round(opens in a new tab)](https://esp.ethereum.foundation/academic-
grants). You can find information on active and upcoming funding opportunities
on [the Ethereum grants page](/en/community/grants/).

## Protocol research

Protocol research is concerned with Ethereum's base layer - the set of rules
defining how nodes connect, communicate, exchange and store Ethereum data and
come to consensus about the state of the blockchain. Protocol research gets
divided into two top-level categories: consensus and execution.

### Consensus

Consensus research is concerned with [Ethereum's proof-of-stake
mechanism](/en/developers/docs/consensus-mechanisms/pos/). Some example
consensus research topics are:

  * identifying and patching vulnerabilities;
  * quantifying cryptoeconomic security;
  * increasing the security or performance of client implementations;
  * and developing light clients.

As well as forward-looking research, some fundamental redesigns of the
protocol, such as single slot finality, are being researched to allow for
significant improvements to Ethereum. Furthermore, the efficiency, safety, and
monitoring of peer-to-peer networking between consensus clients are also
important research topics.

#### Background reading

  * [Introduction to proof-of-stake](/en/developers/docs/consensus-mechanisms/pos/)
  * [Casper-FFG paper(opens in a new tab)](https://arxiv.org/abs/1710.09437)
  * [Casper-FFG explainer(opens in a new tab)](https://arxiv.org/abs/1710.09437)
  * [Gasper paper(opens in a new tab)](https://arxiv.org/abs/2003.03052)

#### Recent research

  * [Ethresear.ch Consensus(opens in a new tab)](https://ethresear.ch/c/consensus/29)
  * [Availability/Finality dilemma(opens in a new tab)](https://arxiv.org/abs/2009.04987)
  * [Single slot finality(opens in a new tab)](https://ethresear.ch/t/a-model-for-cumulative-committee-based-finality/10259)
  * [Proposer-builder separation(opens in a new tab)](https://notes.ethereum.org/@vbuterin/pbs_censorship_resistance)

### Execution

The execution layer is concerned with executing transactions, running the
[Ethereum virtual machine (EVM)](/en/developers/docs/evm/) and generating
execution payloads to pass to the consensus layer. There are many active areas
of research, including:

  * building out light client support;
  * researching gas limits;
  * and incorporating new data structures (e.g. Verkle Tries).

#### Background reading

  * [Introduction to the EVM](/en/developers/docs/evm/)
  * [Ethresear.ch execution layer(opens in a new tab)](https://ethresear.ch/c/execution-layer-research/37)

#### Recent research

  * [Database optimizations(opens in a new tab)](https://github.com/ledgerwatch/erigon/blob/devel/docs/programmers_guide/db_faq.md)
  * [State expiry(opens in a new tab)](https://notes.ethereum.org/@vbuterin/state_expiry_eip)
  * [Paths to state expiry(opens in a new tab)](https://hackmd.io/@vbuterin/state_expiry_paths)
  * [Verkle and state expiry proposal(opens in a new tab)](https://notes.ethereum.org/@vbuterin/verkle_and_state_expiry_proposal)
  * [History management(opens in a new tab)](https://eips.ethereum.org/EIPS/eip-4444)
  * [Verkle Trees(opens in a new tab)](https://vitalik.eth.limo/general/2021/06/18/verkle.html)
  * [Data availability sampling(opens in a new tab)](https://github.com/ethereum/research/wiki/A-note-on-data-availability-and-erasure-coding)

## Client Development

Ethereum clients are implementations of the Ethereum protocol. Client
development makes the outcomes from protocol research into reality by building
them into these clients. Client development includes updating the client
specifications as well as building specific implementations.

An Ethereum node is required to run two pieces of software:

  1. a consensus client to keep track of the head of the blockchain, gossip blocks and handle consensus logic
  2. an execution client to support the Ethereum Virtual Machine and execute transactions and smart contracts

See the [nodes and clients page](/en/developers/docs/nodes-and-clients/) for
more detail on nodes and clients and for a list of all current client
implementations. You can also find a history of all Ethereum upgrades on the
[history page](/en/history/).

### Execution Clients

  * [Execution client specification(opens in a new tab)](https://github.com/ethereum/execution-specs)
  * [Execution API spec(opens in a new tab)](https://github.com/ethereum/execution-apis)

### Consensus Clients

  * [Consensus client specification(opens in a new tab)](https://github.com/ethereum/consensus-specs)
  * [Beacon API specification(opens in a new tab)](https://ethereum.github.io/beacon-APIs/#/Beacon/getStateRoot)

## Scaling and performance

Scaling Ethereum is a large area of focus for Ethereum researchers. Current
approaches include offloading transactions onto rollups and making them as
cheap as possible using data blobs. Introductory information on scaling
Ethereum is available on our [scaling page](/en/developers/docs/scaling/).

### Layer 2

There are now several Layer 2 protocols that scale Ethereum using different
techniques for batching transactions and securing them on Ethereum layer 1.
This is a very rapidly growing topic with a lot of research and development
potential.

#### Background reading

  * [Introduction to layer 2](/en/layer-2/)
  * [Polynya: Rollups, DA and modular chains(opens in a new tab)](https://polynya.medium.com/rollups-data-availability-layers-modular-blockchains-introductory-meta-post-5a1e7a60119d)

#### Recent research

  * [Arbitrum's fair-ordering for sequencers(opens in a new tab)](https://eprint.iacr.org/2021/1465)
  * [ethresear.ch Layer 2(opens in a new tab)](https://ethresear.ch/c/layer-2/32)
  * [Rollup-centric roadmap(opens in a new tab)](https://ethereum-magicians.org/t/a-rollup-centric-ethereum-roadmap/4698)
  * [L2Beat(opens in a new tab)](https://l2beat.com/)

### Bridges

One particular area of layer 2 that requires more research and development is
safe and performant bridges. This includes bridges between various Layer 2s
and bridges between Layer 1 and Layer 2. This is a particularly important area
of research because bridges are commonly targeted by hackers.

#### Background reading

  * [Introduction to blockchain bridges](/en/bridges/)
  * [Vitalik on bridges(opens in a new tab)](https://old.reddit.com/r/ethereum/comments/rwojtk/ama_we_are_the_efs_research_team_pt_7_07_january/hrngyk8/)
  * [Blockchain bridges article(opens in a new tab)](https://medium.com/1kxnetwork/blockchain-bridges-5db6afac44f8)
  * [Value locked in bridges(opens in a new tab)](https://dune.com/eliasimos/Bridge-Away-\(from-Ethereum\))

#### Recent research

  * [Validating bridges(opens in a new tab)](https://stonecoldpat.github.io/images/validatingbridges.pdf)

### Sharding

Sharding Ethereum's blockchain has long been part of the development roadmap.
However, new scaling solutions such as "Danksharding" are currently taking
center stage.

The precursor to full Danksharding known as Proto-Danksharding went live with
the Cancun-Deneb ("Dencun") network upgrade.

[More about the Dencun upgrade](/en/roadmap/dencun/)

#### Background reading

  * [Proto-Danksharding notes(opens in a new tab)](https://notes.ethereum.org/@vbuterin/proto_danksharding_faq)
  * [Bankless Danksharding video(opens in a new tab)](https://www.youtube.com/watch?v=N5p0TB77flM)
  * [Ethereum Sharding Research Compendium(opens in a new tab)](https://notes.ethereum.org/@serenity/H1PGqDhpm?type=view)
  * [Danksharding (Polynya)(opens in a new tab)](https://polynya.medium.com/danksharding-36dc0c8067fe)

#### Recent research

  * [EIP-4844: Proto-Danksharding(opens in a new tab)](https://eips.ethereum.org/EIPS/eip-4844)
  * [Vitalik on sharding and data availability sampling(opens in a new tab)](https://hackmd.io/@vbuterin/sharding_proposal)

### Hardware

[Running nodes](/en/developers/docs/nodes-and-clients/run-a-node/) on modest
hardware is fundamental to keeping Ethereum decentralized. Therefore, active
research into minimizing the hardware requirements to run nodes is an
important area of research.

#### Background reading

  * [Ethereum on ARM(opens in a new tab)](https://ethereum-on-arm-documentation.readthedocs.io/en/latest/)

#### Recent research

  * [ecdsa on FPGAs(opens in a new tab)](https://ethresear.ch/t/does-ecdsa-on-fpga-solve-the-scaling-problem/6738)

## Security

Security is a broad topic that might include spam/scam prevention, wallet
security, hardware security, crypto-economic security, bug hunting and testing
of applications and client software and key-management. Contributing to
knowledge in these areas will help stimulate mainstream adoption.

### Cryptography & ZKP

Zero-knowledge proofs (ZKP) and cryptography are critical for building privacy
and security into Ethereum and its applications. Zero-knowledge is a
relatively young but fast-moving space with many open research and development
opportunities. Some possibilities include developing more efficient
implementations of the [Keccak hashing algorithm(opens in a new
tab)](https://hackmd.io/sK7v0lr8Txi1bgION1rRpw?view#Overview), finding better
polynomial commitments than currently exist or reducing the cost of ecdsa
public key generation and signature verification circuits.

#### Background reading

  * [0xparc blog(opens in a new tab)](https://0xparc.org/blog)
  * [zkp.science(opens in a new tab)](https://zkp.science/)
  * [Zero Knowledge podcast(opens in a new tab)](https://zeroknowledge.fm/)

#### Recent research

  * [Recent advance in elliptic curve cryptography(opens in a new tab)](https://ethresear.ch/t/the-ec-fft-algorithm-without-elliptic-curve-and-isogenies/11346)
  * [Ethresear.ch ZK(opens in a new tab)](https://ethresear.ch/c/zk-s-nt-arks/13)

### Wallets

Ethereum wallets can be browser extensions, desktop and mobile apps or smart
contracts on Ethereum. There is active research into social recovery wallets
that reduce some of the risk associated with individual-user key management.
Associated with development of wallets is research into alternative forms of
account abstraction, which is an important area of nascent research.

#### Background reading

  * [Introduction to wallets](/en/wallets/)
  * [Introduction to wallet security](/en/security/)
  * [ethresear.ch Security(opens in a new tab)](https://ethresear.ch/tag/security)
  * [EIP-2938 Account Abstraction(opens in a new tab)](https://eips.ethereum.org/EIPS/eip-2938)
  * [EIP-4337 Account Abstraction(opens in a new tab)](https://eips.ethereum.org/EIPS/eip-4337)

#### Recent research

  * [Validation focused smart contract wallets(opens in a new tab)](https://ethereum-magicians.org/t/validation-focused-smart-contract-wallets/6603)
  * [The future of accounts(opens in a new tab)](https://ethereum-magicians.org/t/validation-focused-smart-contract-wallets/6603)
  * [EIP-3074 AUTH and AUTHCALL Opcodes(opens in a new tab)](https://eips.ethereum.org/EIPS/eip-3074)
  * [Publishing code at an EOA address(opens in a new tab)](https://eips.ethereum.org/EIPS/eip-5003)

## Community, education and outreach

Onboarding new users onto Ethereum requires new educational resources and
approaches to outreach. This might include blog posts and articles, books,
podcasts, memes, teaching resources, events and anything else that builds
communities, welcomes new starters and educates people about Ethereum.

### UX/UI

To onboard more people onto Ethereum, the ecosystem must improve the UX/UI.
This will require designers and product experts to re-examine the design of
wallets and apps.

#### Background reading

  * [Ethresear.ch UX/UI(opens in a new tab)](https://ethresear.ch/c/ui-ux/24)

#### Recent research

  * [Web3 Design Discord(opens in a new tab)](https://discord.gg/FsCFPMTSm9)
  * [Web3 Design Principles(opens in a new tab)](https://www.web3designprinciples.com/)
  * [Ethereum Magicians UX discussion(opens in a new tab)](https://ethereum-magicians.org/t/og-council-ux-follow-up/9032/3)

### Economics

Economics research in Ethereum broadly follows two approaches: validate the
security of mechanisms relying on economic incentives ("microeconomics") and
analyze the flows of value between protocols, applications and users
("macroeconomics"). There are complex crypto-economic factors relating to
Ethereum's native asset (ether) and the tokens built on top of it (for example
NFTs and ERC20 tokens).

#### Background reading

  * [Robust Incentives Group(opens in a new tab)](https://ethereum.github.io/rig/)
  * [ETHconomics workshop at Devconnect(opens in a new tab)](https://www.youtube.com/playlist?list=PLTLjFJ0OQOj5PHRvA2snoOKt2udVsyXEm)

#### Recent research

  * [Empirical analysis of EIP1559(opens in a new tab)](https://arxiv.org/abs/2201.05574)
  * [Circulating supply equilibrium(opens in a new tab)](https://ethresear.ch/t/circulating-supply-equilibrium-for-ethereum-and-minimum-viable-issuance-during-the-proof-of-stake-era/10954)
  * [Quantifying MEV: How dark is the forest?(opens in a new tab)](https://arxiv.org/abs/2101.05511)

### Blockspace and fee markets

Blockspace markets govern the inclusion of end-user transactions, either
directly on Ethereum (Layer 1) or on bridged networks, e.g., rollups (Layer
2). On Ethereum, transactions are submitted to the fee market deployed in-
protocol as EIP-1559, protecting the chain from spam and pricing congestion.
On both layers, transactions may produce externalities, known as Maximal
Extractable Value (MEV), which induce new market structures to capture or
manage these externalities.

#### Background reading

  * [Transaction Fee Mechanism Design for the Ethereum Blockchain: An Economic Analysis of EIP-1559 (Tim Roughgarden, 2020)(opens in a new tab)](https://timroughgarden.org/papers/eip1559.pdf)
  * [Simulations of EIP-1559 (Robust Incentives Group)(opens in a new tab)](https://ethereum.github.io/abm1559)
  * [Rollup economics from first principles(opens in a new tab)](https://barnabe.substack.com/p/understanding-rollup-economics-from?utm_source=url)
  * [Flash Boys 2.0: Frontrunning, Transaction Reordering, and Consensus Instability in Decentralized Exchanges(opens in a new tab)](https://arxiv.org/abs/1904.05234)

#### Recent research

  * [Multidimensional EIP-1559 video presentation(opens in a new tab)](https://youtu.be/QbR4MTgnCko)
  * [Cross domain MEV(opens in a new tab)](http://arxiv.org/abs/2112.01472)
  * [MEV auctions(opens in a new tab)](https://ethresear.ch/t/mev-auction-auctioning-transaction-ordering-rights-as-a-solution-to-miner-extractable-value/6788)

### Proof-of-stake incentives

Validators use Ethereum's native asset (ether) as collateral against dishonest
behavior. The cryptoeconomics of this determines the security of the network.
Sophisticated validators may be able to exploit the nuances of the incentive
layer to launch explicit attacks.

#### Background reading

  * [Ethereum economics masterclass and economic model(opens in a new tab)](https://github.com/CADLabs/ethereum-economic-model)
  * [Simulations of PoS incentives (Robust Incentives Group)(opens in a new tab)](https://ethereum.github.io/beaconrunner/)

#### Recent research

  * [Increasing censorship resistance of transactions under proposer/builder separation (PBS)(opens in a new tab)](https://notes.ethereum.org/s3JToeApTx6CKLJt8AbhFQ)
  * [Three Attacks on PoS Ethereum(opens in a new tab)](https://arxiv.org/abs/2110.10086)

### Liquid staking and derivatives

Liquid staking allows users with less than 32 ETH to receive staking yields by
swapping ether for a token representing staked ether that can be used in DeFi.
However, the incentives and market dynamics associated with liquid staking are
still being discovered, as well as its effect on Ethereum's security (e.g.
centralization risks).

#### Background reading

  * [Ethresear.ch liquid staking(opens in a new tab)](https://ethresear.ch/search?q=liquid%20staking)
  * [Lido: The road to trustless Ethereum staking(opens in a new tab)](https://blog.lido.fi/the-road-to-trustless-ethereum-staking/)
  * [Rocket Pool: Staking protocol introduction(opens in a new tab)](https://medium.com/rocket-pool/rocket-pool-staking-protocol-part-1-8be4859e5fbd)

#### Recent research

  * [Handling withdrawals from Lido(opens in a new tab)](https://ethresear.ch/t/handling-withdrawals-in-lidos-eth-liquid-staking-protocol/8873)
  * [Withdrawal credentials(opens in a new tab)](https://ethresear.ch/t/withdrawal-credential-rotation-from-bls-to-eth1/8722)
  * [The risks of Liquid Staking Derivatives(opens in a new tab)](https://notes.ethereum.org/@djrtwo/risks-of-lsd)

## Testing

### Formal verification

Formal verification is writing code to verify that Ethereum's consensus
specifications are correct and bug-free. There is an executable version of the
specification written in Python that requires maintenance and development.
Further research can help to improve the Python implementation of the
specification and add tools that can more robustly verify correctness and
identify issues.

#### Background reading

  * [Introduction to formal verification(opens in a new tab)](https://ptolemy.berkeley.edu/projects/embedded/research/vis/doc/VisUser/vis_user/node4.html)
  * [Formal Verification (Intel)(opens in a new tab)](https://www.cl.cam.ac.uk/~jrh13/papers/mark10.pdf)

#### Recent research

  * [Formal verification of the deposit contract(opens in a new tab)](https://github.com/runtimeverification/deposit-contract-verification)
  * [Formal verification of the Beacon Chain specification(opens in a new tab)](https://github.com/runtimeverification/deposit-contract-verification)

## Data science and analytics

There is a need for more data analysis tools and dashboards that give detailed
information about activity on Ethereum and the health of the network.

### Background reading

  * [Dune Analytics(opens in a new tab)](https://dune.com/browse/dashboards)
  * [Client diversity dashboard(opens in a new tab)](https://clientdiversity.org/)

#### Recent research

  * [Robust Incentives Group Data Analysis(opens in a new tab)](https://ethereum.github.io/rig/)

## Apps and tooling

The application layer supports a diverse ecosystem of programs that settle
transactions on Ethereum's base layer. Development teams are constantly
finding new ways to leverage Ethereum to create composable, permissionless and
censorship-resistant versions of important Web2 apps or create completely new
Web3-native concepts. At the same time, new tooling is being developed that
makes building dapps on Ethereum less complex.

### DeFi

Decentralized finance (DeFi) is one of the primary classes of application
built on top of Ethereum. DeFi aims to create composable "money legos" that
allow users to store, transfer, lend, borrow and invest crypto-assets using
smart contracts. DeFi is a fast-moving space that is constantly updating.
Research into secure, efficient and accessible protocols is continuously
needed.

#### Background reading

  * [DeFi](/en/defi/)
  * [Coinbase: What is DeFi?(opens in a new tab)](https://www.coinbase.com/learn/crypto-basics/what-is-defi)

#### Recent research

  * [Decentralized finance, centralized ownership?(opens in a new tab)](https://arxiv.org/pdf/2012.09306.pdf)
  * [Optimism: The road to sub-dollar transactions(opens in a new tab)](https://medium.com/ethereum-optimism/the-road-to-sub-dollar-transactions-part-2-compression-edition-6bb2890e3e92)

### DAOs

An impactful use case for Ethereum is the ability to organize in a
decentralized manner through the use of DAOs. There is a lot of active
research into how DAOs on Ethereum can be developed and utilized to execute
improved forms of governance, as a trust-minimized coordination tool, greatly
expanding peoples options beyond traditional corporations and organizations.

#### Background reading

  * [Introduction to DAOs](/en/dao/)
  * [Dao Collective(opens in a new tab)](https://daocollective.xyz/)

#### Recent research

  * [Mapping the DAO ecosystem(opens in a new tab)](https://www.researchgate.net/publication/358694594_Mapping_out_the_DAO_Ecosystem_and_Assessing_DAO_Autonomy)

### Developer tools

Tools for Ethereum developers are rapidly improving. There is lots of active
research and development to do in this general area.

#### Background reading

  * [Tooling by programming language](/en/developers/docs/programming-languages/)
  * [Developer Frameworks](/en/developers/docs/frameworks/)
  * [Consensus developer tools list(opens in a new tab)](https://github.com/ConsenSys/ethereum-developer-tools-list)
  * [Token standards](/en/developers/docs/standards/tokens/)
  * [CryptoDevHub: EVM Tools(opens in a new tab)](https://cryptodevhub.io/wiki/ethereum-virtual-machine-tools)

#### Recent research

  * [Eth R&D Discord Consensus Tooling channel(opens in a new tab)](https://discordapp.com/channels/595666850260713488/746343380900118528)

### Oracles

Oracles import off-chain data onto the blockchain in a permissionless and
decentralized way. Getting this data on-chain enables dapps to be reactive to
real-world phenomena such as price fluctuations in real-world assets, events
in off-chain apps, or even changes in the weather.

#### Background reading

  * [Introduction to Oracles](/en/developers/docs/oracles/)

#### Recent Research

  * [Survey of blockchain oracles(opens in a new tab)](https://arxiv.org/pdf/2004.07140.pdf)
  * [Chainlink white paper(opens in a new tab)](https://chain.link/whitepaper)

### App security

Hacks on Ethereum generally exploit vulnerabilities in individual applications
rather than in the protocol itself. Hackers and app developers are locked in
an arms race to develop new attacks and defenses. This means there is always
important research and development required to keep apps safe from hacks.

#### Background reading

  * [Wormhole exploit report(opens in a new tab)](https://blog.chainalysis.com/reports/wormhole-hack-february-2022/)
  * [List of Ethereum contract hack post-mortems(opens in a new tab)](https://forum.openzeppelin.com/t/list-of-ethereum-smart-contracts-post-mortems/1191)
  * [Rekt News(opens in a new tab)](https://twitter.com/RektHQ?s=20&t=3otjYQdM9Bqk8k3n1a1Adg)

#### Recent research

  * [ethresear.ch Applications(opens in a new tab)](https://ethresear.ch/c/applications/18)

### Technology stack

Decentralizing the entire Ethereum tech stack is an important research area.
Currently, dapps on Ethereum commonly have some points of centralization
because they rely on centralized tooling or infrastructure.

#### Background reading

  * [Ethereum stack](/en/developers/docs/ethereum-stack/)
  * [Coinbase: Intro to Web3 Stack(opens in a new tab)](https://blog.coinbase.com/a-simple-guide-to-the-web3-stack-785240e557f0)
  * [Introduction to smart contracts](/en/developers/docs/smart-contracts/)
  * [Introduction to decentralized storage](/en/developers/docs/storage/)

#### Recent research

  * [Smart contract composability](/en/developers/docs/smart-contracts/composability/)

### Was this article helpful?

YesNo

  * [Edit page(opens in a new tab)](https://github.com/ethereum/ethereum-org-website/tree/dev/public/content/community/research/index.md)
  * On this page

    * How Ethereum research works
    * General research resources
    * Sources of Funding
    * Protocol research
      * Consensus
        * Background reading
        * Recent research
      * Execution
        * Background reading
        * Recent research
    * Client Development
      * Execution Clients
      * Consensus Clients
    * Scaling and performance
      * Layer 2
        * Background reading
        * Recent research
      * Bridges
        * Background reading
        * Recent research
      * Sharding
        * Background reading
        * Recent research
      * Hardware
        * Background reading
        * Recent research
    * Security
      * Cryptography & ZKP
        * Background reading
        * Recent research
      * Wallets
        * Background reading
        * Recent research
    * Community, education and outreach
      * UX/UI
        * Background reading
        * Recent research
      * Economics
        * Background reading
        * Recent research
      * Blockspace and fee markets
        * Background reading
        * Recent research
      * Proof-of-stake incentives
        * Background reading
        * Recent research
      * Liquid staking and derivatives
        * Background reading
        * Recent research
    * Testing
      * Formal verification
        * Background reading
        * Recent research
    * Data science and analytics
      * Background reading
        * Recent research
    * Apps and tooling
      * DeFi
        * Background reading
        * Recent research
      * DAOs
        * Background reading
        * Recent research
      * Developer tools
        * Background reading
        * Recent research
      * Oracles
        * Background reading
        * Recent Research
      * App security
        * Background reading
        * Recent research
      * Technology stack
        * Background reading
        * Recent research

Website last updated: May 22, 2024

[(opens in a new tab)](https://github.com/ethereum/ethereum-org-
website)[(opens in a new tab)](https://twitter.com/ethdotorg)[(opens in a new
tab)](https://discord.gg/ethereum-org)

### Learn

  * [Learn Hub](/en/learn/)
  * [What is Ethereum?](/en/what-is-ethereum/)
  * [What is ether (ETH)?](/en/eth/)
  * [Ethereum wallets](/en/wallets/)
  * [What is Web3?](/en/web3/)
  * [Smart contracts](/en/smart-contracts/)
  * [Gas fees](/en/gas/)
  * [Run a node](/en/run-a-node/)
  * [Ethereum security and scam prevention](/en/security/)
  * [Quiz Hub](/en/quizzes/)
  * [Ethereum glossary](/en/glossary/)

### Use

  * [Guides](/en/guides/)
  * [Choose your wallet](/en/wallets/find-wallet/)
  * [Get ETH](/en/get-eth/)
  * [Dapps - Decentralized applications](/en/dapps/)
  * [Stablecoins](/en/stablecoins/)
  * [NFTs - Non-fungible tokens](/en/nft/)
  * [DeFi - Decentralized finance](/en/defi/)
  * [DAOs - Decentralized autonomous organizations](/en/dao/)
  * [Decentralized identity](/en/decentralized-identity/)
  * [Stake ETH](/en/staking/)
  * [Layer 2](/en/layer-2/)

### Build

  * [Builder's home](/en/developers/)
  * [Tutorials](/en/developers/tutorials/)
  * [Documentation](/en/developers/docs/)
  * [Learn by coding](/en/developers/learning-tools/)
  * [Set up local environment](/en/developers/local-environment/)
  * [Grants](/en/community/grants/)
  * [Foundational topics](/en/developers/docs/intro-to-ethereum/)
  * [UX/UI design fundamentals](/en/developers/docs/design-and-ux/)
  * [Enterprise - Mainnet Ethereum](/en/enterprise/)
  * [Enterprise - Private Ethereum](/en/enterprise/private-ethereum/)

### Participate

  * [Community hub](/en/community/)
  * [Online communities](/en/community/online/)
  * [Ethereum events](/en/community/events/)
  * [Contributing to ethereum.org](/en/contributing/)
  * [Translation Program](/en/contributing/translation-program/)
  * [Ethereum bug bounty program](/en/bug-bounty/)
  * [Ethereum Foundation](/en/foundation/)
  * [Ethereum Foundation Blog(opens in a new tab)](https://blog.ethereum.org/)
  * [Ecosystem Support Program(opens in a new tab)](https://esp.ethereum.foundation)
  * [Devcon(opens in a new tab)](https://devcon.org/)

### Research

  * [Ethereum Whitepaper](/en/whitepaper/)
  * [Ethereum roadmap](/en/roadmap/)
  * [Improved security](/en/roadmap/security/)
  * [Technical history of Ethereum](/en/history/)
  * [Open research](/en/community/research/)
  * [Ethereum Improvement Proposals](/en/eips/)
  * [Ethereum governance](/en/governance/)

  * [About us](/en/about/)
  * [Ethereum brand assets](/en/assets/)
  * [Code of conduct](/en/community/code-of-conduct/)
  * [Jobs](/en/about/#open-jobs)
  * [Privacy policy](/en/privacy-policy/)
  * [Terms of use](/en/terms-of-use/)
  * [Cookie policy](/en/cookie-policy/)
  * [Press Contact(opens in a new tab)](mailto:press@ethereum.org)

Is this page helpful?

