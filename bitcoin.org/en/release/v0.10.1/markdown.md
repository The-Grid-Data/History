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

[![Bitcoin](/img/bitcoin-core/bitcoin-core.svg?1716491272)](/en/bitcoin-core/)

  * Features
    * [Overview](/en/bitcoin-core/features/)
    * [Validation](/en/bitcoin-core/features/validation)
    * [Privacy](/en/bitcoin-core/features/privacy)
    * [Requirements](/en/bitcoin-core/features/requirements)
    * [User Interface](/en/bitcoin-core/features/user-interface)
    * [Network Support](/en/bitcoin-core/features/network-support)
  * [Get Help](/en/bitcoin-core/help)
  * Contribute
    * [Bug reports](/en/bitcoin-core/contribute/issues)
    * [Code](/en/development)
    * [Documentation](/en/bitcoin-core/contribute/documentation)
    * [Translations](/en/bitcoin-core/contribute/translations)
    * [Tech Support](/en/bitcoin-core/contribute/support)
  * [News](/en/version-history)
  * [Download](/en/download)

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

[Bitcoin](/en/) > [Core](/en/bitcoin-core/) > [News](/en/version-history) >
0.10.1

# Bitcoin Core version 0.10.1 released

27 April 2015

ALL TOPICS

  * Upgrading and downgrading
    * How to Upgrade
    * Downgrade warning
  * Notable changes
  * 0.10.1 Change log
  * Credits

Bitcoin Core version 0.10.1 is now available from:

<https://bitcoin.org/bin/bitcoin-core-0.10.1/>

This is a new minor version release, bringing bug fixes and translation
updates. If you are using 0.10.0, it is recommended to upgrade to this
version.

Please report bugs using the issue tracker at github:

<https://github.com/bitcoin/bitcoin/issues>

# Upgrading and downgrading

## How to Upgrade

If you are running an older version, shut it down. Wait until it has
completely shut down (which might take a few minutes for older versions), then
run the installer (on Windows) or just copy over /Applications/Bitcoin-Qt (on
Mac) or bitcoind/bitcoin-qt (on Linux).

## Downgrade warning

Because release 0.10.0 and later makes use of headers-first synchronization
and parallel block download (see further), the block files and databases are
not backwards-compatible with pre-0.10 versions of Bitcoin Core or other
software:

  * Blocks will be stored on disk out of order (in the order they are received, really), which makes it incompatible with some tools or other programs. Reindexing using earlier versions will also not work anymore as a result of this.

  * The block index database will now hold headers for which no block is stored on disk, which earlier versions wonât support.

If you want to be able to downgrade smoothly, make a backup of your entire
data directory. Without this your node will need start syncing (or importing
from bootstrap.dat) anew afterwards. It is possible that the data from a
completely synchronised 0.10 node may be usable in older versions as-is, but
this is not supported and may break as soon as the older version attempts to
reindex.

This does not affect wallet forward or backward compatibility.

# Notable changes

This is a minor release and hence there are no notable changes. For the
notable changes in 0.10, refer to the release notes for the 0.10.0 release at
<https://github.com/bitcoin/bitcoin/blob/v0.10.0/doc/release-notes.md>

# 0.10.1 Change log

Detailed release notes follow. This overview includes changes that affect
external behavior, not code moves, refactors or string updates.

RPC:

  * [`7f502be`](https://github.com/bitcoin/bitcoin/commit/7f502be) fix crash: createmultisig and addmultisigaddress
  * [`eae305f`](https://github.com/bitcoin/bitcoin/commit/eae305f) Fix missing lock in submitblock

Block (database) and transaction handling:

  * [`1d2cdd2`](https://github.com/bitcoin/bitcoin/commit/1d2cdd2) Fix InvalidateBlock to add chainActive.Tip to setBlockIndexCandidates
  * [`c91c660`](https://github.com/bitcoin/bitcoin/commit/c91c660) fix InvalidateBlock to repopulate setBlockIndexCandidates
  * [`002c8a2`](https://github.com/bitcoin/bitcoin/commit/002c8a2) fix possible block db breakage during re-index
  * [`a1f425b`](https://github.com/bitcoin/bitcoin/commit/a1f425b) Add (optional) consistency check for the block chain data structures
  * [`1c62e84`](https://github.com/bitcoin/bitcoin/commit/1c62e84) Keep mempool consistent during block-reorgs
  * [`57d1f46`](https://github.com/bitcoin/bitcoin/commit/57d1f46) Fix CheckBlockIndex for reindex
  * [`bac6fca`](https://github.com/bitcoin/bitcoin/commit/bac6fca) Set nSequenceId when a block is fully linked

P2P protocol and network code:

  * [`78f64ef`](https://github.com/bitcoin/bitcoin/commit/78f64ef) donât trickle for whitelisted nodes
  * [`ca301bf`](https://github.com/bitcoin/bitcoin/commit/ca301bf) Reduce fingerprinting through timestamps in âaddrâ messages.
  * [`200f293`](https://github.com/bitcoin/bitcoin/commit/200f293) Ignore getaddr messages on Outbound connections.
  * [`d5d8998`](https://github.com/bitcoin/bitcoin/commit/d5d8998) Limit message sizes before transfer
  * [`aeb9279`](https://github.com/bitcoin/bitcoin/commit/aeb9279) Better fingerprinting protection for non-main-chain getdatas.
  * [`cf0218f`](https://github.com/bitcoin/bitcoin/commit/cf0218f) Make addrmanâs bucket placement deterministic (countermeasure 1 against eclipse attacks, see http://cs-people.bu.edu/heilman/eclipse/)
  * [`0c6f334`](https://github.com/bitcoin/bitcoin/commit/0c6f334) Always use a 50% chance to choose between tried and new entries (countermeasure 2 against eclipse attacks)
  * [`214154e`](https://github.com/bitcoin/bitcoin/commit/214154e) Do not bias outgoing connections towards fresh addresses (countermeasure 2 against eclipse attacks)
  * [`aa587d4`](https://github.com/bitcoin/bitcoin/commit/aa587d4) Scale up addrman (countermeasure 6 against eclipse attacks)
  * [`139cd81`](https://github.com/bitcoin/bitcoin/commit/139cd81) Cap nAttempts penalty at 8 and switch to pow instead of a division loop

Validation:

  * [`d148f62`](https://github.com/bitcoin/bitcoin/commit/d148f62) Acquire CCheckQueueâs lock to avoid race condition

Build system:

  * [`8752b5c`](https://github.com/bitcoin/bitcoin/commit/8752b5c) 0.10 fix for crashes on OSX 10.6

Wallet:

  * N/A

GUI:

  * [`2c08406`](https://github.com/bitcoin/bitcoin/commit/2c08406) some mac specifiy cleanup (memory handling, unnecessary code)
  * [`81145a6`](https://github.com/bitcoin/bitcoin/commit/81145a6) fix OSX dock icon window reopening
  * [`786cf72`](https://github.com/bitcoin/bitcoin/commit/786cf72) fix a issue where âcommand line optionsâ-action overwrite âPreferenceâ-action (on OSX)

Tests:

  * [`1117378`](https://github.com/bitcoin/bitcoin/commit/1117378) add RPC test for InvalidateBlock

Miscellaneous:

  * [`c9e022b`](https://github.com/bitcoin/bitcoin/commit/c9e022b) Initialization: set Boost path locale in main thread
  * [`23126a0`](https://github.com/bitcoin/bitcoin/commit/23126a0) Sanitize command strings before logging them.
  * [`323de27`](https://github.com/bitcoin/bitcoin/commit/323de27) Initialization: setup environment before starting QT tests
  * [`7494e09`](https://github.com/bitcoin/bitcoin/commit/7494e09) Initialization: setup environment before starting tests
  * [`df45564`](https://github.com/bitcoin/bitcoin/commit/df45564) Initialization: set fallback locale as environment variable

# Credits

Thanks to everyone who contributed to this release:

  * Alex Morcos
  * Cory Fields
  * dexX7
  * fsb4000
  * Gavin Andresen
  * Gregory Maxwell
  * Ivan Pustogarov
  * Jonas Nick
  * Jonas Schnelli
  * Matt Corallo
  * mrbandrews
  * Pieter Wuille
  * Ruben de Vries
  * Suhas Daftuar
  * Wladimir J. van der Laan

As well as everyone that helped translating on
[Transifex](https://www.transifex.com/projects/p/bitcoin/).

[Go back to the version history](/en/version-history)

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
Bitcoin Core pages on Bitcoin.org are [maintained separately](/en/bitcoin-
core/about-site) from the rest of the site.

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

