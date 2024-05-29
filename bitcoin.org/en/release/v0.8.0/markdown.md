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
0.8.0

# Bitcoin-Qt version 0.8.0 released

19 February 2013

Bitcoin-Qt version 0.8.0 are now available from:
<http://sourceforge.net/projects/bitcoin/files/Bitcoin/bitcoin-0.8.0/>

This is a major release designed to improve performance and handle the
increasing volume of transactions on the network.

Please report bugs using the issue tracker at github:
<https://github.com/bitcoin/bitcoin/issues>

## How to Upgrade

If you are running an older version, shut it down. Wait until it has
completely shut down (which might take a few minutes for older versions), then
run the installer (on Windows) or just copy over /Applications/Bitcoin-Qt (on
Mac) or bitcoind/bitcoin-qt (on Linux).

The first time you run after the upgrade a re-indexing process will be started
that will take anywhere from 30 minutes to several hours, depending on the
speed of your machine.

## Incompatible Changes

This release no longer maintains a full index of historical transaction ids by
default, so looking up an arbitrary transaction using the getrawtransaction
RPC call will not work. If you need that functionality, you must run once with
-txindex=1 -reindex=1 to rebuild block-chain indices (see below for more
details).

## Improvements

Mac and Windows binaries are signed with certificates owned by the Bitcoin
Foundation, to be compatible with the new security features in OSX 10.8 and
Windows 8.

LevelDB, a fast, open-source, non-relational database from Google, is now used
to store transaction and block indices. LevelDB works much better on machines
with slow I/O and is faster in general. Berkeley DB is now only used for the
wallet.dat file (public and private wallet keys and transactions relevant to
you).

Pieter Wuille implemented many optimizations to the way transactions are
verified, so a running, synchronized node uses less working memory and does
much less I/O. He also implemented parallel signature checking, so if you have
a multi-CPU machine all CPUs will be used to verify transactions.

## New Features

âBloom filterâ support in the network protocol for sending only relevant
transactions to lightweight clients.

contrib/verifysfbinaries is a shell-script to verify that the binary downloads
at sourceforge have not been tampered with. If you are able, you can help make
everybodyâs downloads more secure by running this occasionally to check PGP
signatures against download file checksums.

contrib/spendfrom is a python-language command-line utility that demonstrates
how to use the âraw transactionsâ JSON-RPC api to send coins received from
particular addresses (also known as âcoin controlâ).

## New/changed settings (command-line or bitcoin.conf file)

dbcache : controls LevelDB memory usage.

par : controls how many threads to use to validate transactions. Defaults to
the number of CPUs on your machine, use -par=1 to limit to a single CPU.

txindex : maintains an extra index of old, spent transaction ids so they will
be found by the getrawtransaction JSON-RPC method.

reindex : rebuild block and transaction indices from the downloaded block
data.

## New JSON-RPC API Features

lockunspent / listlockunspent allow locking transaction outputs for a period
of time so they will not be spent by other processes that might be accessing
the same wallet.

addnode / getaddednodeinfo methods, to connect to specific peers without
restarting.

importprivkey now takes an optional boolean parameter (default true) to
control whether or not to rescan the blockchain for transactions after
importing a new private key.

## Important Bug Fixes

Privacy leak: the position of the âchangeâ output in most transactions was
not being properly randomized, making network analysis of the transaction
graph to identify usersâ wallets easier.

Zero-confirmation transaction vulnerability: accepting zero-confirmation
transactions (transactions that have not yet been included in a block) from
somebody you do not trust is still not recommended, because there will always
be ways for attackers to double-spend zero-confirmation transactions. However,
this release includes a bug fix that makes it a little bit more difficult for
attackers to double-spend a certain type (âlockTime in the futureâ) of
zero-confirmation transaction.

## Dependency Changes

Qt 4.8.3 (compiling against older versions of Qt 4 should continue to work)

## Thanks to everybody who contributed to this release:

  * Alexander Kjeldaas
  * Andrey Alekseenko
  * Arnav Singh
  * Christian von Roques
  * Eric Lombrozo
  * Forrest Voight
  * Gavin Andresen
  * Gregory Maxwell
  * Jeff Garzik
  * Luke Dashjr
  * Matt Corallo
  * Mike Cassano
  * Mike Hearn
  * Peter Todd
  * Philip Kaufmann
  * Pieter Wuille
  * Richard Schwab
  * Robert Backhaus
  * Rune K. Svendsen
  * Sergio Demian Lerner
  * Wladimir J. van der Laan
  * burger2
  * default
  * fanquake
  * grimd34th
  * justmoon
  * redshark1802
  * tucenaber
  * xanatos

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

