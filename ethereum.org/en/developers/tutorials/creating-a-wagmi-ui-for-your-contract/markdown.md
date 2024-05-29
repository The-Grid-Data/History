Skip to main content

[](/en/)

  * Learn
  * Use
  * Build
  * Participate
  * Research

Search```K`

Languages EN

# Building a user interface for your contract

typescriptreactvitewagmifrontend

Beginner

![✍️](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/270d.svg)Ori
Pomerantz

![📆](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4c6.svg)
November 1, 2023

![⏱️](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/23f1.svg)15
minute read minute read

On this page

  * Why is this important
  * Greeter application
    * Installation
    * File walk through
      * index.html
      * src/main.tsx
      * src/App.tsx
      * src/components/Greeter.tsx
        * Greeter component
        * ShowGreeting component
        * ShowObject component
        * The final export
      * src/wagmi.ts
    * Adding another blockchain

You found a feature we need in the Ethereum ecosystem. You wrote the smart
contracts to implement it, and maybe even some related code that runs
offchain. This is great! Unfortunately, without a user interface you aren't
going to have any users, and the last time you wrote a web site people used
dial-up modems and JavaScript was new.

This article is for you. I assume you know programming, and maybe a bit of
JavaScript and HTML, but that your user interface skills are rusty and out of
date. Together we will go over a simple modern application so you'll see how
it's done these days.

## Why is this important

In theory, you could just have people use [Etherscan(opens in a new
tab)](https://holesky.etherscan.io/address/0x432d810484add7454ddb3b5311f0ac2e95cecea8#writeContract)
or [Blockscout(opens in a new tab)](https://eth-
holesky.blockscout.com/address/0x432d810484AdD7454ddb3b5311f0Ac2E95CeceA8?tab=write_contract)
to interact with your contracts. That will be great for the experienced
Ethereans. But we are trying to serve [another billion people(opens in a new
tab)](https://blog.ethereum.org/2021/05/07/ethereum-for-the-next-billion).
This won't happen without a great user experience, and a friendly user
interface is a big part of that.

## Greeter application

There is a lot of theory behind for a modern UI works, and [a lot of good
sites(opens in a new tab)](https://react.dev/learn/thinking-in-react) [that
explain it(opens in a new tab)](https://wagmi.sh/core/getting-started).
Instead of repeating the fine work done by those sites, I'm going to assume
you prefer to learn by doing and start with an application you can play with.
You still need the theory to get things done, and we'll get to it - we'll just
go source file by source file, and discuss things as we get to them.

### Installation

  1. If necessary, add [the Holesky blockchain(opens in a new tab)](https://chainlist.org/?search=holesky&testnets=true) to your wallet and [get test ETH(opens in a new tab)](https://www.holeskyfaucet.io/).

  2. Clone the github repository.
    
        1git clone https://github.com/qbzzt/20230801-modern-ui.git

  3. Install the necessary packages.
    
        1cd 20230801-modern-ui
    
    2pnpm install

  4. Start the application.
    
        1pnpm dev

  5. Browse to the URL shown by the application. In most cases, that is <http://localhost:5173/>[(opens in a new tab)](http://localhost:5173/).

  6. You can see the contract source code, a slightly modified version of Hardhat's Greeter, [on a blockchain explorer(opens in a new tab)](https://eth-holesky.blockscout.com/address/0x432d810484AdD7454ddb3b5311f0Ac2E95CeceA8?tab=contract).

### File walk through

#### `index.html`

This file is standard HTML boilerplate except for this line, which imports the
script file.

    
    
    1<script type="module" src="/src/main.tsx"></script>

#### `src/main.tsx`

The file extension tells us that this file is a [React component(opens in a
new tab)](https://www.w3schools.com/react/react_components.asp) written in
[TypeScript(opens in a new tab)](https://www.typescriptlang.org/), an
extension of JavaScript that supports [type checking(opens in a new
tab)](https://en.wikipedia.org/wiki/Type_system#Type_checking). TypeScript is
compiled into JavaScript, so we can use it for client-side execution.

    
    
    1import '@rainbow-me/rainbowkit/styles.css'
    
    2import { RainbowKitProvider } from '@rainbow-me/rainbowkit'
    
    3import * as React from 'react'
    
    4import * as ReactDOM from 'react-dom/client'
    
    5import { WagmiConfig } from 'wagmi'
    
    6import { chains, config } from './wagmi'

Import the library code we need.

    
    
    1import { App } from './App'

Import the React component that implements the application (see below).

    
    
    1ReactDOM.createRoot(document.getElementById('root')!).render(

Create the root React component. The parameter to `render` is [JSX(opens in a
new tab)](https://www.w3schools.com/react/react_jsx.asp), an extension
language that uses both HTML and JavaScript/TypeScript. The exclamation point
here tells the TypeScript component: "you don't know that
`document.getElementById('root')` will be a valid parameter to
`ReactDOM.createRoot`, but don't worry - I'm the developer and I'm telling you
there will be".

    
    
    1  <React.StrictMode>

The application is going inside [a `React.StrictMode` component(opens in a new
tab)](https://react.dev/reference/react/StrictMode). This component tells the
React library to insert additional debugging checks, which is useful during
development.

    
    
    1    <WagmiConfig config={config}>

The application is also inside [a `WagmiConfig` component(opens in a new
tab)](https://wagmi.sh/react/WagmiConfig). [The wagmi (we are going to make
it) library(opens in a new tab)](https://wagmi.sh/) connects the React UI
definitions with [the viem library(opens in a new tab)](https://viem.sh/) for
writing an Ethereum decentralized application.

    
    
    1      <RainbowKitProvider chains={chains}>

And finally, [a `RainbowKitProvider` component(opens in a new
tab)](https://www.rainbowkit.com/). This component handles logging on and the
communication between the wallet and the application.

    
    
    1        <App />

Now we can have the component for the application, which actually implements
the UI. The `/>` at the end of the component tells React that this component
doesn't have any definitions inside it, as per the XML standard.

    
    
    1      </RainbowKitProvider>
    
    2    </WagmiConfig>
    
    3  </React.StrictMode>,
    
    4)

Of course, we have to close off the other components.

#### `src/App.tsx`

    
    
    1import { ConnectButton } from '@rainbow-me/rainbowkit'
    
    2import { useAccount } from 'wagmi'
    
    3import { Greeter } from './components/Greeter'
    
    4
    
    5export function App() {

This is the standard way to create a React component - define a function that
is called every time it needs to be rendered. This function typically has some
TypeScript or JavaScript code on top, followed by a `return` statement that
returns the JSX code.

    
    
    1  const { isConnected } = useAccount()

Here we use [`useAccount`(opens in a new
tab)](https://wagmi.sh/react/hooks/useAccount) to check if we are connected to
a blockchain through a wallet or not.

By convention, in React functions called `use...` are [hooks(opens in a new
tab)](https://www.w3schools.com/react/react_hooks.asp) that return some kind
of data. When you use such hooks, not only does your component get the data,
but when that data changes the component is re-rendered with the updated
information.

    
    
    1  return (
    
    2    <>

The JSX of a React component _has_ to return one component. When we have
multiple components and we don't have anything that wraps up "naturally" we
use an empty component (`<> ... </>`) to make them into a single component.

    
    
    1      <h1>Greeter</h1>
    
    2      <ConnectButton />

We get [the `ConnectButton` component(opens in a new
tab)](https://www.rainbowkit.com/docs/connect-button) from RainbowKit. When we
are not connected, it gives us a `Connect Wallet` button that opens a modal
that explains wallets and lets you choose which one you use. When we are
connected, it displays the blockchain we use, our account address, and our ETH
balance. We can use these displays to switch network or to disconnect.

    
    
    1      {isConnected && (

When we need to insert actual JavaScript (or TypeScript that will be compiled
to JavaScript) into a JSX, we use brackets (`{}`).

The syntax `a && b` is short for [`a ? b : a`(opens in a new
tab)](https://www.w3schools.com/react/react_es6_ternary.asp). That is, if `a`
is true it evaluates to `b` and otherwise it evaluates to `a` (which can be
`false`, `0`, etc). This is an easy way to tell React that a component should
only be displayed if a certain condition is fulfilled.

In this case, we only want to show the user `Greeter` if the user is connected
to a blockchain.

    
    
    1          <Greeter />
    
    2      )}
    
    3    </>
    
    4  )
    
    5}

#### `src/components/Greeter.tsx`

This file contains most of the UI functionality. It includes definitions that
would normally be in multiple files, but as this is a tutorial the program is
optimized for being easy to understand the first time, rather than performance
or ease of maintenance.

    
    
    1import { useState, ChangeEventHandler } from 'react'
    
    2import {  useNetwork, 
    
    3          useContractRead, 
    
    4          usePrepareContractWrite, 
    
    5          useContractWrite, 
    
    6          useContractEvent 
    
    7        } from 'wagmi'

We use these library functions. Again, they are explained below where they are
used.

    
    
    1import { AddressType } from 'abitype'

[The `abitype` library(opens in a new tab)](https://abitype.dev/) provides us
with TypeScript definitions for various Ethereum data types, such as
[`AddressType`(opens in a new tab)](https://abitype.dev/config#addresstype).

    
    
    1let greeterABI = [
    
    2  .
    
    3  .
    
    4  .
    
    5] as const   // greeterABI

The ABI for the `Greeter` contract. If you are developing the contracts and UI
at the same time you'd normally put them in the same repository and use the
ABI generated by the Solidity compiler as a file in your application. However,
this is not necessary here because the contract is already developed and not
going to change.

    
    
    1type AddressPerBlockchainType = {
    
    2  [key: number]: AddressType
    
    3}

TypeScript is strongly typed. We use this definition to specify the address in
which the `Greeter` contract is deployed on different chains. The key is a
number (the chainId), and the value is an `AddressType` (an address).

    
    
    1const contractAddrs: AddressPerBlockchainType = {
    
    2  // Holesky
    
    3  17000: '0x432d810484AdD7454ddb3b5311f0Ac2E95CeceA8',
    
    4
    
    5  // Sepolia
    
    6  11155111: '0x7143d5c190F048C8d19fe325b748b081903E3BF0'
    
    7}

The address of the contract on the two supported networks: [Holesky(opens in a
new tab)](https://eth-
holesky.blockscout.com/address/0x432d810484AdD7454ddb3b5311f0Ac2E95CeceA8?tab=contact_code)
and [Sepolia(opens in a new tab)](https://eth-
sepolia.blockscout.com/address/0x7143d5c190F048C8d19fe325b748b081903E3BF0?tab=contact_code).

Note: There is actually a third definition, for Redstone Holesky, it will be
explained below.

    
    
    1type ShowObjectAttrsType = {
    
    2  name: string,
    
    3  object: any
    
    4}

This type is used as a parameter to the `ShowObject` component (explained
later). It includes the name of the object and its value, which are displayed
for debugging purposes.

    
    
    1type ShowGreetingAttrsType = {
    
    2  greeting: string | undefined
    
    3}

At any moment in time we may either know what the greeting is (because we read
it from the blockchain) or not know (because we haven't received it yet). So
it is useful to have a type that can be either a string or nothing.

##### `Greeter`component

    
    
    1const Greeter = () => {

Finally, we get the define the component.

    
    
    1  const { chain } = useNetwork()

Information about the chain we are using, courtesy of [wagmi(opens in a new
tab)](https://wagmi.sh/react/hooks/useNetwork). Because this is a hook
(`use...`), every time this information changes the component gets redrawn.

    
    
    1  const greeterAddr = chain && contractAddrs[chain.id]

The address of the Greeter contract, which varies by chain (and which is
`undefined` if we don't have chain information or we are on a chain without
that contract).

    
    
    1  const readResults = useContractRead({
    
    2    address: greeterAddr,
    
    3    abi: greeterABI,
    
    4    functionName: "greet" , // No arguments
    
    5    watch: true    
    
    6  })

[The `useContractRead` hook(opens in a new
tab)](https://wagmi.sh/react/hooks/useContractRead) reads information from a
contract. You can see exactly what information it returns expand `readResults`
in the UI. In this case we want it to keep looking so we'll be informed when
the greeting changes.

**Note:** We could listen to [`setGreeting` events(opens in a new
tab)](https://eth-
holesky.blockscout.com/address/0x432d810484AdD7454ddb3b5311f0Ac2E95CeceA8?tab=logs)
to know when the greeting changes and update that way. However, while it may
be more efficient, it will not apply in all cases. When the user switches to a
different chain the greeting also changes, but that change is not accompanied
by an event. We could have one part of the code listening for events and
another to identify chain changes, but that would be more complicated than
just setting [the `watch` parameter(opens in a new
tab)](https://wagmi.sh/react/hooks/useContractRead#watch-optional).

    
    
    1  const [ newGreeting, setNewGreeting ] = useState("")

React's [`useState` hook(opens in a new
tab)](https://www.w3schools.com/react/react_usestate.asp) lets us specify a
state variable, whose value persists from one rendering of the component to
another. The initial value is the parameter, in this case the empty string.

The `useState` hook returns a list with two values:

  1. The current value of the state variable.
  2. A function to modify the state variable when needed. As this is a hook, every time it is called the component is rendered again.

In this case, we are using a state variable for the new greeting the user
wants to set.

    
    
    1  const greetingChange : ChangeEventHandler<HTMLInputElement> = (evt) => 
    
    2    setNewGreeting(evt.target.value)

This is the event handler for when the new greeting input field changes. The
type, [`ChangeEventHandler<HTMLInputElement>`(opens in a new
tab)](https://react-typescript-cheatsheet.netlify.app/docs/basic/getting-
started/forms_and_events/), specifies that this is handler for a value change
of an HTML input element. The `<HTMLInputElement>` part is used because this
is a [generic type(opens in a new
tab)](https://www.w3schools.com/typescript/typescript_basic_generics.php).

    
    
    1  const preparedTx = usePrepareContractWrite({
    
    2    address: greeterAddr,
    
    3    abi: greeterABI,
    
    4    functionName: 'setGreeting',
    
    5    args: [ newGreeting ]
    
    6  })
    
    7  const workingTx = useContractWrite(preparedTx.config)  

This is the process to submit a blockchain transaction from the client
perspective:

  1. Send the transaction to a node in the blockchain using [`eth_estimateGas`(opens in a new tab)](https://docs.alchemy.com/reference/eth-estimategas).
  2. Wait for a response from the node.
  3. When the response is received, ask the user to sign the transaction through the wallet. This step _has_ to happen after the node response is received because the user is shown the gas cost of the transaction before signing it.
  4. Wait for the user for approve.
  5. Send the transaction again, this time using [`eth_sendRawTransaction`(opens in a new tab)](https://docs.alchemy.com/reference/eth-sendrawtransaction).

Step 2 is likely to take a perceptible amount of time, during which users
would wonder if their command was really received by the user interface and
why they aren't being asked to sign the transaction already. That makes for
bad user experience (UX).

The solution is to use [prepare hooks(opens in a new
tab)](https://wagmi.sh/react/prepare-hooks). Every time that a parameter
changes, immediately send the node the `eth_estimateGas` request. Then, when
the user actually wants to send the transaction (in this case by pressing
**Update greeting**), the gas cost is known and the user can see the wallet
page immediately.

    
    
    1  return (

Now we can finally create the actual HTML to return.

    
    
    1    <>
    
    2      <h2>Greeter</h2>
    
    3      {
    
    4        !readResults.isError && !readResults.isLoading &&
    
    5          <ShowGreeting greeting={readResults.data} />
    
    6      }
    
    7      <hr />

Create a `ShowGreeting` component (explained below), but only if the greeting
was read successfully from the blockchain.

    
    
    1      <input type="text" 
    
    2        value={newGreeting}
    
    3        onChange={greetingChange}
    
    4      />

This is the input text field where the user can set a new greeting. Every time
the user presses a key, we call `greetingChange` which calls `setNewGreeting`.
As `setNewGreeting` comes from the `useState` hook, it causes the `Greeter`
component to be rendered again. This means that:

  * We need to specify `value` to keep the value of the new greeting, because otherwise it would turn back into the default, the empty string.
  * `usePrepareContractWrite` is called every time `newGreeting` changes, which means it is always going to have the latest `newGreeting` in the prepared transaction.

    
    
    1      <button disabled={!workingTx.write}
    
    2              onClick={workingTx.write}
    
    3      >
    
    4        Update greeting
    
    5      </button>

If there is no `workingTx.write` then we are still waiting for information
necessary for sending the greeting update, so the button is disabled. If there
is a `workingTx.write` value then that is the function to call to send the
transaction.

    
    
    1      <hr />
    
    2      <ShowObject name="readResults" object={readResults} />
    
    3      <ShowObject name="preparedTx" object={preparedTx} />
    
    4      <ShowObject name="workingTx" object={workingTx} />
    
    5    </>
    
    6  )
    
    7}

Finally, to help you see what we're doing, show the three objects we use:

  * `readResults`
  * `preparedTx`
  * `workingTx`

##### `ShowGreeting`component

This component shows

    
    
    1const ShowGreeting = (attrs : ShowGreetingAttrsType) => {

A component function receives a parameter with all the attributes of the
component.

    
    
    1  return <b>{attrs.greeting}</b>
    
    2}

##### `ShowObject`component

For information purposes, we use the `ShowObject` component to show the
important objects (`readResults` for reading the greeting and `preparedTx` and
`workingTx` for transactions we create).

    
    
    1const ShowObject = (attrs: ShowObjectAttrsType ) => {
    
    2  const keys = Object.keys(attrs.object)
    
    3  const funs = keys.filter(k => typeof attrs.object[k] == "function")
    
    4  return <>
    
    5    <details>

We don't want to clutter the UI with all the information, so to make it
possible to view them or close them, we use a [`details`(opens in a new
tab)](https://www.w3schools.com/tags/tag_details.asp) tag.

    
    
    1      <summary>{attrs.name}</summary>
    
    2      <pre>
    
    3        {JSON.stringify(attrs.object, null, 2)}

Most of the fields are displayed using [`JSON.stringify`(opens in a new
tab)](https://www.w3schools.com/js/js_json_stringify.asp).

    
    
    1      </pre>
    
    2      { funs.length > 0 &&
    
    3        <>
    
    4          Functions:
    
    5          <ul>

The exception is functions, which aren't part of [the JSON standard(opens in a
new tab)](https://www.json.org/json-en.html), so they have to be displayed
separately.

    
    
    1          {funs.map((f, i) =>

Within JSX, code inside `{` curly brackets `}` is interpreted as JavaScript.
Then, the code inside the `(` regular brackets `)`, is interpreted again as
JSX.

    
    
    1           (<li key={i}>{f}</li>)
    
    2                )}

React requires tags in the [DOM Tree(opens in a new
tab)](https://www.w3schools.com/js/js_htmldom.asp) to have distinct
identifiers. This means that children of the same tag (in this case, [the
unordered list(opens in a new
tab)](https://www.w3schools.com/tags/tag_ul.asp)), need different `key`
attributes.

    
    
    1          </ul>
    
    2        </>
    
    3      }
    
    4    </details>
    
    5  </>
    
    6}

End the various HTML tags.

##### The final `export`

    
    
    1export { Greeter }

The `Greeter` component is the one we need to export for the application.

#### `src/wagmi.ts`

Finally, various definitions related to WAGMI are in `src/wagmi.ts`. I am not
going to explain everything here, because most of it is boilerplate you are
unlikely to need to change.

The code here isn't exactly the same as [on github(opens in a new
tab)](https://github.com/qbzzt/20230801-modern-ui/blob/main/src/wagmi.ts)
because later in the article we add another chain ([Redstone Holesky(opens in
a new tab)](https://redstone.xyz/docs/network-info)).

    
    
    1import { getDefaultWallets } from '@rainbow-me/rainbowkit'
    
    2import { configureChains, createConfig } from 'wagmi'
    
    3import { holesky, sepolia } from 'wagmi/chains'

Import the blockchains the application supports. You can see the list of
supported chains [in the viem github(opens in a new
tab)](https://github.com/wagmi-dev/viem/tree/main/src/chains/definitions).

    
    
    1import { publicProvider } from 'wagmi/providers/public'
    
    2
    
    3const walletConnectProjectId = 'c96e690bb92b6311e8e9b2a6a22df575'

To be able to use [WalletConnect(opens in a new
tab)](https://walletconnect.com/) you need a project ID for your application.
You can get it [on cloud.walletconnect.com(opens in a new
tab)](https://cloud.walletconnect.com/sign-in).

    
    
    1const { chains, publicClient, webSocketPublicClient } = configureChains(
    
    2  [ holesky, sepolia ],
    
    3  [
    
    4    publicProvider(),
    
    5  ],
    
    6) 
    
    7
    
    8const { connectors } = getDefaultWallets({
    
    9  appName: 'My wagmi + RainbowKit App',
    
    10  chains,
    
    11  projectId: walletConnectProjectId,
    
    12})
    
    13
    
    14export const config = createConfig({
    
    15  autoConnect: true,
    
    16  connectors,
    
    17  publicClient,
    
    18  webSocketPublicClient,
    
    19})
    
    20
    
    21export { chains }
    
    Show all

### Adding another blockchain

These days there are a lot of [L2 scaling solution(opens in a new
tab)](https://ethereum.org/en/layer-2/), and you might want to support some
that viem does not support yet. To do it, you modify `src/wagmi.ts`. These
instructions explain how to add [Redstone Holesky(opens in a new
tab)](https://redstone.xyz/docs/network-info).

  1. Import the `defineChain` type from viem.
    
        1import { defineChain } from 'viem'

  2. Add the network definition.
    
        1const redstoneHolesky = defineChain({
    
    2   id: 17_001,
    
    3   name: 'Redstone Holesky',
    
    4   network: 'redstone-holesky',
    
    5   nativeCurrency: {
    
    6     decimals: 18,
    
    7     name: 'Ether',
    
    8     symbol: 'ETH',
    
    9   },
    
    10   rpcUrls: {
    
    11     default: {
    
    12       http: ['https://rpc.holesky.redstone.xyz'],
    
    13       webSocket: ['wss://rpc.holesky.redstone.xyz/ws'],
    
    14   },
    
    15   public: {  
    
    16       http: ['https://rpc.holesky.redstone.xyz'],
    
    17       webSocket: ['wss://rpc.holesky.redstone.xyz/ws'],
    
    18     },
    
    19   },
    
    20   blockExplorers: {
    
    21     default: { name: 'Explorer', url: 'https://explorer.holesky.redstone.xyz' },
    
    22   },
    
    23})
    
    Show all

  3. Add the new chain to the `configureChains` call.
    
        1 const { chains, publicClient, webSocketPublicClient } = configureChains(
    
    2   [ holesky, sepolia, redstoneHolesky ],
    
    3   [ publicProvider(), ],
    
    4 ) 

  4. Ensure that the application knows the address for your contracts on the new network. In this case, we modify `src/components/Greeter.tsx`:
    
        1const contractAddrs : AddressPerBlockchainType = {
    
    2  // Holesky
    
    3  17000: '0x432d810484AdD7454ddb3b5311f0Ac2E95CeceA8',
    
    4    
    
    5  // Redstone Holesky
    
    6  17001: '0x4919517f82a1B89a32392E1BF72ec827ba9986D3',
    
    7    
    
    8  // Sepolia
    
    9  11155111: '0x7143d5c190F048C8d19fe325b748b081903E3BF0'
    
    10}    
    
    Show all

# Conclusion

Of course, you don't really care about providing a user interface for
`Greeter`. You want to create a user interface for your own contracts. To
create your own application, run these steps:

  1. Specify to create a wagmi application.
    
        1pnpm create wagmi

  2. Name the application.

  3. Select **React** framework.

  4. Select the **Vite** variant.

  5. You can [add Rainbow kit(opens in a new tab)](https://www.rainbowkit.com/docs/installation#manual-setup).

Now go and make your contracts usable for the wide world.

w

Last edit: [@wackerow(opens in a new tab)](https://github.com/wackerow), March
13, 2024

See contributors

### Was this tutorial helpful?

YesNo

  * [Edit page(opens in a new tab)](https://github.com/ethereum/ethereum-org-website/tree/dev/public/content/developers/tutorials/creating-a-wagmi-ui-for-your-contract/index.md)
  * On this page

    * Why is this important
    * Greeter application
      * Installation
      * File walk through
        * index.html
        * src/main.tsx
        * src/App.tsx
        * src/components/Greeter.tsx
          * Greeter component
          * ShowGreeting component
          * ShowObject component
          * The final export
        * src/wagmi.ts
      * Adding another blockchain

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

