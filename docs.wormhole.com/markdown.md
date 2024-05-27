[![Logo](https://docs.wormhole.com/~gitbook/image?url=https%3A%2F%2F2048606572-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-
x-
prod.appspot.com%2Fo%2Fspaces%252F-MkD9YTtNUKJxtD9pDF-%252Flogo%252FwDuyYbL23bEko4ezEGwc%252Fwomrhole-
logo-full-color-
rgb-2000px%254072ppi.png%3Falt%3Dmedia%26token%3D065af9da-9035-441f-becd-924e7f965fd6&width=192&dpr=4&quality=100&sign=8b6d8ac729cc648283eccfaedf1d2a7c7a22aec027e5adaeae5dc5f7f2d3b1ce)![Logo](https://docs.wormhole.com/~gitbook/image?url=https%3A%2F%2F2048606572-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-
x-
prod.appspot.com%2Fo%2Fspaces%252F-MkD9YTtNUKJxtD9pDF-%252Flogo%252FIjJdYB4dIhpx6D2W6rvK%252Fwomrhole-
logo-reverse-
rgb-2000px%254072ppi.png%3Falt%3Dmedia%26token%3D53c890ce-0be0-4055-9ab9-b725392febca&width=192&dpr=4&quality=100&sign=cca296aceaf381ee2668c9a68a137496b0131a6c4a8d0e5e439065347fb218fb)](/wormhole)

SearchCtrl \+ K

  * [Introduction](/wormhole)

  * Quick Start

    * [Developing Cross Chain Dapps](/wormhole/quick-start/cross-chain-dev)

      * [Standard Relayer](/wormhole/quick-start/cross-chain-dev/standard-relayer)

      * [Specialized Relayer](/wormhole/quick-start/cross-chain-dev/specialized-relayer)

    * [Tutorials](/wormhole/quick-start/tutorials)

      * [Hello Wormhole](/wormhole/quick-start/tutorials/hello-wormhole)

        * [Hello Wormhole Explained](/wormhole/quick-start/tutorials/hello-wormhole/hello-wormhole-explained)

        * [Beyond Hello Wormhole](/wormhole/quick-start/tutorials/hello-wormhole/beyond-hello-wormhole)

      * [Hello Token](/wormhole/quick-start/tutorials/hello-token)

      * [CCTP](/wormhole/quick-start/tutorials/cctp)

        * [USDC Transfers With Connect SDK](/wormhole/quick-start/tutorials/cctp/sdk)

      * [Simple Relayer](/wormhole/quick-start/tutorials/relayer)

        * [Advanced Relayer Example](/wormhole/quick-start/tutorials/relayer/advanced-example)

    * [Demos](/wormhole/quick-start/demos)

    * [Wormhole Connect: Bridging Made Easy](/wormhole/quick-start/wh-connect)

  * Explore Wormhole

    * [Architecture](/wormhole/explore-wormhole/components)

    * [Security](/wormhole/explore-wormhole/security)

    * [Core Contracts](/wormhole/explore-wormhole/core-contracts)

    * [Guardians](/wormhole/explore-wormhole/guardian)

    * [VAAs](/wormhole/explore-wormhole/vaa)

    * [Relayers](/wormhole/explore-wormhole/relayer)

    * [Spy](/wormhole/explore-wormhole/spy)

    * [Gateway](/wormhole/explore-wormhole/gateway)

      * [Onboarding](/wormhole/explore-wormhole/gateway/onboard)

  * Reference

    * [Constants Reference](/wormhole/reference/constants)

    * [Development Environment](/wormhole/reference/dev-env)

      * [Tilt](/wormhole/reference/dev-env/tilt)

      * [Tooling](/wormhole/reference/dev-env/tooling)

    * [Blockchain Platforms](/wormhole/reference/blockchain-environments)

      * [Algorand](/wormhole/reference/blockchain-environments/algorand)

      * [Aptos](/wormhole/reference/blockchain-environments/aptos)

      * [CosmWasm](/wormhole/reference/blockchain-environments/cosmwasm)

      * [EVM](/wormhole/reference/blockchain-environments/evm)

        * [Relayer](/wormhole/reference/blockchain-environments/evm/relayer)

      * [Near](/wormhole/reference/blockchain-environments/near)

      * [Solana](/wormhole/reference/blockchain-environments/solana)

      * [Sui](/wormhole/reference/blockchain-environments/sui)

    * [API Docs](/wormhole/reference/api-docs)

      * [Wormholescan API](/wormhole/reference/api-docs/swagger)

    * [SDK Docs](/wormhole/reference/sdk-docs)

      * [Legacy SDK](/wormhole/reference/sdk-docs/legacy-sdk)

    * [CLI Docs](/wormhole/reference/cli-docs)

    * [Glossary](/wormhole/reference/glossary)

  * Wormhole Connect

    * [Overview](/wormhole/wormhole-connect/overview)

    * [Configuration](/wormhole/wormhole-connect/configuration)

  * Queries

    * [Overview](/wormhole/queries/overview)

    * [Getting Started](/wormhole/queries/getting-started)

    * [FAQs](/wormhole/queries/faqs)

  * External Links

    * [Explorer](https://wormholescan.io/)
    * [Ecosystem](https://wormhole.com/ecosystem)
    * [Guardian Dashboard](https://wormhole-foundation.github.io/wormhole-dashboard/)
    * [Portal Bridge Docs](https://www.portalbridge.com/docs/)
    * [Discord](https://discord.gg/hJfuptmg6b)
    * [Twitter](https://twitter.com/wormhole)
    * [Github](https://github.com/wormhole-foundation)

[Powered by
GitBook](https://www.gitbook.com/?utm_source=content&utm_medium=trademark&utm_campaign=-MkD9YTtNUKJxtD9pDF-)

# Introduction

Wormhole is a generic **message passing protocol** that enables communication
between blockchains.

![](https://docs.wormhole.com/~gitbook/image?url=https%3A%2F%2F2048606572-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-
x-prod.appspot.com%2Fo%2Fspaces%252F-MkD9YTtNUKJxtD9pDF-%252Fuploads%252Fgit-
blob-3326d3a40177a273c047e6386367a82d826b83b7%252Foversimplified.jpg%3Falt%3Dmedia&width=768&dpr=4&quality=100&sign=baa265dcd44e3219b102a208bd0ab323a59288dee23d3aecdd46cb95bccb639a)

Overview

The above is an _oversimplified_ illustration of the protocol, details about
the architecture and components are available [here](/wormhole/explore-
wormhole/components)

This simple **message passing protocol** enables developers and users of
[cross chain applications](/wormhole/reference/glossary#xdapps) built by
developers to leverage the advantages of multiple ecosystems.

###

What Isn't Wormhole?

Wormhole is _not_ a blockchain itself, it provides a means of communication
between blockchains or rollups.

Wormhole is _not_ a token bridge, though there are [protocols built on
Wormhole](https://www.portalbridge.com/#/transfer) that serve this purpose.

###

What can Wormhole be used for?

Consider the following examples of potential applications that are now
possible with Wormhole:

  1. **Cross Chain Exchange** : Using [Wormhole Connect](/wormhole/quick-start/wh-connect), a developer can build an exchange that allows deposits from any Wormhole connected chain, massively increasing the liquidity their users can access.

  2. **Cross Chain Governance** : If a group of NFT collections on different networks wanted their holders to vote on a combined proposal, they could pick a "voting" chain, and use Wormhole to communicate votes cast on their disparate chains to the voting chain.

  3. **Cross Chain Game** : A game could be built and played on a performant network like Solana, and it's rewards issued as NFTs on a different network, for example Ethereum.

##

Get Started

###

Quick Start Tutorials

Tutorials are available to get started quickly and explain the concepts
involved.

[![Cover](https://docs.wormhole.com/~gitbook/image?url=https%3A%2F%2F2048606572-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-
x-prod.appspot.com%2Fo%2Fspaces%252F-MkD9YTtNUKJxtD9pDF-%252Fuploads%252Fgit-
blob-6704d151fb9d7da3592d2dcc1b3b910c0bcc0c93%252Fwh-connect-
default.png%3Falt%3Dmedia&width=376&dpr=4&quality=100&sign=0ce5f0ba618ddbac06059fe80403da8cd5cb8fe892ec5c0f3efbc701fa3a3e82)**Quick
Start** \- Off ChainIntegrate Wormhole Connect to a new or existing web
UI](https://github.com/wormhole-
foundation/docs.wormhole.com/blob/main/docs/tutorials/quick-start/wormhole-
connect/wh-
connect.md)[![Cover](https://docs.wormhole.com/~gitbook/image?url=https%3A%2F%2F2048606572-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-
x-prod.appspot.com%2Fo%2Fspaces%252F-MkD9YTtNUKJxtD9pDF-%252Fuploads%252Fgit-
blob-ef2f7a48a7c20a32418f7cd81320196b3f909ab4%252Fwh-line-
art.png%3Falt%3Dmedia&width=376&dpr=4&quality=100&sign=9d030553999839168dbccaec9ca11619b6da8e16d368cc9413fac9fea8acbf99)**Quick
Start** \- On ChainSend your first cross chain message](/wormhole/quick-
start/cross-chain-dev)

More tutorials are available [here](https://github.com/wormhole-
foundation/docs.wormhole.com/blob/main/docs/tutorials/quick-start/README.md).

###

Explore

Find out more about the Wormhole ecosystem, components, and protocols.

[![Cover](https://docs.wormhole.com/~gitbook/image?url=https%3A%2F%2F2048606572-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-
x-prod.appspot.com%2Fo%2Fspaces%252F-MkD9YTtNUKJxtD9pDF-%252Fuploads%252Fgit-
blob-e4d10cb3b7f8175d8ab9358d88139f634e1a70ca%252Fdetailed-
flow.jpg%3Falt%3Dmedia&width=376&dpr=4&quality=100&sign=46e937991977877372672883a1be57b09773bfe8e9c5f919733274538d8fc6f4)**Architecture**
Dig into the components of the protocol](/wormhole/explore-
wormhole/components)[![Cover](https://docs.wormhole.com/~gitbook/image?url=https%3A%2F%2F2048606572-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-
x-prod.appspot.com%2Fo%2Fspaces%252F-MkD9YTtNUKJxtD9pDF-%252Fuploads%252Fgit-
blob-d0979f08691ae1024b28c54dfd2e4459ee14cc3b%252Fprotocols.png%3Falt%3Dmedia&width=376&dpr=4&quality=100&sign=bfa4768c938798247cad8d7f0d1db597a903240f9d168655a5019b19bdd08b79)**Protocol
Specifications** Find out more about the protocols built on top of
Wormhole](https://github.com/wormhole-
foundation/wormhole/tree/main/whitepapers)

###

Demos

Demos provide more realistic implementations than Tutorials

[![Cover](https://docs.wormhole.com/~gitbook/image?url=https%3A%2F%2F2048606572-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-
x-prod.appspot.com%2Fo%2Fspaces%252F-MkD9YTtNUKJxtD9pDF-%252Fuploads%252Fgit-
blob-c4d7ec15aa7beac6952a3730a650a418ee85ddb8%252Fscaffolding.jpg%3Falt%3Dmedia&width=376&dpr=4&quality=100&sign=ce756471d7a6d0181492c26e56329899ef68a341862ed9602423cf93a8d67b92)**Wormhole
Scaffolding** Quickly spin up a project with the Scaffolding
repo](https://github.com/wormhole-foundation/wormhole-
scaffolding)[![Cover](https://docs.wormhole.com/~gitbook/image?url=https%3A%2F%2F2048606572-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-
x-prod.appspot.com%2Fo%2Fspaces%252F-MkD9YTtNUKJxtD9pDF-%252Fuploads%252Fgit-
blob-2cf164ae108ea5e6dc8e13cb7284d27f5ff91468%252Fprojects.png%3Falt%3Dmedia&width=376&dpr=4&quality=100&sign=48a0b29844d75375c1505effee6bcd02101278b6065ec1c44759566834979e1a)**xDapp
book projects** Run and learn from example
programs](https://github.com/wormhole-foundation/xdapp-
book/tree/main/projects)

More Demos are available [here](/wormhole/quick-start/demos).

###

Wormhole integration complete?

Let us know so we can list your project in our ecosystem directory and
introduce you to our global, multichain community!

[Reach out
now!](https://forms.clickup.com/45049775/f/1aytxf-10244/JKYWRUQ70AUI99F32Q)

##

Supported Blockchains

Wormhole supports a growing number of blockchains

[![Cover](https://docs.wormhole.com/~gitbook/image?url=https%3A%2F%2F2048606572-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-
x-prod.appspot.com%2Fo%2Fspaces%252F-MkD9YTtNUKJxtD9pDF-%252Fuploads%252Fgit-
blob-3ecaabaf18e4a2949454de21ce7e483d0d0f9bb8%252Facala.svg%3Falt%3Dmedia&width=245&dpr=4&quality=100&sign=2e71a5608def4b71cae56e36901ce317e76fbc37e48075062129bcdd58d0587b)**Acala**](/wormhole/reference/blockchain-
environments/evm#acala)[![Cover](https://docs.wormhole.com/~gitbook/image?url=https%3A%2F%2F2048606572-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-
x-prod.appspot.com%2Fo%2Fspaces%252F-MkD9YTtNUKJxtD9pDF-%252Fuploads%252Fgit-
blob-65c0beb39f62d68fd57af7703195e24107699cb6%252Falgorand.svg%3Falt%3Dmedia&width=245&dpr=4&quality=100&sign=2bd22110a1478b0200cc6d9d31bd9ef6e9e3df6d3a5e8d2dac85aaa5699d42cd)**Algorand**](/wormhole/reference/blockchain-
environments/algorand#algorand)[![Cover](https://docs.wormhole.com/~gitbook/image?url=https%3A%2F%2F2048606572-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-
x-prod.appspot.com%2Fo%2Fspaces%252F-MkD9YTtNUKJxtD9pDF-%252Fuploads%252Fgit-
blob-9dd84dd2aa9037c1606321c07ac201858bfeea94%252Faptos.svg%3Falt%3Dmedia&width=245&dpr=4&quality=100&sign=453d9e23d1c633df0e1bea17e6b0d71c7a5d919dad31cda8c4a3eeea8db2fffe)**Aptos**](/wormhole/reference/blockchain-
environments/aptos#aptos)[![Cover](https://docs.wormhole.com/~gitbook/image?url=https%3A%2F%2F2048606572-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-
x-prod.appspot.com%2Fo%2Fspaces%252F-MkD9YTtNUKJxtD9pDF-%252Fuploads%252Fgit-
blob-
ec4822d468aaeb3137c4a390f8e243873faed6fc%252Farbitrum.svg%3Falt%3Dmedia&width=245&dpr=4&quality=100&sign=3e2b8969cfb82eb6a71ba6c94e4c74f170b7628bf7756c637ecb362c8bbf0c08)**Arbitrum**](/wormhole/reference/blockchain-
environments/evm#arbitrum)[![Cover](https://docs.wormhole.com/~gitbook/image?url=https%3A%2F%2F2048606572-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-
x-prod.appspot.com%2Fo%2Fspaces%252F-MkD9YTtNUKJxtD9pDF-%252Fuploads%252Fgit-
blob-
ec4822d468aaeb3137c4a390f8e243873faed6fc%252Farbitrum_sepolia.svg%3Falt%3Dmedia&width=245&dpr=4&quality=100&sign=84b1ca2786110f1219081bb5482a180a95c68291062faffe8ab67688de400f41)**Arbitrum
Sepolia**](/wormhole/reference/blockchain-
environments/evm#arbitrum_sepolia)[![Cover](https://docs.wormhole.com/~gitbook/image?url=https%3A%2F%2F2048606572-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-
x-prod.appspot.com%2Fo%2Fspaces%252F-MkD9YTtNUKJxtD9pDF-%252Fuploads%252Fgit-
blob-97457ade59797bfba322168fd3d5376c828dee8c%252Favalanche.svg%3Falt%3Dmedia&width=245&dpr=4&quality=100&sign=5cd7606f24bba86e586fb2621608ea8d5c156290ad9b058ecd383331b21d7b0f)**Avalanche**](/wormhole/reference/blockchain-
environments/evm#avalanche)[![Cover](https://docs.wormhole.com/~gitbook/image?url=https%3A%2F%2F2048606572-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-
x-prod.appspot.com%2Fo%2Fspaces%252F-MkD9YTtNUKJxtD9pDF-%252Fuploads%252Fgit-
blob-41288872bc552e8822f8760e39b9829a60a31e33%252Fbase.svg%3Falt%3Dmedia&width=245&dpr=4&quality=100&sign=66885eaa91fa4ef63b7518715d219719abc3ad1144661eb61e77cc5a1d903399)**Base**](/wormhole/reference/blockchain-
environments/evm#base)[![Cover](https://docs.wormhole.com/~gitbook/image?url=https%3A%2F%2F2048606572-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-
x-prod.appspot.com%2Fo%2Fspaces%252F-MkD9YTtNUKJxtD9pDF-%252Fuploads%252Fgit-
blob-41288872bc552e8822f8760e39b9829a60a31e33%252Fbase_sepolia.svg%3Falt%3Dmedia&width=245&dpr=4&quality=100&sign=11b67b79efd557a4fe34f5b57f3b210d1560d565bcdb7ef464bb78497725a47e)**Base
Sepolia**](/wormhole/reference/blockchain-
environments/evm#base_sepolia)[![Cover](https://docs.wormhole.com/~gitbook/image?url=https%3A%2F%2F2048606572-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-
x-prod.appspot.com%2Fo%2Fspaces%252F-MkD9YTtNUKJxtD9pDF-%252Fuploads%252Fgit-
blob-d7e094872b7499cd9d448e180b395a848deb8a12%252Fberachain.svg%3Falt%3Dmedia&width=245&dpr=4&quality=100&sign=e1467fa42ce8872586c572284731d2d8cf069954621c41ed0bfd047fd1ed2c8e)**Berachain**](/wormhole/reference/blockchain-
environments/evm#berachain)[![Cover](https://docs.wormhole.com/~gitbook/image?url=https%3A%2F%2F2048606572-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-
x-prod.appspot.com%2Fo%2Fspaces%252F-MkD9YTtNUKJxtD9pDF-%252Fuploads%252Fgit-
blob-4426a47a16532d5219ee736a777713d8dc05165b%252Fblast.svg%3Falt%3Dmedia&width=245&dpr=4&quality=100&sign=1d6e219f5793723caf34a986eb97ed526c8b2e7ac54e36551337474ce957df2f)**Blast**](/wormhole/reference/blockchain-
environments/evm#blast)[![Cover](https://docs.wormhole.com/~gitbook/image?url=https%3A%2F%2F2048606572-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-
x-prod.appspot.com%2Fo%2Fspaces%252F-MkD9YTtNUKJxtD9pDF-%252Fuploads%252Fgit-
blob-a230021c195aafe37a8f57e50721bc31eb65a948%252Fbsc.svg%3Falt%3Dmedia&width=245&dpr=4&quality=100&sign=49b38663d3e113dd83f49618e0fe955939e499cd70b26e7112fd59a7c1c77308)**BNB
Smart Chain**](/wormhole/reference/blockchain-
environments/evm#bsc)[![Cover](https://docs.wormhole.com/~gitbook/image?url=https%3A%2F%2F2048606572-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-
x-prod.appspot.com%2Fo%2Fspaces%252F-MkD9YTtNUKJxtD9pDF-%252Fuploads%252Fgit-
blob-0034b6a792bfc060b858ab423461ac36dfdb05e0%252Fcelestia.svg%3Falt%3Dmedia&width=245&dpr=4&quality=100&sign=c0a91e1170ff81b8617dee348434db34d1511196e5defb88fc3351378fc8662b)**Celestia**](/wormhole/reference/blockchain-
environments/cosmwasm#celestia)[![Cover](https://docs.wormhole.com/~gitbook/image?url=https%3A%2F%2F2048606572-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-
x-prod.appspot.com%2Fo%2Fspaces%252F-MkD9YTtNUKJxtD9pDF-%252Fuploads%252Fgit-
blob-
cf17826082d15ab7a45149fa7af12c6959e0f9f3%252Fcelo.svg%3Falt%3Dmedia&width=245&dpr=4&quality=100&sign=10a55b55236046c7109c0795b95b485ed456c038613e92215f7fbffaa0d1fbe7)**Celo**](/wormhole/reference/blockchain-
environments/evm#celo)[![Cover](https://docs.wormhole.com/~gitbook/image?url=https%3A%2F%2F2048606572-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-
x-prod.appspot.com%2Fo%2Fspaces%252F-MkD9YTtNUKJxtD9pDF-%252Fuploads%252Fgit-
blob-
bdc37656dd6d146bd298d895c40522c9fa6656c7%252Fcosmoshub.svg%3Falt%3Dmedia&width=245&dpr=4&quality=100&sign=4d30929b324742c79d3bf011fc7b5ae27f22f1e53c6178ff250f44bb6736aad4)**Cosmoshub**](/wormhole/reference/blockchain-
environments/cosmwasm#cosmoshub)[![Cover](https://docs.wormhole.com/~gitbook/image?url=https%3A%2F%2F2048606572-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-
x-prod.appspot.com%2Fo%2Fspaces%252F-MkD9YTtNUKJxtD9pDF-%252Fuploads%252Fgit-
blob-c19e60c9796c66e290cb0549d599ac3432409afe%252Fdymension.svg%3Falt%3Dmedia&width=245&dpr=4&quality=100&sign=b298484f064ff529e17cd5e34ff5bbcda022570b0a04ef04f597e7095898db08)**Dymension**](/wormhole/reference/blockchain-
environments/cosmwasm#dymension)[![Cover](https://docs.wormhole.com/~gitbook/image?url=https%3A%2F%2F2048606572-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-
x-prod.appspot.com%2Fo%2Fspaces%252F-MkD9YTtNUKJxtD9pDF-%252Fuploads%252Fgit-
blob-a77c4ef8243f93d61839fb234ba4bceda786643b%252Fethereum.svg%3Falt%3Dmedia&width=245&dpr=4&quality=100&sign=b5144839c9329246918236381da28a00a070204b282bc475d333846367143c12)**Ethereum**](/wormhole/reference/blockchain-
environments/evm#ethereum)[![Cover](https://docs.wormhole.com/~gitbook/image?url=https%3A%2F%2F2048606572-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-
x-prod.appspot.com%2Fo%2Fspaces%252F-MkD9YTtNUKJxtD9pDF-%252Fuploads%252Fgit-
blob-856da6fc64ad47642a79c2e967ccd8430d886314%252Fevmos.svg%3Falt%3Dmedia&width=245&dpr=4&quality=100&sign=8d1ce6f26cf6af662d77d7ea4e984e7dc7f6de87cdda234b10415ae0559efa2a)**Evmos**](/wormhole/reference/blockchain-
environments/cosmwasm#evmos)[![Cover](https://docs.wormhole.com/~gitbook/image?url=https%3A%2F%2F2048606572-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-
x-prod.appspot.com%2Fo%2Fspaces%252F-MkD9YTtNUKJxtD9pDF-%252Fuploads%252Fgit-
blob-2ba19877a41ee82010875a5518e8d68f3ce1effd%252Ffantom.svg%3Falt%3Dmedia&width=245&dpr=4&quality=100&sign=4d27acd06c7492afec61d980f07f501b97cdd1ff9ff1ac746aaf78677984ea1f)**Fantom**](/wormhole/reference/blockchain-
environments/evm#fantom)[![Cover](https://docs.wormhole.com/~gitbook/image?url=https%3A%2F%2F2048606572-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-
x-prod.appspot.com%2Fo%2Fspaces%252F-MkD9YTtNUKJxtD9pDF-%252Fuploads%252Fgit-
blob-0a72e0bdc5f4cfe8bc945a9a1f5887e585c1edb9%252Fgnosis.svg%3Falt%3Dmedia&width=245&dpr=4&quality=100&sign=1b86d31e36cc8bb2af4a0a47607abf391be8a6f8e6a2a4ea063ec103f3cc56c5)**Gnosis**](/wormhole/reference/blockchain-
environments/evm#gnosis)[![Cover](https://docs.wormhole.com/~gitbook/image?url=https%3A%2F%2F2048606572-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-
x-prod.appspot.com%2Fo%2Fspaces%252F-MkD9YTtNUKJxtD9pDF-%252Fuploads%252Fgit-
blob-a77c4ef8243f93d61839fb234ba4bceda786643b%252Fholesky.svg%3Falt%3Dmedia&width=245&dpr=4&quality=100&sign=817f42301c37bf208e98178559cded192194c9625cc9685275f85918cb1a3a91)**Ethereum
Holesky**](/wormhole/reference/blockchain-
environments/evm#holesky)[![Cover](https://docs.wormhole.com/~gitbook/image?url=https%3A%2F%2F2048606572-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-
x-prod.appspot.com%2Fo%2Fspaces%252F-MkD9YTtNUKJxtD9pDF-%252Fuploads%252Fgit-
blob-2a7e7257fb8f521c0a79595cd58b65d04adee7c4%252Finjective.svg%3Falt%3Dmedia&width=245&dpr=4&quality=100&sign=0df1f2b0f35f7a6aef975df6af2ef545446a2165bee297889c8f294b98fc215c)**Injective**](/wormhole/reference/blockchain-
environments/cosmwasm#injective)[![Cover](https://docs.wormhole.com/~gitbook/image?url=https%3A%2F%2F2048606572-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-
x-prod.appspot.com%2Fo%2Fspaces%252F-MkD9YTtNUKJxtD9pDF-%252Fuploads%252Fgit-
blob-9adc2f0afb92650cc606b29f907b7773051eb8bf%252Fkarura.svg%3Falt%3Dmedia&width=245&dpr=4&quality=100&sign=6c8342b01e4ca7c37a2e7b5002132382db1116ff70f810d1fc79df4ca3d876bb)**Karura**](/wormhole/reference/blockchain-
environments/evm#karura)[![Cover](https://docs.wormhole.com/~gitbook/image?url=https%3A%2F%2F2048606572-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-
x-prod.appspot.com%2Fo%2Fspaces%252F-MkD9YTtNUKJxtD9pDF-%252Fuploads%252Fgit-
blob-4086eb5225dd136c1c2cd0aaf2902f43f5d963a8%252Fklaytn.svg%3Falt%3Dmedia&width=245&dpr=4&quality=100&sign=bb6e06d098dbb6ded975a93d8df1426c879dde969335f04fc5e28b8935a95678)**Klaytn**](/wormhole/reference/blockchain-
environments/evm#klaytn)[![Cover](https://docs.wormhole.com/~gitbook/image?url=https%3A%2F%2F2048606572-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-
x-prod.appspot.com%2Fo%2Fspaces%252F-MkD9YTtNUKJxtD9pDF-%252Fuploads%252Fgit-
blob-d51b03d3e63e74863307d9642e43e212e68a3ff5%252Fkujira.svg%3Falt%3Dmedia&width=245&dpr=4&quality=100&sign=4231e2ed24690ebab8cad6a216cbf348aa0f9acdaf4089ba54c6609e4ffe9e03)**Kujira**](/wormhole/reference/blockchain-
environments/cosmwasm#kujira)[![Cover](https://docs.wormhole.com/~gitbook/image?url=https%3A%2F%2F2048606572-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-
x-prod.appspot.com%2Fo%2Fspaces%252F-MkD9YTtNUKJxtD9pDF-%252Fuploads%252Fgit-
blob-1a35f4c3b39e6234fe2d9fdcfcc32c3f51c82eee%252Flinea.svg%3Falt%3Dmedia&width=245&dpr=4&quality=100&sign=35fb28318a4825ececbfcdc7386cd677d6122699be719836659a5ecb0f28509f)**Linea**](/wormhole/reference/blockchain-
environments/evm#linea)[![Cover](https://docs.wormhole.com/~gitbook/image?url=https%3A%2F%2F2048606572-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-
x-prod.appspot.com%2Fo%2Fspaces%252F-MkD9YTtNUKJxtD9pDF-%252Fuploads%252Fgit-
blob-51447703f8c76cebd7f738911eb9aa95399c54f7%252Fmantle.svg%3Falt%3Dmedia&width=245&dpr=4&quality=100&sign=7477329c733582e30cb6099b38063e2464a5f96b0008550f8fa8efaf2d47b1a6)**Mantle**](/wormhole/reference/blockchain-
environments/evm#mantle)[![Cover](https://docs.wormhole.com/~gitbook/image?url=https%3A%2F%2F2048606572-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-
x-prod.appspot.com%2Fo%2Fspaces%252F-MkD9YTtNUKJxtD9pDF-%252Fuploads%252Fgit-
blob-50678dc34aca936ea7da37cc70a5fcef9f3a9469%252Fmoonbeam.svg%3Falt%3Dmedia&width=245&dpr=4&quality=100&sign=e21fba4328159ca9d87539f8b115e06b00134db6af9c97560a6d8bb4eb5cec4a)**Moonbeam**](/wormhole/reference/blockchain-
environments/evm#moonbeam)[![Cover](https://docs.wormhole.com/~gitbook/image?url=https%3A%2F%2F2048606572-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-
x-prod.appspot.com%2Fo%2Fspaces%252F-MkD9YTtNUKJxtD9pDF-%252Fuploads%252Fgit-
blob-923fb49131487fb7c08e029553b5e0253c26d4d6%252Fnear.svg%3Falt%3Dmedia&width=245&dpr=4&quality=100&sign=decf022dd4b3c86eed7f23e57218770c1aaad695aaca416eba9b1f91187bf5a5)**NEAR**](/wormhole/reference/blockchain-
environments/near#near)[![Cover](https://docs.wormhole.com/~gitbook/image?url=https%3A%2F%2F2048606572-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-
x-prod.appspot.com%2Fo%2Fspaces%252F-MkD9YTtNUKJxtD9pDF-%252Fuploads%252Fgit-
blob-7d3a07fad397e6c0794a23fe9a9ff2457e6e3b37%252Fneon.svg%3Falt%3Dmedia&width=245&dpr=4&quality=100&sign=f97750151f93cc8eda353cc41cc44f0c8b38682d5df366bc36865d708c6991f6)**Neon**](/wormhole/reference/blockchain-
environments/evm#neon)[![Cover](https://docs.wormhole.com/~gitbook/image?url=https%3A%2F%2F2048606572-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-
x-prod.appspot.com%2Fo%2Fspaces%252F-MkD9YTtNUKJxtD9pDF-%252Fuploads%252Fgit-
blob-
df05ebaeed1529bd0cf2071c832f0080dfe4d864%252Fneutron.svg%3Falt%3Dmedia&width=245&dpr=4&quality=100&sign=6209fd148a443daa643c1c7f62e51fd2f8050052cbb94e392615fe6816d0f322)**Neutron**](/wormhole/reference/blockchain-
environments/cosmwasm#neutron)[![Cover](https://docs.wormhole.com/~gitbook/image?url=https%3A%2F%2F2048606572-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-
x-prod.appspot.com%2Fo%2Fspaces%252F-MkD9YTtNUKJxtD9pDF-%252Fuploads%252Fgit-
blob-03d31e32407d731c373c988e8f7ecffe2daeb730%252Foasis.svg%3Falt%3Dmedia&width=245&dpr=4&quality=100&sign=c1af30ef27ada81e86175f36e2b44f5387609c1250b424ac3d9899d122dab036)**Oasis**](/wormhole/reference/blockchain-
environments/evm#oasis)[![Cover](https://docs.wormhole.com/~gitbook/image?url=https%3A%2F%2F2048606572-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-
x-prod.appspot.com%2Fo%2Fspaces%252F-MkD9YTtNUKJxtD9pDF-%252Fuploads%252Fgit-
blob-d745e3011192ff53cfbc73483add958677eaac55%252Foptimism.svg%3Falt%3Dmedia&width=245&dpr=4&quality=100&sign=b348063b365f78addfa75d3b68698af1afcaf114770b869e5d8fe85269e29cf5)**Optimism**](/wormhole/reference/blockchain-
environments/evm#optimism)[![Cover](https://docs.wormhole.com/~gitbook/image?url=https%3A%2F%2F2048606572-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-
x-prod.appspot.com%2Fo%2Fspaces%252F-MkD9YTtNUKJxtD9pDF-%252Fuploads%252Fgit-
blob-d745e3011192ff53cfbc73483add958677eaac55%252Foptimism_sepolia.svg%3Falt%3Dmedia&width=245&dpr=4&quality=100&sign=3d3788d6886f959ec9a2777f185dbbcf468727b73fdc4fe68dc6f561204ee0a5)**Optimism
Sepolia**](/wormhole/reference/blockchain-
environments/evm#optimism_sepolia)[![Cover](https://docs.wormhole.com/~gitbook/image?url=https%3A%2F%2F2048606572-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-
x-prod.appspot.com%2Fo%2Fspaces%252F-MkD9YTtNUKJxtD9pDF-%252Fuploads%252Fgit-
blob-
fa14ec47ca743b1bf36f004775f84561714f564c%252Fosmosis.svg%3Falt%3Dmedia&width=245&dpr=4&quality=100&sign=147f55ce005c8cb8fce6a43cdf5ae254bc9209bc6ff0c5b51f3b6ca8f0398412)**Osmosis**](/wormhole/reference/blockchain-
environments/cosmwasm#osmosis)[![Cover](https://docs.wormhole.com/~gitbook/image?url=https%3A%2F%2F2048606572-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-
x-prod.appspot.com%2Fo%2Fspaces%252F-MkD9YTtNUKJxtD9pDF-%252Fuploads%252Fgit-
blob-509726f75f9a7fcf9978aaec82f86128b5ffdf21%252Fpolygon.svg%3Falt%3Dmedia&width=245&dpr=4&quality=100&sign=8810d3ebf35df4cf8a35e835593f87b6613e13ed24591aca463a039935478787)**Polygon**](/wormhole/reference/blockchain-
environments/evm#polygon)[![Cover](https://docs.wormhole.com/~gitbook/image?url=https%3A%2F%2F2048606572-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-
x-prod.appspot.com%2Fo%2Fspaces%252F-MkD9YTtNUKJxtD9pDF-%252Fuploads%252Fgit-
blob-509726f75f9a7fcf9978aaec82f86128b5ffdf21%252Fpolygon_sepolia.svg%3Falt%3Dmedia&width=245&dpr=4&quality=100&sign=f3e23d089071c1449a08a2d04696692d866e69d6e7873fa1fbf494a9ac42b4de)**Polygon
Sepolia**](/wormhole/reference/blockchain-
environments/evm#polygon_sepolia)[![Cover](https://docs.wormhole.com/~gitbook/image?url=https%3A%2F%2F2048606572-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-
x-prod.appspot.com%2Fo%2Fspaces%252F-MkD9YTtNUKJxtD9pDF-%252Fuploads%252Fgit-
blob-294f46e096a757f4d03f6717dde03812afd86a14%252Fprovenance.svg%3Falt%3Dmedia&width=245&dpr=4&quality=100&sign=3ad950adfcc908183beb3fa0f6955e67e6c1de7803dcf2e30abe8a671fc018e9)**Provenance**](/wormhole/reference/blockchain-
environments/cosmwasm#provenance)[![Cover](https://docs.wormhole.com/~gitbook/image?url=https%3A%2F%2F2048606572-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-
x-prod.appspot.com%2Fo%2Fspaces%252F-MkD9YTtNUKJxtD9pDF-%252Fuploads%252Fgit-
blob-
deb0824b2f6aff76dd7e44b985019b73323708da%252Fpythnet.svg%3Falt%3Dmedia&width=245&dpr=4&quality=100&sign=8025604b8dc91fa3dcbb5c443349e6ead73c5a59e63714f1e8d6334b4c7c9028)**Pythnet**](/wormhole/reference/blockchain-
environments/solana#pythnet)[![Cover](https://docs.wormhole.com/~gitbook/image?url=https%3A%2F%2F2048606572-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-
x-prod.appspot.com%2Fo%2Fspaces%252F-MkD9YTtNUKJxtD9pDF-%252Fuploads%252Fgit-
blob-
bfc81967e458e3118c4c16858faa948a2deba770%252Frootstock.svg%3Falt%3Dmedia&width=245&dpr=4&quality=100&sign=85543e342497eb1e666c32bf50a64b8aa33a9eff9dcd3a5fcd19cbd40cb07415)**Rootstock**](/wormhole/reference/blockchain-
environments/evm#rootstock)[![Cover](https://docs.wormhole.com/~gitbook/image?url=https%3A%2F%2F2048606572-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-
x-prod.appspot.com%2Fo%2Fspaces%252F-MkD9YTtNUKJxtD9pDF-%252Fuploads%252Fgit-
blob-465743abb55bfb1af94cc2ca706373dc5f9205d0%252Fscroll.svg%3Falt%3Dmedia&width=245&dpr=4&quality=100&sign=02ebdf488f7615a14c99bc5bb1d73609d63127f6967010742c9f886904af3cd7)**Scroll**](/wormhole/reference/blockchain-
environments/evm#scroll)[![Cover](https://docs.wormhole.com/~gitbook/image?url=https%3A%2F%2F2048606572-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-
x-prod.appspot.com%2Fo%2Fspaces%252F-MkD9YTtNUKJxtD9pDF-%252Fuploads%252Fgit-
blob-97860987333531c98586e6a5c6209c1b9f2068e6%252Fseda.svg%3Falt%3Dmedia&width=245&dpr=4&quality=100&sign=02600c0516ab380511a4e0b59480125aba960fe6835bcae42ff72a389b2253e6)**Seda**](/wormhole/reference/blockchain-
environments/cosmwasm#seda)[![Cover](https://docs.wormhole.com/~gitbook/image?url=https%3A%2F%2F2048606572-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-
x-prod.appspot.com%2Fo%2Fspaces%252F-MkD9YTtNUKJxtD9pDF-%252Fuploads%252Fgit-
blob-a8a01c24b0bb5add88bc68de2ae8664c00a4062a%252Fsei.svg%3Falt%3Dmedia&width=245&dpr=4&quality=100&sign=86c2b7f1c0788f3609afe4410cc7dd0796bec2a791d08f2c1e1facb34fb49959)**Sei**](/wormhole/reference/blockchain-
environments/cosmwasm#sei)[![Cover](https://docs.wormhole.com/~gitbook/image?url=https%3A%2F%2F2048606572-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-
x-prod.appspot.com%2Fo%2Fspaces%252F-MkD9YTtNUKJxtD9pDF-%252Fuploads%252Fgit-
blob-a8a01c24b0bb5add88bc68de2ae8664c00a4062a%252Fseievm.svg%3Falt%3Dmedia&width=245&dpr=4&quality=100&sign=56dfba675052b87d35370decffd073406a44775220737317f077df073c7e03d7)**Seievm**](/wormhole/reference/blockchain-
environments/evm#seievm)[![Cover](https://docs.wormhole.com/~gitbook/image?url=https%3A%2F%2F2048606572-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-
x-prod.appspot.com%2Fo%2Fspaces%252F-MkD9YTtNUKJxtD9pDF-%252Fuploads%252Fgit-
blob-a77c4ef8243f93d61839fb234ba4bceda786643b%252Fsepolia.svg%3Falt%3Dmedia&width=245&dpr=4&quality=100&sign=b1c3ca85d0f5a7a9890b68ba7066eb25f243611f37a1b077bbf00364e319b2aa)**Ethereum
Sepolia**](/wormhole/reference/blockchain-
environments/evm#sepolia)[![Cover](https://docs.wormhole.com/~gitbook/image?url=https%3A%2F%2F2048606572-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-
x-prod.appspot.com%2Fo%2Fspaces%252F-MkD9YTtNUKJxtD9pDF-%252Fuploads%252Fgit-
blob-0bc268d3d0ecc12656b3dd9115b49d4453ecfe81%252Fsolana.svg%3Falt%3Dmedia&width=245&dpr=4&quality=100&sign=02913ef2bfadd6ef2f7fbb7c81d8dd99adf9a9975bf35f6e418a5d78dff80308)**Solana**](/wormhole/reference/blockchain-
environments/solana#solana)[![Cover](https://docs.wormhole.com/~gitbook/image?url=https%3A%2F%2F2048606572-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-
x-prod.appspot.com%2Fo%2Fspaces%252F-MkD9YTtNUKJxtD9pDF-%252Fuploads%252Fgit-
blob-735dac53948f5d38b72d01c84dd4cc68e40f3e01%252Fstargaze.svg%3Falt%3Dmedia&width=245&dpr=4&quality=100&sign=f125f6c20c98e9111d6e454df0b1389db39a0bec132f8edcd3047e83be59ed51)**Stargaze**](/wormhole/reference/blockchain-
environments/cosmwasm#stargaze)[![Cover](https://docs.wormhole.com/~gitbook/image?url=https%3A%2F%2F2048606572-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-
x-prod.appspot.com%2Fo%2Fspaces%252F-MkD9YTtNUKJxtD9pDF-%252Fuploads%252Fgit-
blob-5feb14763913edd8f5f4ab5224241ed44b93feee%252Fsui.svg%3Falt%3Dmedia&width=245&dpr=4&quality=100&sign=4d2ddfc8e37573b9fcb7b5571f7df244585dba2fd039bbed2cb22239e4a64343)**Sui**](/wormhole/reference/blockchain-
environments/sui#sui)[![Cover](https://docs.wormhole.com/~gitbook/image?url=https%3A%2F%2F2048606572-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-
x-prod.appspot.com%2Fo%2Fspaces%252F-MkD9YTtNUKJxtD9pDF-%252Fuploads%252Fgit-
blob-a89918bb7bbfc3e203318425c4347bf4cad56701%252Fterra.svg%3Falt%3Dmedia&width=245&dpr=4&quality=100&sign=76f23b8d7bfe0a298022a512aa5391020d8d9e5e8e73f4a467f278ddc026365e)**Terra**](/wormhole/reference/blockchain-
environments/cosmwasm#terra)[![Cover](https://docs.wormhole.com/~gitbook/image?url=https%3A%2F%2F2048606572-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-
x-prod.appspot.com%2Fo%2Fspaces%252F-MkD9YTtNUKJxtD9pDF-%252Fuploads%252Fgit-
blob-39c6a1c0526bf32a7cdcd279d759e86ef226deb5%252Fterra2.svg%3Falt%3Dmedia&width=245&dpr=4&quality=100&sign=4afab0b2224d621cf1ff3dcaf1c16063ee968bea53289db07207e769c5a79bb4)**Terra2**](/wormhole/reference/blockchain-
environments/cosmwasm#terra2)[![Cover](https://docs.wormhole.com/~gitbook/image?url=https%3A%2F%2F2048606572-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-
x-prod.appspot.com%2Fo%2Fspaces%252F-MkD9YTtNUKJxtD9pDF-%252Fuploads%252Fgit-
blob-2ff5dd603b1de06bf92d9e33c0ee082cbd188fdc%252Fxlayer.svg%3Falt%3Dmedia&width=245&dpr=4&quality=100&sign=bcafad11af479b0d622ac5a0c72d241ec45778f780665fed5ab351745f43b5ce)**Xlayer**](/wormhole/reference/blockchain-
environments/evm#xlayer)[![Cover](https://docs.wormhole.com/~gitbook/image?url=https%3A%2F%2F2048606572-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-
x-prod.appspot.com%2Fo%2Fspaces%252F-MkD9YTtNUKJxtD9pDF-%252Fuploads%252Fgit-
blob-63f341e6af0c5da2b1c1b0c0d2e74d8f1f764177%252Fxpla.svg%3Falt%3Dmedia&width=245&dpr=4&quality=100&sign=bdc8fa9be178ff0db396ef91113a224dcdd3a9bfdd6f1859cb64101c883193e9)**Xpla**](/wormhole/reference/blockchain-
environments/cosmwasm#xpla)

Last updated 9 days ago

On this page

  * What Isn't Wormhole?
  * What can Wormhole be used for?
  * Get Started
  * Quick Start Tutorials
  * Explore
  * Demos
  * Supported Blockchains

Was this helpful?

[Edit on GitHub](https://github.com/wormhole-
foundation/docs.wormhole.com/blob/main/docs/README.md)

