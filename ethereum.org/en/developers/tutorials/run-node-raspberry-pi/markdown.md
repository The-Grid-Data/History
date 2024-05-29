Skip to main content

[](/en/)

  * Learn
  * Use
  * Build
  * Participate
  * Research

Search```K`

Languages EN

# How to turn your Raspberry Pi 4 into a node just by flashing the MicroSD
card

clientsexecution layerconsensus layernodes

Intermediate

![✍️](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/270d.svg)EthereumOnArm

![📚](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4da.svg)[Ethereum
on ARM(opens in a new tab)](https://ethereum-on-arm-
documentation.readthedocs.io/en/latest/)

![📆](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4c6.svg)
June 10, 2022

![⏱️](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/23f1.svg)8
minute read minute read

On this page

  * Why run Ethereum on ARM?
  * How does it work?
  * Note on execution and consensus clients
  * Downloading the Image
  * Flashing the MicroSD
  * Start the node
  * Validators
  * More details
  * Feedback appreciated
  * References

**Ethereum on Arm is a custom Linux image that can turn a Raspberry Pi into an
Ethereum node.**

To use Ethereum on Arm to turn a Raspberry Pi into an Ethereum node, the
following hardware is recommended:

  * Raspberry 4 (model B 8GB), Odroid M1 or Rock 5B (8GB/16GB RAM) board
  * MicroSD Card (16 GB Class 10 minimum)
  * 2 TB SSD minimum USB 3.0 disk or an SSD with a USB to SATA case.
  * Power supply
  * Ethernet cable
  * Port forwarding (see clients for further info)
  * A case with heatsink and fan
  * USB keyboard, Monitor and HDMI cable (micro-HDMI) (Optional)

## Why run Ethereum on ARM?

ARM boards are very affordable, flexible, small computers. They are good
choices for running Ethereum nodes because they can be bought cheaply,
configured so that all their resources focus just on the node, making them
efficient, they consume low amounts of power and are physically small so they
can fit unobtrusively in any home. It is also very easy to spin up nodes
because the Raspberry Pi's MicroSD can simply be flashed with a prebuilt
image, with no downloading or building software required.

## How does it work?

The Raspberry Pi's memory card is flashed with a prebuilt image. This image
contains everything needed to run an Ethereum node. With a flashed card, all
the user needs to do is power-on the Raspberry Pi. All the processes required
to run the node are automatically started. This works because the memory card
contains a Linux-based operating system (OS) on top of which system-level
processes are automatically run that turn the unit into an Ethereum node.

Ethereum cannot be run using the popular Raspberry Pi Linux OS "Raspbian"
because Raspbian still uses a 32-bit architecture which leads Ethereum users
to run into memory issues and consensus clients do not support 32-bit
binaries. To overcome this, the Ethereum on Arm team migrated to a native
64-bit OS called "Armbian".

**Images take care of all the necessary steps** , from setting up the
environment and formatting the SSD disk to installing and running the Ethereum
software as well as starting the blockchain synchronization.

## Note on execution and consensus clients

The Ethereum on Arm image includes prebuilt execution and consensus clients as
services. An Ethereum node requires both clients to be synced and running. You
are only required to download and flash the image and then start the services.
The image is preloaded with the following execution clients:

  * Geth
  * Nethermind
  * Besu

and the following consensus clients:

  * Lighthouse
  * Nimbus
  * Prysm
  * Teku

You should choose one of each to run - all execution clients are compatible
with all consensus clients. If you do not explicitly select a client, the node
will fall back to its defaults - Geth and Lighthouse - and run them
automatically when the board is powered up. You must open port 30303 on your
router so Geth can find and connect to peers.

## Downloading the Image

The Raspberry Pi 4 Ethereum image is a "plug and play" image that
automatically installs and sets up both the execution and consensus clients,
configuring them to talk to each other and connect to the Ethereum network.
All the user needs to do is start their processes using a simple command.

Download the Raspberry Pi image from [Ethereum on Arm(opens in a new
tab)](https://ethereumonarm-
my.sharepoint.com/:u:/p/dlosada/Ec_VmUvr80VFjf3RYSU-
NzkBmj2JOteDECj8Bibde929Gw?download=1) and verify the SHA256 hash:

    
    
    1# From directory containing the downloaded image
    
    2shasum -a 256 ethonarm_22.04.00.img.zip
    
    3# Hash should output: fb497e8f8a7388b62d6e1efbc406b9558bee7ef46ec7e53083630029c117444f

Note that images for Rock 5B and Odroid M1 boards are available at the
Ethereum-on-Arm [downloads page(opens in a new tab)](https://ethereum-on-arm-
documentation.readthedocs.io/en/latest/quick-guide/download-and-install.html).

## Flashing the MicroSD

The MicroSD card that will be used for the Raspberry Pi should first be
inserted into a desktop or laptop so it can be flashed. Then, the following
terminal commands will flash the downloaded image onto the SD card:

    
    
    1# check the MicroSD card name
    
    2sudo fdisk -l
    
    3
    
    4>> sdxxx

It is really important to get the name correct because the next command
includes `dd` which completely erases the existing content of the card before
pushing the image onto it. To continue, navigate to the directory containing
the zipped image:

    
    
    1# unzip and flash image
    
    2unzip ethonarm_22.04.00.img.zip
    
    3sudo dd bs=1M if=ethonarm_22.04.00.img of=/dev/<sdxx> conv=fdatasync status=progress

The card is now flashed, so it can be inserted into the Raspberry Pi.

## Start the node

With the SD card inserted into the Raspberry Pi, connect the ethernet cable
and SSD then switch the power on. The OS will boot up and automatically start
performing the preconfigured tasks that turn the Raspberry Pi into an Ethereum
node, including installing and building the client software. This will
probably take 10-15 minutes.

Once everything is installed and configured, log in to the device via an ssh
connection or using the terminal directly if a monitor and keyboard is
attached to the board. Use the `ethereum` account to log in, as this has
permissions required to start the node.

    
    
    1User: ethereum
    
    2Password: ethereum

The default execution client, Geth, will start automatically. You can confirm
this by checking the logs using the following terminal command:

    
    
    1sudo journalctl -u geth -f

The consensus client does need to be started explicitly. To do this, first
open port 9000 on your router so that Lighthouse can find and connect to
peers. Then enable and start the lighthouse service:

    
    
    1sudo systemctl enable lighthouse-beacon
    
    2sudo systemctl start lighthouse-beacon

Check the client using the logs:

    
    
    1sudo journalctl -u lighthouse-beacon

Note that the consensus client will sync in a few minutes because it uses
checkpoint sync. The execution client will take longer - potentially several
hours, and it will not start until the consensus client is already finished
syncing (this is because the execution client needs a target to sync to, which
the synced consensus client provides).

With the Geth and Lighthouse services running and synced, your Raspberry Pi is
now an Ethereum node! It is most common to interact with the Ethereum network
using Geth's Javascript console, which can be attached to the Geth client on
port 8545. It is also possible to submit commands formatted as JSON objects
using a request tool such as Curl. See more in the [Geth documentation(opens
in a new tab)](https://geth.ethereum.org/).

Geth is preconfigured to report metrics to a Grafana dashboard which can be
viewed in the browser. More advanced users might wish to use this feature to
monitor the health of their node by navigating to `ipaddress:3000`, passing
`user: admin` and `passwd: ethereum`.

## Validators

A validator can also be optionally added to the consensus client. The
validator software allows your node to participate actively in consensus and
provides the network with cryptoeconomic security. You get rewarded for this
work in ETH. To run a validator, you must first have 32 ETH, which must be
deposited into the deposit contract. The deposit can be made by following the
step-by-step guide on the [Launchpad(opens in a new
tab)](https://launchpad.ethereum.org/). Do this on a desktop/laptop, but do
not generate keys — this can be done directly on the Raspberry Pi.

Open a terminal on the Raspberry Pi and run the following command to generate
the deposit keys:

    
    
    1sudo apt-get update
    
    2sudo apt-get install staking-deposit-cli
    
    3cd && deposit new-mnemonic --num_validators 1

(Or download the [staking-deposit-cli(opens in a new
tab)](https://github.com/ethereum/staking-deposit-cli) to run on an airgapped
machine, and run the `deposit new-mnemnonic` command)

Keep the mnemonic phrase safe! The command above generated two files in the
node's keystore: the validator keys and a deposit data file. The deposit data
needs to be uploaded into the launchpad, so it must be copied from the
Raspberry Pi to the desktop/laptop. This can be done using an ssh connection
or any other copy/paste method.

Once the deposit data file is available on the computer running the launchpad,
it can be dragged and dropped onto the `+` on the launchpad screen. Follow the
instructions on the screen to send a transaction to the deposit contract.

Back on the Raspberry Pi, a validator can be started. This requires importing
the validator keys, setting the address to collect rewards, and then starting
the preconfigured validator process. The example below is for
Lighthouse—instructions for other consensus clients are available on the
[Ethereum on Arm docs(opens in a new tab)](https://ethereum-on-arm-
documentation.readthedocs.io/en/latest/):

    
    
    1# import the validator keys
    
    2lighthouse account validator import --directory=/home/ethereum/validator_keys
    
    3
    
    4# set the reward address
    
    5sudo sed -i 's/<ETH_ADDRESS>' /etc/ethereum/lighthouse-validator.conf
    
    6
    
    7# start the validator
    
    8sudo systemctl start lighthouse-validator

Congratulations, you now have a full Ethereum node and validator running on a
Raspberry Pi!

## More details

This page gave an overview of how to set up a Geth-Lighthouse node and
validator using Raspberry Pi. More detailed instructions are available on the
[Ethereum-on-Arm website(opens in a new tab)](https://ethereum-on-arm-
documentation.readthedocs.io/en/latest/index.html).

## Feedback appreciated

We know the Raspberry Pi has a massive user base that could have a very
positive impact on the health of the Ethereum network. Please dig into the
details in this tutorial, try running on testnets, check out the Ethereum on
Arm GitHub, give feedback, raise issues and pull requests and help advance the
technology and documentation!

## References

  1. <https://ubuntu.com/download/raspberry-pi>[(opens in a new tab)](https://ubuntu.com/download/raspberry-pi)
  2. <https://wikipedia.org/wiki/Port_forwarding>[(opens in a new tab)](https://wikipedia.org/wiki/Port_forwarding)
  3. <https://prometheus.io>[(opens in a new tab)](https://prometheus.io)
  4. <https://grafana.com>[(opens in a new tab)](https://grafana.com)
  5. <https://forum.armbian.com/topic/5565-zram-vs-swap/>[(opens in a new tab)](https://forum.armbian.com/topic/5565-zram-vs-swap/)
  6. <https://geth.ethereum.org>[(opens in a new tab)](https://geth.ethereum.org)
  7. <https://nethermind.io>[(opens in a new tab)](https://nethermind.io)
  8. <https://www.hyperledger.org/projects/besu>[(opens in a new tab)](https://www.hyperledger.org/projects/besu)
  9. <https://github.com/prysmaticlabs/prysm>[(opens in a new tab)](https://github.com/prysmaticlabs/prysm)
  10. <https://lighthouse.sigmaprime.io>[(opens in a new tab)](https://lighthouse.sigmaprime.io)
  11. <https://ethersphere.github.io/swarm-home>[(opens in a new tab)](https://ethersphere.github.io/swarm-home)
  12. <https://raiden.network>[(opens in a new tab)](https://raiden.network)
  13. <https://ipfs.io>[(opens in a new tab)](https://ipfs.io)
  14. <https://status.im>[(opens in a new tab)](https://status.im)
  15. <https://vipnode.org>[(opens in a new tab)](https://vipnode.org)

n

Last edit: [@nixorokish(opens in a new tab)](https://github.com/nixorokish),
April 17, 2024

See contributors

### Was this tutorial helpful?

YesNo

  * [Edit page(opens in a new tab)](https://github.com/ethereum/ethereum-org-website/tree/dev/public/content/developers/tutorials/run-node-raspberry-pi/index.md)
  * On this page

    * Why run Ethereum on ARM?
    * How does it work?
    * Note on execution and consensus clients
    * Downloading the Image
    * Flashing the MicroSD
    * Start the node
    * Validators
    * More details
    * Feedback appreciated
    * References

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

