[![Logo](https://docs.apricot.one/~gitbook/image?url=https%3A%2F%2F31048181-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-
legacy-files%2Fo%2Fspaces%252F-Mgy_H-
REivbwMEM9tBd%252Favatar-1628857981784.png%3Fgeneration%3D1628857982016022%26alt%3Dmedia&width=32&dpr=4&quality=100&sign=2d00488fb3e7edeb3dcaef88564579a78b66c960f2f612726c377bebdfd9b178)![Logo](https://docs.apricot.one/~gitbook/image?url=https%3A%2F%2F31048181-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-
legacy-files%2Fo%2Fspaces%252F-Mgy_H-
REivbwMEM9tBd%252Favatar-1628857981784.png%3Fgeneration%3D1628857982016022%26alt%3Dmedia&width=32&dpr=4&quality=100&sign=2d00488fb3e7edeb3dcaef88564579a78b66c960f2f612726c377bebdfd9b178)Apricot
Finance](/)

SearchCtrl \+ K

  * [Overview](/)

  * [Video Walkthrough](/video-walkthrough)

  * [Apricot EDU](/apricot-edu)

  * [Relevant Links](/relevant-links)

  * Product User Guide

    * [UI & Connect Wallet](/product/ui-overview-and-connect-wallet)

    * [Dashboard](/product/dashboard)

    * [Apricot Lend](/product/apricot-lend)

    * [X-Farm](/product/stable-farming)

    * [In-App Swap](/product/in-app-swap)

    * [Apricot Assist](/product/apricot-assist)

    * [Glossary](/product/glossary)

    * [FAQ-APYs](/product/faq)

    * [FAQ-Farming](/product/faq-farming)

    * [FAQ-Miscellaneous](/product/faq-miscellaneous)

  * Cookbook

  * Protocol Details

    * [Interest Rates](/protocol-details/interest-rates)

    * [Liquidity Mining Program](/protocol-details/apricot-liquidity-mining-reward)

    * [Liquidation Threshold & LTV](/protocol-details/risk-parameters)

    * [Fees](/protocol-details/fees)

    * [Liquidation Penalty](/protocol-details/liquidation-penalty)

    * [Price Oracles](/protocol-details/price-oracles)

  * Developer Docs

    * [Client Interface](/developer-docs/client-interface)

    * [Liquidator Interface](/developer-docs/liquidator-interface)

[Powered by
GitBook](https://www.gitbook.com/?utm_source=content&utm_medium=trademark&utm_campaign=-Mgy_H-
REivbwMEM9tBd)

# Overview

Lend. Farm. Stay Protected.

###

What is Apricot?

Apricot is a next-gen lending protocol that supports leveraged yield farming
on Solana. Our mission is to help users maximize yield while protecting their
downsides.

With Apricot, users can:

  * Deposit assets to earn interests (Apricot Lend)

  * Borrow assets for trading or leveraged yield farming (Apricot Cross-Farm)

  * Pre-configure when and how automated deleveraging takes place (Apricot Assist)

###

Apricot Lend

Apricot Lend provides standard lending and borrowing services: users deposit
assets to earn interests, and use their deposited assets as collateral to
borrow other assets.

###

Apricot Cross-Farm (X-Farm)

Apricot X-Farm provides **cross-margin** leveraged yield farming service for
users to maximize yield from their existing holdings.

Let's take USDT-USDC LP farming for example. In other leveraged yield farming
protocols, users would need to own some amount of USDT and USDC before they
can start farming the stablecoin pair. If they do not have USDT and USDC
sitting in their wallet, they would have to swap other tokens into these
stablecoins first.

On Apricot X-Farm, users do not need to own any amount of USDT or USDC to
start farming. Instead, they can collateralize their non-stablecoin assets to
borrow the stablecoins with up to 3x leverage, and start farming USDT-USDC LP
right away. These stablecoins will then be auto-pooled and staked for LP
tokens, resulting in 3x farming yield.

In short, using X-Farm, users can:

  1. Deposit any supported assets they already own (e.g. SOL, BTC, USDT, USDC, etc.)

  2. Start farming LP tokens at up to 3x leverage, using entirely borrowed assets

  3. The LP tokens in your account are auto-staked and periodically compounded, so you start earning 3x LP farming yield right away

In this way, X-Farm efficiently increases users' access to additional yield
without forcing them to sell any assets.

But wait, what about the risk of liquidation?

###

Apricot Assist 1.0

Fear not, Apricot Assist is designed specifically to help users manage their
leveraged positions to reduce liquidation risks through an automated self-
deleveraging mechanism. With Apricot Assist, users will be able to control:

  * **When** to start selling or redeeming your collateral assets

  * **What** and **how much** assets should be sold or redeemed

Take the example above where a user has opened a 3x leverage USDT-USDC LP
position against SOL. However, now the price of SOL fall dramatically
overnight. The user can stay protected if he or she has configured Apricot
Assist to perform the following deleveraging actions:

  * **When:** when "borrow limit used" reaches 95% (liquidation at 100%)

  * **What** and **how** : redeem X amount of USDT-USDC LP tokens back to USDT and USDC, and repay the corresponding debt to get back to 90% "borrow limit used"

Apricot Assist's timely intervention produces the following outcomes:

  * “borrow limit used” goes down to 90%, back to **safety**

  * All initial SOL principal is **preserved**

  * Size of USDC-USDT LP position has decreased (**lower leverage ratio** , less rewards)

As a user, you can program when Apricot Assist gets activated and how many LP
tokens get redeemed and etc. using the **Assist Simulator**.

Note that current version of Apricot Assist 1.0 only supports the repayment of
stablecoin debt. In near future, there will be additional support for the
repayment of non-stable tokens. For more details, please refer to the Apricot
Assist section under Product User Guide.

[NextVideo Walkthrough](/video-walkthrough)

Last updated 2 years ago

On this page

  * What is Apricot?
  * Apricot Lend
  * Apricot Cross-Farm (X-Farm)
  * Apricot Assist 1.0

Was this helpful?

