![Close](/img/icons/ico_close.svg?1716491272)

Bitcoin.org is a community funded project, donations are appreciated and used
to improve the website.

Make a donation

Bitcoin.org needs your support!

Ã

Donate to Bitcoin.org

Use this QR code or address below

[ bc1qx3u4njquj0ux63030r4nat8awqrlm0x2zlt96h
](bitcoin:bc1qx3u4njquj0ux63030r4nat8awqrlm0x2zlt96h)

$5.00

(... BTC)

$25.00

(... BTC)

$50.00

(... BTC)

[![Bitcoin](/img/icons/logotop.svg?1716491272)](/en/)

  * Introduction
    * [Individuals](/en/bitcoin-for-individuals)
    * [Businesses](/en/bitcoin-for-businesses)
    * [Developers](https://developer.bitcoin.org/)
    * [Getting started](/en/getting-started)
    * [How it works](/en/how-it-works)
    * [White paper](/en/bitcoin-paper)
  * Resources
    * [Resources](/en/resources)
    * [Exchanges](/en/exchanges)
    * [Community](/en/community)
    * [Documentation](https://developer.bitcoin.org/)
    * [Vocabulary](/en/vocabulary)
    * [Events](/en/events)
    * [Bitcoin Core](/en/bitcoin-core/)
  * [Innovation](/en/innovation)
  * Participate
    * [Support Bitcoin](/en/support-bitcoin)
    * [Buy Bitcoin](/en/buy)
    * [Running a full node](/en/full-node)
    * [Development](/en/development)
  * [FAQ](/en/faq)

  * English
    *       * [Bahasa Indonesia](/id/)
      * [CatalÃ ](/ca/)
      * [Dansk](/da/)
      * [Deutsch](/de/)
      * [English](/en/)
      * [EspaÃ±ol](/es/)
      * [FranÃ§ais](/fr/)
      * [Italiano](/it/)
      * [Magyar](/hu/)
      * [Nederlands](/nl/)
      * [Polski](/pl/)
      * [PortuguÃªs Brasil](/pt_BR/)
      * [RomÃ¢nÄ](/ro/)
      * [SlovenÅ¡Äina](/sl/)
      * [Srpski](/sr/)
      * [Svenska](/sv/)
    *       * [TÃ¼rkÃ§e](/tr/)
      * [ÎÎ»Î»Î·Î½Î¹ÎºÎ¬](/el/)
      * [Ð±ÑÐ»Ð³Ð°ÑÑÐºÐ¸](/bg/)
      * [Ð ÑÑÑÐºÐ¸Ð¹](/ru/)
      * [Ð£ÐºÑÐ°ÑÐ½ÑÑÐºÐ°](/uk/)
      * [ÕÕ¡ÕµÕ¥ÖÕ¥Õ¶](/hy/)
      * [Ø§ÙØ¹Ø±Ø¨ÙØ©](/ar/)
      * [ÙØ§Ø±Ø³Û](/fa/)
      * [×¢××¨××ª](/he/)
      * [à¤¹à¤¿à¤¨à¥à¤¦à¥](/hi/)
      * [íêµ­ì´](/ko/)
      * [ááááá](/km/)
      * [æ¥æ¬èª](/ja/)
      * [ç®ä½ä¸­æ](/zh_CN/)
      * [ç¹é«ä¸­æ](/zh_TW/)

Bahasa Indonesia CatalÃ  Dansk Deutsch English EspaÃ±ol FranÃ§ais Italiano
Magyar Nederlands Polski PortuguÃªs Brasil RomÃ¢nÄ SlovenÅ¡Äina Srpski
Svenska TÃ¼rkÃ§e ÎÎ»Î»Î·Î½Î¹ÎºÎ¬ Ð±ÑÐ»Ð³Ð°ÑÑÐºÐ¸ Ð ÑÑÑÐºÐ¸Ð¹
Ð£ÐºÑÐ°ÑÐ½ÑÑÐºÐ° ÕÕ¡ÕµÕ¥ÖÕ¥Õ¶ Ø§ÙØ¹Ø±Ø¨ÙØ© ÙØ§Ø±Ø³Û ×¢××¨××ª
à¤¹à¤¿à¤¨à¥à¤¦à¥ íêµ­ì´ ááááá æ¥æ¬èª ç®ä½ä¸­æ
ç¹é«ä¸­æ Language: en

[Blog home](/en/blog) | [Subscribe to RSS feed](/en/rss/blog.xml) | [Post history](https://github.com/bitcoin-dot-org/bitcoin.org/commits/master/_posts/2017-06-17-bitcoin-core-0-14-2-released.md) | [Report issue](https://github.com/bitcoin-dot-org/bitcoin.org/issues/new?body=Source%20File%3A%20_posts/2017-06-17-bitcoin-core-0-14-2-released.md%0A%0A)

# Bitcoin Core Version 0.14.2 Released

ALL TOPICS

  * Compatibility
  * Notable changes
    * miniupnp CVE-2017-8798
  * Known Bugs
  * 0.14.2 Change log
    * RPC and other APIs
    * P2P protocol and network code
    * Build system
    * Miscellaneous
    * GUI
    * Wallet
  * Credits

![Bitcoin Core Version 0.14.2](/img/blog/free/bitcoin-
core-0142.png?1716491272)

[Bitcoin Core version 0.14.2 is now
available](https://bitcoin.org/en/download).

This is a new minor version release, including various bugfixes and
performance improvements, as well as updated translations.

Please report bugs using the [issue tracker on
GitHub](https://github.com/bitcoin/bitcoin/issues).

[Subscribe here](https://bitcoincore.org/en/list/announcements/join/) to
receive security and update notifications.

## Compatibility

Bitcoin Core is extensively tested on multiple operating systems using the
Linux kernel, macOS 10.8+, and Windows Vista and later.

Microsoft ended support for Windows XP on [April 8th,
2014](https://www.microsoft.com/en-us/WindowsForBusiness/end-of-xp-support),
No attempt is made to prevent installing or running the software on Windows
XP, you can still do so at your own risk but be aware that there are known
instabilities and issues. Please do not report issues about Windows XP to the
[issue tracker](https://github.com/bitcoin/bitcoin/issues).

Bitcoin Core should also work on most other Unix-like systems but is not
frequently tested on them.

## Notable changes

### miniupnp CVE-2017-8798

Bundled miniupnpc was updated to 2.0.20170509. This fixes an integer
signedness error (present in MiniUPnPc v1.4.20101221 through v2.0) that allows
remote attackers (within the LAN) to cause a denial of service or possibly
have unspecified other impact.

This only affects users that have explicitly enabled UPnP through the GUI
setting or through the `-upnp` option, as since the last UPnP vulnerability
(in Bitcoin Core 0.10.3) it has been disabled by default.

If you use this option, it is recommended to upgrade to this version as soon
as possible.

## Known Bugs

Since 0.14.0 the approximate transaction fee shown in Bitcoin-Qt when using
coin control and smart fee estimation does not reflect any change in target
from the smart fee slider. It will only present an approximate fee calculated
using the default target. The fee calculated using the correct target is still
applied to the transaction and shown in the final send confirmation dialog.

## 0.14.2 Change log

Detailed release notes follow. This overview includes changes that affect
behavior, not code moves, refactors and string updates. For convenience in
locating the code changes and accompanying discussion, both the pull request
and git merge commit are mentioned.

### RPC and other APIs

  * #10410 `321419b` Fix importwallet edge case rescan bug (ryanofsky)

### P2P protocol and network code

  * #10424 `37a8fc5` Populate services in GetLocalAddress (morcos)
  * #10441 `9e3ad50` Only enforce expected services for half of outgoing connections (theuni)

### Build system

  * #10414 `ffb0c4b` miniupnpc 2.0.20170509 (fanquake)
  * #10228 `ae479bc` Regenerate bitcoin-config.h as necessary (theuni)

### Miscellaneous

  * #10245 `44a17f2` Minor fix in build documentation for FreeBSD 11 (shigeya)
  * #10215 `0aee4a1` Check interruptNet during dnsseed lookups (TheBlueMatt)

### GUI

  * #10231 `1e936d7` Reduce a significant cs_main lock freeze (jonasschnelli)

### Wallet

  * #10294 `1847642` Unset change position when there is no change (instagibbs)

## Credits

Thanks to everyone who directly contributed to this release:

  * Alex Morcos
  * Cory Fields
  * fanquake
  * Gregory Sanders
  * Jonas Schnelli
  * Matt Corallo
  * Russell Yanofsky
  * Shigeya Suzuki
  * Wladimir J. van der Laan

As well as everyone that helped translating on
[Transifex](https://www.transifex.com/projects/p/bitcoin/).

Posted to the [Bitcoin.org Site Blog](/en/blog) on 17 June 2017 by [Will
Binns](https://github.com/wbnns)

[ ![Bitcoin](/img/icons/logo-footer.svg?1716491272) ](/en/)

Support Bitcoin.org: Donate

[bc1qx3u4njquj0ux63030r4nat8awqrlm0x2zlt96h](bitcoin:bc1qx3u4njquj0ux63030r4nat8awqrlm0x2zlt96h)

Introduction:

  * [Individuals](/en/bitcoin-for-individuals)
  * [Businesses](/en/bitcoin-for-businesses)
  * [Developers](https://developer.bitcoin.org/)
  * [Getting started](/en/getting-started)
  * [How it works](/en/how-it-works)
  * [You need to know](/en/you-need-to-know)
  * [White paper](/en/bitcoin-paper)

Resources:

  * [Resources](/en/resources)
  * [Exchanges](/en/exchanges)
  * [Community](/en/community)
  * [Vocabulary ](/en/vocabulary)
  * [Events](/en/events)
  * [Bitcoin Core](/en/bitcoin-core/)

Participate:

  * [Support Bitcoin](/en/support-bitcoin)
  * [Buy Bitcoin](/en/buy)
  * [Running a full node](/en/full-node)
  * [Development](/en/development)

Other:

[Avoid Scams](/en/scams) [Legal](/en/legal) [Privacy Policy](/en/privacy)
[Press](/en/press) [About bitcoin.org](/en/about-us) [Blog](/en/blog)

Â© Bitcoin Project 2009-2024 Released under the [MIT
license](http://opensource.org/licenses/mit-license.php)

[Network Status](/en/alerts)

  * English
    *       * [Bahasa Indonesia](/id/)
      * [CatalÃ ](/ca/)
      * [Dansk](/da/)
      * [Deutsch](/de/)
      * [English](/en/)
      * [EspaÃ±ol](/es/)
      * [FranÃ§ais](/fr/)
      * [Italiano](/it/)
      * [Magyar](/hu/)
      * [Nederlands](/nl/)
      * [Polski](/pl/)
      * [PortuguÃªs Brasil](/pt_BR/)
      * [RomÃ¢nÄ](/ro/)
      * [SlovenÅ¡Äina](/sl/)
      * [Srpski](/sr/)
      * [Svenska](/sv/)
    *       * [TÃ¼rkÃ§e](/tr/)
      * [ÎÎ»Î»Î·Î½Î¹ÎºÎ¬](/el/)
      * [Ð±ÑÐ»Ð³Ð°ÑÑÐºÐ¸](/bg/)
      * [Ð ÑÑÑÐºÐ¸Ð¹](/ru/)
      * [Ð£ÐºÑÐ°ÑÐ½ÑÑÐºÐ°](/uk/)
      * [ÕÕ¡ÕµÕ¥ÖÕ¥Õ¶](/hy/)
      * [Ø§ÙØ¹Ø±Ø¨ÙØ©](/ar/)
      * [ÙØ§Ø±Ø³Û](/fa/)
      * [×¢××¨××ª](/he/)
      * [à¤¹à¤¿à¤¨à¥à¤¦à¥](/hi/)
      * [íêµ­ì´](/ko/)
      * [ááááá](/km/)
      * [æ¥æ¬èª](/ja/)
      * [ç®ä½ä¸­æ](/zh_CN/)
      * [ç¹é«ä¸­æ](/zh_TW/)

Bahasa Indonesia CatalÃ  Dansk Deutsch English EspaÃ±ol FranÃ§ais Italiano
Magyar Nederlands Polski PortuguÃªs Brasil RomÃ¢nÄ SlovenÅ¡Äina Srpski
Svenska TÃ¼rkÃ§e ÎÎ»Î»Î·Î½Î¹ÎºÎ¬ Ð±ÑÐ»Ð³Ð°ÑÑÐºÐ¸ Ð ÑÑÑÐºÐ¸Ð¹
Ð£ÐºÑÐ°ÑÐ½ÑÑÐºÐ° ÕÕ¡ÕµÕ¥ÖÕ¥Õ¶ Ø§ÙØ¹Ø±Ø¨ÙØ© ÙØ§Ø±Ø³Û ×¢××¨××ª
à¤¹à¤¿à¤¨à¥à¤¦à¥ íêµ­ì´ ááááá æ¥æ¬èª ç®ä½ä¸­æ
ç¹é«ä¸­æ en

