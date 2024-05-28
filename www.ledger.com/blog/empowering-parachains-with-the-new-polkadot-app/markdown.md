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

[Blog](https://www.ledger.com/blog/empowering-parachains-with-the-new-
polkadot-app) __[Blog posts](https://www.ledger.com/category/blog-posts "Blog
posts")

[Blog posts](https://www.ledger.com/category/blog-posts "Blog posts"), [Tech](https://www.ledger.com/category/tech "Tech") | 12/01/2023 

# Empowering Parachains with the new Polkadot app: The Secure Way Forward

The Polkadot ecosystem is about to take a giant leap forward with the
development of a new Polkadot Ledger embedded application, a groundbreaking
project driven by the collaboration of Alzymologist Oy and Zondax.

[Blog](https://www.ledger.com/blog/empowering-parachains-with-the-new-
polkadot-app) __[Blog posts](https://www.ledger.com/category/blog-posts "Blog
posts")

The Polkadot ecosystem is about to take a giant leap forward with the
development of a new Polkadot Ledger embedded application, a groundbreaking
project driven by the collaboration of Alzymologist Oy and
[Zondax](https://zondax.ch/) described in this
[proposal](https://polkadot.polkassembly.io/referenda/62). This initiative
aims to create a robust, offline devices friendly, metadata protocol, and
implement it in Ledger devices. This project will mark a significant milestone
in enhancing the security and functionality of the entire Polkadot network.

##### **Understanding the Challenge**

Before we delve into the new Polkadot app, let’s grasp the challenge it
addresses. While many blockchain systems support offline signing for air-
gapped wallets and lightweight embedded devices, only a few allow full message
decoding on the offline signer’s side. Polkadot, built on the Polkadot SDK, is
one of these few, and it provides a solid foundation to elevate transaction
security and network resilience. However, this comes with a set of challenges:

  1.  **Large Metadata** : A metadata entity, describing chain interfaces and properties, poses challenges for efficient transfer to cold storage devices due to its significant size.
  2. **Metadata Authenticity** : Ensuring the authenticity of metadata is challenging and often relies on trusted parties, which may create centralized points of failure.

##### **The new Polkadot app Solution**

The new Polkadot embedded app is a secure, hardware wallet application
designed for Ledger devices. It’s versatile and capable of handling parachains
and relay chains without being affected by runtime upgrades. The goal is to
provide a single application for the entire Polkadot ecosystem without
compromising security.

###### **Key Features**

  1. **Metadata Integration** : The new Polkadot app includes metadata in transaction signatures, enhancing the network’s security. This metadata is used for transaction rendering, ensuring users can verify the transaction details.
  2. **Reduced Metadata Size** : To optimize metadata for small embedded devices, a succinct metadata representation is proposed. It involves a Merkle tree to shorten the metadata’s size and make it more manageable for devices with limited RAM.
  3. **Dynamic Parsing** : The app can parse metadata efficiently, even on devices with limited dynamic memory.
  4. **Extended Signature Mode** : The app introduces an extended signature mode with a domain separation feature. It doesn’t require the inclusion of the root of the Merkle tree in transactions, reducing overhead.

###### **Collaborative Effort**

The success of this initiative depends on collaboration among multiple
stakeholders, including Zondax, integral components of the Polkadot ecosystem
like Parity, and Ledger. Funded through the Polkadot Treasury, this joint
effort aims to provide a long-term, secure, and generic solution.

##### **The Impact**

The new Polkadot app will be available for all Polkadot-SDK-based chains,
significantly enhancing offline device security and usability. The benefits
include:

  * **Improved Ecosystem Resilience** : Enhancing network security and removing significant user experience issues.
  * **Innovation Acceleration** : Enabling teams to innovate and develop new features for relay chains, parachains, and current/future users.
  * **Network Adoption** : Facilitating a smoother and more user-friendly adoption of the Polkadot ecosystem.

##### **Conclusion**

The new Polkadot app is poised to be a game-changer for operating the Polkadot
ecosystem. It represents a step towards greater security, reliability, and
efficiency.

Stay tuned for more updates as this project continues to unfold. Zondax will
keep the latest developments updates on the [new Polkadot app dedicated
forum](https://forum.polkadot.network/t/polkadot-generic-ledger-app/4295)  
A support article is being prepared to be published on [Ledger
docs](https://support.ledger.com/hc/en-
us/categories/4404376139409-Documentation-?docs=true). It will detail the
different interactions enabled by the new Polkadot application.

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

