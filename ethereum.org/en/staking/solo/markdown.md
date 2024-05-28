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
  2. [Staking](/en/staking/)/
  3. [Solo staking](/en/staking/solo/)

# Solo stake your ETH

  * Receive maximum rewards directly from the protocol for keeping your validator properly functioning and online
  * Run home hardware and personally add to the security and decentralization of the Ethereum network
  * Remove trust, and never give up control of the keys to your funds

On this page

  * What is solo staking?
  * Why stake solo?
  * Considerations before staking solo
  * How it works
  * Get started on the Staking Launchpad
  * What to consider with node and client setup tools
  * Explore node and client setup tools
    * Node tools
    * Key Generators
  * Explore solo staking guides
  * Frequently asked questions
  * Further reading

![Leslie the rhino on her own computer
chip.](/_next/image/?url=%2Fstaking%2Fleslie-solo.png&w=828&q=75)

Staking Options

[Staking home](/en/staking/)[Solo staking](/en/staking/solo/)[Staking as a
service](/en/staking/saas/)[Pooled staking](/en/staking/pools/)[About
withdrawals](/en/staking/withdrawals/)

## On this page

  * What is solo staking?
  * Why stake solo?
  * Considerations before staking solo
  * How it works
  * Get started on the Staking Launchpad
  * What to consider with node and client setup tools
  * Explore node and client setup tools
  * Explore solo staking guides
  * Frequently asked questions
  * Further reading

## What is solo staking?

Solo staking is the act of [running an Ethereum node](/en/run-a-node/)
connected to the internet and depositing 32 ETH to activate a validator,
giving you the ability to participate directly in network consensus.

**Solo staking increases the decentralization of the Ethereum network** ,
making Ethereum more censorship-resistant and robust against attacks. Other
staking methods may not help the network in the same ways. Solo staking is the
best staking option for securing Ethereum.

An Ethereum node consists of both an execution layer (EL) client, as well as a
consensus layer (CL) client. These clients are software that work together,
along with a valid set of signing keys, to verify transactions and blocks,
attest to the correct head of the chain, aggregate attestations, and propose
blocks.

Solo stakers are responsible for operating the hardware needed to run these
clients. It is highly recommended to use a dedicated machine for this that you
operate from home–this is extremely beneficial to the health of the network.

A solo staker receives rewards directly from the protocol for keeping their
validator properly functioning and online.

## Why stake solo?

Solo staking comes with more responsibility but provides you with maximum
control over your funds and staking setup.

![💸](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4b8.svg)

### Earn fresh ETH

Earn ETH-denominated rewards directly from the protocol when your validator is
online, without any middlemen taking a cut.

![🎛️](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f39b.svg)

### Full control

Keep your own keys. Choose the combination of clients and hardware that allows
you to minimize your risk and best contribute to the health and security of
the network. Third-party staking services make these decisions for you, and
they don't always make the safest choices.

![🔐](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f510.svg)

### Network security

Solo staking is the most impactful way to stake. By running a validator on
your own hardware at home, you strengthen the robustness, decentralization,
and security of the Ethereum protocol.

## Considerations before staking solo

As much as we wish that solo staking was accessible and risk free to everyone,
this is not reality. There are some practical and serious considerations to
keep in mind before choosing to solo stake your ETH.

###

Required reading

More

When operating your own node you should spend some time learning how to use
the software you've chosen. This involves reading relevant documentation and
being attune to communication channels of those dev teams.

The more you understand about the software you're running and how proof-of-
stake works, the less risky it will be as a staker, and the easier it will be
to fix any issues that may arise along the way as a node operator.

###

Comfortable with computers

More

Node setup requires a reasonable comfort level when working with computers,
although new tools are making this easier over time. Understanding of the
command-line interface is helpful, but no longer strictly required.

It also requires very basic hardware setup, and some understanding of minimum
recommended specs.

###

Secure key management

More

Just like how private keys secure your Ethereum address, you will need to
generate keys specifically for your validator. You must understand how to keep
any seed phrases or private keys safe and secure. [Ethereum security and scam
prevention](/en/security/)

###

Maintenance

More

Hardware occasionally fails, network connections error out, and client
software occasionally needs upgrading. Node maintenance is inevitable and will
occasionally require your attention. You'll want to be sure you stay aware of
any anticipated network upgrades, or other critical client upgrades.

###

Reliable uptime

More

Your rewards are proportional to the time your validator is online and
properly attesting. Downtime incurs penalties proportional to how many other
validators are offline at the same time, but does not result in slashing.
Bandwidth also matters, as rewards are decreased for attestations that are not
received in time. Requirements will vary, but a minimum of 10 Mb/s up and down
is recommended.

###

Slashing risk

More

Different from inactivity penalties for being offline, _slashing_ is a much
more serious penalty reserved for malicious offenses. By running a minority
client with your keys loaded on only one machine at time, your risk of being
slashed is minimized. That being said, all stakers must be aware of the risks
of slashing.[ More on slashing and validator lifecycle(opens in a new
tab)](https://medium.com/prysmatic-labs/eth2-slashing-prevention-
tips-f6faa5025f50/)

## Comparison with other options

### Staking as a service (SaaS)

With SaaS providers you're still required to deposit 32 ETH, but don't have to
run hardware. You typically maintain access to your validator keys, but also
need to share your signing keys so the operator can act on behalf of your
validator. This introduces a layer of trust not present when running your own
hardware, and unlike solo staking at home, SaaS does not help as much with
geographic distribution of nodes. If you're uncomfortable operating hardware
but still looking to stake 32 ETH, using a SaaS provider may be a good option
for you.

[Learn more about staking as a service](/en/staking/saas/)

### Pooled staking

Solo staking is significantly more involved than staking with a pooling
service, but offers full access to ETH rewards, and full control over the
setup and security of your validator. Pooled staking has a significantly lower
barrier to entry. Users can stake small amounts of ETH, are not required to
generate validator keys, and have no hardware requirements beyond a standard
internet connection. Liquidity tokens enable the ability to exit from staking
before this is enabled at the protocol level. If you're interested in these
features, pooled staking may be a good fit.

[Learn more about pooled staking](/en/staking/pools/)

## How it works

  1. Get some hardware: You need to [run a node](/en/run-a-node/) to stake

  2. Sync an execution layer client

  3. Sync a consensus layer client

  4. Generate your keys and load them into your validator client

  5. Monitor and maintain your node

![](/_next/image/?url=%2F_next%2Fstatic%2Fmedia%2Fhackathon_transparent.0818b178.png&w=828&q=75)

While active you will earn ETH rewards, which will be periodically deposited
into your withdrawal address.

If ever desired, you can exit as a validator which eliminates the requirement
to be online, and stops any further rewards. Your remaining balance will then
be withdrawn to the withdrawal address that you designate during setup.

[More on staking withdrawals](/en/staking/withdrawals/)

## Get started on the Staking Launchpad

The Staking Launchpad is an open source application that will help you become
a staker. It will guide you through choosing your clients, generate your keys
and depositing your ETH to the staking deposit contract. A checklist is
provided to make sure you've covered everything to get your validator set up
safely.

Choose network

Goerli testnet

Solo validators are expected to **test their setup** and operational skills on
the Goerli testnet before risking funds. Remember it is important to choose a
[minority client](/en/developers/docs/nodes-and-clients/client-diversity/) as
it improves the security of the network and limits your risk.

If you're comfortable with it, you can set up everything needed from the
command line using the Staking Launchpad alone.

[Start staking on Goerli testnet(opens in a new
tab)](https://goerli.launchpad.ethereum.org)

To make things easier, check out some of the tools and guides below that can
help you alongside the Staking Launchpad to get your clients set up with ease.

Software tools and guide

## What to consider with node and client setup tools

There are a growing number of tools and services to help you solo stake your
ETH, but each come with different risks and benefits.

Attribute indicators are used below to signal notable strengths or weaknesses
a listed staking tool may have. Use this section as a reference for how we
define these attributes while you’re choosing what tools to help with your
staking journey.

Staking Considerations

Open sourceAuditedBug bountyBattle testedTrustlessPermissionlessMulti-
clientSelf custodyEconomical

  * Open source
  * Audited
  * Bug bounty
  * Battle tested
  * Trustless
  * Permissionless
  * Multi-client
  * Self custody
  * Economical

### Open source

Essential code is 100% open source and available to the public to fork and use

Open source

Closed source

## Explore node and client setup tools

There are a variety of options available to help you with your setup. Use the
above indicators to help guide you through the tools below.

![⚠️](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/26a0.svg)

Products and services are listed as a convenience for the Ethereum community.
Inclusion of a product or service **does not represent an endorsement** from
the ethereum.org website team, or the Ethereum Foundation.

### Node tools

#### Rocket Pool CLI

From 10.4 ETH

LinuxmacOSWindowsCLI

Open source

Audited

Bug bounty

Battle tested

Trustless

Permissionless

Multi-client

Self custody

Economical

[Get started(opens in a new tab)](https://rocketpool.net/node-operators)

#### Avado

From 10.4 ETH

BrowserGUI

Open source

Audited

Bug bounty

Battle tested

Trustless

Permissionless

Multi-client

Self custody

Economical

[Get started(opens in a new tab)](https://ava.do/)

#### DAppNode

From 10.4 ETH

BrowserGUI

Open source

Audited

Bug bounty

Battle tested

Trustless

Permissionless

Multi-client

Self custody

Economical

[Get started(opens in a new tab)](https://dappnode.io)

#### Stereum

From 32 ETH

LinuxmacOSWindowsGUI

Open source

Audited

Bug bounty

Battle tested

Trustless

Permissionless

Multi-client

Self custody

Economical

[Get started(opens in a new tab)](https://stereum.net/ethereum-node-setup/)

#### eth-docker

From 32 ETH

LinuxCLI

Open source

Audited

Bug bounty

Battle tested

Trustless

Permissionless

Multi-client

Self custody

Economical

[Get started(opens in a new tab)](https://eth-docker.net)

#### Vouch + Dirk

From 32 ETH

LinuxWindowsCLI

Open source

Audited

Bug bounty

Battle tested

Trustless

Permissionless

Multi-client

Self custody

Economical

[Get started(opens in a new tab)](https://www.attestant.io/posts/introducing-
vouch/)

#### Ethereum on Arm

From 32 ETH

LinuxCLI

Open source

Audited

Bug bounty

Battle tested

Trustless

Permissionless

Multi-client

Self custody

Economical

[Get started(opens in a new tab)](https://ethereum-on-arm-
documentation.readthedocs.io/)

#### Launchnodes

From 32 ETH

LinuxmacOSWindowsCLIAWSAzure

Open source

Audited

Bug bounty

Battle tested

Trustless

Permissionless

Multi-client

Self custody

Economical

[Get started(opens in a new tab)](https://launchnodes.com/)

Please note the importance of choosing a [minority
client](/en/developers/docs/nodes-and-clients/client-diversity/) as it
improves the security of the network, and limits your risk. Tools that allow
you to setup minority client are denoted as _"multi-client."_

### Key Generators

These tools can be used as an alternative to the [Staking Deposit CLI(opens in
a new tab)](https://github.com/ethereum/staking-deposit-cli/) to help with key
generation.

#### Wagyu Key Gen

LinuxmacOSWindowsGUI

Open source

Audited

Bug bounty

Battle tested

Permissionless

Self custody

[Get started(opens in a new tab)](https://wagyu.gg/)

#### ethdo

LinuxWindowsCLI

Open source

Audited

Bug bounty

Battle tested

Permissionless

Self custody

[Get started(opens in a new tab)](https://github.com/wealdtech/ethdo)

#### Avado

BrowserGUI

Open source

Audited

Bug bounty

Battle tested

Permissionless

Self custody

[Get started(opens in a new tab)](https://ava.do/)

Have a suggestion for a staking tool we missed? Check out our [product listing
policy](/en/contributing/adding-staking-products/) to see if it would be a
good fit, and to submit it for review.

## Explore solo staking guides

[CoinCashew's Ethereum 2.0 Guide(opens in a new
tab)](https://www.coincashew.com/coins/overview-eth/guide-or-how-to-setup-a-
validator-on-eth2-mainnet)

Linux (CLI)

↗

[Somer Esat(opens in a new tab)](https://github.com/SomerEsat/ethereum-
staking-guide)

Linux (CLI)

↗

[Rocket Pool Node Operators(opens in a new tab)](https://rocketpool.net/node-
operators)

Linux, macOS (CLI)

↗

## Frequently asked questions

These are a few of the most common questions about staking that are worth
knowing about.

###

What is a validator?

More

A _validator_ is a virtual entity that lives on Ethereum and participates in
the consensus of the Ethereum protocol. Validators are represented by a
balance, public key, and other properties. A _validator client_ is the
software that acts on behalf of the validator by holding and using its private
key. A single validator client can hold many key pairs, controlling many
validators.

###

Can I deposit more than 32 ETH?

More

Each key-pair associated with a validator requires exactly 32 ETH to be
activated. More ETH deposited to a single set of keys does not increase
rewards potential, as each validator is limited to an [effective balance(opens
in a new tab)](https://www.attestant.io/posts/understanding-validator-
effective-balance/) of 32 ETH. This means that staking is done in 32 ETH
increments, each with it's own set of keys and balance.

Do not deposit more than 32 ETH for a single validator. It will not increase
your rewards. If a withdrawal address has been set for the validator, excess
funds over 32 ETH will be automatically withdrawn to this address during the
next [validator sweep](/en/staking/withdrawals/#validator-sweeping).

If solo staking seems too demanding for you, consider using a [staking-as-a-
service](/en/staking/saas/) provider, or if you're working with less than 32
ETH, check out the [staking pools](/en/staking/pools/).

###

Will I be slashed if I go offline? (tldr: No.)

More

Going offline when the network is finalizing properly will NOT result in
slashing. Small _inactivity penalties_ are incurred if your validator is not
available to attest for a given epoch (each 6.4 minutes long), but this is
very different to _slashing_. These penalties are slightly less than the
reward you would have earned had the validator been available to attest, and
losses can be earned back with approximately an equal amount of time back
online again.

Note that penalties for inactivity are proportional to how many validators are
offline at the same time. In cases where a large portion of the network is all
offline at once, the penalties for each of these validators will be greater
than when a single validator is unavailable.

In extreme cases if the network stops finalizing as a result of more than a
third of the validators being offline, these users will suffer what is known
as a _quadratic inactivity leak_ , which is an exponential drain of ETH from
offline validator accounts. This enables the network to eventually self-heal
by burning the ETH of inactive validators until their balance reaches 16 ETH,
at which point they will be automatically ejected from the validator pool. The
remaining online validators will eventually comprise over 2/3 the network
again, satisfying the supermajority needed to once again finalize the chain.

###

How do I ensure I don't get slashed?

More

In short, this can never be fully guaranteed, but if you act in good faith,
run a minority client and only keep your signing keys on one machine at a
time, the risk of getting slashed is nearly zero.

There are only a few specific ways that can result in a validator getting
slashed and ejected from the network. At time of writing, the slashings that
have occurred have been exclusively a product of redundant hardware setups
where signing keys are stored on two separate machines at once. This can
inadvertently result in a _double vote_ from your keys, which is a slashable
offense.

Running a supermajority client (any client used by over 2/3 the network) also
holds the risk of potential slashing in the event this client has a bug that
results in a chain fork. This can result in a faulty fork that gets finalized.
To correct back to the intended chain would require submitting a _surround
vote_ by trying to undo a finalized block. This is also a slashable offense
and can be avoided simply by running a minority client instead.

Equivalent bugs in a _minority client would never finalize_ and thus would
never result in a surround vote, and would simply result in inactivity
penalties, _not slashing_.

  * [Learn more about the importance of running a minority client.(opens in a new tab)](https://hackernoon.com/ethereums-client-diversity-problem)
  * [Learn more about slashing prevention(opens in a new tab)](https://medium.com/prysmatic-labs/eth2-slashing-prevention-tips-f6faa5025f50)

###

Which client is best?

More

Individual clients may vary slightly in terms of performance and user
interface, as each are developed by different teams using a variety of
programming languages. That being said, none of them are "best." All
production clients are excellent pieces of software, that all perform the same
core functions to sync and interact with the blockchain.

Since all production clients provide the same basic functionality, it is
actually very important that you choose a **minority client** , meaning any
client that is NOT currently being used by a majority of validators on the
network. This may sound counterintuitive, but running a majority or
supermajority client puts you at an increased risk of slashing in the event of
a bug in that client. Running a minority client drastically limits these
risks.

[Learn more about why client diversity is critical(opens in a new
tab)](https://mirror.xyz/jmcook.eth/S7ONEka_0RgtKTZ3-dakPmAHQNPvuj15nh0YGKPFriA)

###

Can I just use a VPS (virtual private server)?

More

Although a virtual private server (VPS) can be used as a replacement to home
hardware, the physical access and location of your validator client _does
matter_. Centralized cloud solutions such as Amazon Web Services or Digital
Ocean allow the convenience of not having to obtain and operate hardware, at
the expense of centralizing the network.

The more validator clients running on a single centralized cloud storage
solution, the more dangerous it becomes for these users. Any event that takes
these providers offline, whether by an attack, regulatory demands, or just
power/internet outages, will result in every validator client that relies on
this server to go offline at the same time.

Offline penalties are proportional to how many others are offline at the same
time. Using a VPS greatly increases the risk that offline penalties will be
more severe, and increases your risk of quadratic leaking or slashing in the
event the outage is large enough. To minimize your own risk, and the risk to
the network, users are strongly encouraged to obtain and operate their own
hardware.

###

How do I unlock my rewards or get my ETH back?

More

Withdrawals of any kind from the Beacon Chain require withdrawal credentials
to be set.

New stakers set this at time of key generation and deposit. Existing stakers
who did not already set this can upgrade their keys to support this
functionality.

Once withdrawal credentials are set, reward payments (accumulated ETH over the
initial 32) will be periodically distributed to the withdrawal address
automatically.

To unlock and receive your entire balance back you must also complete the
process of exiting your validator.

[More on staking withdrawals](/en/staking/withdrawals/)

## Further reading

  * [The Ethereum Staking Directory(opens in a new tab)](https://www.staking.directory/) \- _Eridian and Spacesider_
  * [Ethereum's Client Diversity Problem(opens in a new tab)](https://hackernoon.com/ethereums-client-diversity-problem) \- _@emmanuelawosika 2022_
  * [Helping Client Diversity(opens in a new tab)](https://www.attestant.io/posts/helping-client-diversity/) \- _Jim McDonald 2022_
  * [Client diversity on Ethereum's consensus layer(opens in a new tab)](https://mirror.xyz/jmcook.eth/S7ONEka_0RgtKTZ3-dakPmAHQNPvuj15nh0YGKPFriA) \- _jmcook.eth 2022_
  * [How To: Shop For Ethereum Validator Hardware(opens in a new tab)](https://www.youtube.com/watch?v=C2wwu1IlhDc) \- _EthStaker 2022_
  * [Step by Step: How to join the Ethereum 2.0 Testnet(opens in a new tab)](https://kb.beaconcha.in/guides/tutorial-eth2-multiclient) \- _Butta_
  * [Eth2 Slashing Prevention Tips(opens in a new tab)](https://medium.com/prysmatic-labs/eth2-slashing-prevention-tips-f6faa5025f50) \- _Raul Jordan 2020_

## Test your Ethereum knowledge

Solo staking

Question number 1:What happens if a validator goes offline?

A

No affect on rewards

B

Inactivity penalties are incurred only while unavailable

C

Immediate slashing and removal from the network

D

One week delay before slashing and ejection

Check answer

![Image of the Rhino mascot for the staking
launchpad.](/_next/image/?url=%2F_next%2Fstatic%2Fmedia%2Fenterprise-
eth.d2a3f314.png&w=750&q=75)

## Join the staker community

EthStaker is a community for everyone to discuss and learn about staking on
Ethereum. Join tens of thousands of members from around the globe for advice,
support, and to talk all things staking.

[Discord(opens in a new tab)](https://discord.gg/ethstaker)[Reddit(opens in a
new tab)](https://reddit.com/r/ethstaker)[Website(opens in a new
tab)](https://ethstaker.cc)

### Was this page helpful?

YesNo

Staking Options

[Staking home](/en/staking/)[Solo staking](/en/staking/solo/)[Staking as a
service](/en/staking/saas/)[Pooled staking](/en/staking/pools/)[About
withdrawals](/en/staking/withdrawals/)

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

