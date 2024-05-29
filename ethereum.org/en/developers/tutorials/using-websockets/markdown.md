Skip to main content

[](/en/)

  * Learn
  * Use
  * Build
  * Participate
  * Research

Search```K`

Languages EN

# Using WebSockets

alchemywebsocketsqueryingjavascript

Beginner

![✍️](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/270d.svg)Elan
Halpern

![📚](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4da.svg)[Alchemy
docs(opens in a new tab)](https://docs.alchemyapi.io/guides/using-websockets)

![📆](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4c6.svg)
December 1, 2020

![⏱️](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/23f1.svg)6
minute read minute read

On this page

  * WebSockets vs. HTTP(opens in a new tab)
  * Try it out
  * How to use WebSockets
  * With Web3
  * Subscription API
    * eth_subscribe
    * eth_unsubscribe

This is an entry level guide to using WebSockets and Alchemy to make requests
to the Ethereum blockchain.

## (opens in a new tab)WebSockets vs. HTTP

Unlike HTTP, with WebSockets, you don't need to continuously make requests
when you want specific information. WebSockets maintain a network connection
for you (if done right) and listen for changes.

As with any network connection, you should not assume that a WebSocket will
remain open forever without interruption, but correctly handling dropped
connections and reconnection by hand can be challenging to get right. Another
downside of WebSockets is that you do not get HTTP status codes in the
response, but only the error message.

​[Alchemy Web3(opens in a new tab)](https://docs.alchemy.com/reference/api-
overview) automatically adds handling for WebSocket failures and retries with
no configuration necessary.

## Try it out

The easiest way to test out WebSockets is to install a command line tool for
making WebSocket requests such as [wscat(opens in a new
tab)](https://github.com/websockets/wscat). Using wscat, you can send requests
as follows:

_Note: if you have an Alchemy account you can replace`demo` with your own API
key. [Sign up for a free Alchemy account here!(opens in a new
tab)](https://auth.alchemyapi.io/signup)_

    
    
    1wscat -c wss://eth-mainnet.ws.alchemyapi.io/ws/demo
    
    2
    
    3>  {"jsonrpc":  "2.0", "id": 0, "method":  "eth_gasPrice"}
    
    4
    
    5<  {"jsonrpc":  "2.0", "result":  "0xb2d05e00", "id": 0}
    
    6

## How to use WebSockets

To begin, open a WebSocket using the WebSocket URL for your app. You can find
your app's WebSocket URL by opening the app's page in [your dashboard(opens in
a new tab)](https://dashboard.alchemyapi.io/) and clicking "View Key". Note
that your app's URL for WebSockets is different from its URL for HTTP
requests, but both can be found by clicking "View Key".

[![Where to find your WebSocket URL in your Alchemy
dashboard](/content/developers/tutorials/using-websockets/use-
websockets.gif)](/content/developers/tutorials/using-websockets/use-
websockets.gif)

Any of the APIs listed in the [Alchemy API Reference(opens in a new
tab)](https://docs.alchemyapi.io/documentation/alchemy-api-reference/) can be
used via WebSocket. To do so, use the same payload that would be sent as the
body of a HTTP POST request, but instead send that payload through the
WebSocket.

## With Web3

Transitioning to WebSockets while using a client library like Web3 is simple.
Simply pass the WebSocket URL instead of the HTTP one when instantiating your
Web3 client. For example:

    
    
    1const web3 = new Web3("wss://eth-mainnet.ws.alchemyapi.io/ws/your-api-key")
    
    2
    
    3web3.eth.getBlockNumber().then(console.log) // -> 7946893
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

## Subscription API

When connected through a WebSocket, you may use two additional methods:
`eth_subscribe` and `eth_unsubscribe`. These methods will allow you to listen
for particular events and be notified immediately.

### `eth_subscribe`

Creates a new subscription for specified events. [Learn more about
`eth_subscribe`(opens in a new tab)](https://docs.alchemy.com/reference/eth-
subscribe).

#### Parameters

  1. Subscription types
  2. Optional params

The first argument specifies the type of event for which to listen. The second
argument contains additional options which depend on the first argument. The
different description types, their options, and their event payloads are
described below.

#### Returns

The subscription ID: This ID will be attached to any received events, and can
also be used to cancel the subscription using `eth_unsubscribe`.

#### Subscription events

While the subscription is active, you will receive events which are objects
with the following fields:

  * `jsonrpc`: Always "2.0"
  * `method`: Always "eth_subscription"
  * `params`: An object with the following fields:
    * `subscription`: The subscription ID returned by the `eth_subscribe` call which created this subscription.
    * `result`: An object whose contents vary depending on the type of subscription.

#### Subscription types

  1. `alchemy_newFullPendingTransactions`

Returns the transaction information for all transactions that are added to the
pending state. This subscription type subscribes to pending transactions,
similar to the standard Web3 call `web3.eth.subscribe("pendingTransactions")`,
but differs in that it emits _full transaction information_ rather than just
transaction hashes.

Example:

    
    
    1>  {"jsonrpc":  "2.0",  "id":  1,  "method":  "eth_subscribe",  "params":  ["alchemy_newFullPendingTransactions"]}
    
    2
    
    3<  {"id":1,"result":"0x9a52eeddc2b289f985c0e23a7d8427c8","jsonrpc":"2.0"}
    
    4<  {
    
    5      "jsonrpc":"2.0",
    
    6      "method":"eth_subscription",
    
    7      "params":{
    
    8          "result":{
    
    9          "blockHash":null,
    
    10          "blockNumber":null,
    
    11          "from":"0xa36452fc31f6f482ad823cd1cf5515177d57667f",
    
    12          "gas":"0x1adb0",
    
    13          "gasPrice":"0x7735c4d40",
    
    14          "hash":"0x50bff0736c713458c92dd1848d12f3354149be1363123dae35e94e0f2a9d56bf",
    
    15"input":"0xa9059cbb0000000000000000000000000d0707963952f2fba59dd06f2b425ace40b492fe0000000000000000000000000000000000000000000015b1111266cfca100000",
    
    16          "nonce":"0x0",
    
    17          "to":"0xea38eaa3c86c8f9b751533ba2e562deb9acded40",
    
    18          "transactionIndex":null,
    
    19          "value":"0x0",
    
    20          "v":"0x26",
    
    21          "r":"0x195c2c1ed126088e12d290aa93541677d3e3b1d10f137e11f86b1b9227f01e3b",
    
    22          "s":"0x60fc4edbf1527832a2a36dbc1e63ed6193a6eee654472fbebbf88ef1750b5344"},
    
    23          "subscription":"0x9a52eeddc2b289f985c0e23a7d8427c8"
    
    24      }
    
    25  }
    
    26
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

  2. `newHeads`

Emits an event any time a new header is added to the chain, including during a
chain reorganization.

When a chain reorganization occurs, this subscription will emit an event
containing all new headers for the new chain. In particular, this means that
you may see multiple headers emitted with the same height, and when this
happens the later header should be taken as the correct one after a
reorganization.

Example:

    
    
    1>  {"jsonrpc":  "2.0",  "id":  1,  "method":  "eth_subscribe",  "params":  ["newHeads"]}
    
    2
    
    3<  {"jsonrpc":"2.0","id":2,"result":"0x9ce59a13059e417087c02d3236a0b1cc"}
    
    4<  {
    
    5  "jsonrpc":  "2.0",
    
    6  "method":  "eth_subscription",
    
    7  "params":  {
    
    8      "result":  {
    
    9          "extraData":  "0xd983010305844765746887676f312e342e328777696e646f7773",
    
    10          "gasLimit":  "0x47e7c4",
    
    11          "gasUsed":  "0x38658",
    
    12          "logsBloom":
    
    13"0x00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000",
    
    14          "nonce":  "0x084149998194cc5f",
    
    15          "number":  "0x1348c9",
    
    16          "parentHash":  "0x7736fab79e05dc611604d22470dadad26f56fe494421b5b333de816ce1f25701",
    
    17          "receiptRoot":  "0x2fab35823ad00c7bb388595cb46652fe7886e00660a01e867824d3dceb1c8d36",
    
    18          "sha3Uncles":  "0x1dcc4de8dec75d7aab85b567b6ccd41ad312451b948a7413f0a142fd40d49347",
    
    19          "stateRoot":  "0xb3346685172db67de536d8765c43c31009d0eb3bd9c501c9be3229203f15f378",
    
    20          "timestamp":  "0x56ffeff8",
    
    21          "transactionsRoot":  "0x0167ffa60e3ebc0b080cdb95f7c0087dd6c0e61413140e39d94d3468d7c9689f"
    
    22      },
    
    23  "subscription":  "0x9ce59a13059e417087c02d3236a0b1cc"
    
    24  }
    
    25}
    
    26
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

  3. `logs`

Emits logs which are part of newly added blocks that match specified filter
criteria.

When a chain reorganization occurs, logs which are part of blocks on the old
chain will be emitted again with the property `removed` set to `true`.
Further, logs which are part of the blocks on the new chain are emitted,
meaning that it is possible to see logs for the same transaction multiple
times in the case of a reorganization.

Parameters

  1. An object with the following fields:
     * `address` (optional): either a string representing an address or an array of such strings.
       * Only logs created from one of these addresses will be emitted.
     * `topics`: an array of topic specifiers.
       * Each topic specifier is either `null`, a string representing a topic, or an array of strings.
       * Each position in the array which is not `null` restricts the emitted logs to only those who have one of the given topics in that position.

Some examples of topic specifications:

  * `[]`: Any topics allowed.
  * `[A]`: A in first position (and anything after).
  * `[null, B]`: Anything in first position and B in second position (and anything after).
  * `[A, B]`: A in first position and B in second position (and anything after).
  * `[[A, B], [A, B]]`: (A or B) in first position and (A or B) in second position (and anything after).

Example:

    
    
    1>  {"jsonrpc":  "2.0",  "id":  1,  "method":  "eth_subscribe",  "params":  ["logs",  {"address":  "0x8320fe7702b96808f7bbc0d4a888ed1468216cfd",  "topics":  ["0xd78a0cb8bb633d06981248b816e7bd33c2a35a6089241d099fa519e361cab902"]}]}
    
    2
    
    3<  {"jsonrpc":"2.0","id":2,"result":"0x4a8a4c0517381924f9838102c5a4dcb7"}
    
    4<  {
    
    5  "jsonrpc":  "2.0",
    
    6  "method":  "eth_subscription",
    
    7  "params":  {
    
    8      "subscription":  "0x4a8a4c0517381924f9838102c5a4dcb7",
    
    9      "result":  {
    
    10          "address":  "0x8320fe7702b96808f7bbc0d4a888ed1468216cfd",
    
    11          "blockHash":  "0x61cdb2a09ab99abf791d474f20c2ea89bf8de2923a2d42bb49944c8c993cbf04",
    
    12          "blockNumber":  "0x29e87",
    
    13          "data": "0x00000000000000000000000000000000000000000000000000000000000000010000000000000000000000000000000000000000000000000000000000000003",
    
    14          "logIndex":"0x0",
    
    15          "topics":["0xd78a0cb8bb633d06981248b816e7bd33c2a35a6089241d099fa519e361cab902"],
    
    16          "transactionHash":  "0xe044554a0a55067caafd07f8020ab9f2af60bdfe337e395ecd84b4877a3d1ab4",
    
    17          "transactionIndex":  "0x0"
    
    18      }
    
    19  }
    
    20}
    
    21
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

### `eth_unsubscribe`

Cancels an existing subscription so that no further events are sent.

Parameters

  1. Subscription ID, as previously returned from an `eth_subscribe` call.

Returns

`true` if a subscription was successfully cancelled, or `false` if no
subscription existed with the given ID.

Example:

**Request**

    
    
     1curl https://eth-mainnet.alchemyapi.io/v2/your-api-key
    
    2-X POST
    
    3-H "Content-Type: application/json"
    
    4-d '{"id": 1, "method": "eth_unsubscribe", "params": ["0x9cef478923ff08bf67fde6c64013158d"]}'
    
    5
    
    6

**Result**

    
    
     1{
    
    2  "jsonrpc": "2.0",
    
    3  "id": 1,
    
    4  "result": true
    
    5}
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

* * *

[Sign up with Alchemy(opens in a new tab)](https://auth.alchemyapi.io/signup)
for free, check out [our documentation(opens in a new
tab)](https://docs.alchemyapi.io/), and for the latest news, follow us on
[Twitter(opens in a new tab)](https://twitter.com/AlchemyPlatform).

p

Last edit: [@pettinarip(opens in a new tab)](https://github.com/pettinarip),
December 8, 2023

See contributors

### Was this tutorial helpful?

YesNo

  * [Edit page(opens in a new tab)](https://github.com/ethereum/ethereum-org-website/tree/dev/public/content/developers/tutorials/using-websockets/index.md)
  * On this page

    * WebSockets vs. HTTP(opens in a new tab)
    * Try it out
    * How to use WebSockets
    * With Web3
    * Subscription API
      * eth_subscribe
      * eth_unsubscribe

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

