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

[Blog](https://www.ledger.com/blog-cargo-checkct-our-home-made-tool-guarding-
against-timing-attacks-is-now-open-source) __[Blog
posts](https://www.ledger.com/category/blog-posts "Blog posts")

[Blog posts](https://www.ledger.com/category/blog-posts "Blog posts"), [Donjon](https://www.ledger.com/category/donjon "Donjon") | 05/17/2024 

# Cargo-checkct: our home-made tool guarding against timing attacks is now
open-source!

The Ledger Donjon team is thrilled to present cargo-checkct, our in-house tool
designed to defend against timing attacks.

[Blog](https://www.ledger.com/blog-cargo-checkct-our-home-made-tool-guarding-
against-timing-attacks-is-now-open-source) __[Blog
posts](https://www.ledger.com/category/blog-posts "Blog posts")

The Ledger Donjon team is thrilled to present**[cargo-
checkct](https://github.com/Ledger-Donjon/cargo-checkct)**, our in-house open-
source tool designed to defend against timing attacks. In this article, we’ll
delve into the concept of timing attacks, explore why timing vulnerabilities
in cryptography libraries are so hard to detect, and explain the role of
cargo-checkct in addressing these challenges.

##### Timing attacks

Side-channel vulnerabilities, and timing vulnerabilities in particular, may
allow an attacker to extract secret data – be it authentication data like PINs
or passwords, or secret keys used in cryptographic operations – from an
otherwise secure system. **The exploitation of such vulnerabilities** can seem
a bit esoteric or theoretical at first, but it is important to realize that
they in fact very much **lead to practical, and devastating, real-world
attacks**1. This is particularly dire for embedded systems, that an attacker
can manipulate and instrument to better observe leakage more easily than could
be done for a remote system.

In fact the principle underpinning timing attacks is, at its core, extremely
simple, once you wrap your head around it: **if a secret-manipulating programs
runs faster for some values of the secret than for some other values, then as
an attacker, measuring that program’s execution time directly gives me
information about the secret!** Not all such leakages are created equal, of
course, and some vulnerabilities might only allow to recover some bits of the
secret – yet just as often, timing leaks can be exploited to entirely recover
the secret in only a few rounds of measuring the target program’s execution.

Upon realizing that this is a serious threat, and not merely a theoretical
issue, the next step is to look for constructs introducing timing differences
in secret-manipulating code, so as to be able to avoid using them. Perhaps the
most obvious way in which a program’s execution time can vary depending on the
value of the manipulated secret, is if the program includes conditional
branches dependent on the secret, as is for instance very tempting when
implementing a PIN comparison function, which could look something like this:

    
    
    pub fn verify_pin(candidate_pin_to_verify: &[u8; PIN_LEN], actual_valid_secret_pin: &[u8; PIN_LEN]) -> bool {
        for (l, r) in candidate_pin_to_verify
            .iter()
            .zip(actual_valid_secret_pin.iter())
        {
            if l != r {
                return false;
            }
        }
    
        true
    }

There is another very important class of timing leakages however, that is way
less obvious at first sight, and is linked to the presence of
microarchitectural intermediates between a processor core and memory:
**caches**. The purpose of caches is of course to speed up loads and stores
from and to memory, by, well, caching recently used data. But if attacker-
controlled programs are allowed to run concurrently (or in parallel, if at
least one layer of caching is shared between several cores) with our otherwise
isolated secret-manipulating program, then the attacker code’s timing will
become dependent on the memory addresses accessed by our program, and vice-
versa, thereby creating an observable timing channel leaking information about
the manipulated secrets! Thus any secret-manipulating program running on a
target with caches should be very careful never to access memory at secret-
dependent addresses.

Those problems, and the attacks they enable, have been widely known for three
decades now, yet they
[still](https://hg.mozilla.org/projects/nss/rev/b090a1e5dcdfc5772671063cfe9ebeadabd29ad3)
plague modern day, widely used implementations. Interestingly enough, the
situation is in many ways akin to that of memory corruption, with [phrack’s
article on stack smashing](http://phrack.org/issues/49/14.html) being
published the exact same year as Kocher’s [seminal paper on timing
attacks](https://paulkocher.com/doc/TimingAttacks.pdf). Both kinds of
vulnerabilities have since evolved far beyond the boundaries of their original
expositions of course, with ROP, JOP and heap exploitation on the one hand,
and cache related side-channels on the other (not to mention speculative
execution). But, crucially, both kinds of vulnerabilities are still commonly
found in computer systems that we very much rely upon for safety and privacy.

A lot of work has of course gone into tackling the menace of memory corruption
bugs, from the development of mitigations and the rise of fuzzing as a
somewhat common tool to use, to the always wider adoption of memory-safe
languages. The same is true for side-channel vulnerabilities in cryptography
libraries and embedded systems, with, in particular, the development of [many
tools](https://arxiv.org/pdf/2310.08153.pdf) to detect, or even soundly rule
out, timings vulnerabilities. **And yet, none of these tools have really seen
wide adoption by cryptography libraries developers.**

##### The (cryptographic) constant-time policy

If you think about it, there are two conceptually simple ways to tackle the
problem of verifying that an implementation does not leak secrets via timing
channels. The simplest one would certainly be to run the code many times with
different secret data, and measure its timing, so that any statistically
significant variation can be interpreted as the tell-tale sign of the presence
of a timing vulnerability. There are at least two problems with this approach,
though, that severely limit its applicability:

  * First of all, while such a measured timing is a good proxy for control-flow based leaks, it is not very clear how to simulate the influences an attacker could have on the state of the caches while the program is running. 
  * But even then, execution timing depends both on the machine code that gets generated by the compiler, and on the microarchitectural details of the actual hardware implementation, so that strictly speaking, measurement campaigns would have to be run for every specific targeted SoC, which would effectively shift the verification burden to the downstream users of cryptography libraries.

The other general approach one could take is to directly verify that the code
does not take control-flow decision based on secret data, nor accesses memory
at secret-dependent addresses, as we have previously identified those two
patterns as the sources of timing leaks (this is called the (cryptographic)
constant-time policy in the literature). How hard can it be? Well, it turns
out that, while this is certainly doable, a very annoying problem is that
general-purpose compilers (think GCC, Clang/LLVM) do not preserve those two
properties while compiling programs down to machine code! And not only do they
not preserve it in theory, but they do not preserve it in practice too,
regularly wreaking havoc in cryptography libraries2. Fortunately, some ways of
writing things have been found that most often (and currently) prevent the
compiler from introducing timing leaks, as used for instance in the [subtle
crate](https://crates.io/crates/subtle) – but there is really no guarantee.

So, realistically, the only sound and portable (from one implementation of an
ISA to another) way to go about verifying constant-timedness of cryptography
libraries would be to verify that the constant-time policy is respected at the
machine code level. This is not an easy thing to do, yet amazingly, this is
exactly what the `checkct` plugin of
[Binsec](https://github.com/binsec/binsec) allows one to do! It does so using
(an elaborate version of) symbolic execution, and is perfectly sound, under
the assumption that instructions themselves execute in time independent from
their operands3.

##### Where does cargo-checkt comes into the picture

Binsec is great, yet cryptography libraries developers and maintainers still
do not have a simple, clear way to monitor the timing behavior of their code
in CI, although helpful tools do exist, like [dudect-
bencher](https://crates.io/crates/dudect-bencher). One of the main
difficulties is that verifying cryptographic libraries requires writing a
verification driver or harness, that builds inputs to the function under test,
before calling the latter, much like fuzzing. This is less than ideal, as it
adds up to the cost of writing and maintaining cryptographic code. But it can
be done, and can be made easier with some relatively simple tooling
streamlining the process.

We have developed [**cargo-checkct**](https://github.com/Ledger-Donjon/cargo-
checkct) with this exact goal in mind, aiming to make it easy to verify
constant-timedness of Rust cryptography libraries using `binsec`, and with the
hope of bringing the benefits of the latest research to the greatest number.
**With`cargo-checkct` you can generate all the boiler-plate part of the
verification driver, and automatically generate an appropriate `binsec` script
to run the actual verification, in the matter of a couple command line
calls.**

As every tool of course, `cargo-checkct` comes with a number of limitations,
some inherited from `binsec`, and some its very own, yet as the examples
provided in the repository aim to show, it does enable the verification of
cryptography libraries from [dalek-cryptography](https://github.com/dalek-
cryptography) or [RustCrypto](https://github.com/RustCrypto), and many more.
We are thus very excited to open-source it, with the hope that it can
contribute to the overall improvement of the security of cryptography at
large, and make a concrete dent into the problem of ruling out timing leaks in
practice.

The repository (<https://github.com/Ledger-Donjon/cargo-checkct>) is the best
place to look if you are interested in more details and examples, but just to
give you a taste of what using `cargo-checkct` looks like, let’s quickly take
the [x25519-dalek](https://crates.io/crates/x25519-dalek) crate as example.
Verifying that the provided Diffie-Hellman implementation is constant-time on
both `thumb` and `riscv` targets is a mere matter of running `cargo-checkct
init`, implementing a simple harness:

    
    
    pub fn checkct() {
        use dalek::{PublicKey, EphemeralSecret, SharedSecret};
        let mut public_key_bytes = [0u8; 32];
        PublicRng.fill_bytes(&mut public_key_bytes);
    
        let public = PublicKey::from(public_key_bytes);
        let ephemeral = EphemeralSecret::random_from_rng(PrivateRng);
        let shared_secret = ephemeral.diffie_hellman(&public);
        core::hint::black_box(shared_secret);
    }

and finally running `cargo-checkct run`, which in addition to tunneling back
some of `binsec` detailed output, crucially outputs (in this instance, and as
of this writing) a reassuring `SECURE` status.

##### TL;DR

All cryptography libraries should consistently produce constant-time machine
code on all architectures they target, under risk of complete breakage. Alas
this is extremely hard to ensure in CI, allowing severe vulnerabilities to
regularly surface in critical code. `cargo-checkct` is here to solve this
issue, focusing in particular on `no_std`-capable Rust libraries. [Try it
out](https://github.com/Ledger-Donjon/cargo-checkct)!

* * *

Charles CHRISTEN  
Security Engineer – Ledger Donjon

  1. See for instance [cachebleed](https://faculty.cc.gatech.edu/~genkin/cachebleed/index.html) for a relatively recent demonstrated attack on OpenSSL. ↩︎
  2. This happened quite recently in `secp256k1` for instance, see [https://github.com/bitcoin-core/secp256k1/blob/master/CHANGELOG.md#032—2023-05-13](https://github.com/bitcoin-core/secp256k1/blob/master/CHANGELOG.md#032---2023-05-13). ↩︎
  3. This can happen both at the lower end, for multiplications and divisions on very small microcontrollers, and at the higher end, as exemplified by the necessary introduction of the [DIT bit in Armv8.4-A](https://developer.arm.com/documentation/ka005181/latest/).  ↩︎

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

## Your Cookies preferences !

We use cookies to analyse the traffic on our site, enhance your experience and
deliver marketing contents that are relevant to your interests. Please note
that you can change your cookie settings and withdraw your consent at any time
from our[Cookie Policy](https://shop.ledger.com/pages/cookie-policy)

Reject All Accept All

Cookies Settings

![Ledger Logo](https://cdn.cookielaw.org/logos/df21fb3f-71b8-491b-89ee-
eb777bcaf866/56e0a676-5d93-4a14-bfc7-7a2d75f2b993/15ffac82-5822-4def-b3b3-a595598861a2/White_64.png)

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
[More information](https://shop.ledger.com/pages/cookie-policy)

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

