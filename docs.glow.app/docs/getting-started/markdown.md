Jump to Content

[![Glow](https://files.readme.io/41e06ed-GlowIcon.svg)](https://glow.app)

[ __Guides](/docs)[ __API Reference](/reference)

v1.0

* * *

[Log In](/login?redirect_uri=/docs/getting-
started)[![Glow](https://files.readme.io/41e06ed-
GlowIcon.svg)](https://glow.app)

 __

[Log In](/login?redirect_uri=/docs/getting-started)

v1.0[ __Guides](/docs)[ __API Reference](/reference) Loading…

Search

## Integrating with Glow

  * [ __Glow Javascript SDK](/docs/getting-started)
    * [ Detecting Glow](/docs/detecting-glow)
    * [Connecting and Signing In](/docs/connecting-signing-in)
    * [Signing Messages](/docs/signing-messages)
    * [Executing Transactions](/docs/executing-transactions)
  * [ __Glow ID](/docs/glow-id)
    * [ Registering for Glow ID](/docs/registering-for-glow-id)
    * [Resolve Glow ID via Chain](/docs/resolving-glow-id)
    * [Resolve Glow ID via API](/docs/resolve-glow-id-via-api)

Powered by [__](https://readme.com?ref_src=hub&project=glowwallet)

# Glow Javascript SDK

Integrate your site with Glow wallet.

[__Suggest Edits](/edit/getting-started)

##

About Glow

Glow is a non-custodial crypto wallet for the Solana blockchain.

Glow is available as a browser extension, an iOS app, and an Android app. With
the iOS app, Glow includes a mobile Safari extension that lets users interact
with applications right from the Safari browser. For Android, a browser is
built into the app.

As a developer, you can use the same JavaScript SDK to integrate your site
with Glow across all platforms.

##

Installing the SDK

The library can be installed via `npm` or `yarn`:

Shell

    
    
    # Using npm
    npm install @glow-xyz/glow-client
    
    # Using yarn
    yarn add @glow-xyz/glow-client
    

In addition, a React wrapper is provided, which helpful if you are building a
React app. To install, run:

Shell

    
    
    # Using npm
    npm install @glow-xyz/glow-react
    
    # Using yarn
    yarn add @glow-xyz/glow-react
    

##

Getting Started

Once you install the library, you are ready to connect your site to Glow.

To do so, first detect whether the user has Glow installed. Then, prompt the
user to sign in with Glow so that you can connect to the wallet, authenticate
the user, and be ready to perform actions. Finally, use the connection to
execute transactions or sign messages.

__Updated over 1 year ago

* * *

  * __Table of Contents
  *     * About Glow
    * Installing the SDK
    * Getting Started

