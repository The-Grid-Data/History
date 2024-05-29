Skip to main content

[](/en/)

  * Learn
  * Use
  * Build
  * Participate
  * Research

Search```K`

Languages EN

# Solidity and Truffle continuous integration setup

soliditysmart contractstestingtruffleganache

Intermediate

![✍️](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/270d.svg)Markus
Waas

![📚](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4da.svg)[soliditydeveloper.com(opens
in a new tab)](https://soliditydeveloper.com/continuous-integration)

![📆](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4c6.svg)
June 5, 2020

![⏱️](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/23f1.svg)4
minute read minute read

On this page

  * Setting up Travis CI
  * Setting up Circle CI
  * Adding the eth-gas-reporter plugin
    * Step 1: Install the eth-gas-reporter plugin and codechecks
    * Step 2: Add the plugin to the mocha settings inside your truffle-config.js
    * Step 3: Add a codechecks.yml to your project's root directory
    * Step 4: Run codechecks after the test command
    * Step 5: Create a Codechecks account
  * Adding the solidity-coverage plugin
    * Step 1: Create a metacoin project and install coverage tools
    * Step 2: Add solidity-coverage to the plugins array in truffle-config.js
    * Step 3: Add the coverage commands to the .travis.yml or Circle CI config.yml
    * Step 4: Add repository to coveralls
  * Further ideas

Continuous integration (CI) with Truffle is great for developing once you have
a basic set of tests implemented. It allows you to run very long tests, ensure
all tests pass before merging a [pull request(opens in a new
tab)](https://help.github.com/en/github/collaborating-with-issues-and-pull-
requests/creating-a-pull-request) and to keep track of various statistics
using additional tools.

We will use the [Truffle Metacoin Box(opens in a new
tab)](https://www.trufflesuite.com/boxes/metacoin) to setup our continuous
integration. You can either choose Travis CI or Circle CI.

## Setting up Travis CI

Adding [Travis CI(opens in a new tab)](https://travis-ci.org/) is straight-
forward. You will only need to add a `.travis.yml` config file to the root
folder of the project:

    
    
    1language: node_js
    
    2node_js:
    
    3  - 10
    
    4
    
    5cache: npm
    
    6
    
    7before_script:
    
    8  - echo fs.inotify.max_user_watches=524288 | sudo tee -a /etc/sysctl.conf && sudo sysctl -p
    
    9
    
    10script:
    
    11  - npm test
    
    Show all

We are keeping it simple for now and are only running the test script which
executes the Truffle unit tests. But we have one problem, there won't be a
blockchain available on the Travis CI machine. A simple fix for this is to
`npm install ganache-cli` and simply run it before the test. You can do this
by adding a bash script with the line npx `ganache-cli > /dev/null` and before
the `npx truffle test` call. The [full example bash script(opens in a new
tab)](https://github.com/gorgos/Truffle-CI-
Example/blob/master/scripts/run_tests.sh).

## Setting up Circle CI

[CircleCi(opens in a new tab)](https://circleci.com/) requires a longer config
file. The additional [`npm ci`(opens in a new
tab)](https://docs.npmjs.com/cli/ci.html) command is automatically done in
Travis. It installs dependencies faster and more securely than `npm install`
does. We again use the same script from the Travis version to run ganache-cli
before the tests.

    
    
    1version: 2
    
    2
    
    3aliases:
    
    4  - &defaults
    
    5    docker:
    
    6      - image: circleci/node:10
    
    7
    
    8  - &cache_key_node_modules
    
    9    key: v1-node_modules-{{ checksum "package-lock.json" }}
    
    10
    
    11jobs:
    
    12  dependencies:
    
    13    <<: *defaults
    
    14    steps:
    
    15      - checkout
    
    16      - restore_cache:
    
    17          <<: *cache_key_node_modules
    
    18      - run:
    
    19          name: Install npm dependencies
    
    20          command: |
    
    21            if [ ! -d node_modules ]; then
    
    22              npm ci
    
    23            fi
    
    24      - persist_to_workspace:
    
    25          root: .
    
    26          paths:
    
    27            - node_modules
    
    28            - build
    
    29      - save_cache:
    
    30          paths:
    
    31            - node_modules
    
    32          <<: *cache_key_node_modules
    
    33
    
    34  test:
    
    35    <<: *defaults
    
    36    steps:
    
    37      - checkout
    
    38      - attach_workspace:
    
    39          at: .
    
    40      - run:
    
    41          name: Unit tests
    
    42          command: npm test
    
    43
    
    44workflows:
    
    45  version: 2
    
    46  everything:
    
    47    jobs:
    
    48      - dependencies
    
    49      - test:
    
    50          requires:
    
    51            - dependencies
    
    Show all

## Adding the eth-gas-reporter plugin

The eth-gas-reporter plugin is quite useful for keeping track of the gas costs
of your smart contract functions. Having it in your CI will further be useful
for showing diffs when adding pull requests.

### Step 1: Install the eth-gas-reporter plugin and codechecks

    
    
    npm install --save-dev eth-gas-reporter
    
    npm install --save-dev @codechecks/client

### Step 2: Add the plugin to the mocha settings inside your truffle-config.js

[See options(opens in a new tab)](https://github.com/cgewecke/eth-gas-
reporter#options)

    
    
    1module.exports = {
    
    2  networks: { ... },
    
    3  mocha: {
    
    4    reporter: 'eth-gas-reporter',
    
    5    reporterOptions: {
    
    6      excludeContracts: ['Migrations']
    
    7    }
    
    8  }
    
    9};
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

### Step 3: Add a codechecks.yml to your project's root directory

    
    
    1checks:
    
    2  - name: eth-gas-reporter/codechecks

### Step 4: Run codechecks after the test command

    
    
    - npm test
    
    - npx codechecks

### Step 5: Create a Codechecks account

  * Create an account with [Codechecks(opens in a new tab)](http://codechecks.io/).
  * Add the GitHub repo to it.
  * Copy the secret and add the `CC_SECRET=COPIED SECRET` to your CI (see here for [Travis(opens in a new tab)](https://docs.travis-ci.com/user/environment-variables/), here for [CircleCi(opens in a new tab)](https://circleci.com/docs/2.0/env-vars/#setting-an-environment-variable-in-a-project)).
  * Now go ahead and create a pull request.

That's it. You will now find a nice report about changes in gas costs of your
pull request.

[![Example gas
reports](/_next/image/?url=%2Fcontent%2Fdevelopers%2Ftutorials%2Fsolidity-and-
truffle-continuous-integration-setup%2Fgas-
reports.png&w=1920&q=75)](/content/developers/tutorials/solidity-and-truffle-
continuous-integration-setup/gas-reports.png)

## Adding the solidity-coverage plugin

With the solidity-coverage plugin you can check how much of your code paths
are covered by your tests. Adding this to your CI makes is very convenient to
use once it is set up.

### Step 1: Create a metacoin project and install coverage tools

    
    
    npm install --save-dev truffle coveralls solidity-coverage

### Step 2: Add solidity-coverage to the plugins array in truffle-config.js

    
    
    1module.exports = {
    
    2  networks: {...},
    
    3  plugins: ["solidity-coverage"]
    
    4}
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

### Step 3: Add the coverage commands to the .travis.yml or Circle CI
config.yml

    
    
    - npx truffle run coverage
    
    - cat coverage/lcov.info | npx coveralls

Solidity coverage starts its own ganache-cli, so we don't have to worry about
this. Do not replace the regular test command though, coverage's ganache-cli
works differently and is therefore no replacement for running regular unit
tests.

### Step 4: Add repository to coveralls

  * Create an account with [Coveralls(opens in a new tab)](https://coveralls.io/).
  * Add the GitHub repo to it.
  * Now go ahead and create a pull request.

[![Example
coverall](/_next/image/?url=%2Fcontent%2Fdevelopers%2Ftutorials%2Fsolidity-
and-truffle-continuous-integration-
setup%2Fcoverall.png&w=1920&q=75)](/content/developers/tutorials/solidity-and-
truffle-continuous-integration-setup/coverall.png)

## Further ideas

  * [MythX(opens in a new tab)](https://mythx.io/): With MythX you can automatically analyze your smart contract security. So it makes a lot of sense to [add this to your CI(opens in a new tab)](https://blog.mythx.io/howto/mythx-and-continuous-integration-part-1-circleci/).
  * [Linting(opens in a new tab)](https://wikipedia.org/wiki/Lint_%28software%29): Good code can be enforced to some degree with linting tools. [Eslint(opens in a new tab)](https://eslint.org/) works great for JavaScript, is [easy to setup(opens in a new tab)](https://eslint.org/docs/user-guide/getting-started), while [Solhint(opens in a new tab)](https://protofire.github.io/solhint/) can be used for Solidity.
  * Long tests: Sometimes you may want to add extreme tests, e.g., testing a contracts with hundreds of users. This takes a lot of time. Instead of running those in every test run, add them to the CI.

There you have it. Continuous integration is a very useful strategy for your
developments. You can check out a full example at [Truffle-CI-Example(opens in
a new tab)](https://github.com/gorgos/Truffle-CI-Example). Just make sure to
remove Circle-CI or Travis, one is enough!

n

Last edit: [@nhsz(opens in a new tab)](https://github.com/nhsz), August 15,
2023

See contributors

### Was this tutorial helpful?

YesNo

  * [Edit page(opens in a new tab)](https://github.com/ethereum/ethereum-org-website/tree/dev/public/content/developers/tutorials/solidity-and-truffle-continuous-integration-setup/index.md)
  * On this page

    * Setting up Travis CI
    * Setting up Circle CI
    * Adding the eth-gas-reporter plugin
      * Step 1: Install the eth-gas-reporter plugin and codechecks
      * Step 2: Add the plugin to the mocha settings inside your truffle-config.js
      * Step 3: Add a codechecks.yml to your project's root directory
      * Step 4: Run codechecks after the test command
      * Step 5: Create a Codechecks account
    * Adding the solidity-coverage plugin
      * Step 1: Create a metacoin project and install coverage tools
      * Step 2: Add solidity-coverage to the plugins array in truffle-config.js
      * Step 3: Add the coverage commands to the .travis.yml or Circle CI config.yml
      * Step 4: Add repository to coveralls
    * Further ideas

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

