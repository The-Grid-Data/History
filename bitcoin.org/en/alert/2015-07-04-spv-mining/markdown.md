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

[Network alerts history](/en/alerts) | [ ![rss](/img/icons/header_rss.svg?1716491272) Subscribe to RSS feed](/en/rss/alerts.rss) | [Post history](https://github.com/bitcoin-dot-org/bitcoin.org/commits/master/_alerts/2015-07-04-spv-mining.md) | [Report issue](https://github.com/bitcoin-dot-org/bitcoin.org/issues/new?body=Source%20File%3A%20_alerts/2015-07-04-spv-mining.md%0A%0A)

# Some Miners Generating Invalid Blocks

4 July 2015

ALL TOPICS

  * When Will Things Go Back To Normal?
  * Whatâs Happening
  * Updates
  * Invalid Blocks

_This document is being updated as new information arrives. Last update:
2015-07-15 13:00. All times are UTC._

**Note: this situation has not been fully resolved, and it does not appear
that it will be fully resolved anytime soon. Users of the affected wallets
listed below are still advised to wait additional confirmations or to switch
to a safer wallet.**

##Summary

Your bitcoins are safe if you received them in transactions confirmed before
2015-07-15 12:00 UTC.

However, there has been a problem with a planned upgrade. For bitcoins
received later than the time above, confirmation scores are significantly less
reliable then they usually are for users of certain software:

  * **Lightweight ([SPV](http://bitcoin.stackexchange.com/questions/4649/what-is-an-spv-client)) wallet users** should wait an additional 30 confirmations more than you would normally wait. Electrum users, please see [this note](https://en.bitcoin.it/wiki/July_2015_Forks#Electrum).
  * **Bitcoin Core 0.9.4 or earlier users** should wait an additional 30 confirmations more than you would normally wait or upgrade to [Bitcoin Core 0.10.2](/en/download).
  * **Web wallet users** should wait an additional 30 confirmations more than you would normally wait, unless you know for sure that your wallet is secured by Bitcoin Core 0.9.5 or later.
  * **Bitcoin Core 0.9.5 or later users are unaffected.** (Note: [upgrade to 0.10.2](/en/download) is recommended due to denial-of-service vulnerabilities unrelated to this alert.)

##Miners

If you pool mine, please switch to a pool that properly validates blocks. The
Wiki Mining Pool Comparison page currently contains a list of [known (or
suspected) good and bad
pools](https://en.bitcoin.it/wiki/Comparison_of_mining_pools#SPV_Mining_.2F_Old_Bitcoin_Core).

If you solo mine, please switch to Bitcoin Core 0.10.2.

## When Will Things Go Back To Normal?

The problem is miners creating invalid blocks. Some software can detect that
those blocks are invalid and reject them; other software canât detect that
blocks are invalid, so they show confirmations that arenât real.

  * **Bitcoin Core 0.9.5 and later** never had any problems because it could detect which blocks were invalid.
  * **Bitcoin Core 0.9.4 and earlier** will never provide as much security as later versions of Bitcoin Core because it doesnât know about the additional [BIP66](https://github.com/bitcoin/bips/blob/master/bip-0066.mediawiki) consensus rules. [Upgrade](/en/download) is recommended to return to full node security.
  * **Lightweight (SPV) wallets** are not safe for less than 30 confirmations until all the major pools switch to full validation.
  * **Web wallets** are very diverse in what infrastructure they run and how they handle double spends, so unless you know for sure that they use Bitcoin Core 0.9.5 or later for full validation, you should assume they have the same security as the lightweight wallets described above.

## What's Happening

Summary: Some miners are currently generating invalid blocks. Almost all
software (besides Bitcoin Core 0.9.5 and later) will accept these invalid
blocks under certain conditions.

So far, the following forks of two or more blocks have occurred:

Start date | End time | Blocks [1] | Double Spends  
---|---|---|---  
4 July @ 02:10 | 03:50 | 6 | 0  
5 July @ 21:50 | 23:40 | 3 | Not yet known  
  
The paragraphs that follow explain the cause more throughly.

For several months, an increasing amount of mining hash rate has been
signaling its intent to begin enforcing
[BIP66](https://github.com/bitcoin/bips/blob/master/bip-0066.mediawiki) strict
DER signatures. As part of the BIP66 rules, once 950 of the last 1,000 blocks
were version 3 (v3) blocks, all upgraded miners would reject version 2 (v2)
blocks.

Early morning on 4 July 2015, the 950/1000 (95%) threshold was reached.
Shortly thereafter, a small miner (part of the non-upgraded 5%) mined an
invalid blockâas was an expected occurrence. Unfortunately, it turned out
that roughly half the network hash rate was mining without fully validating
blocks (called SPV mining), and built new blocks on top of that invalid block.

Note that the roughly 50% of the network that was SPV mining had explicitly
indicated that they would enforce the BIP66 rules. By not doing so, several
large miners have lost over $50,000 dollars worth of mining income so far.

All software that assumes blocks are valid (because invalid blocks cost miners
money) is at risk of showing transactions as confirmed when they really
arenât. This particularly affects lightweight (SPV) wallets and software
such as old versions of Bitcoin Core which have been downgraded to SPV-level
security by the new BIP66 consensus rules.

The recommended fix, which was attempted, was to get all miners off of SPV
mining and back to full validation (at least temporarily). If this happens,
Bitcoin.org will reduce its current recommendation of waiting 30 extra
confirmations to a lower number.

## Updates

  1. **6 July 04:00:** A new fork occurred starting 5 July at 21:30 with three blocks before the valid chain again became the strongest chain. See the recently-added list of forks. Reports that the situation has passed are **not correct.** Please continue to wait 30 more confirmations than you usually would wait before accepting a transaction.

## Invalid Blocks

Please see the list of [invalid block
hashes](https://en.bitcoin.it/wiki/July_2015_Forks#Invalid_Block_Hashes) on
the Bitcoin Wiki.

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

