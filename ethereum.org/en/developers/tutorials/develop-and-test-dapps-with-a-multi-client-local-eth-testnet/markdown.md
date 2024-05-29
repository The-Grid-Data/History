Skip to main content

[](/en/)

  * Learn
  * Use
  * Build
  * Participate
  * Research

Search```K`

Languages EN

# How to develop and test a dApp on a local, multi-client testnet

clientsnodessmart contractscomposabilityconsensus layerexecution layertesting

Intermediate

![✍️](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/270d.svg)Tedi
Mitiku

![📆](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4c6.svg)
April 11, 2023

![⏱️](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/23f1.svg)11
minute read minute read

On this page

  * Introduction
    * What is Kurtosis?
  * Setting up Kurtosis
  * Instantiating a local Ethereum testnet
    * Review
  * Connect your dApp development environment to the local Ethereum testnet
    * Setup the dApp development environment
    * Configure Hardhat to use the local testnet
    * Deploy and test your dApp locally
    * Review
  * Configuring the local Ethereum testnet
    * Changing the client configurations and number of nodes
  * Conclusion
    * Other examples and guides

## Introduction

This guide walks you through the process of instantiating a configurable local
Ethereum testnet, deploying a smart contract to it, and using the testnet to
run tests against your dApp. This guide is designed for dApp developers who
want to develop and test their dApps locally against different network
configurations before deploying to a live testnet or the mainnet.

In this guide, you will:

  * Instantiate a local Ethereum testnet with the [`eth-network-package`(opens in a new tab)](https://github.com/kurtosis-tech/eth-network-package) using [Kurtosis(opens in a new tab)](https://www.kurtosis.com/),
  * Connect your Hardhat dApp development environment to the local testnet to compile, deploy, and test a dApp, and
  * Configure the local testnet, including parameters like number of nodes and specific EL/CL client pairings, to enable development and testing workflows against various network configurations.

### What is Kurtosis?

[Kurtosis(opens in a new tab)](https://www.kurtosis.com/) is a composable
build system designed for configuring multi-container test environments. It
specifically enables developers to create reproducible environments that
require dynamic setup logic, such as blockchain testnets.

In this guide, the Kurtosis eth-network-package spins up a local Ethereum
testnet with support for the [`geth`(opens in a new
tab)](https://geth.ethereum.org/) Execution Layer (EL) client, as well as
[`teku`(opens in a new tab)](https://consensys.net/knowledge-
base/ethereum-2/teku/), [`lighthouse`(opens in a new
tab)](https://lighthouse.sigmaprime.io/), and [`lodestar`(opens in a new
tab)](https://lodestar.chainsafe.io/) Consensus Layer (CL) clients. This
package serves as a configurable and composable alternative to networks in
frameworks like Hardhat Network, Ganache, and Anvil. Kurtosis offers
developers greater control and flexibility over the testnets they use, which
is a major reason why the [Ethereum Foundation used Kurtosis to test the
Merge(opens in a new tab)](https://www.kurtosis.com/blog/testing-the-ethereum-
merge) and continues to use it for testing network upgrades.

## Setting up Kurtosis

Before you proceed, make sure you have:

  * [Installed and started the Docker engine(opens in a new tab)](https://docs.kurtosis.com/next/install#i-install--start-docker) on your local machine
  * [Installed the Kurtosis CLI(opens in a new tab)](https://docs.kurtosis.com/next/install#ii-install-the-cli) (or upgraded it to the latest release, if you already have the CLI installed)
  * Installed [Node.js(opens in a new tab)](https://nodejs.org/en), [yarn(opens in a new tab)](https://classic.yarnpkg.com/lang/en/docs/install/#mac-stable), and [npx(opens in a new tab)](https://www.npmjs.com/package/npx) (for your dApp environment)

## Instantiating a local Ethereum testnet

To spin up a local Ethereum testnet, run:

    
    
    1kurtosis --enclave local-eth-testnet run github.com/kurtosis-tech/eth-network-package
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Note: This command names your network: "local-eth-testnet” using the
`--enclave` flag.

Kurtosis will print the steps its taking under the hood as it works to
interpret, validate, and then execute the instructions. At the end, you should
see an output that resembles the following:

    
    
    1INFO[2023-04-04T18:09:44-04:00] ======================================================
    
    2INFO[2023-04-04T18:09:44-04:00] ||          Created enclave: local-eth-testnet      ||
    
    3INFO[2023-04-04T18:09:44-04:00] ======================================================
    
    4Name:            local-eth-testnet
    
    5UUID:            39372d756ae8
    
    6Status:          RUNNING
    
    7Creation Time:   Tue, 04 Apr 2023 18:09:03 EDT
    
    8
    
    9========================================= Files Artifacts =========================================
    
    10UUID           Name
    
    11d4085a064230   cl-genesis-data
    
    121c62cb792e4c   el-genesis-data
    
    13bd60489b73a7   genesis-generation-config-cl
    
    14b2e593fe5228   genesis-generation-config-el
    
    15d552a54acf78   geth-prefunded-keys
    
    165f7e661eb838   prysm-password
    
    17054e7338bb59   validator-keystore-0
    
    18
    
    19========================================== User Services ==========================================
    
    20UUID           Name                                           Ports                                         Status
    
    21e20f129ee0c5   cl-client-0-beacon                             http: 4000/tcp -> <http://127.0.0.1:54261>    RUNNING
    
    22                                                              metrics: 5054/tcp -> <http://127.0.0.1:54262>
    
    23                                                              tcp-discovery: 9000/tcp -> 127.0.0.1:54263
    
    24                                                              udp-discovery: 9000/udp -> 127.0.0.1:60470
    
    25a8b6c926cdb4   cl-client-0-validator                          http: 5042/tcp -> 127.0.0.1:54267             RUNNING
    
    26                                                              metrics: 5064/tcp -> <http://127.0.0.1:54268>
    
    27d7b802f623e8   el-client-0                                    engine-rpc: 8551/tcp -> 127.0.0.1:54253       RUNNING
    
    28                                                              rpc: 8545/tcp -> 127.0.0.1:54251
    
    29                                                              tcp-discovery: 30303/tcp -> 127.0.0.1:54254
    
    30                                                              udp-discovery: 30303/udp -> 127.0.0.1:53834
    
    31                                                              ws: 8546/tcp -> 127.0.0.1:54252
    
    32514a829c0a84   prelaunch-data-generator-1680646157905431468   <none>                                        STOPPED
    
    3362bd62d0aa7a   prelaunch-data-generator-1680646157915424301   <none>                                        STOPPED
    
    3405e9619e0e90   prelaunch-data-generator-1680646157922872635   <none>                                        STOPPED
    
    35
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Congratulations! You used Kurtosis to instantiate a local Ethereum testnet,
with a CL (`lighthouse`) and EL client (`geth`), over Docker.

### Review

In this section, you executed a command that directed Kurtosis to use the
[`eth-network-package` hosted remotely on GitHub(opens in a new
tab)](https://github.com/kurtosis-tech/eth-network-package) to spin up a local
Ethereum testnet within a Kurtosis [Enclave(opens in a new
tab)](https://docs.kurtosis.com/concepts-reference/enclaves/). Inside your
enclave, you will find both "file artifacts" and "user services".

The [File Artifacts(opens in a new tab)](https://docs.kurtosis.com/concepts-
reference/files-artifacts/) in your enclave include all the data generated and
utilized to bootstrap the EL and CL clients. The data was created using the
`prelaunch-data-generator` service built from this [Docker image(opens in a
new tab)](https://github.com/ethpandaops/ethereum-genesis-generator)

User services display all the containerized services operating in your
enclave. You will notice that a single node, featuring both an EL client and a
CL client, has been created.

## Connect your dApp development environment to the local Ethereum testnet

### Setup the dApp development environment

Now that you have a running local testnet, you can connect your dApp
development environment to use your local testnet. The Hardhat framework will
be used in this guide to deploy a blackjack dApp to your local testnet.

To set up your dApp development environment, clone the repository that
contains our sample dApp and install its dependencies, run:

    
    
    1git clone https://github.com/kurtosis-tech/awesome-kurtosis.git && cd awesome-kurtosis/smart-contract-example && yarn
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

The [smart-contract-example(opens in a new tab)](https://github.com/kurtosis-
tech/awesome-kurtosis/tree/main/smart-contract-example) folder used here
contains the typical setup for a dApp developer using the [Hardhat(opens in a
new tab)](https://hardhat.org/) framework:

  * [`contracts/`(opens in a new tab)](https://github.com/kurtosis-tech/awesome-kurtosis/tree/main/smart-contract-example/contracts) contains a few simple smart contracts for a Blackjack dApp
  * [`scripts/`(opens in a new tab)](https://github.com/kurtosis-tech/awesome-kurtosis/tree/main/smart-contract-example/scripts) contains a script to deploy a token contract to your local Ethereum network
  * [`test/`(opens in a new tab)](https://github.com/kurtosis-tech/awesome-kurtosis/tree/main/smart-contract-example/test) contains a simple .js test for your token contract to confirm each player in our Blackjack dApp has 1000 minted for them
  * [`hardhat.config.ts`(opens in a new tab)](https://github.com/kurtosis-tech/awesome-kurtosis/blob/main/smart-contract-example/hardhat.config.ts) configures your Hardhat setup

### Configure Hardhat to use the local testnet

With your dApp development environment set up, you will now connect Hardhat to
use the local Ethereum testnet generated using Kurtosis. To accomplish this,
replace `<$YOUR_PORT>` in the `localnet` struct in your `hardhat.config.ts`
config file with the port of the rpc uri output from any `el-client-<num>`
service. In this sample case, the port would be `64248`. Your port will be
different.

Example in `hardhat.config.ts`:

    
    
    1localnet: {
    
    2url: 'http://127.0.0.1:<$YOUR_PORT>',// TODO: REPLACE $YOUR_PORT WITH THE PORT OF A NODE URI PRODUCED BY THE ETH NETWORK KURTOSIS PACKAGE
    
    3
    
    4// These are private keys associated with prefunded test accounts created by the eth-network-package
    
    5// <https://github.com/kurtosis-tech/eth-network-package/blob/main/src/prelaunch_data_generator/genesis_constants/genesis_constants.star>
    
    6accounts: [
    
    7    "ef5177cd0b6b21c87db5a0bf35d4084a8a57a9d6a064f86d51ac85f2b873a4e2",
    
    8    "48fcc39ae27a0e8bf0274021ae6ebd8fe4a0e12623d61464c498900b28feb567",
    
    9    "7988b3a148716ff800414935b305436493e1f25237a2a03e5eebc343735e2f31",
    
    10    "b3c409b6b0b3aa5e65ab2dc1930534608239a478106acf6f3d9178e9f9b00b35",
    
    11    "df9bb6de5d3dc59595bcaa676397d837ff49441d211878c024eabda2cd067c9f",
    
    12    "7da08f856b5956d40a72968f93396f6acff17193f013e8053f6fbb6c08c194d6",
    
    13  ],
    
    14},
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Once you save your file, your Hardhat dApp development environment is now
connected to your local Ethereum testnet! You can verify that your testnet is
working by running:

    
    
    1npx hardhat balances --network localnet
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

The output should look something like this:

    
    
    10x878705ba3f8Bc32FCf7F4CAa1A35E72AF65CF766 has balance 10000000000000000000000000
    
    20x4E9A3d9D1cd2A2b2371b8b3F489aE72259886f1A has balance 10000000000000000000000000
    
    30xdF8466f277964Bb7a0FFD819403302C34DCD530A has balance 10000000000000000000000000
    
    40x5c613e39Fc0Ad91AfDA24587e6f52192d75FBA50 has balance 10000000000000000000000000
    
    50x375ae6107f8cC4cF34842B71C6F746a362Ad8EAc has balance 10000000000000000000000000
    
    60x1F6298457C5d76270325B724Da5d1953923a6B88 has balance 10000000000000000000000000
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

This confirms that Hardhat is using your local testnet and detects the pre-
funded accounts created by the `eth-network-package`.

### Deploy and test your dApp locally

With the dApp development environment fully connected to the local Ethereum
testnet, you can now run development and testing workflows against your dApp
using the local testnet.

To compile and deploy the `ChipToken.sol` smart contract for local prototyping
and development, run:

    
    
    1npx hardhat compile
    
    2npx hardhat run scripts/deploy.ts --network localnet
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

The output should look something like:

    
    
    1ChipToken deployed to: 0xAb2A01BC351770D09611Ac80f1DE076D56E0487d
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Now try running the `simple.js` test against your local dApp to confirm each
player in our Blackjack dApp has 1000 minted for them:

The output should look something like this:

    
    
    1npx hardhat test --network localnet
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

The output should look something like this:

    
    
    1ChipToken
    
    2    mint
    
    3      ✔ should mint 1000 chips for PLAYER ONE
    
    4
    
    5  1 passing (654ms)
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

### Review

At this point, you’ve now set up a dApp development environment, connected it
to a local Ethereum network created by Kurtosis, and have compiled, deployed,
and ran a simple test against your dApp.

Now let’s explore how you can configure the underlying network for testing our
dApps under varying network configurations.

## Configuring the local Ethereum testnet

### Changing the client configurations and number of nodes

Your local Ethereum testnet can be configured to use different EL and CL
client pairs, as well as a varying number of nodes, depending on the scenario
and specific network configuration you want to develop or test. This means
that, once set up, you can spin up a customized local testnet and use it to
run the same workflows (deployment, tests, etc.) under various network
configurations to ensure everything works as expected. To learn more about the
other parameters you can modify, visit this link.

Give it a try! You can pass various configuration options to the `eth-network-
package` via a JSON file. This network params JSON file provides the specific
configurations that Kurtosis will use to set up the local Ethereum network.

Take the default configuration file and edit it to spin up two nodes with
different EL/CL pairs:

  * Node 1 with `geth`/`lighthouse`
  * Node 2 with `geth`/`lodestar`
  * Node 3 with `geth`/`teku`

This configuration creates a heterogeneous network of Ethereum node
implementations for testing your dApp. Your configuration file should now look
like:

    
    
    1{
    
    2  "participants":
    
    3    [
    
    4      {
    
    5        "el_client_type": "geth",
    
    6        "el_client_image": "",
    
    7        "el_client_log_level": "",
    
    8        "cl_client_type": "lighthouse",
    
    9        "cl_client_image": "",
    
    10        "cl_client_log_level": "",
    
    11        "beacon_extra_params": [],
    
    12        "el_extra_params": [],
    
    13        "validator_extra_params": [],
    
    14        "builder_network_params": null,
    
    15      },
    
    16      {
    
    17        "el_client_type": "geth",
    
    18        "el_client_image": "",
    
    19        "el_client_log_level": "",
    
    20        "cl_client_type": "lodestar",
    
    21        "cl_client_image": "",
    
    22        "cl_client_log_level": "",
    
    23        "beacon_extra_params": [],
    
    24        "el_extra_params": [],
    
    25        "validator_extra_params": [],
    
    26        "builder_network_params": null,
    
    27      },
    
    28      {
    
    29        "el_client_type": "geth",
    
    30        "el_client_image": "",
    
    31        "el_client_log_level": "",
    
    32        "cl_client_type": "teku",
    
    33        "cl_client_image": "",
    
    34        "cl_client_log_level": "",
    
    35        "beacon_extra_params": [],
    
    36        "el_extra_params": [],
    
    37        "validator_extra_params": [],
    
    38        "builder_network_params": null,
    
    39      },
    
    40    ],
    
    41  "network_params":
    
    42    {
    
    43      "preregistered_validator_keys_mnemonic": "giant issue aisle success illegal bike spike question tent bar rely arctic volcano long crawl hungry vocal artwork sniff fantasy very lucky have athlete",
    
    44      "num_validator_keys_per_node": 64,
    
    45      "network_id": "3151908",
    
    46      "deposit_contract_address": "0x4242424242424242424242424242424242424242",
    
    47      "seconds_per_slot": 12,
    
    48      "genesis_delay": 120,
    
    49      "capella_fork_epoch": 5,
    
    50    },
    
    51}
    
    Show all

Each `participants` struct maps to a node in the network, so 3 `participants`
structs will tell Kurtosis to spin up 3 nodes in your network. Each
`participants` struct will allow you to specify the EL and CL pair used for
that specific node.

The `network_params` struct configures the network settings that are used to
create the genesis files for each node as well as other settings like the
seconds per slot of the network.

Save your edited params file in any directory you wish (in the example below,
it is saved to the desktop) and then use it to run your Kurtosis package by
running:

    
    
    1kurtosis clean -a && kurtosis run --enclave local-eth-testnet github.com/kurtosis-tech/eth-network-package "$(cat ~/eth-network-params.json)"
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Note: the `kurtosis clean -a` command is used here to instruct Kurtosis to
destroy the old testnet and its contents before starting a new one up.

Again, Kurtosis will work for a bit and print out the individual steps that
are taking place. Eventually, the output should look something like:

    
    
    1Starlark code successfully run. No output was returned.
    
    2INFO[2023-04-07T11:43:16-04:00] ==========================================================
    
    3INFO[2023-04-07T11:43:16-04:00] ||          Created enclave: local-eth-testnet          ||
    
    4INFO[2023-04-07T11:43:16-04:00] ==========================================================
    
    5Name:            local-eth-testnet
    
    6UUID:            bef8c192008e
    
    7Status:          RUNNING
    
    8Creation Time:   Fri, 07 Apr 2023 11:41:58 EDT
    
    9
    
    10========================================= Files Artifacts =========================================
    
    11UUID           Name
    
    12cc495a8e364a   cl-genesis-data
    
    137033fcdb5471   el-genesis-data
    
    14a3aef43fc738   genesis-generation-config-cl
    
    158e968005fc9d   genesis-generation-config-el
    
    163182cca9d3cd   geth-prefunded-keys
    
    178421166e234f   prysm-password
    
    18d9e6e8d44d99   validator-keystore-0
    
    1923f5ba517394   validator-keystore-1
    
    204d28dea40b5c   validator-keystore-2
    
    21
    
    22========================================== User Services ==========================================
    
    23UUID           Name                                           Ports                                            Status
    
    24485e6fde55ae   cl-client-0-beacon                             http: 4000/tcp -> http://127.0.0.1:65010         RUNNING
    
    25                                                              metrics: 5054/tcp -> http://127.0.0.1:65011
    
    26                                                              tcp-discovery: 9000/tcp -> 127.0.0.1:65012
    
    27                                                              udp-discovery: 9000/udp -> 127.0.0.1:54455
    
    2873739bd158b2   cl-client-0-validator                          http: 5042/tcp -> 127.0.0.1:65016                RUNNING
    
    29                                                              metrics: 5064/tcp -> http://127.0.0.1:65017
    
    301b0a233cd011   cl-client-1-beacon                             http: 4000/tcp -> 127.0.0.1:65021                RUNNING
    
    31                                                              metrics: 8008/tcp -> 127.0.0.1:65023
    
    32                                                              tcp-discovery: 9000/tcp -> 127.0.0.1:65024
    
    33                                                              udp-discovery: 9000/udp -> 127.0.0.1:56031
    
    34                                                              validator-metrics: 5064/tcp -> 127.0.0.1:65022
    
    35949b8220cd53   cl-client-1-validator                          http: 4000/tcp -> 127.0.0.1:65028                RUNNING
    
    36                                                              metrics: 8008/tcp -> 127.0.0.1:65030
    
    37                                                              tcp-discovery: 9000/tcp -> 127.0.0.1:65031
    
    38                                                              udp-discovery: 9000/udp -> 127.0.0.1:60784
    
    39                                                              validator-metrics: 5064/tcp -> 127.0.0.1:65029
    
    40c34417bea5fa   cl-client-2                                    http: 4000/tcp -> 127.0.0.1:65037                RUNNING
    
    41                                                              metrics: 8008/tcp -> 127.0.0.1:65035
    
    42                                                              tcp-discovery: 9000/tcp -> 127.0.0.1:65036
    
    43                                                              udp-discovery: 9000/udp -> 127.0.0.1:63581
    
    44e19738e6329d   el-client-0                                    engine-rpc: 8551/tcp -> 127.0.0.1:64986          RUNNING
    
    45                                                              rpc: 8545/tcp -> 127.0.0.1:64988
    
    46                                                              tcp-discovery: 30303/tcp -> 127.0.0.1:64987
    
    47                                                              udp-discovery: 30303/udp -> 127.0.0.1:55706
    
    48                                                              ws: 8546/tcp -> 127.0.0.1:64989
    
    49e904687449d9   el-client-1                                    engine-rpc: 8551/tcp -> 127.0.0.1:64993          RUNNING
    
    50                                                              rpc: 8545/tcp -> 127.0.0.1:64995
    
    51                                                              tcp-discovery: 30303/tcp -> 127.0.0.1:64994
    
    52                                                              udp-discovery: 30303/udp -> 127.0.0.1:58096
    
    53                                                              ws: 8546/tcp -> 127.0.0.1:64996
    
    54ad6f401126fa   el-client-2                                    engine-rpc: 8551/tcp -> 127.0.0.1:65003          RUNNING
    
    55                                                              rpc: 8545/tcp -> 127.0.0.1:65001
    
    56                                                              tcp-discovery: 30303/tcp -> 127.0.0.1:65000
    
    57                                                              udp-discovery: 30303/udp -> 127.0.0.1:57269
    
    58                                                              ws: 8546/tcp -> 127.0.0.1:65002
    
    5912d04a9dbb69   prelaunch-data-generator-1680882122181135513   <none>                                           STOPPED
    
    605b45f9c0504b   prelaunch-data-generator-1680882122192182847   <none>                                           STOPPED
    
    613d4aaa75e218   prelaunch-data-generator-1680882122201668972   <none>                                           STOPPED
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Congratulations! You’ve successfully configured your local testnet to have 3
nodes instead of 1. To run the same workflows you did before against your dApp
(deploy & test), perform the same operations we did before by replacing the
`<$YOUR_PORT>` in the `localnet` struct in your `hardhat.config.ts` config
file with the port of the rpc uri output from any `el-client-<num>` service in
your new, 3-node local testnet.

## Conclusion

And that's it! To recap this short guide, you:

  * Created a local Ethereum testnet over Docker using Kurtosis
  * Connected your local dApp development environment to the local Ethereum network
  * Deployed a dApp and ran a simple test against it on the local Ethereum network
  * Configured the underlying Ethereum network to have 3 nodes

We’d love to hear from you on what went well for you, what could be improved,
or to answer any of your questions. Don’t hesitate to reach out via
[GitHub(opens in a new tab)](https://github.com/kurtosis-
tech/kurtosis/issues/new/choose) or [email us(opens in a new
tab)](mailto:feedback@kurtosistech.com)!

### Other examples and guides

We encourage you to check out our [quickstart(opens in a new
tab)](https://docs.kurtosis.com/quickstart) (where you’ll build a Postgres
database and API on top) and our other examples in our [awesome-kurtosis
repository(opens in a new tab)](https://github.com/kurtosis-tech/awesome-
kurtosis) where you’ll find some great examples, including packages for:

  * [Spinning up the same local Ethereum testnet(opens in a new tab)](https://github.com/kurtosis-tech/eth2-package), but with additional services connected such as a transaction spammer (to simulate transactions), a fork monitor, and a connected Grafana and Prometheus instance
  * Performing a [sub-networking test(opens in a new tab)](https://github.com/kurtosis-tech/awesome-kurtosis/tree/main/ethereum-network-partition-test) against the same local Ethereum network

p

Last edit: [@pettinarip(opens in a new tab)](https://github.com/pettinarip),
October 10, 2023

See contributors

### Was this tutorial helpful?

YesNo

  * [Edit page(opens in a new tab)](https://github.com/ethereum/ethereum-org-website/tree/dev/public/content/developers/tutorials/develop-and-test-dapps-with-a-multi-client-local-eth-testnet/index.md)
  * On this page

    * Introduction
      * What is Kurtosis?
    * Setting up Kurtosis
    * Instantiating a local Ethereum testnet
      * Review
    * Connect your dApp development environment to the local Ethereum testnet
      * Setup the dApp development environment
      * Configure Hardhat to use the local testnet
      * Deploy and test your dApp locally
      * Review
    * Configuring the local Ethereum testnet
      * Changing the client configurations and number of nodes
    * Conclusion
      * Other examples and guides

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

