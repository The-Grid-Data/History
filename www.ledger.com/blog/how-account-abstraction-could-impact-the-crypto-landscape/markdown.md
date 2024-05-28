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

[Blog](https://www.ledger.com/blog/how-account-abstraction-could-impact-the-
crypto-landscape) __[Blog posts](https://www.ledger.com/category/blog-posts
"Blog posts")

[Blog posts](https://www.ledger.com/category/blog-posts "Blog posts"), [Tech](https://www.ledger.com/category/tech "Tech"), [Thought leadership](https://www.ledger.com/category/thought-leadership "Thought leadership") | 09/12/2023 

# How ‘Account Abstraction’ Could Impact The Crypto Landscape?

Charles Guillemet, CTO at Ledger, explores how the concept of “Account
Abstraction” will radically improve user experience in crypto and why hardware
wallets will serve as foundational roots of trust in this new paradigm.

[Blog](https://www.ledger.com/blog/how-account-abstraction-could-impact-the-
crypto-landscape) __[Blog posts](https://www.ledger.com/category/blog-posts
"Blog posts")

The global internet revolution has ushered in an undeniable wave of
digitization that is now spreading to the very concept of ownership with the
rise of blockchain technologies. As we navigate this transition from one
Internet era to the next, from Web2 to Web3, the friction for users only seems
to intensify. Blockchain interactions remain complex and primitive; they lack
security and ease of use, especially regarding account management and logins,
deterring too many from entering the crypto field.

Account Abstraction, a blockchain-enabled technology allowing people to use
smart contracts as their accounts and set their own flexible rules for wallet
management, is a significant promise to alleviate this friction and inculcate
enhanced user rules and security measures in the crypto space.

In this article, I delve into the concept of Account Abstraction and explore
how it could underpin the future of blockchain technologies.

##### Externally Owned Account (EOA): blockchains’ initial principle

To fully understand “account abstraction” technologies, one must seize the
initial paradigm of blockchains implementation, rooted in what we commonly
call “Externally Owned Account” (EOA).

An EOA works with users generating cryptographic pairs of keys: a public key
for creating addresses and a private key allowing their owners to control an
account. Within the EOA framework, the signer and the account are the same
entity. Once the pair of keys is generated, users prove ownership of the
address by computing a digital signature to execute transactions. The
decentralized consensus validates these transactions by verifying that the
signature is correct and has actually been computed using the private key that
corresponds to the given address.

EOA is at the core of the original design of Bitcoin and Ethereum. Despite
being quite elementary, **this mechanism is incredibly efficient for a
pseudonymous network of users to transfer value in a permissionless
environment**. However, its design is limiting when it comes to implementing
enhanced features such as governance, recovery mechanisms, or more generally
code execution.

Some major blockchain protocols already feature such use cases.

###### The case of Bitcoin:

Bitcoin has a limited (on purpose) programming language that allows its
protocol to enforce on-chain rules when interacting with accounts. For
instance, Bitcoin’s scripting language enables users to create multisig
wallets that enforce spending rules over the user’s UTXO (unspent transaction
output).

Additionally, timelocks can be implemented, too. For example, on Bitcoin, it’s
possible to create a multisig wallet that implements the following rules, as
shown in the illustration shown below:

  * 3 signers are registered on a given wallet.
  * 2 signatures out of 3 are necessary to move funds.
  * No fund can move before a given block.

![](https://www.ledger.com/wp-content/uploads/2023/09/unnamed-2.png)

While the set of rules and the scripting language of Bitcoin may be somewhat
limited, they still enable the design of the [Lightning
network](https://www.ledger.com/academy/glossary/lightning-
network#:~:text=The%20Lightning%20Network%20is%20a%20secondary%20layer%20built%20on%20the,architecture\)%20base%20level%20Bitcoin%20blockchain.).

###### The case of Ethereum:

On Ethereum, the design principle is different since the original vision was
to create **a decentralized, trustless computing machine**. Contrary to
Bitcoin, the language semantic is Turing complete, enabling to compute
anything easily, including the execution of arbitrary programs (smart
contracts) that run on-chain and provide trusted computing. These smart
contracts also enable enhanced designs and incredible innovations, including
Automated Market Makers (AMM). However, Ethereum’s language leads to
undecidability problems, but that’s another story.

One of  the main limits of  Ethereum’s design is the fact that all smart
contract executions must originate from an EOA. For instance, it’s impossible
to create a standalone smart contract that executes itself at each block.
Doing so would require an EOA that triggers transactions and pays for gas
execution at each block.

##### On-chain smart contract implementation: some interesting ideas

Leveraging sophisticated smart contract design for on-chain governance has
already been  implemented in diverse ways.

###### Safe: on-chain multisig with minimal governance level:

Crypto platforms such as Safe did a great job at providing an on-chain
multisig that enables users to set a minimal level of governance rules over an
account.

With Safe, multiple parties jointly control an Ethereum wallet and set custom
rules and conditions for transactions, such as requiring a minimum number of
signatures or approvals before the execution of a transaction. The different
signers can customize security settings according to their preferences. For
example, they can set daily spending limits, enable hardware wallet
integration for additional security, or require multiple levels of
authentication for specific transactions. These smart accounts are controlled
by several EOAs  issuing valid on-chain signatures then triggering the token
transaction held in the smart contract.

###### Threshold Signature Schemes (TSS): off-chain governance at minimal
fees:

Recent cryptography research worked on creating threshold signature schemes
(also known as threshold signature schemes (TSS) or multi-party computation
(MPC)) to implement the multi-authorization part of the governance, off-chain.

This idea has interesting advantages. In particular, it’s directly compatible
with the EOA model and minimizes fees.

###### Elliptic Curve Digital Signature Algorithm (ECDSA): secure, with strong
drawbacks:

Ethereum and Bitcoin blockchains use an Elliptic Curve Digital Signature
Algorithm (ECDSA) signature scheme for transactions.

However, contrary to Schnorr’s signature, ECDSA is not **provably secure under
DLP difficulty and Random Oracle Model**. Furthermore, ECDSA has not been
created to natively support Threshold Signature Schemes, leading to clunky
designs. More specifically, Signature aggregation of other Signature schemes
is provably secure, while ECDSA’s is not. Equations of Threshold Signature
Schemes over ECDSA are hacky, leading to regular implementation issues. Last
but not least, there’s currently no TSS scheme running in secure enclaves,
leading to dangerous security tradeoffs.

##### Account Abstraction: the real game-changer crypto needs?

The great novelty ushered in by the concept of ‘Account Abstraction’ is the
use of on-chain smart contracts to implement the wallet and the governance
rules around it. These ideas have already been implemented in multiple smart
contract accounts, including Argent, or with minimal governance with on-chain
multisig such as Safe.

Much progress has been made in this area over the past months and years, and a
few standardization trials have been attempted. The recent standard that had a
lot of traction is known as ERC-4337. This standard provides a comprehensive
framework for implementing different types of operations with a given and
flexible governance.

More specifically, ERC-4337 solves the technical specificities of implementing
Account Abstraction in a EOA blockchain context, including:

  * Operation intent.
  * Operation validation.
  * Execution and fees payment (remember, on Ethereum, all operations are triggered by an EOA which pays fees. So, ERC4337 provides an incentive framework for decentralized bundlers to trigger the execution of the operations that users intend to execute.)
  * The nonce, an anti replay mechanism that was just incremental for EOAs and can be more sophisticated here.

When it comes to governance, it’s possible to create different signers and
quorums to complete specific operations. Schematically, the user will interact
with his smart contract, the smart contract then verifies whether governance
rules are met, and finally executes the operations.

Verifying the governance can be as complex. One of the benefits of having this
logic running on-chain with a Turing complete language is that it’s possible
to create arbitrary governance rules and  to implement signature verification
for any algorithm. As mentioned above, ECDSA scheme has plenty of limitations,
first of all it’s not suited for signature aggregation (MPC / TSS), and
secondly it’s not supported by current implementations in mobile’s secure
enclaves.

###### An improved User Experience & flexible Security:

Thanks to Account Abstraction, it is possible to perform several atomic calls
to different contracts in the same transaction with a smart account, leading
to great improvements when navigating typical DApps (for example, it is no
longer necessary to send 2 distinct transactions for an ERC-20 token approval
then a deposit), as well as for the security of the user (for example ENS
resolution can be directly performed by the smart contract account.)

###### The path to innovative Social Recovery methods:

By enabling complex operations at the account level, Account Abstraction can
realize various advanced use cases, such as social recovery. In this scenario,
users can designate a group of trusted guardians who can grant them access to
their account should they lose access. EIP 5883 and the more recent EIP 7093
outline interesting methods for implementing such social mechanisms.

Once more, users can specify both a threshold and a set of rules that will
initiate the account recovery process in the event of access loss, which could
radically improve user experience in crypto.

###### BLS/Schnorr signature aggregation:

As mentioned before, another weakness of ECDSA is the clunky Threshold
signature design. Contrary to ECDSA, BLS and Schnorr have been designed for
supporting Threshold signature scheme, and these standards are essentially
additive. In brief, it’s possible to compute a valid signature by adding
several partial signatures with strong security guarantees.

Implementing BLS or Schnorr signers could allow some token governance while
minimizing fees at verification by the smart contract (One verification
instead of one verification per signature.) This aggregation mechanism is
described and implemented optionally as part of the EIP 4337 standard.

##### What’s next for the adoption of Account Abstraction?

###### The case of Passkeys:

Account Abstraction is in direct competition with software wallets in the EOA
context. [The security model of software wallets is very
weak](https://www.ledger.com/blog/software-wallets), as any malware can drain
users’ funds due to their inherent Internet connectivity and more generally
their wider attack surface. Software wallets can’t really do better since SoC
(System On Chip) based designs (smartphones) are very heterogeneous and do not
all contain a secure enclave.

When they do contain a secure enclave, developers can’t load their own code to
implement Ethereum/Bitcoin signatures. In this context it’s simply NOT
possible to leverage the only security features contained in high end phones.

By incorporating the Account abstraction logic, developers can access a secure
enclave digital signatures implementation. This includes WebAuthn, which is
readily available at the OS level through passkeys standard.

It’s also possible to establish an on-chain rule in which the signatures
originate from users’ passkeys. These passkeys use a different Elliptic curve
than the one used on the Ethereum blockchain, but as the signature
verification can be implemented on the smart contract itself, this mechanism
becomes achievable.

![](https://www.ledger.com/wp-content/uploads/2023/09/Capture-
decran-2023-09-12-a-16.42.17.png)

![](https://www.ledger.com/wp-content/uploads/2023/09/Capture-
decran-2023-09-12-a-16.48.48-1.png)

Regarding UX, users can benefit from a broad integration within Apple, Google,
and Microsoft ecosystems. It also gives a better level of security than a full
software wallet. Additionally, the smart contract can enforce various kinds of
governance and security mechanisms on-chain. For instance, each transaction
execution can be secured by a Web3 firewall that is implemented off-chain and
authorizes the smart contract to execute a specific transaction. Such a
mechanism allows flexible security guards according to the user risk profile.

On the security front, such a setup (Account Abstraction with Passkeys
authenticator) provides better guarantees than current mobile wallets. Modern
smartphones can use Trustzone to implement passkeys. Nonetheless, the current
landscape of passkeys implementation is not satisfactory for the following
reasons:

  * Passkeys is likely implemented in [full software](https://security.googleblog.com/2022/10/SecurityofPasskeysintheGooglePasswordManager.html) mode for Android and iOS. They don’t leverage the embedded Secure element (yet?).

  * Smartphones don’t implement Trusted User Interface and passkeys framework doesn’t provide the necessary information to users when they sign which means you could consent for transactions that you don’t understand.

##### Account Abstraction and the importance of Hardware Wallets as roots of
trust

The concept of Account Abstraction empowers the fine-grained governance of
diverse assets within a smart contract. When utilizing a wallet for micro-
payments, these governance rules enable the execution of low-value
transactions easily. Conversely, for higher-value transactions, a heightened
level of security remains paramount, making hardware wallets the indisputable
choice by far.

For instance, Account Abstraction will enable:

  * **Pocket money,** which can be spent using passkeys on any smartphone.

  * **Higher value transactions,** all requiring secure hardware wallet signature and Web3 firewall.

  * **Life Saving and Identity management,** requiring hardware wallet signature + passkey + timelock + Web3 firewall.

**As they continue to develop, these governance rules will need to be enacted
with hardware wallets serving as the foundational root of trust, as these
devices enable uncompromising security and ownership. Indeed, while Account
Abstraction changes the security model, the overall wallet still needs strong
security guarantees. The design of the governance rules holds paramount
importance from a security perspective, especially in safeguarding the keys
responsible for their modification.   Additionally, the different signers able
to interact with the Account Abstraction layer will still need certain forms
of secrets (private keys) to authenticate themselves. Protecting these secrets
and providing the user with all the necessary information to consent to any
blockchain interaction remains crucial, even in an Account Abstraction
framework.**

###### Closing Thoughts:

As previously explored, the EOA paradigm remains somewhat rudimentary. In
contrast, Account Abstraction’s capacity to enforce complex on-chain rules is
likely to become a radical game-changer for crypto users. Interestingly, the
recent progress around EIP 4337 brings us closer to this significant shift.

Of course, several challenges lie ahead.

One of these challenges is that the blockchain itself executes the Account
Abstraction’s flexible governance model, which means that the execution comes
at high costs compared to regular EOA transactions. On Ethereum’s Layer-1, the
chain isn’t very scalable, and the execution is consequently quite costly.
**However, on scalable Layer-2s, Account Abstraction could become the default
choice where users define complex governance rules enforced by the Layer-2
consensus and anchored in the Ethereum Layer-1.**  

Another challenge is the fundamental need to create a standard way to interact
with Account Abstraction frameworks, so far focused on EVM chains. These
generic wallets offer a wide range of possibilities, including high
flexibility. However, without standardization, they could also remain
proprietary, which, in turn, could challenge mass adoption.** **

In fact, we will likely witness a future where the Account Abstraction
paradigm could become a fundamental feature of EVM chains, while EOA
interaction could play a pivotal role in other blockchain networks, including
Bitcoin, even though such a fragmented protocol landscape isn’t desirable for
users. We can also anticipate that these changes, driven by Account
Abstraction, will eventually be integrated at the blockchain level. One thing
is certain: Account Abstraction belongs to the future of blockchain.

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

