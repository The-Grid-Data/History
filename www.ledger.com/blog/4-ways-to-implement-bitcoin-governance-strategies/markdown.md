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

[Blog](https://www.ledger.com/blog/4-ways-to-implement-bitcoin-governance-
strategies) __[Blog posts](https://www.ledger.com/category/blog-posts "Blog
posts")

[Blog posts](https://www.ledger.com/category/blog-posts "Blog posts"), [Tech](https://www.ledger.com/category/tech "Tech"), [Thought leadership](https://www.ledger.com/category/thought-leadership "Thought leadership") | 10/20/2023 

# 4 Ways To Implement Bitcoin Governance Strategies

Charles Guillemet, CTO at Ledger, explores different options to implement
Bitcoin governance strategies at the institutional level.

[Blog](https://www.ledger.com/blog/4-ways-to-implement-bitcoin-governance-
strategies) __[Blog posts](https://www.ledger.com/category/blog-posts "Blog
posts")

  
Things to know:_  
_  
---  
  
– _Your Ledger devices are extremely useful for letting users self-custody
their Bitcoin. But what if you’re an organization, or a financial institution?
_  
  
– _Multiple solutions exist to implement Bitcoin Governance with complex
rules. Among them are Miniscript, Multi-Party Computation (MPC), as well as
MuSig2 and FROST. Our Ledger devices already support Miniscript, and I’m glad
to announce that we will support MuSig2 in the coming months._  
  
– _We have also developed[the Ledger Vault](https://enterprise.ledger.com/) to
empower organizations and financial institutions to efficiently manage Bitcoin
and other crypto assets. _  
  
_– This solution leverages Hardware Security Modules (HSMs) and Personal
Security Devices (PSDs). We have loaded the Ledger Operating System with its
security property, isolation, and cryptographic implementation on the secure
hardware and a governance framework.  _  
  
  
  
When a friend introduced me to the Bitcoin whitepaper in 2011, I decided to
study this protocol’s cryptography, technology, double-spending problem, and
decentralized consensus. I returned to my friend and told him: “Your Bitcoin
thing is pretty interesting, but frankly, I don’t understand the use case!”
When I joined Ledger in 2017, he made fun of me: “Do you finally get it?” he
said. Yes, I finally got it.

Bitcoin is revolutionary because it brings something unprecedented:
“Permissionless Money”. With Bitcoin, you don’t need to ask anyone to own and
spend your digital value. No state, bank, or third-party can ever interfere
with the value you hold and transact. With Bitcoin, you possess a piece of the
Internet with complete self-sovereignty and freedom.

##### Two properties enabling permissionlessness: “decentralized consensus” &
“self-custody”

The first property that contributes to Bitcoin’s permissionless nature is
known as “decentralized consensus”. With Bitcoin, you have decentralized pools
of miners that are incentivized to secure the network and prevent censorship
over the execution of transactions. Simply put, when you want to make a
transaction, no one can prevent you from making it.

The second property is self-custody. With self-custody, you own your value,
and no one can prevent you from owning it, which allows you to control your
crypto-assets fully. In order to own Bitcoin, you simply have to generate a
public (which is essentially your address) and a private key (your key to
prove ownership over your assets). If you lose your private key, you lose your
assets, and if an attacker accesses your private key, he will be able to make
a transaction… and there’s nothing you can do to revert it.

This need to protect your private keys from hackers is why we’ve built our
[Ledger Nano devices.](https://shop.ledger.com/) This hardware embeds a secure
element, where your secrets are generated within the enclave, and the
cryptography is implemented within it so that your secrets don’t have to leave
the enclave. Your device also features a trusted display, allowing you to
understand the transaction you are about to consent to signing.

**All of the elements I’ve explained above are pretty simple, but mostly apply
to individuals. What does it mean when you are a group of people, an
organization, or a financial institution?  **

##### Leveraging Bitcoin at the institutional level

You may not want to store your assets on a Ledger Nano when you are an
exchange (some did it at the expense of their customers, including FTX and
QuadrigaCX). These devices are perfectly secure; you could keep billions on
them, but you want to avoid the operational risk of having a single person
from your organization fully controlling all the customers’ funds.

Who has access to the coin if organization X decides to buy $100 Million worth
of bitcoin? Who can rule whether they use it this way or that way? **These are
crucial questions, so let’s consider what kind of governance we can have over
Bitcoin.**

###### The initial and onchain option: MultiSig on Bitcoin

It used to be _Partially Signed Bitcoin Transactions (PSBT)._ This is not very
well known, but you have a scripting language called Script on Bitcoin. With
this scripting language, you can define an account with different rules
enforced on-chain. So, you can create a rule saying: _‘I can spend X amount of
Bitcoin when I have these signatures.’_ Then, the blockchain verifies that
these free signatures happen.

Script is great, but the Script language can be cumbersome to verify. That’s
why Miniscript was created in 2019. Miniscript is a language for representing
Bitcoin Scripts in a structured way, enabling efficient analysis, composition,
generic signing, and more. For instance, “Alice can spend (main path), or a
3-of-3 of Bob, Carol, and Dave can spend, but after three months, two
signatures are enough (secondary spending path).”

![](https://www.ledger.com/wp-content/uploads/2023/10/Capture-
decran-2023-10-20-a-16.13.04-1024x427.png)

Our hardware wallet devices have supported both PSBT and [Miniscript on SegWit
for over a year](https://blog.ledger.com/miniscript-is-coming/) and Miniscript
on Taproot will be supported in the next release. You can leverage all the
security properties of Ledger devices and an onchain governance over Bitcoin
accounts. You can even leverage miniscript with Ledger in order to [further
minimize trust](https://www.ledger.com/blog/towards-a-trustless-bitcoin-
wallet-with-miniscript).

###### Multi-Party Computation (MPC) solutions

MPC stands for secure Multi-Party Computation. That’s a wide field of
cryptography that consists in doing computation in a distributed manner, such
as, for example, jointly computing signatures. In particular, in a t-of-n
threshold signature scheme, the signing key is distributed in n shares and a
subset of t shares is required to compute a valid signature (where typically
n=3 and t=2). From a blockchain standpoint, the resulting signature looks like
a standard “single-party” signature.

It’s pretty elegant, but there are a few drawbacks to the currently
implemented solutions.

  * The first drawback is address management. Existing threshold signature schemes are not compatible with BIP32, meaning it is not possible to have HD (hierarchical deterministic) wallets as with a standard seed. Additionally, due to the specific nature of MPC-based wallet, recovering your wallet on a standard BIP39 wallet could be impossible, which is a limitation to self sovereignty.

  * The second drawback is that current secure hardware does not support MPC today. That means that the cryptography of MPC protocols must be implemented in software, which is not a good practice. I often hear some dismissive marketing saying that as it’s MPC, there is no secret. This is not true. You still have secret key shards, and you need to secure them. 

  * The third drawback is that currently available MPC protocols rely on ECDSA, the original signature scheme used in Bitcoin, resulting in complex and hard to implement schemes, as testified by the multiple vulnerabilities found in existing MPC wallets.

###### MuSig2 and FROST

The good news is: Schnorr signatures have been standardized on Bitcoin around
three years ago with the Taproot upgrade. The Schnorr signature scheme is
really better than ECDSA for various reasons. First, it has better security
guarantees than ECDSA which is not provably secure, and second, its algebraic
structure is much simpler than ECDSA, which means that MPC protocols for
Schnorr are much easier to design.

It’s been standardized on Bitcoin with these two papers. [The first one is
MuSig2](https://eprint.iacr.org/2020/1261), allowing multi-signature (i.e.,
n-of-n threshold signatures), and [the second one is
FROST](https://eprint.iacr.org/2020/852.pdf), enabling you to do arbitrary
t-of-n threshold signatures.

**At Ledger, we are already supporting Schnorr on our devices and working on
supporting MuSig2, allowing multi-signatures on-chain on Bitcoin, in the
coming months.  **

###### Ledger Enterprise for Tailored Institutional Governance

While perhaps not as widely well known as Ledger’s retail solutions, [we have
developed a suite of products](https://enterprise.ledger.com/) designed to
empower enterprises, organizations, and financial institutions in the secure
and efficient management of digital assets at scale. This innovative solution
leverages Ledger’s robust technology and secure hardware along with a flexible
governance framework on top of it.

The solution is called Ledger Vault. It leverages Hardware Security Modules
(HSMs) and Personal Security Devices (PSDs). We have loaded the Ledger
Operating System with its security property, isolation, and cryptographic
implementation on the secure hardware, and on top of this, a governance
framework.

With Ledger Vault, you can achieve the same level of security and self-custody
as Ledger Nanos, but with the valuable addition of a governance layer allowing
corporations to establish various organizational roles, including shared
owners, administrators, and operators.

Depending on these roles, you can define rules and policies to regulate access
and transactions. For example, it permits you to grant a specific group access
to a set of accounts and restrict them to transactions to particular
addresses. If a group intends to execute a transaction exceeding a certain
threshold, it requires the consensus of three out of five approvals.

The governance can also be based on KYC/AML checks and connected to other
actors like exchanges through our product TRADELINK, further enhancing its
adaptability and compliance capabilities.

Ledger Vault offers this high level of flexibility within a secure framework,
and is specifically designed to cater to the self-custody governance needs of
institutional users. Its universality across different blockchains makes it a
standout solution in the digital asset management space, ensuring it meets the
diverse needs of users across the blockchain ecosystem.

##### Closing Thoughts

As I’ve outlined above, Bitcoin is game-changing because it brings
permissionless money, something enabled by two key concepts: decentralized
consensus and self-custody. Self-custody is more complex when it comes to
organizations, and my conviction is that self-custody is fully compatible with
companies if you have some predetermined levels of governance over the tokens.

Then, you have different possibilities. Some are on-chain, others are off-
chain, but you can also consider a mix of them. At Ledger, we are supporting
PSBT and Miniscript on Ledger Nano devices. We are also working on
implementing MuSig2, which is coming soon. For enterprise organizations, we
are offering Ledger Vault, provided by Ledger Enterprise.

When you set up these solutions, you need to strongly consider governance
frameworks. Governance includes who can access and who can spend the digital
assets. It’s also about determining thresholds, maintaining whitelists, etc.
Then you also have to think about security: where the essential materials are
stored, how they are secured, how the cryptography is implemented. You must
also strongly consider control, which means: who has access to the shards?
This becomes particularly critical in a multisig setup that depends on a third
party you don’t particularly trust. Finally, backup and interoperability are
essential aspects. Having a backup and testing it is something you need to
consider. Interoperability is significant, too. If your provider disappears,
you need to keep control over your wallet.

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

