Metaco.com will be sunset as of June 7, 2024

[Learn more](https://ripple.com/solutions/digital-asset-custody/ "Learn more")

Skip to main content

[![Metaco](https://www.metaco.com/wp-
content/themes/metaco/assets/images/logo.svg?x88149)![](https://www.metaco.com/wp-
content/themes/metaco/assets/images/logo-w.svg?x88149)](https://www.metaco.com)

  * Solutions __

__Solutions

Solutions

    * [__Global Custodians Build tomorrow's market infrastructure ](https://www.metaco.com/audiences/global-custodians-top-tier-banks/)
    * [__Universal Banks Satisfy demand for new asset classes ](https://www.metaco.com/audiences/universal-banks/)
    * [__Neobanks & FintechsFind new routes to monetization ](https://www.metaco.com/audiences/neobanks-fintechs/)
    * [__Regulated Exchanges Grow volumes and profit margins ](https://www.metaco.com/audiences/regulated-exchanges/)
    * [__Corporates Boost customer loyalty and engagement ](https://www.metaco.com/audiences/corporates/)

  * Platform __

__Platform

Platform

Deploy ambitious digital asset use cases with the most secure and versatile
infrastructure.

    * [__Harmonize™ Platform Overview Issue, store, trade, transfer, settle and service any type of digital asset. ](https://www.metaco.com/platform/harmonize/)
    * [__Custody Hot, warm and institutional cold storage ](https://www.metaco.com/platform/custody/)
    * [__Trading Powerful order execution, funding and settlement ](https://www.metaco.com/platform/trading/)
    * [__Web3 Web3 Portal spanning NFTs, DeFi and DApps ](https://www.metaco.com/platform/web3/)
    * [__Governance Entirely customizable risk and compliance controls ](https://www.metaco.com/platform/governance/)
    * [__Orchestration A single source of truth for managing all digital assets ](https://www.metaco.com/platform/orchestration/)
    * [__Tokenization Asset-agnostic smart contract management framework ](https://www.metaco.com/platform/tokenization/)
    * [__Integration Fully integrable platform following enterprise standards ](https://www.metaco.com/platform/integration/)
    * [__Security Highest protection against insider and external threats ](https://www.metaco.com/platform/security/)

  * Company __

__Company

Company

    * [__About](https://www.metaco.com/company/about/)
    * [__Media & news](https://www.metaco.com/company/media-coverage-press-releases/)
    * [__Careers](https://www.metaco.com/careers/)

  * Resources __

__Resources

Resources

    * [__Talks](https://www.metaco.com/resources/talks/)
    * [__Webinars](https://www.metaco.com/resources/webinars/)
    * [__Case studies](https://www.metaco.com/resources/case-studies/)
    * [__Reports](https://www.metaco.com/resources/reports/)
    * [__Blog](https://www.metaco.com/resources/blog/)

[Contact](https://www.metaco.com/contact/ "Contact")

[Blog](https://www.metaco.com/category/blog/)

# MPC and HSM for Key Management Part 1: Demystifying Technology Options for
Digital Asset Custody

  *  __ November 16, 2023
  *  __7 min

Share

  * [ __](https://www.linkedin.com/sharing/share-offsite/?url=https%3A%2F%2Fwww.metaco.com%2Fblog%2Fmpc-and-hsm-for-key-management-part-1-demystifying-technology-options-for-digital-asset-custody%2F)
  * [__](https://twitter.com/intent/tweet?text=Metaco+https%3A%2F%2Fwww.metaco.com%2Fblog%2Fmpc-and-hsm-for-key-management-part-1-demystifying-technology-options-for-digital-asset-custody%2F+via+%40metaco_sa)

The rapidly growing universe of[digital asset types, tokenization and use
cases](https://www.metaco.com/blog/tokenization-asset-ownership-etf-reit/) is
driving an urgent demand for more secure institutional digit asset custody
solutions. Providers are rushing to fulfill this need by providing high net
worth individuals, family offices, enterprises and others with a wider array
of custodian options[1].

Banks and financial services institutions have a unique opportunity to
leverage their long history as custodians of traditional assets to diversify
their portfolios and offer trusted digital asset custody solutions for
clients. But how to make sense of the different key management technology and
protection options available?

In this first post in a two-part series, we’ll look at three technology
decisions providers must make as part of rolling out a crypto custody
solution.

### Hot Wallets, Cold Wallets and Everything in Between

At the core of any custodian strategy lies the ability to securely hold and
access a range of digital assets. This access is granted through cryptographic
private keys, which enable the transfer or control of the asset. Securing
these keys is paramount, and that begins with a choice of wallet.

Hot wallets are those connected to the web. Designed for real-time
transactions, they are ideal for high-frequency, low-risk activities. They are
ideal for permissioned use cases requiring fast, automated access to liquidity
and web transactions, for example conveniently accessing funds on the go.
However, their constant connection to the internet—while convenient for
accessing funds—makes them more vulnerable to attacks and often requires the
use of additional advanced protection technologies.

On the other hand, cold wallets feature offline storage of private keys within
a physical hardware wallet, which means the process of accessing funds within
a cold wallet can be extremely manual. While this can pose challenges for many
institutional needs, it also helps to de-risk the storage of digital assets.
Given their nature and enhanced security to mitigate the risk of cyber-
attacks, they are best used for crypto custody or low-frequency, high-risk
transactions.

Another more recent form of cold wallet technology to come on the scene is
air-gapped cold wallets, which are hardware wallets completely disconnected
from any wireless network, including WiFi and bluetooth. “Air-gap” is a
computer security term referring to the complete isolation of a device or a
network from other networks or devices[2].

Last but not least, account abstraction—which leverages smart contracts to
manage funds—allows users to retain full control over their wallet and
funds[3]. They are protected by a multi signature wallet from either cold
wallets or hot wallets.

![](https://www.metaco.com/wp-content/uploads/2023/11/metaco-
blog-03-website.jpg?x88149)

### To Shard or Not to Shard: HSM and MPC Wallet Explained

Within institutional wallets, there are two primary options today for managing
private keys. The most straightforward and simplest to understand are Hardware
Security Modules (HSMs). These are physical hardware devices or cloud-based
storage options that have been specifically developed to protect crypto keys
using a combination of physical security, cryptographic isolation, secure
communications and detailed audits and logs. They are ideal for use cases like
air-gapped wallets that are disconnected from the internet, high-level
security standards or assets held in long-term storage.

While secure options for owners, HSMs are useless if the wrong person acquires
control of the device. Multiparty Computation (MPC) technique was developed to
avoid this single point of failure. This cryptographic technique involves
“sharding” private keys into multiple distinct shares (often 2-3 shards) that
are geographically distributed across multiple databases, cloud services or
other storage options. This means that even if one part of a private key is
compromised, the overall key remains unusable.

To add these extra layers of security and peace of mind, an MPC wallet
requires additional computational resources. This performance tax is why most
MPC solutions are limited to 3-4 different shards and better suited for
permissioned use cases, fast or automated access to liquidity, and scenarios
where cost, compliance or technical limitations make HSMs unfeasible.

Some MPC solutions have adopted versions of this approach where the service
provider holds at least one of the key shards. However, this model means that
the bank doesn’t have complete control of their own crypto assets and those of
their clients. Mature regulated entities are ultimately responsible for the
safekeeping of those assets, but are relinquishing part of that control with
these types of solutions. To ensure the utmost safety and security, the
physical storage of key share material should be managed by a single
entity—the institution itself.

### SaaS vs On-Prem Deployments

Beyond wallet types and key protection strategies, custodians must decide
whether to host their custody solution with a provider or on their own
servers.

A Software as a Service (SaaS) implementation is fairly straightforward.
Managed by a third-party provider such as Metaco, they run in the cloud,
allowing for fast deployment and near instant scaling. Like with other SaaS
solutions, they require less up-front cost or ongoing resources. Everything is
stored in the cloud and managed by the third-party, making them deploy-and-
forget solutions that allow providers to focus on their core business
requirements.

Conversely, on-premise (on-prem) custody solutions offer complete control of
all data and processes and are ideal for banks and financial instructions that
have strict risk, compliance or regulatory requirements. In these setups, the
institution designs and provisions the hardware, manages and maintains all
security considerations, and services process and software upgrades for the
life of the system. The trade off for this control is the high up-front cost
to deploy a solution and the ongoing resource requirements to manage it.

While these choices can seem overwhelming, the digital asset use cases for
each provider and their clients will help dictate which combination of wallet,
key security and solution type is best.

Contact the Metaco team to learn more about the technical considerations and
solutions criteria that will inform digital asset custody provider technology
choices.

[1] https://www.pwchk.com/en/press-room/press-releases/pr-110723.html

[2] https://beincrypto.com/learn/air-gapped-wallets/#h-what-are-air-gapped-
wallets

[3] https://cryptoforinnovation.org/what-is-account-abstraction-and-why-is-it-
important/

## Subscribe to future **Metaco insights**

[ Subscribe](https://go.metaco.com/l/1003211/2023-09-22/qzqx "Subscribe")

![](https://www.metaco.com/wp-
content/themes/metaco/assets/images/footer.png?x88149)

[![Metaco](https://www.metaco.com/wp-
content/themes/metaco/assets/images/logo-w.svg?x88149)](https://www.metaco.com)

  * [Solutions](https://www.metaco.com/audiences/)
    * [Global Custodians](https://www.metaco.com/audiences/global-custodians-top-tier-banks/)
    * [Universal Banks](https://www.metaco.com/audiences/universal-banks/)
    * [Neobanks & Fintechs](https://www.metaco.com/audiences/neobanks-fintechs/)
    * [Regulated Exchanges](https://www.metaco.com/audiences/regulated-exchanges/)
    * [Corporates](https://www.metaco.com/audiences/corporates/)
  * [Platform](https://www.metaco.com/platform/)
    * [Harmonize™](https://www.metaco.com/platform/harmonize/)
    * [Custody](https://www.metaco.com/platform/custody/)
    * [Trading](https://www.metaco.com/platform/trading/)
    * [Web3](https://www.metaco.com/platform/web3/)
    * [Governance](https://www.metaco.com/platform/governance/)
    * [Orchestration](https://www.metaco.com/platform/orchestration/)
    * [Tokenization](https://www.metaco.com/platform/tokenization/)
    * [Integration](https://www.metaco.com/platform/integration/)
    * [Security](https://www.metaco.com/platform/security/)
  * [Company](https://www.metaco.com/company/media-coverage-press-releases/)
    * [About](https://www.metaco.com/company/about/)
    * [Media & news](https://www.metaco.com/company/media-coverage-press-releases/)
    * [Jobs](https://www.metaco.com/jobs/)
  * [Resources](https://www.metaco.com/resources/)
    * [Talks](https://www.metaco.com/resources/talks/)
    * [Webinars](https://www.metaco.com/resources/webinars/)
    * [Case studies](https://www.metaco.com/resources/case-studies/)
    * [Reports](https://www.metaco.com/resources/reports/)
    * [Blog](https://www.metaco.com/resources/blog/)

![](https://www.metaco.com/wp-
content/uploads/2022/10/sco2.png?x88149)![](https://www.metaco.com/wp-
content/uploads/2022/10/iso27001.png?x88149)

  * [__](https://www.twitter.com/metaco_sa "Twitter: Follow Metaco \(open in new window\)")
  * [__](https://www.linkedin.com/company/metaco-ag/ "Linkedin: Follow Metaco \(open in new window\)")
  * [__](https://www.youtube.com/channel/UC4MLOKnJD9bXfHVXMnHM7ow "Youtube: Follow Metaco \(open in new window\)")
  * [__](https://open.spotify.com/show/0IiI7iftR3F3RqinfJbpRT "Spotify: Follow Metaco \(open in new window\)")

© 2015-2024 - Metaco SA - All Rights Reserved |[ Terms & Conditions](https://www.metaco.com/terms-conditions/) | [Privacy Policy](https://www.metaco.com/privacy-policy/) | [Cookie policy](https://www.metaco.com/cookie-policy/)

