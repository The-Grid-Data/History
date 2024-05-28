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

[Blog home](/en/blog) | [Subscribe to RSS feed](/en/rss/blog.xml) | [Post history](https://github.com/bitcoin-dot-org/bitcoin.org/commits/master/_posts/2017-04-22-bitcoin-core-0-14-1-released.md) | [Report issue](https://github.com/bitcoin-dot-org/bitcoin.org/issues/new?body=Source%20File%3A%20_posts/2017-04-22-bitcoin-core-0-14-1-released.md%0A%0A)

# Bitcoin Core Version 0.14.1 Released

ALL TOPICS

  * Compatibility
  * Notable changes
    * RPC changes
    * Mining
    * UTXO memory accounting
  * 0.14.1 Change log
    * RPC and other APIs
    * Block and transaction handling
    * P2P protocol and network code
    * Build system
    * GUI
    * Mining
    * Tests and QA
    * Miscellaneous
  * Credits

![Bitcoin Core Version 0.14.1](/img/blog/free/bitcoin-
core-0141.png?1716491272)

[Bitcoin Core version 0.14.1 is now
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

### RPC changes

  * The first positional argument of `createrawtransaction` was renamed from `transactions` to `inputs`.
  * The argument of `disconnectnode` was renamed from `node` to `address`.

These interface changes break compatibility with 0.14.0, when the named
arguments functionality, introduced in 0.14.0, is used. Client software using
these calls with named arguments needs to be updated.

### Mining

In previous versions, getblocktemplate required segwit support from downstream
clients/miners once the feature activated on the network. In this version, it
now supports non-segwit clients even after activation, by removing all segwit
transactions from the returned block template. This allows non-segwit miners
to continue functioning correctly even after segwit has activated.

Due to the limitations in previous versions, getblocktemplate also recommended
non-segwit clients to not signal for the segwit version-bit. Since this is no
longer an issue, getblocktemplate now always recommends signalling segwit for
all miners. This is safe because ability to enforce the rule is the only
required criteria for safe activation, not actually producing segwit-enabled
blocks.

### UTXO memory accounting

Memory usage for the UTXO cache is being calculated more accurately, so that
the configured limit (`-dbcache`) will be respected when memory usage peaks
during cache flushes. The memory accounting in prior releases is estimated to
only account for half the actual peak utilization.

The default `-dbcache` has also been changed in this release to 450MiB. Users
who currently set `-dbcache` to a high value (e.g. to keep the UTXO more fully
cached in memory) should consider increasing this setting in order to achieve
the same cache performance as prior releases. Users on low-memory systems
(such as systems with 1GB or less) should consider specifying a lower value
for this parameter.

Additional information relating to running on low-memory systems can be found
here: [reducing-bitcoind-memory-
usage.md](https://gist.github.com/laanwj/efe29c7661ce9b6620a7).

## 0.14.1 Change log

Detailed release notes follow. This overview includes changes that affect
behavior, not code moves, refactors and string updates. For convenience in
locating the code changes and accompanying discussion, both the pull request
and git merge commit are mentioned.

### RPC and other APIs

  * #10084 `142fbb2` Rename first named arg of createrawtransaction (MarcoFalke)
  * #10139 `f15268d` Remove auth cookie on shutdown (practicalswift)
  * #10146 `2fea10a` Better error handling for submitblock (rawodb, gmaxwell)
  * #10144 `d947afc` Prioritisetransaction wasnât always updating ancestor fee (sdaftuar)
  * #10204 `3c79602` Rename disconnectnode argument (jnewbery)

### Block and transaction handling

  * #10126 `0b5e162` Compensate for memory peak at flush time (sipa)
  * #9912 `fc3d7db` Optimize GetWitnessHash() for non-segwit transactions (sdaftuar)
  * #10133 `ab864d3` Clean up calculations of pcoinsTip memory usage (morcos)

### P2P protocol and network code

  * #9953/#10013 `d2548a4` Fix shutdown hang with >= 8 -addnodes set (TheBlueMatt)
  * #10176 `30fa231` net: gracefully handle NodeId wrapping (theuni)

### Build system

  * #9973 `e9611d1` depends: fix zlib build on osx (theuni)

### GUI

  * #10060 `ddc2dd1` Ensure an item exists on the rpcconsole stack before adding (achow101)

### Mining

  * #9955/#10006 `569596c` Donât require segwit in getblocktemplate for segwit signalling or mining (sdaftuar)
  * #9959/#10127 `b5c3440` Prevent slowdown in CreateNewBlock on large mempools (sdaftuar)

### Tests and QA

  * #10157 `55f641c` Fix the `mempool_packages.py` test (sdaftuar)

### Miscellaneous

  * #10037 `4d8e660` Trivial: Fix typo in help getrawtransaction RPC (keystrike)
  * #10120 `e4c9a90` util: Work around (virtual) memory exhaustion on 32-bit w/ glibc (laanwj)
  * #10130 `ecc5232` bitcoin-tx input verification (awemany, jnewbery)

## Credits

Thanks to everyone who directly contributed to this release:

  * Alex Morcos
  * Andrew Chow
  * Awemany
  * Cory Fields
  * Gregory Maxwell
  * James Evans
  * John Newbery
  * MarcoFalke
  * Matt Corallo
  * Pieter Wuille
  * practicalswift
  * rawodb
  * Suhas Daftuar
  * Wladimir J. van der Laan

As well as everyone that helped translating on
[Transifex](https://www.transifex.com/projects/p/bitcoin/).

Posted to the [Bitcoin.org Site Blog](/en/blog) on 22 April 2017 by [Will
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

