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

[Network alerts history](/en/alerts) | [ ![rss](/img/icons/header_rss.svg?1716491272) Subscribe to RSS feed](/en/rss/alerts.rss) | [Post history](https://github.com/bitcoin-dot-org/bitcoin.org/commits/master/_alerts/2013-03-15-upgrade-deadline.html) | [Report issue](https://github.com/bitcoin-dot-org/bitcoin.org/issues/new?body=Source%20File%3A%20_alerts/2013-03-15-upgrade-deadline.html%0A%0A)

# 15 May 2013 Upgrade Deadline

15 March 2013

ALL TOPICS

  * What is happening
  * If you cannot upgrade to version 0.8.1
  * If you cannot upgrade to a backport
  * Miners/mining pool operators
  * Why this is necessary

## What is happening

If you are using an old version of Bitcoin-Qt (or bitcoind, the server bitcoin
software), you must either upgrade to version 0.8.0 or later before May 15,
2013, upgrade to an up-to-date "backport" release, or modify a file and
restart bitcoin to work around a bug with the old software.

This bug does not affect any bitcoins you already have, but if you do nothing
you will be out of sync with the rest of the Bitcoin network and will be
unable to receive bitcoins (payments sent to you will look like they never get
confirmed, or will be confirmed very slowly). You also risk being the victim
of a "double-spend" attack, where somebody sends you bitcoins that the rest of
the network would reject as invalid.

We recommend that you [upgrade to version
0.8.1](http://sourceforge.net/projects/bitcoin/files/Bitcoin/bitcoin-0.8.1/)
before the 15th of May to avoid any issues. If you are a solo miner or mining
pool operator, please see the the notes at the end of this page for how to
upgrade safely.

## If you cannot upgrade to version 0.8.1

If you cannot upgrade to the latest version, [backports to older branches are
now in final testing](https://bitcointalk.org/?topic=199699). These include
not only compatibility for the 15 May changes, but also fixes for known
vulnerabilities and bugs, which have already been included and tested in the
latest release.

## If you cannot upgrade to a backport

If you cannot upgrade to any of the above, you can still avoid the problem.
Create a file called DB_CONFIG in the bitcoin data directory, containing this
line:

>
>     set_lk_max_locks 537000
>  

[Look here](https://en.bitcoin.it/wiki/Data_directory) if you need help
finding the bitcoin data directory.

## Miners/mining pool operators

If you are creating new blocks (you are a solo miner or mining pool operator),
then you should be aware that upgrading from 0.7 to 0.8 requires a lengthy re-
indexing operation; you **must** wait for the reindex to complete before
serving work to miners.

And if you are creating blocks and cannot upgrade to version 0.8.1 or a
backport for some reason, you should **not** set_lk_max_locks in a DB_CONFIG
file until May 15th; if you increase locks before then you run the risk of
creating or building on blocks incompatible with the rest of the network.

## Why this is necessary

A bug caused a [temporary block chain fork on 11 March, 2013](/chainfork).
After investigating that bug, we determined that the bug can happen even if
the entire network was still running old versions of Bitcoin-Qt/bitcoind.
Therefore, the only option is to require everybody to either upgrade or
workaround the bug.

_This notice last updated: Fri, 10 May 2013 21:30:00 UTC_

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

