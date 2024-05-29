Skip to main content

[](/en/)

  * Learn
  * Use
  * Build
  * Participate
  * Research

Search```K`

Languages EN

# The Graph: Fixing Web3 data querying

soliditysmart contractsqueryingthe graphcreate-eth-appreact

Intermediate

![✍️](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/270d.svg)Markus
Waas

![📚](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4da.svg)[soliditydeveloper.com(opens
in a new tab)](https://soliditydeveloper.com/thegraph)

![📆](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4c6.svg)
September 6, 2020

![⏱️](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/23f1.svg)8
minute read minute read

On this page

  * Without The Graph...
  * Let me introduce you to GraphQL
  * What is The Graph?
  * How to create a Subgraph
    * Manifest (subgraph.yaml)
    * Schema (schema.graphql)
    * Mapping (mapping.ts)
  * Using it in the Frontend
  * The Graph server
    * Graph Explorer: The hosted service
    * Running your own node
  * The decentralized future

This time we will take a closer look at The Graph which essentially became
part of the standard stack for developing dapps in the last year. Let's first
see how we would do things the traditional way...

## Without The Graph...

So let's go with a simple example for illustration purposes. We all like
games, so imagine a simple game with users placing bets:

    
    
    1pragma solidity 0.7.1;
    
    2
    
    3contract Game {
    
    4    uint256 totalGamesPlayerWon = 0;
    
    5    uint256 totalGamesPlayerLost = 0;
    
    6    event BetPlaced(address player, uint256 value, bool hasWon);
    
    7
    
    8    function placeBet() external payable {
    
    9        bool hasWon = evaluateBetForPlayer(msg.sender);
    
    10
    
    11        if (hasWon) {
    
    12            (bool success, ) = msg.sender.call{ value: msg.value * 2 }('');
    
    13            require(success, "Transfer failed");
    
    14            totalGamesPlayerWon++;
    
    15        } else {
    
    16            totalGamesPlayerLost++;
    
    17        }
    
    18
    
    19        emit BetPlaced(msg.sender, msg.value, hasWon);
    
    20    }
    
    21}
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Now let's say in our dapp, we want to display total bets, the total games
lost/won and also update it whenever someone plays again. The approach would
be:

  1. Fetch `totalGamesPlayerWon`.
  2. Fetch `totalGamesPlayerLost`.
  3. Subscribe to `BetPlaced` events.

We can listen to the [event in Web3(opens in a new
tab)](https://docs.web3js.org/api/web3/class/Contract#events) as shown on the
right, but it requires handling quite a few cases.

    
    
    1GameContract.events.BetPlaced({
    
    2    fromBlock: 0
    
    3}, function(error, event) { console.log(event); })
    
    4.on('data', function(event) {
    
    5    // event fired
    
    6})
    
    7.on('changed', function(event) {
    
    8    // event was removed again
    
    9})
    
    10.on('error', function(error, receipt) {
    
    11    // tx rejected
    
    12});
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Now this is still somewhat fine for our simple example. But let's say we want
to now display the amounts of bets lost/won only for the current player. Well
we're out of luck, you better deploy a new contract that stores those values
and fetch them. And now imagine a much more complicated smart contract and
dapp, things can get messy quickly.

[![One Does Not Simply
Query](/_next/image/?url=%2Fcontent%2Fdevelopers%2Ftutorials%2Fthe-graph-
fixing-web3-data-querying%2Fone-does-not-simply-
query.jpg&w=1504&q=75)](/content/developers/tutorials/the-graph-fixing-
web3-data-querying/one-does-not-simply-query.jpg)

You can see how this is not optimal:

  * Doesn't work for already deployed contracts.
  * Extra gas costs for storing those values.
  * Requires another call to fetch the data for an Ethereum node.

[![Thats not good
enough](/_next/image/?url=%2Fcontent%2Fdevelopers%2Ftutorials%2Fthe-graph-
fixing-web3-data-querying%2Fnot-good-
enough.jpg&w=1080&q=75)](/content/developers/tutorials/the-graph-fixing-
web3-data-querying/not-good-enough.jpg)

Now let's look at a better solution.

## Let me introduce you to GraphQL

First let's talk about GraphQL, originally designed and implemented by
Facebook. You might be familiar with the traditional REST API model. Now
imagine instead you could write a query for exactly the data that you wanted:

[![GraphQL API vs. REST
API](/_next/image/?url=%2Fcontent%2Fdevelopers%2Ftutorials%2Fthe-graph-fixing-
web3-data-
querying%2Fgraphql.jpg&w=1920&q=75)](/content/developers/tutorials/the-graph-
fixing-web3-data-querying/graphql.jpg)

[![](https://cdn0.scrvt.com/b095ee27d37b3d7b6b150adba9ac6ec8/42226f4816a77656/bc5c8b270798/graphql-
querygif.gif)(opens in a new
tab)](https://cdn0.scrvt.com/b095ee27d37b3d7b6b150adba9ac6ec8/42226f4816a77656/bc5c8b270798/graphql-
querygif.gif)

The two images pretty much capture the essence of GraphQL. With the query on
the right we can define exactly what data we want, so there we get everything
in one request and nothing more than exactly what we need. A GraphQL server
handles the fetching of all data required, so it is incredibly easy for the
frontend consumer side to use. [This is a nice explanation(opens in a new
tab)](https://www.apollographql.com/blog/graphql-explained-5844742f195e/) of
how exactly the server handles a query if you're interested.

Now with that knowledge, let's finally jump into blockchain space and The
Graph.

## What is The Graph?

A blockchain is a decentralized database, but in contrast to what's usually
the case, we don't have a query language for this database. Solutions for
retrieving data are painful or completely impossible. The Graph is a
decentralized protocol for indexing and querying blockchain data. And you
might have guessed it, it's using GraphQL as query language.

[![The Graph](/_next/image/?url=%2Fcontent%2Fdevelopers%2Ftutorials%2Fthe-
graph-fixing-web3-data-
querying%2Fthegraph.png&w=1920&q=75)](/content/developers/tutorials/the-graph-
fixing-web3-data-querying/thegraph.png)

Examples are always the best to understand something, so let's use The Graph
for our GameContract example.

## How to create a Subgraph

The definition for how to index data is called subgraph. It requires three
components:

  1. Manifest (`subgraph.yaml`)
  2. Schema (`schema.graphql`)
  3. Mapping (`mapping.ts`)

### Manifest (`subgraph.yaml`)

The manifest is our configuration file and defines:

  * which smart contracts to index (address, network, ABI...)
  * which events to listen to
  * other things to listen to like function calls or blocks
  * the mapping functions being called (see `mapping.ts` below)

You can define multiple contracts and handlers here. A typical setup would
have a subgraph folder inside the Truffle/Hardhat project with its own
repository. Then you can easily reference the ABI.

For convenience reasons you also might want to use a template tool like
mustache. Then you create a `subgraph.template.yaml` and insert the addresses
based on the latest deployments. For a more advanced example setup, see for
example the [Aave subgraph repo(opens in a new
tab)](https://github.com/aave/aave-protocol/tree/master/thegraph).

And the full documentation can be seen [here(opens in a new
tab)](https://thegraph.com/docs/en/developing/creating-a-subgraph/#the-
subgraph-manifest).

    
    
    1specVersion: 0.0.1
    
    2description: Placing Bets on Ethereum
    
    3repository: - GitHub link -
    
    4schema:
    
    5  file: ./schema.graphql
    
    6dataSources:
    
    7  - kind: ethereum/contract
    
    8    name: GameContract
    
    9    network: mainnet
    
    10    source:
    
    11      address: '0x2E6454...cf77eC'
    
    12      abi: GameContract
    
    13      startBlock: 6175244
    
    14    mapping:
    
    15      kind: ethereum/events
    
    16      apiVersion: 0.0.1
    
    17      language: wasm/assemblyscript
    
    18      entities:
    
    19        - GameContract
    
    20      abis:
    
    21        - name: GameContract
    
    22          file: ../build/contracts/GameContract.json
    
    23      eventHandlers:
    
    24        - event: PlacedBet(address,uint256,bool)
    
    25          handler: handleNewBet
    
    26      file: ./src/mapping.ts
    
    Show all

### Schema (`schema.graphql`)

The schema is the GraphQL data definition. It will allow you to define which
entities exist and their types. Supported types from The Graph are

  * Bytes
  * ID
  * String
  * Boolean
  * Int
  * BigInt
  * BigDecimal

You can also use entities as type to define relationships. In our example we
define a 1-to-many relationship from player to bets. The ! means the value
can't be empty. The full documentation can be seen [here(opens in a new
tab)](https://thegraph.com/docs/en/developing/creating-a-subgraph/#the-
subgraph-manifest).

    
    
    1type Bet @entity {
    
    2  id: ID!
    
    3  player: Player!
    
    4  playerHasWon: Boolean!
    
    5  time: Int!
    
    6}
    
    7
    
    8type Player @entity {
    
    9  id: ID!
    
    10  totalPlayedCount: Int
    
    11  hasWonCount: Int
    
    12  hasLostCount: Int
    
    13  bets: [Bet]!
    
    14}
    
    Show all

### Mapping (`mapping.ts`)

The mapping file in The Graph defines our functions that transform incoming
events into entities. It is written in AssemblyScript, a subset of Typescript.
This means it can be compiled into WASM (WebAssembly) for more efficient and
portable execution of the mapping.

You will need to define each function named in the `subgraph.yaml` file, so in
our case we need only one: `handleNewBet`. We first try to load the Player
entity from the sender address as id. If it doesn't exist, we create a new
entity and fill it with starting values.

Then we create a new Bet entity. The id for this will be
`event.transaction.hash.toHex() + "-" + event.logIndex.toString()` ensuring
always a unique value. Using only the hash isn't enough as someone might be
calling the placeBet function several times in one transaction via a smart
contract.

Lastly we can update the Player entity with all the data. Arrays cannot be
pushed to directly, but need to be updated as shown here. We use the id to
reference the bet. And `.save()` is required at the end to store an entity.

The full documentation can be seen here:
<https://thegraph.com/docs/en/developing/creating-a-subgraph/#writing-
mappings>[(opens in a new
tab)](https://thegraph.com/docs/en/developing/creating-a-subgraph/#writing-
mappings). You can also add logging output to the mapping file, see
[here(opens in a new tab)](https://thegraph.com/docs/assemblyscript-api#api-
reference).

    
    
    1import { Bet, Player } from "../generated/schema"
    
    2import { PlacedBet } from "../generated/GameContract/GameContract"
    
    3
    
    4export function handleNewBet(event: PlacedBet): void {
    
    5  let player = Player.load(event.transaction.from.toHex())
    
    6
    
    7  if (player == null) {
    
    8    // create if doesn't exist yet
    
    9    player = new Player(event.transaction.from.toHex())
    
    10    player.bets = new Array<string>(0)
    
    11    player.totalPlayedCount = 0
    
    12    player.hasWonCount = 0
    
    13    player.hasLostCount = 0
    
    14  }
    
    15
    
    16  let bet = new Bet(
    
    17    event.transaction.hash.toHex() + "-" + event.logIndex.toString()
    
    18  )
    
    19  bet.player = player.id
    
    20  bet.playerHasWon = event.params.hasWon
    
    21  bet.time = event.block.timestamp
    
    22  bet.save()
    
    23
    
    24  player.totalPlayedCount++
    
    25  if (event.params.hasWon) {
    
    26    player.hasWonCount++
    
    27  } else {
    
    28    player.hasLostCount++
    
    29  }
    
    30
    
    31  // update array like this
    
    32  let bets = player.bets
    
    33  bets.push(bet.id)
    
    34  player.bets = bets
    
    35
    
    36  player.save()
    
    37}
    
    Show all

## Using it in the Frontend

Using something like Apollo Boost, you can easily integrate The Graph in your
React dapp (or Apollo-Vue). Especially when using React hooks and Apollo,
fetching data is as simple as writing a single GraphQL query in your
component. A typical setup might look like this:

    
    
    1// See all subgraphs: https://thegraph.com/explorer/
    
    2const client = new ApolloClient({
    
    3  uri: "{{ subgraphUrl }}",
    
    4})
    
    5
    
    6ReactDOM.render(
    
    7  <ApolloProvider client={client}>
    
    8    <App />
    
    9  </ApolloProvider>,
    
    10  document.getElementById("root")
    
    11)
    
    Show all

And now we can write for example a query like this. This will fetch us

  * how many times current user has won
  * how many times current user has lost
  * a list of timestamps with all his previous bets

All in one single request to the GraphQL server.

    
    
    1const myGraphQlQuery = gql`
    
    2    players(where: { id: $currentUser }) {
    
    3      totalPlayedCount
    
    4      hasWonCount
    
    5      hasLostCount
    
    6      bets {
    
    7        time
    
    8      }
    
    9    }
    
    10`
    
    11
    
    12const { loading, error, data } = useQuery(myGraphQlQuery)
    
    13
    
    14React.useEffect(() => {
    
    15  if (!loading && !error && data) {
    
    16    console.log({ data })
    
    17  }
    
    18}, [loading, error, data])
    
    Show all

[![Magic](/_next/image/?url=%2Fcontent%2Fdevelopers%2Ftutorials%2Fthe-graph-
fixing-web3-data-
querying%2Fmagic.jpg&w=1200&q=75)](/content/developers/tutorials/the-graph-
fixing-web3-data-querying/magic.jpg)

But we're missing one last piece of the puzzle and that's the server. You can
either run it yourself or use the hosted service.

## The Graph server

### Graph Explorer: The hosted service

The easiest way is to use the hosted service. Follow the instructions
[here(opens in a new tab)](https://thegraph.com/docs/en/deploying/deploying-a-
subgraph-to-hosted/) to deploy a subgraph. For many projects you can actually
find existing subgraphs in the [explorer(opens in a new
tab)](https://thegraph.com/explorer/).

[![The Graph-
Explorer](/_next/image/?url=%2Fcontent%2Fdevelopers%2Ftutorials%2Fthe-graph-
fixing-web3-data-querying%2Fthegraph-
explorer.png&w=1920&q=75)](/content/developers/tutorials/the-graph-fixing-
web3-data-querying/thegraph-explorer.png)

### Running your own node

Alternatively you can run your own node. Docs [here(opens in a new
tab)](https://github.com/graphprotocol/graph-node#quick-start). One reason to
do this might be using a network that's not supported by the hosted service.
The currently supported networks [can be found here(opens in a new
tab)](https://thegraph.com/docs/en/developing/supported-networks/).

## The decentralized future

GraphQL supports streams as well for newly incoming events. These are
supported on the graph through [Substreams(opens in a new
tab)](https://thegraph.com/docs/en/substreams/) which are currently in open
beta.

In [2021(opens in a new tab)](https://thegraph.com/blog/mainnet-migration/)
The Graph began its transition to a decentralized indexing network. You can
read more about the architecture of this decentralized indexing network
[here(opens in a new tab)](https://thegraph.com/docs/en/network/explorer/).

Two key aspects are:

  1. Users pay the indexers for queries.
  2. Indexers stake Graph Tokens (GRT).

l

Last edit: [@lukassim(opens in a new tab)](https://github.com/lukassim), April
26, 2024

See contributors

### Was this tutorial helpful?

YesNo

  * [Edit page(opens in a new tab)](https://github.com/ethereum/ethereum-org-website/tree/dev/public/content/developers/tutorials/the-graph-fixing-web3-data-querying/index.md)
  * On this page

    * Without The Graph...
    * Let me introduce you to GraphQL
    * What is The Graph?
    * How to create a Subgraph
      * Manifest (subgraph.yaml)
      * Schema (schema.graphql)
      * Mapping (mapping.ts)
    * Using it in the Frontend
    * The Graph server
      * Graph Explorer: The hosted service
      * Running your own node
    * The decentralized future

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

