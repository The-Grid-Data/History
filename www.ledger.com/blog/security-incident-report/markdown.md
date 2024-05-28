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

[Blog](https://www.ledger.com/blog/security-incident-report) __[Blog
posts](https://www.ledger.com/category/blog-posts "Blog posts")

[Blog posts](https://www.ledger.com/category/blog-posts "Blog posts"), [Tech](https://www.ledger.com/category/tech "Tech") | 12/20/2023 

# Security Incident Report

[Blog](https://www.ledger.com/blog/security-incident-report) __[Blog
posts](https://www.ledger.com/category/blog-posts "Blog posts")

Date of the report: **2023-12-20**

Date of the incident: **2023-12-14**

Type of Incident Detected: **Unauthorized Access & Malicious Code**

##### Executive Summary

Ledger detected an exploit using Ledger Connect Kit on Thursday the 14th of
December 2023. This exploit injected malicious code inside DApps that were
using Ledger Connect Kit, tricking EVM DApp users into signing transactions
that drain their wallets. The exploit was quickly spotted and a resolution was
implemented briefly after. In the meantime, a low volume of users fell into
the attack and signed transactions draining their wallet.

##### Timeline

_Timeline hours are detailed using the time zone Central European Time (CET):_

**2023-12-14: Morning:** A former Ledger Employee fell victim to a
sophisticated phishing attack that gained access to their NPMJS account,
bypassing 2FA, using the individual’s session token.

**2023-12-14 – 09:49AM / 10:44AM / 11:37AM:** The attacker published on NPMJS
(a package manager for Javascript code shared between apps), a malicious
version of the Ledger Connect Kit (affecting versions 1.1.5, 1.1.6, and
1.1.7). The malicious code used a rogue WalletConnect project to reroute
assets to hackers’ wallets.

**2023-12-14: 1.45PM:** Ledger was made aware of the ongoing attack thanks to
the prompt reaction of different actors in the ecosystem, including Blockaid
who reached out to the Ledger team and shared updates on X.

**2023-12-14: 2.18PM:** Ledger’s technology and security teams were alerted to
the attack and a genuine version of Ledger Connect Kit fix was deployed by
Ledger teams within 40 minutes of Ledger becoming aware. Due to the nature of
CDN (Content Delivery Network) and caching mechanisms on the Internet, the
malicious file remained accessible for a little longer. From the compromission
of NPMJS to the complete resolution, approximately 5 hours have passed. This
extended availability of the malicious code was a result of the time taken for
the CDN to propagate and update its caches globally with the latest, genuine
version of the file. Despite the file’s five hour presence, we estimate from
our investigation that the window during which user assets were actively
drained was confined to less than two hours in total.

Ledger coordinated swiftly with our partner WalletConnect, who disabled the
rogue WalletConnect instance used to drain assets from the users.

**2023-12-14: 2.55 PM** Upon our coordination, Tether froze the USDT of the
attacker(s) (cf.
[TX](https://etherscan.io/tx/0xf2b76233561ded9382612352eb4cd511e081b715b577c2e2236704af9e8050f4)).

##### Root Cause Analysis, Findings and Preventing Measures

###### Context

Ledger _Connect-Kit_ is a Java Script open source library allowing developers
to connect their DApps to Ledger hardware. It can be integrated using the
_Connect-Kit-loader_ component that allows a DApp to load the Connect-Kit at
runtime from a CDN. This allows DApp developers to always have the most recent
version of the _Connect-Kit_ without the need to manually update package
versions and release new builds. The CDN used by Ledger for the distribution
is NPMJS. Most DApps have integrated the _Connect-Kit_ using the mentioned
Connect-Kit-loader.

In the Ledger Connect Kit exploit, the attacker did not at any time have
access to any Ledger infrastructure, Ledger code repository, or to DApps
themselves. The attacker was able to push a malicious code package within the
CDN in place of the Connect-Kit itself. This malicious Connect-Kit code was
then dynamically loaded by DApps who already integrate the Connect-Kit-loader.

The Ledger Connect Kit exploit highlights risks Ledger and the industry
collectively face to protect users, and it is also a reminder that
collectively we need to continue to raise the bar for security around DApps
where users will engage in browser-based signing. It was Ledger’s service that
was exploited this time, but in the future this could happen to another
service or library.

![](https://www.ledger.com/wp-content/uploads/2023/12/Capture-
decran-2023-12-20-a-10.51.56-1024x572.png)

##### Root cause

In order to be able to push the malicious code package on NPMJS, the attacker
phished a former employee to leverage the individual’s access on NPMJS. The
access of the former employee to Ledger’s systems (including Github, SSO based
services, all internal Ledger tools, and external tools) were properly
revoked, but unfortunately the former employees’ access to NPMJS was not
properly revoked.

We can confirm this was an unfortunate isolated incident. Accesses to Ledger
infrastructure by Ledger employees are automatically revoked during employee
offboarding, however, due to how current technology services and tools
currently operate globally, we cannot automatically revoke access to certain
external tools (NPMJS included), and these must be handled manually with an
employee offboarding checklist for each individual. Ledger has an existing and
regularly updated offboarding procedure where we remove departing employees
from all external tools. In this individual case, the access was not manually
revoked on the NPMJS, which we regret, and are auditing with an external third
party partner.

This was a sophisticated attack conducted by the attacker. Despite having
enforced two-factor authentication (2FA) on the NPMJS targeted account, which
would normally deter many attempts, the attacker circumvented this security
measure by exploiting an API key associated with the former employee’s
account.

This specific attack enabled the attacker to upload a new malicious version of
the Ledger Connect Kit which contained what is referred to as the Angel
Drainer malware. Angel Drainer is a malware as a service that is specifically
designed to craft malicious transactions that are draining wallets when
signed. It’s a complete infrastructure specialized on EVM chains that deploys
smart contracts on demand and crafts tailored transactions in order to
maximize damage.

Unfortunately, [**NPMJS.com**](http://npmjs.com/) does not allow multi-
authorization or signature verification for automatic**** publishing. We’re
working on adding ad hoc mechanisms enforcing further controls at the
deployment stage.

##### Findings

This was a well prepared attack executed by experienced attacker(s). The
phishing technique implemented did not focus on credentials, which is what we
see in most Front-End attacks affecting the ecosystem, but instead the
attacker worked directly on the session token.

The malware used was Angel Drainer, and the Ledger security team has seen in
the past three months an increase of criminal activities using this malware
(please refer to this published [Blockaid
report](https://www.blockaid.io/post/attack-report-ledger-connect-kit)). We
can also see on-chain that the funds stolen are being split: 85% to the
exploiter and 15% to Angel Drainer, which could be seen as a malware as a
service.

![](https://www.ledger.com/wp-content/uploads/2023/12/Capture-
decran-2023-12-20-a-10.53.26-1024x588.png)

This Angel Drainer tricks users into signing different types of transactions
depending on the type of asset it is currently targeting. For ERC20 and NFT
tokens, it requests users to sign _approval_ and _permit_ messages. For native
tokens, the drainer asks the user to sign either a fake “claim” transaction
where the _claim_ method simply sweeps the funds, or simple token transfers
that can be later sweeped by deploying a smart contract at the corresponding
address.

This is why we continue to encourage Clear Signing as an industry, so users
can verify what they see on a trusted display on their Ledger hardware device.

##### Remedial actions

The Ledger security and technology teams, including the Ledger executive team,
are currently reviewing and auditing all our access controls on Ledger
internal and external tools and systems that we use.

Ledger will reinforce its policies when it comes to code review, deployment,
distribution, and access controls, including adding all external tools to our
maintenance and off-boarding checks. We’ll continue to generalize code signing
when relevant. Additionally we are conducting recurrent internal audits to
make sure this is properly implemented.

Ledger already organizes security training sessions, including phishing
training. The internal security training program will also be reinforced at
the start of 2024 for all employees in their respective departments. Ledger
already organizes regular third party security assessments and will continue
to prioritize these assessments.  

In early 2024, a specific third party audit will be conducted focused on
access control, code promotion and distribution.

In addition, we’ll reinforce our infrastructure monitoring and alerting
systems to be able to detect and react even faster to future incidents..

Finally, we’ll double down on preventing Blind Signing, removing it as an
option for Ledger users to ensure utmost security practices, and educate users
on the potential impact of signing transactions without either a secure
display or understanding what they are signing by not using Clear Signing.

We thank again our partners in the ecosystem for swiftly working with the
Ledger teams on identifying and resolving the exploit.

[](https://www.facebook.com/Ledger/)
[__](https://www.instagram.com/ledger/)[](https://twitter.com/Ledger)
[](https://www.linkedin.com/company/ledgerhq/)
[](https://www.reddit.com/r/ledgerwallet/)
[__](https://www.tiktok.com/@ledger)

More articles

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

[](https://www.ledger.com/ledger-and-samsung-strengthen-their-partnership-
providing-uncompromising-security-to-the-samsung-tv "Ledger and Samsung
Strengthen Their Partnership, Providing Uncompromising Security to the Samsung
TV ")

[Blog posts](https://www.ledger.com/category/blog-posts "Blog posts"), [Company](https://www.ledger.com/category/company-news "Company") | 04/11/2024 

Ledger and Samsung Strengthen Their Partnership, Providing Uncomp...

[Read more](https://www.ledger.com/ledger-and-samsung-strengthen-their-
partnership-providing-uncompromising-security-to-the-samsung-tv "Ledger and
Samsung Strengthen Their Partnership, Providing Uncompromising Security to the
Samsung TV ")

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

![](https://t.co/1/i/adsct?bci=4&eci=3&event=%7B%7D&event_id=d3664a8f-5cf2-43cc-8b59-1c3801323701&integration=gtm&p_id=Twitter&p_user_id=0&pl_id=f0b811f5-a361-43fd-875d-477ff1758568&tw_document_href=https%3A%2F%2Fwww.ledger.com%2Fblog%2Fsecurity-
incident-
report&tw_iframe_status=0&txn_id=nzkax&type=javascript&version=2.3.30)![](https://analytics.twitter.com/1/i/adsct?bci=4&eci=3&event=%7B%7D&event_id=d3664a8f-5cf2-43cc-8b59-1c3801323701&integration=gtm&p_id=Twitter&p_user_id=0&pl_id=f0b811f5-a361-43fd-875d-477ff1758568&tw_document_href=https%3A%2F%2Fwww.ledger.com%2Fblog%2Fsecurity-
incident-
report&tw_iframe_status=0&txn_id=nzkax&type=javascript&version=2.3.30)

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

![](https://bat.bing.com/action/0?ti=134633242&tm=gtm002&Ver=2&mid=cc862f54-7fb9-4bcd-9785-c60b35163389&sid=cdd84e501cfd11ef8e7c0bd86e468225&vid=cdd85d301cfd11ef8118f33c95a91a95&vids=1&msclkid=N&pi=918639831&lg=en-
US&sw=800&sh=600&sc=24&tl=Security%20Incident%20Report%20%7C%20Ledger&p=https%3A%2F%2Fwww.ledger.com%2Fblog%2Fsecurity-
incident-report&r=&lt=3218&evt=pageLoad&sv=1&rn=230494)

![dot image
pixel](https://sp.analytics.yahoo.com/sp.pl?a=10000&d=Tue%2C%2028%20May%202024%2014%3A23%3A08%20GMT&n=0&b=Security%20Incident%20Report%20%7C%20Ledger&.yp=10159916&f=https%3A%2F%2Fwww.ledger.com%2Fblog%2Fsecurity-
incident-report&enc=UTF-8&yv=1.15.1&tagmgr=gtm)
