  * **Wallet**[**Mobile App** The world of Web3 in your pocket](/download)[**Browser Extension** An optimized Web3 experience for desktop](/browser-extension)
  * **Features**[**Swaps** Swap securely and seamlessly](/swap)[**Staking** Earn crypto rewards while securing networks](/staking)[**NFTs** Explore the world of NFTs](/nft)[**Security** Learn how we keep your assets & Web3 journey safe](/security)[**Buy Crypto** Buy crypto in under five minutes](/buy-crypto)[**SWIFT: Smart Contract Wallet** Explore Web3 easily with account abstraction features](/swift)
  * **Build**[**Developer Docs** Get guides for building powerful Web3 applications](https://developer.trustwallet.com/developer/)[**Wallet Core** Open-source, mobile-focused crypto wallet library](https://developer.trustwallet.com/developer/wallet-core)[**Submit dApp** Get your dApp in front of millions](https://developer.trustwallet.com/developer/listing-new-dapps)[**Get assets listed** Elevate your asset’s exposure](https://developer.trustwallet.com/developer/listing-new-assets)
  * **Support**[**FAQ** Get answers to your most pressing questions](https://community.trustwallet.com/c/helpcenter/8)[**Community Forum** Connect with our vibrant and diverse community](https://community.trustwallet.com/)[**Contact Us** Reach out for personalized support](https://support.trustwallet.com/en/support/home)
  * **About**[**About Us** Discover who we are and what drives us](/about-us)[**Careers** Join us in shaping the future of Web3](/careers)[**Press Kit** Download our official logo and other media assets](/press)[**Blog** Stay up-to-date on Web3 trends and insights](/blog)[**Terms of Service** What you need to know to use our services](/terms-of-service)[**Privacy Policy** Your privacy matters, learn how we protect it](/privacy-policy)

DarkLightLanguage

[Download Trust Wallet](/download)

[](/)

![Blue Shield](/_next/static/media/raw.4edbb099.svg)[**Mobile App** The world
of Web3 in your pocket](/download)[**Browser Extension** An optimized Web3
experience for desktop](/browser-extension)

![Blue Shield](/_next/static/media/raw.e7c57d68.svg)[**Swaps** Swap securely
and seamlessly](/swap)[**Staking** Earn crypto rewards while securing
networks](/staking)[**NFTs** Explore the world of NFTs](/nft)[**Security**
Learn how we keep your assets & Web3 journey safe](/security)[**Buy Crypto**
Buy crypto in under five minutes](/buy-crypto)[**SWIFT: Smart Contract
Wallet** Explore Web3 easily with account abstraction features](/swift)

![Blue Shield](/_next/static/media/raw.b373ab3f.svg)[**Developer Docs** Get
guides for building powerful Web3
applications](https://developer.trustwallet.com/developer/)[**Wallet Core**
Open-source, mobile-focused crypto wallet
library](https://developer.trustwallet.com/developer/wallet-core)[**Submit
dApp** Get your dApp in front of
millions](https://developer.trustwallet.com/developer/listing-new-dapps)[**Get
assets listed** Elevate your asset’s
exposure](https://developer.trustwallet.com/developer/listing-new-assets)

![Blue Shield](/_next/static/media/raw.1211abf0.svg)[**FAQ** Get answers to
your most pressing
questions](https://community.trustwallet.com/c/helpcenter/8)[**Community
Forum** Connect with our vibrant and diverse
community](https://community.trustwallet.com/)[**Contact Us** Reach out for
personalized support](https://support.trustwallet.com/en/support/home)

![Blue Shield](/_next/static/media/raw.9a6dd06f.svg)[**About Us** Discover who
we are and what drives us](/about-us)[**Careers** Join us in shaping the
future of Web3](/careers)[**Press Kit** Download our official logo and other
media assets](/press)[**Blog** Stay up-to-date on Web3 trends and
insights](/blog)[**Terms of Service** What you need to know to use our
services](/terms-of-service)[**Privacy Policy** Your privacy matters, learn
how we protect it](/privacy-policy)

[](/)

WalletFeaturesBuildSupportAbout

Language

[Download](/download)

[Home](/)  >  [Blog](/blog)  >  [Announcements](/blog?category=Announcements)
>  [BEP2 Migration Incident: Update and Recommended
Actions](/blog/bep2-migration-incident-update-and-recommended-actions)

##### Announcements

# BEP2 Migration Incident: Update and Recommended Actions

Published on: Mar 28, 2024

##### Share post

[](https://facebook.com/trustwalletapp)[](https://github.com/trustwallet)[](https://instagram.com/trustwallet)[](https://twitter.com/trustwallet)[](https://discord.gg/trustwallet)[](https://reddit.com/r/trustapp)[](https://t.me/trustwallet)

  * **What Happened**
  * **How we fixed the issue**
  * **Recommended Actions for Users**
  * **Frequently Asked Questions (FAQ)**

##### In Brief

Information on the resolved BEP2 to BEP20 migration issue in the Trust Wallet
browser extension. Details on what happened, the fix, and info for affected
users.

![BEP2 Migration Incident: Update and Recommended
Actions](/_next/image?url=https%3A%2F%2Fstrapi-
cdn.trustwallet.com%2Fbep20_comms_4a23b9e08a.png&w=3840&q=75)

### Latest Update for April 8, 2024

_Please note that all reimbursement payments have been completed._

### Summary

On March 16, 2024, our team was alerted via our community that the Trust
Wallet browser extension BEP2 to BEP20 migration feature was not functioning
as expected. In keeping things transparent with our community, this article
outlines the facts of this incident including:

  * What happened

  * How we quickly fixed the issue

  * Who may be affected, and who is not

  * Important information for affected users

**Important:** _It’s critical to note that this issue only affected _one_
feature of the Trust Wallet browser extension for a very brief period of time,
not impacting any other features. Additionally, this issue _did not_ affect
the Trust Wallet mobile app in any way. Both the mobile app and browser
extension remain safe to use._

## What Happened

The BNB Chain team had previously
[announced](https://www.bnbchain.org/en/blog/navigating-the-bnb-beacon-chain-
fusion-roadmap-six-month-plan) the sunsetting of the BNB Beacon Chain (BEP2).
As such, they recommended users to migrate their BEP2 assets to the BNB Smart
Chain (BEP20) to avoid asset loss. In line with our principles of making Web3
easier for millions of people, we decided to build a new tool for the Trust
Wallet browser extension—making this migration process more seamless.

The migration feature, originally added in version 2.7.0 of the browser
extension, functioned normally as expected until the release of version 2.9.0.
However, the update to version 2.9.0 included modifications to the existing
logic that introduced a bug to the migration feature. The bug, which persisted
in extension version 2.9.1, caused migrated assets to be redirected to an
incorrect address, not associated with the user's wallet, leading to a loss of
funds for a very small number of our users.

It’s worth mentioning that this bug was quickly reported by our community
members through our bug bounty program. We appreciate the quick flag.

**Note:** _For clarity, Trust Wallet mobile apps are not affected at all. The
extension bug was _not the result of a security issue_ , nor the result of a
malicious actor. Also, the only versions of the browser extension affected by
this issue were, 2.9.0 and 2.9.1. No other versions of the browser extension
experienced this issue._

Based on the bug reports, our team swiftly fixed the issue, released in
extension version 2.9.2—so any following versions including the recently
released 2.9.3 also include the fix and are safe to use.

## How we fixed the issue

Upon receiving reports, our team investigated and did the following to quickly
mitigate and patch the issue:

  * Included a warning message next to the migration button in the browser extension. Additionally, we temporarily removed any references to migrating assets in the browser extension.

  * Temporarily blocked transactions on the BNB Beacon Chain to avoid users losing funds.

  * Released a new version of the browser extension (in 2.9.2, 2.9.3 and later versions) that removed the bugged migration tool on March 17, 2024.

  * Additionally, an updated and secure migration tool will be released in version 2.10 of the browser extension (early April depending on Chrome Store review and approval duration).

## Recommended Actions for Users

**To ensure you have a fixed version of the extension, we recommend you either
completely quit and restart your browser, or update your browser.** By
default, your browser keeps Chrome extensions up to date, so all users should
have an updated fixed version of the Trust Wallet extension—however restarting
or updating the browser helps to ensure you receive the update.

The latest version of the Trust Wallet browser extension is safe and secure to
use. The Trust Wallet mobile app was not affected by the bug, and remains safe
and secure to use.

The sections below outline who is not affected, who may be, and important
information for those who lost funds due to the bug.

### WHO IS NOT AFFECTED?

  * If you only use Trust Wallet mobile apps.

  * You have used the browser extension, but never utilized the migration feature.

  * You only started using the Trust Wallet browser extension with version 2.9.2 or greater.

### WHO MAY BE AFFECTED?

  * Used the migration feature with extension version 2.9.0 or 2.9.1 before March 17, 2024 15:10 UTC+0, and the transaction was completed but the migrated funds didn’t arrive in the users’ BEP20 address and no longer exist in the original BEP2 address.

### IMPORTANT INFORMATION FOR THOSE AFFECTED

**Latest update for April 8, 2024:** _Please note that all reimbursement
payments have been completed._

If you are an affected user, any lost BEP2 assets caused by the bug in the
extension version 2.9.0 or 2.9.1 will be automatically reimbursed to your
wallet address by mid April, 2024. The reimbursement will be sent to the same
wallet address you initiated the migration from using browser extension
version 2.9.0 or 2.9.1, and where funds were lost. We decided to directly
reimburse the funds to your BEP2 address, as it’s the fastest way to get your
assets back to you and requires least effort from you. For clarity, there are
no actions required for reimbursement if you are an affected user—as the
assets will automatically be sent back to your wallet address.

**Note:** We plan to re-introduce the migration feature in the extension in
early April. If you wish to migrate your BEP2 assets to the BNB Smart Chain
(BEP20) before the migration feature is available in the extension again, you
can use the instructions in [this
guide](https://trustwallet.com/blog/migrating-bep2-assets-to-bep20-using-the-
trust-wallet-mobile-app)—which outlines how to use the Trust Wallet mobile app
for the migration.

## Frequently Asked Questions (FAQ)

### Is it safe to use the Browser Extension?

Yes, it is safe to use. We’ve implemented a fix to the browser extension, and
the updated extension was released. Version 2.9.2, 2.9.3, and greater, all
include this fix. Additionally, no other features of the browser extension
were impacted by the previous issue, and the Trust Wallet mobile app was also
not affected in any way.

### How do I update my browser extension to a fixed version?

By default, your browser keeps chrome extensions up to date. The migration
issue was fixed in extension version 2.9.2. So as long as you’re using 2.9.2,
2.9.3, or greater, you’re using the fixed updated version. If you want to
ensure you have extension version 2.9.2 or greater, follow these steps to
confirm your version number:

  * Select the Extensions icon (puzzle-shape) near the top right of your browser.

  * Select “Manage Extensions”.

  * Locate “Trust Wallet” and click the “Details” button.

  * View the number under the “Version” section.

If you notice you do not yet have one of the updated versions, you can try
either quitting your browser completely and reopening it, or updating the
browser.

### Was Trust Wallet compromised by a malicious actor?

No, Trust Wallet was neither hacked, nor affected by a malicious actor. The
previous bug was not the result of a security issue. As highlighted, during
updates to version 2.9.0, a bug was inadvertently introduced that affected
just only the migration feature of the Trust Wallet browser extension. This
was quickly identified and fixed. The Trust Wallet mobile app was not affected
in any way by this issue. And both the Trust Wallet browser extension and
mobile remain safe and secure to use.

### For affected users, will assets be reimbursed as the original BEP2 asset?

In the vast majority of cases, yes, the original asset that was lost will be
reimbursed as the same asset. The only exception is for the ShareToken (SHR)
BEP2 token. In the case of lost SHR, users will rather be reimbursed an
equivalent value in USDT.

### What should I do if I want to safely migrate my BEP2 assets to BEP20?

For Trust Wallet users who wish to migrate their assets you can do the
following:

  * [Go here for instructions](https://trustwallet.com/blog/migrating-bep2-assets-to-bep20-using-the-trust-wallet-mobile-app) on how to swap BEP2 assets to BEP20 using the Trust Wallet mobile app.

  * Stay tuned as we plan to bring the migration feature back into the browser extension. [Follow us on X for official announcements](https://rebrand.ly/TW-Twitter-Blog).

### How will you ensure this issue doesn’t happen again?

That said, we take full ownership of this situation and appreciate your
patience while any affected users are reimbursed. To help prevent situations
like this from arising again, we will of course continue to utilize our bug
bounty program in addition to implementing even more comprehensive testing
procedures to ensure the robustness of our updates before they are deployed.

The issue, which only affected the migration feature of the browser extension
for a brief period of time, has been resolved. It's an inherent part of
technology development that, despite best efforts, bugs can emerge. This is
why we, like many reputable organizations in the Web3 space and beyond, employ
a bug bounty program. [Learn more about the bug bounty
program](https://bugcrowd.com/binance).

[![Download-Trust-Wallet-Button.png](/_next/image?url=https%3A%2F%2Fstrapi-
cdn.trustwallet.com%2FDownload_Trust_Wallet_Button_3b2b015a21.png&w=3840&q=75)](https://short.trustwallet.com/TW-
blog)

Join the Trust Wallet community on [Telegram](https://rebrand.ly/TW-Telegram-
Announcements) Follow us on [X (formerly Twitter)](https://rebrand.ly/TW-
Twitter-Blog) [Instagram](https://rebrand.ly/TW-Insta-Blog)
[Facebook](https://rebrand.ly/TW-FB-Blog) [Reddit](https://rebrand.ly/TW-
Reddit-Blog)

> **Note:** Any cited numbers, figures, or illustrations are reported at the
> time of writing, and are subject to change.

#### Simple and convenient to use, seamless to explore

[Download Trust Wallet](/download)

##### Stay Connected:

[](https://facebook.com/trustwalletapp)[](https://github.com/trustwallet)[](https://instagram.com/trustwallet)[](https://twitter.com/trustwallet)[](https://discord.gg/trustwallet)[](https://reddit.com/r/trustapp)[](https://t.me/trustwallet)

  * **Wallet**[Mobile App](/download)[Browser Extension](/browser-extension)
  * **Features**[Buy Crypto](/buy-crypto)[Swaps](/swap)[Staking](/staking)[NFTs](/nft)[Security](/security)[SWIFT: Smart Contract Wallet](/swift)
  * **Build**[Developer Docs](https://developer.trustwallet.com/developer/)[Wallet Core](https://developer.trustwallet.com/developer/wallet-core)[Submit dApp](https://developer.trustwallet.com/developer/listing-new-dapps)[Get assets listed](https://developer.trustwallet.com/developer/listing-new-assets)
  * **Support**[FAQ](https://community.trustwallet.com/c/helpcenter/8)[Community Forum](https://community.trustwallet.com/)[Contact Us](https://support.trustwallet.com/en/support/home)
  * **About**[About Us](/about-us)[Careers](/careers)[Press Kit](/press)[Terms of Service](/terms-of-service)[Privacy Policy](/privacy-policy)[Blog](/blog)
  * ![A-LIGN ISO 27701](/_next/static/media/image.8354ab2c.svg)![A-LIGN ISO 27001](/_next/static/media/image.7f0b3bc9.svg)

**Download Trust Wallet**

The most trusted & secure crypto wallet.

[Download for iOS](https://apps.apple.com/app/apple-
store/id1288339409?mt=8)[Download
Extension![Chrome](/_next/static/media/raw.7dd85797.svg)](https://chrome.google.com/webstore/detail/trust-
wallet/egjidjbpglichdcondbcbdnbeeppgdph)[Download APK](/download/apk)[Download
for Android![App
Store](/_next/image?url=%2F_next%2Fstatic%2Fmedia%2Fimage.5ee64b2e.png&w=256&q=75)](https://play.google.com/store/apps/details?id=com.wallet.crypto.trustapp)

