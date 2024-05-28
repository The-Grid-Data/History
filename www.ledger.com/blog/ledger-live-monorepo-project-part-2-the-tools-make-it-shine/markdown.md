[ New: Wallet recovery made easy with Ledger Recover, provided by Coincover
Get started ](https://shop.ledger.com/pages/ledger-recover)

Our Website now exists in . Do you want to change languages?

Yes, please No, I'm good

You can revert to English at any time by clicking on the language menu on the
top right corner of the page.

[ ![Ledger](https://www.ledger.com/wp-
content/themes/ledger-v2/public/images/ledger-logo-long.svg)
](https://www.ledger.com "Ledger")

  * Products
    * [Ledger Stax](https://shop.ledger.com/pages/ledger-stax "Ledger Stax")
    * [Ledger Nano X](https://shop.ledger.com/pages/ledger-nano-x "Ledger Nano X")
    * [Ledger Nano S Plus](https://shop.ledger.com/pages/ledger-nano-s-plus "Ledger Nano S Plus")
    * [Compare our devices](https://shop.ledger.com/pages/hardware-wallets-comparison "Compare our devices")
    * [Packs](https://shop.ledger.com/#category-bundle "Packs")
    * [Accessories](https://shop.ledger.com/#category-accessories "Accessories")
    * [Collaborations](https://www.ledger.com/collaborations "Collaborations")
    * [See all products](https://shop.ledger.com "See all products")
    * [Download Ledger Live](https://www.ledger.com/ledger-live "Download Ledger Live")
    * [Supported crypto](https://www.ledger.com/supported-crypto-assets "Supported crypto")
  * App and services
    * [Ledger Live](https://www.ledger.com/ledger-live "Ledger Live")
    * [Ledger Recover](https://shop.ledger.com/pages/ledger-recover "Ledger Recover")
    * [CL Card](https://www.ledger.com/cl-card "CL Card")
    * [Supported Services](https://www.ledger.com/supported-services "Supported Services")
    * [Crypto Prices](https://www.ledger.com/coin/price "Crypto Prices")
  * Learn
    * [Ledger Academy](https://www.ledger.com/academy "Ledger Academy")
    * [Learn and Earn](https://quest.ledger.com/ "Learn and Earn")
    * [Classroom](https://www.ledger.com/academy/what-is-web-30-everything-you-need-to-know "Classroom")
    * [Blog](/blog "Blog")
    * [What is a crypto wallet](https://www.ledger.com/academy/basic-basics/2-how-to-own-crypto/what-is-a-crypto-wallet "What is a crypto wallet")
    * [How to Buy](https://www.ledger.com/buy "How to Buy")
    * [How to Swap](https://www.ledger.com/swap "How to Swap")
    * [How to Stake](https://www.ledger.com/staking "How to Stake")
  * For Business
    * [Ledger Enterprise Solutions](https://enterprise.ledger.com?utm_source=mainsite&utm_medium=header "Ledger Enterprise Solutions")
    * [Ledger Partners](/partners "Ledger Partners")
    * [Ledger Co-branded Partnership](https://co-branded.ledger.com/ "Ledger Co-branded Partnership")
  * [For Developers](https://developers.ledger.com/ "For Developers")
  * [Support](https://support.ledger.com/hc "Support")
  * English
    * This page is available in English only

[__](https://shop.ledger.com/cart "Ledger Shop")

__

[Blog](https://www.ledger.com/blog/ledger-live-monorepo-project-part-2-the-
tools-make-it-shine) __[Blog posts](https://www.ledger.com/category/blog-posts
"Blog posts")

[Blog posts](https://www.ledger.com/category/blog-posts "Blog posts"), [Tech](https://www.ledger.com/category/tech "Tech") | 11/28/2023 

# Ledger Live Monorepo Project: Part 2 – The Tools (Make it Shine)

[Blog](https://www.ledger.com/blog/ledger-live-monorepo-project-part-2-the-
tools-make-it-shine) __[Blog posts](https://www.ledger.com/category/blog-posts
"Blog posts")

_Second entry of the blog posts series “Ledger Live Monorepo Project”, where a
Ledger developer tells us the story of the Ledger Live codebase huge migration
into a mono repository._ _If you missed part 1, check it out here:_

  * [Part I – Problematics (Make it pain) ](https://www.ledger.com/blog/ledger-live-monorepo-project-part-1-problematics-make-it-pain)

After establishing that a monorepo architecture was a viable solution, we then
started to look into the available tools to put in place our plan.

##### **Handling multiple projects**

In the Ledger Live team we navigate in the JavaScript ecosystem, and
fortunately for us, we already knew of several ways to handle multiple
projects with our package manager. Some of those possible solutions include:

  * **NPM** (has support for workspaces but better alternatives),
  * **Yarn 1** (becoming too old, better and more efficient alternatives),
  * **Yarn ≥ 2** (interesting idea, but plug n play not well supported everywhere, especially with React Native),
  * **PNPM** (symlinks, built with workspaces in mind, disk efficient).

After looking at all these, we decided to go with **[PNPM](https://pnpm.io/)**
for:

  * the disk efficiency (it uses a virtual _store_ and _symlinks_ , so packages are downloaded only once then symlinked to your node_modules from the virtual store),
  * the speed (since packages are cached, subsequent installations are much faster),
  * built in support for workspaces/monorepo architecture (aliases, orchestration etc…).

On paper **PNPM** is an absolute gem, but symlinks were a bit odd to setup
correctly (again, specially with React Native).

![](https://www.ledger.com/wp-content/uploads/2023/11/image-4.png)

Ok, so our choice was made, we would go with **PNPM.**

##### **Script Orchestration**

Even though **PNPM** adds more and more orchestration to its features, it
still doesn’t cover everything we wanted to do, such as:

  * sequential builds,
  * caching.

For these, we found two interesting contenders that we needed to take a look
at:

  * **[NX](https://nx.dev/)** (by the angular team),
  * **[Turborepo](https://turbo.build/)** (which just announced the v1.0.0 when we started working on it, and now working with the Vercel team).

![](https://www.ledger.com/wp-content/uploads/2023/11/image-3-1024x257.png)

We did a proof of concept on both.

**NX** had much more features, generators, automation, great dependency graphs
etc… but, it added a lot of overhead, and since it’s pretty opinionated, we
would have to follow their conventions.

**Turborepo** on the other hand, is pretty basic feature wise. Yet it’s a
convenient plug and play solution that we could change very quickly if the
need ever comes.

Even though **Turborepo** had less features than **NX** , it did the 2 things
we were looking for:

  * Orchestration of builds respecting the dependency tree (and concurrent builds),
  * Caching (builds are cached and ‘replayed’ if their code has not changed).

That, plus the easy drop in / drop out, made us choose the new kid on the
block, **TurboRepo**.

##### **Versioning**

We looked into several solutions as well, but ultimately decided to use[
https://github.com/changesets/changesets](https://github.com/changesets/changesets)
as it was one tool TurboRepo recommended, and after a bit of documentation
reading, seemed to comply with our needs.

![](https://www.ledger.com/wp-content/uploads/2023/11/image-2.png)

Developers would need to be a bit more rigorous in their dev flow and provide
`**changesets**` (file describing which library their code changes, the
severity following the **semver** convention, and a description of the
change). These **`changesets`** are then used to automatically bump the
version of the packages respecting the given severities, as well as automate
the generation of **changelogs**. On top of that, the tools allows for **`pre
release`** mode, the 🍒 on the 🍰.

##### **What’s next ?**

After deciding on the tools, it was time to start working. In the next blog
article, we will talk about the build system and all the dev-ops / automation
/ continuous integration in the context of a mono repository.

* * *

[Valentin DE ALMEIDA](https://twitter.com/val_pinkman)  
Developer Experience & Core Tech – Ledger Live

[](https://www.facebook.com/Ledger/)
[__](https://www.instagram.com/ledger/)[](https://twitter.com/Ledger)
[](https://www.linkedin.com/company/ledgerhq/)
[](https://www.reddit.com/r/ledgerwallet/)
[__](https://www.tiktok.com/@ledger)

More articles

[](https://www.ledger.com/blog-ledger-stax-now-shipping-a-message-from-
ledgers-ceo-pascal-gauthier "Ledger Stax Now Shipping: A Message From Ledger’s
CEO Pascal Gauthier")

[Blog posts](https://www.ledger.com/category/blog-posts "Blog posts"), [Company](https://www.ledger.com/category/company-news "Company") | 05/28/2024 

Ledger Stax Now Shipping: A Message From Ledger’s CEO Pascal Gaut...

[Read more](https://www.ledger.com/blog-ledger-stax-now-shipping-a-message-
from-ledgers-ceo-pascal-gauthier "Ledger Stax Now Shipping: A Message From
Ledger’s CEO Pascal Gauthier")

[](https://www.ledger.com/blog-cargo-checkct-our-home-made-tool-guarding-
against-timing-attacks-is-now-open-source "Cargo-checkct: our home-made tool
guarding against timing attacks is now open-source!")

[Blog posts](https://www.ledger.com/category/blog-posts "Blog posts"), [Donjon](https://www.ledger.com/category/donjon "Donjon") | 05/17/2024 

Cargo-checkct: our home-made tool guarding against timing attacks...

[Read more](https://www.ledger.com/blog-cargo-checkct-our-home-made-tool-
guarding-against-timing-attacks-is-now-open-source "Cargo-checkct: our home-
made tool guarding against timing attacks is now open-source!")

[](https://www.ledger.com/blog/device-apps-tutorials "Master Ledger Device
Apps development with step-by-step tutorials")

[Blog posts](https://www.ledger.com/category/blog-posts "Blog posts"), [Tech](https://www.ledger.com/category/tech "Tech") | 05/07/2024 

Master Ledger Device Apps development with step-by-step tutorials...

[Read more](https://www.ledger.com/blog/device-apps-tutorials "Master Ledger
Device Apps development with step-by-step tutorials")

### Stay in touch

Announcements can be found in our blog. Press contact:  
[media@ledger.com](mailto:media@ledger.com)

  * [__](https://www.reddit.com/r/ledgerwallet/ "Ledger Reddit")
  * [__](https://www.facebook.com/Ledger/ "Ledger Facebook")
  * [__](https://www.instagram.com/ledger/ "Ledger Instagram")
  * [__](https://twitter.com/Ledger "Ledger Twitter")
  * [__](https://www.youtube.com/Ledger "Ledger Youtube")
  * [__](https://www.linkedin.com/company/ledgerhq "Ledger Linkedin company")
  * [__](https://www.tiktok.com/@ledger "Ledger Tiktok")
  * [__](https://discord.com/invite/ledger "Ledger Discord")

### Subscribe to our  
newsletter

New coins supported, blog updates and exclusive offers directly in your inbox

  

Enter your email

Register to newsletter

Your email address will only be used to send you our newsletter, as well as
updates and offers. You can unsubscribe at any time using the link included in
the newsletter.

[Learn more about how we manage your data and your
rights.](https://shop.ledger.com/pages/privacy-notice#ledger-newsletter)

[![](https://www.ledger.com/wp-content/themes/ledger-v2/public/images/ledger-
logo-long.svg)](https://www.ledger.com "Ledger")

  * English
    * This page is available in English only

Copyright © Ledger SAS. All rights reserved. Ledger, Ledger Stax, Ledger Nano
S, Ledger Vault, Bolos are trademarks owned by Ledger SAS.  
  
1 rue du Mail, 75002 Paris, France  
  
Payment methods  
![](/wp-content/uploads/2021/11/logo-paypal-s.png?v=2)  ![](/wp-
content/uploads/2021/11/logo-crypto-s.png?v=6)  ![](/wp-
content/uploads/2021/11/logo-bitpay-s.png?v=6)  
![](/wp-content/uploads/2021/11/layer1.png?v=2)  ![](/wp-
content/uploads/2021/11/logo-visa-s.png?v=2)  ![](/wp-
content/uploads/2021/11/logo-maestro-s.png?v=2)  ![](/wp-
content/uploads/2021/11/logo-mastercard-s.png?v=2)  ![](/wp-
content/uploads/2021/11/logo-cb-s.png?v=2)

  * Products
    * [Ledger Stax](https://shop.ledger.com/pages/ledger-stax)
    * [Ledger Nano X](https://shop.ledger.com/pages/ledger-nano-x)
    * [Ledger Nano S Plus](https://shop.ledger.com/pages/ledger-nano-s-plus)
    * [Compare our devices](https://shop.ledger.com/pages/hardware-wallets-comparison)
    * [Bundles](https://shop.ledger.com/#category-bundle)
    * [Accessories](https://shop.ledger.com/#category-accessories)
    * [All products](https://shop.ledger.com)
    * [Downloads](https://www.ledger.com/ledger-live)

  * Crypto Assets
    * [Bitcoin wallet](https://www.ledger.com/coin/wallet/bitcoin)
    * [Ethereum wallet](https://www.ledger.com/coin/wallet/ethereum)
    * [Cardano wallet](https://www.ledger.com/coin/wallet/cardano)
    * [XRP wallet](https://www.ledger.com/coin/wallet/ripple)
    * [Monero wallet](https://www.ledger.com/coin/wallet/monero)
    * [USDT wallet](https://www.ledger.com/coin/wallet/tether)
    * [See all assets](https://www.ledger.com/supported-crypto-assets)

  * Crypto Services
    * [Crypto Prices](https://www.ledger.com/coin/price)
    * [Buy crypto](https://www.ledger.com/buy)
    * [Staking crypto](https://www.ledger.com/staking)
    * [Swap crypto](https://www.ledger.com/swap)

  * For Business
    * [Ledger Enterprise Solutions](https://enterprise.ledger.com/)

  * For Startups
    * [Funding from Ledger Cathay Capital](https://www.ledger.com/cathay-ledger-fund)

  * For Developers
    * [The Developer Portal](https://developers.ledger.com/)

  * Get started
    * [Start using your Ledger device](https://www.ledger.com/start)
    * [Compatible wallets and services](https://www.ledger.com/ledger-wallets-and-services)
    * [How to buy Bitcoin](https://www.ledger.com/buy-bitcoin)
    * [Guide before buying bitcoin](https://www.ledger.com/buy-bitcoin/how)
    * [Bitcoin Hardware Wallet](https://shop.ledger.com/pages/bitcoin-hardware-wallet)

  * See also
    * [Support](https://support.ledger.com/hc)
    * [Bounty program](https://donjon.ledger.com/bounty/)
    * [Resellers](/reseller)
    * [Ledger Press Kit](https://www.ledger.com/press)
    * [Affiliates](https://www.ledgerwallet.com/affiliates/)
    * [Status](https://status.ledger.com/)
    * [Partners](/partners)

  * Careers
    * [Join us](https://www.ledger.com/career)
    * [All jobs](https://www.ledger.com/jobs)

  * About
    * [Our vision](https://www.ledger.com/blog/we-are-ledger-a-brand-vision)
    * [Ledger Academy](https://www.ledger.com/academy)
    * [The company](/the-company)
    * [The people](/the-people-behind-ledger)
    * [Diversity](https://www.ledger.com/diversity)
    * [Blog](/blog)

  * Legal
    * [Legal Center](https://www.ledger.com/legal-center)
    * [Sales Terms and Conditions](https://shop.ledger.com/pages/terms-and-conditions)
    * [Privacy Policy](https://www.ledger.com/privacy-policy)
    * [Disclaimers](https://shop.ledger.com/pages/disclaimers)

![](https://www.facebook.com/tr?id=237213137153741&ev=PageView&noscript=1)

![](https://t.co/1/i/adsct?bci=4&eci=3&event=%7B%7D&event_id=53268a4e-5590-4578-9570-64713a38dcec&integration=gtm&p_id=Twitter&p_user_id=0&pl_id=1b3ad18d-abd9-4772-9496-581dc742714a&tw_document_href=https%3A%2F%2Fwww.ledger.com%2Fblog%2Fledger-
live-monorepo-project-part-2-the-tools-make-it-
shine&tw_iframe_status=0&txn_id=nzkax&type=javascript&version=2.3.30)![](https://analytics.twitter.com/1/i/adsct?bci=4&eci=3&event=%7B%7D&event_id=53268a4e-5590-4578-9570-64713a38dcec&integration=gtm&p_id=Twitter&p_user_id=0&pl_id=1b3ad18d-abd9-4772-9496-581dc742714a&tw_document_href=https%3A%2F%2Fwww.ledger.com%2Fblog%2Fledger-
live-monorepo-project-part-2-the-tools-make-it-
shine&tw_iframe_status=0&txn_id=nzkax&type=javascript&version=2.3.30)

By clicking “Accept All Cookies”, you agree to the storing of cookies on your
device to enhance site navigation, analyze site usage, and assist in our
marketing efforts.

Cookies Settings Accept All Cookies

![Company Logo](https://cdn.cookielaw.org/logos/df21fb3f-71b8-491b-89ee-
eb777bcaf866/637ca236-af9d-4a40-815f-1b6a15af499d/ea9d9f41-35f0-4c24-9a83-1ef746863067/White_64.png)

## Privacy Preference Center

  * ### Your Privacy

  * ### Strictly Necessary Cookies

  * ### Performance Cookies

  * ### Functional Cookies

  * ### Targeting Cookies

  * ### Social Media Cookies

#### Your Privacy

When you visit any website, it may store or retrieve information on your
browser, mostly in the form of cookies. This information might be about you,
your preferences or your device and is mostly used to make the site work as
you expect it to. The information does not usually directly identify you, but
it can give you a more personalized web experience. Because we respect your
right to privacy, you can choose not to allow some types of cookies. Click on
the different category headings to find out more and change our default
settings. However, blocking some types of cookies may impact your experience
of the site and the services we are able to offer.  
[More information](https://cookiepedia.co.uk/giving-consent-to-cookies)

#### Strictly Necessary Cookies

Always Active

These cookies are necessary for the website to function and cannot be switched
off in our systems. They are usually only set in response to actions made by
you which amount to a request for services, such as setting your privacy
preferences, logging in or filling in forms. You can set your browser to block
or alert you about these cookies, but some parts of the site will not then
work. These cookies do not store any personally identifiable information.

View Vendor Details‎

#### Performance Cookies

Performance Cookies

These cookies allow us to count visits and traffic sources so we can measure
and improve the performance of our site. They help us to know which pages are
the most and least popular and see how visitors move around the site. All
information these cookies collect is aggregated and therefore anonymous. If
you do not allow these cookies we will not know when you have visited our
site, and will not be able to monitor its performance.

View Vendor Details‎

#### Functional Cookies

Functional Cookies

These cookies enable the website to provide enhanced functionality and
personalisation. They may be set by us or by third party providers whose
services we have added to our pages. If you do not allow these cookies then
some or all of these services may not function properly.

View Vendor Details‎

#### Targeting Cookies

Targeting Cookies

These cookies may be set through our site by our advertising partners. They
may be used by those companies to build a profile of your interests and show
you relevant adverts on other sites. They do not store directly personal
information, but are based on uniquely identifying your browser and internet
device. If you do not allow these cookies, you will experience less targeted
advertising.

View Vendor Details‎

#### Social Media Cookies

Social Media Cookies

These cookies are set by a range of social media services that we have added
to the site to enable you to share our content with your friends and networks.
They are capable of tracking your browser across other sites and building up a
profile of your interests. This may impact the content and messages you see on
other websites you visit. If you do not allow these cookies you may not be
able to use or see these sharing tools.

View Vendor Details‎

Back Button

### Vendors List

Filter Button

Consent Leg.Interest

checkbox label label

checkbox label label

checkbox label label

Clear

checkbox label label

Apply Cancel

Confirm My Choices

Allow All

[![Powered by
Onetrust](https://cdn.cookielaw.org/logos/static/powered_by_logo.svg)](https://www.onetrust.com/products/cookie-
consent/)

![](https://bat.bing.com/action/0?ti=134633242&tm=gtm002&Ver=2&mid=79428ed0-8a21-410d-b460-48148a6642d2&sid=bfb35bb01cfd11ef978761e5b767bc8d&vid=bfb37db01cfd11ef93cce7f138683f50&vids=1&msclkid=N&pi=918639831&lg=en-
US&sw=800&sh=600&sc=24&tl=Ledger%20Live%20Monorepo%20Project%3A%20Part%202%20-%20The%20Tools%20\(Make%20it%20Shine\)%20%7C%20Ledger&p=https%3A%2F%2Fwww.ledger.com%2Fblog%2Fledger-
live-monorepo-project-part-2-the-tools-make-it-
shine&r=&lt=2411&evt=pageLoad&sv=1&rn=820776)

![dot image
pixel](https://sp.analytics.yahoo.com/sp.pl?a=10000&d=Tue%2C%2028%20May%202024%2014%3A22%3A44%20GMT&n=0&b=Ledger%20Live%20Monorepo%20Project%3A%20Part%202%20-%20The%20Tools%20\(Make%20it%20Shine\)%20%7C%20Ledger&.yp=10159916&f=https%3A%2F%2Fwww.ledger.com%2Fblog%2Fledger-
live-monorepo-project-part-2-the-tools-make-it-
shine&enc=UTF-8&yv=1.15.1&tagmgr=gtm)

