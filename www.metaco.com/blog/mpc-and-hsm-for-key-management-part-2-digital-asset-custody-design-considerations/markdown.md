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

# MPC and HSM for Key Management Part 2: Digital Asset Custody Design
Considerations

  *  __ November 16, 2023
  *  __6 min

Share

  * [ __](https://www.linkedin.com/sharing/share-offsite/?url=https%3A%2F%2Fwww.metaco.com%2Fblog%2Fmpc-and-hsm-for-key-management-part-2-digital-asset-custody-design-considerations%2F)
  * [__](https://twitter.com/intent/tweet?text=Metaco+https%3A%2F%2Fwww.metaco.com%2Fblog%2Fmpc-and-hsm-for-key-management-part-2-digital-asset-custody-design-considerations%2F+via+%40metaco_sa)

Tokenization, not merely as a technological marvel but as a change catalyst,
can dissolve friction of ownership, value, and participation, even from the
world’s most illiquid traditional assets. Beyond cryptocurrencies, digital
assets can represent mutual funds, real estate, carbon credits, art, precious
metals or even fine wine on a blockchain. The applications and implications
are enormous, with Boston Consulting Group predicting tokenized assets will
grow into a $16 trillion business opportunity by 2030[1].

As the number of digital asset use cases grows, sophisticated institutional
investors and enterprises are increasingly seeking trusted custody options to
protect their portfolios, creating an opening for banks and financial
institutions to expand their custody offerings and meet this need[2].

In part one of this series, we examined the types of technologies banks and
financial institutions must evaluate when developing a digital asset custody
solution , including hot or cold wallets, Hardware Security Modules (HSM)
versus Multiparty Computation (MPC), and on-premise (on-prem) or third-party
hosted solutions.

Part two of this series looks at the different considerations that inform the
optimal design and execution of an institutional crypto custody solution.

### Not Your Keys, Not Your Coins

As this popular maxim implies, custodians must design solutions using robust
technologies and governance policies that maximize key protection and
control[3].

Just because a security solution makes it more difficult to take control of
keys does not mean it’s impregnable. Even Multi-party Computation (MPC)
solutions that split the vault or wallet keys into key fractions or “shards”
are vulnerable if hackers can compromise multiple accounts or signatories.

Institutional custodians and regulated entities cannot afford to simply
default to the most widely-adopted solutions. Instead, they must be rigorous
in their evaluation and deploy, maintain and audit a layered digital asset
custody service that incorporates proper storage, access and governance
protocols that fully comply with rigorous risk management and compliance
requirements.

### Accounting for the Human Element

Institutional custody solutions are much more than just technology protections
for crypto assets and their private keys. Custodians and clients must also
jointly develop detailed internal policies and access controls that outline a
framework and control hierarchy that reduces if not eliminates single points
of failure.

A robust policy engine will include strong technology controls, data
encryption, network security, and limits on individual access so that no one
person performs sensitive transactions in isolation or some individuals
collude to do so with malevolent intention. Of course, this vital layer is
also a point of vulnerability, offering hackers that gain access to it a way
to modify the policies and control the flow of funds.

An effective policy engine is one that combines controls, audits and
monitoring to reinforce security at every step of the control and approval
hierarchy.

![](https://www.metaco.com/wp-content/uploads/2023/11/metaco-
blog-04-website-02.jpg?x88149)

### Transaction Throughput and Scalability

When designing a custodial service, financial service institutions must
account for expected transaction throughput and scalability. Each component of
a solution – wallet type, key protection and hosting – has strengths and
weaknesses relative to speed and volume that, in aggregate, can significantly
impact the viability of an intended use case.

For example, HSM solutions can handle up to 10,000 transactions per second
while an MPC wallet is limited to roughly 20 or less transactions per second.
So, while an HSM solution may be slower to access than a MPC wallet, it offers
more room for transaction volumes to scale over time.

Understanding how environments might change is also important when designing
the optimal system. One custody architecture may work well within a limited
pilot or proof of concept, but quickly become obsolete as throughput grows
within a production environment. Designers must have a grasp on the continuum
of client needs to build optimal, future-proofed solutions.

### Cost and Resource Requirements

Each choice within a custody solution comes with different cost and resource
commitments that must be weighed against client needs and use cases.

While a MPC wallet adds extra layers of security and peace of mind, it
requires additional computational resources. Despite this performance tax, it
still retains the edge over HSMs when protecting against single points of
failure, making it more useful in a hot wallet. Of course, that hot wallet
also comes with tradeoffs, providing greater access and enabling faster
transactions but sacrificing some level of security.

Similarly, institutional providers must weigh cost and resource requirements
when choosing a Software-as-a-Service (SaaS) provider versus building an on-
prem solution. The on-prem path comes with much higher up-front costs and
ongoing maintenance and resource requirements relative to a SaaS option, but
it provides a compelling advantage for those providers who need custom setups
or that must maintain complete control.

Ultimately, banks and financial institutions seeking to capitalize on the
fast-growing market for institutional digital asset custody solutions must
consider all these pros and cons at every step in their build. The key to
designing a strong, multi-tiered solution is combining layers of technology
with processes. Institutional crypto custodians that can offer robust, secure
and adaptable solutions are best able to safeguard client assets and therefore
most likely to capture market share over competitors.

Contact the Metaco team to learn more about MPC and HSM for key management
technology.

[MPC and HSM for Key Management Part 1: Demystifying Technology Options for
Digital Asset Custody](https://www.metaco.com/blog/mpc-and-hsm-for-key-
management-part-1-demystifying-technology-options-for-digital-asset-custody/)

[1] https://web-assets.bcg.com/1e/a2/5b5f2b7e42dfad2cb3113a291222/on-chain-
asset-tokenization.pdf

[2] https://www.pwchk.com/en/press-room/press-releases/pr-110723.html

[3] https://www.gfma.org/policies-resources/gfma-publishes-report-on-impact-
of-dlt-in-global-capital-markets/



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

