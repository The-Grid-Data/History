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
0.8.3

# Bitcoin-Qt version 0.8.3 released

25 June 2013

ALL TOPICS

  * How to Upgrade
  * Fee Policy changes
  * Bitcoin-Qt changes
  * Command-line options
  * JSON-RPC API changes
  * Networking changes
  * Wallet compatibility/rescuing
  * Known Bugs
  * Thanks to everybody who contributed to the 0.8.2 and 0.8.3 releases!

Bitcoin-Qt version 0.8.3 is now available from:
<http://sourceforge.net/projects/bitcoin/files/Bitcoin/bitcoin-0.8.3/>

This is a maintenance release to fix a denial-of-service attack that can cause
nodes to crash.

Please report bugs using the issue tracker at github:
<https://github.com/bitcoin/bitcoin/issues>

## How to Upgrade

If you are running an older version, shut it down. Wait until it has
completely shut down (which might take a few minutes for older versions), then
run the installer (on Windows) or just copy over /Applications/Bitcoin-Qt (on
Mac) or bitcoind/bitcoin-qt (on Linux).

If you are upgrading from version 0.7.2 or earlier, the first time you run
0.8.3 your blockchain files will be re-indexed, which will take anywhere from
30 minutes to several hours, depending on the speed of your machine.

# 0.8.3 Release notes

Truncate over-size messages to prevent a memory exhaustion attack.

Fix a regression that causes excessive re-writing of the `peers.dat` file.

# 0.8.2 Release notes

## Fee Policy changes

The default fee for low-priority transactions is lowered from 0.0005 BTC (for
each 1,000 bytes in the transaction; an average transaction is about 500
bytes) to 0.0001 BTC.

Payments (transaction outputs) of 0.543 times the minimum relay fee
(0.00005430 BTC) are now considered ânon-standardâ, because storing them
costs the network more than they are worth and spending them will usually cost
their owner more in transaction fees than they are worth.

Non-standard transactions are not relayed across the network, are not included
in blocks by most miners, and will not show up in your wallet until they are
included in a block.

The default fee policy can be overridden using the -mintxfee and
-minrelaytxfee command-line options, but note that we intend to replace the
hard-coded fees with code that automatically calculates and suggests
appropriate fees in the 0.9 release and note that if you set a fee policy
significantly different from the rest of the network your transactions may
never confirm.

## Bitcoin-Qt changes

  * New icon and splash screen
  * Improve reporting of synchronization process
  * Remove hardcoded fee recommendations
  * Improve metadata of executable on MacOSX and Windows
  * Move export button to individual tabs instead of toolbar
  * Add âsend coinsâ command to context menu in address book
  * Add âcopy txidâ command to copy transaction IDs from transaction overview
  * Save & restore window size and position when showing & hiding window
  * New translations: Arabic (ar), Bosnian (bs), Catalan (ca), Welsh (cy), Esperanto (eo), Interlingua (la), Latvian (lv) and many improvements to current translations

MacOSX:

  * OSX support for click-to-pay (bitcoin:) links
  * Fix GUI disappearing problem on MacOSX (issue #1522)

Linux/Unix:

  * Copy addresses to middle-mouse-button clipboard

## Command-line options

  * -walletnotify will call a command on receiving transactions that affect the wallet.
  * -alertnotify will call a command on receiving an alert from the network.
  * -par now takes a negative number, to leave a certain amount of cores free.

## JSON-RPC API changes

  * fixed a getblocktemplate bug that caused excessive CPU creating blocks.
  * listunspent now lists account and address infromation.
  * getinfo now also returns the time adjustment estimated from your peers.
  * getpeerinfo now returns bytessent, bytesrecv and syncnode.
  * gettxoutsetinfo returns statistics about the unspent transaction output database.
  * gettxout returns information about a specific unspent transaction output.

## Networking changes

  * Significant changes to the networking code, reducing latency and memory consumption.
  * Avoid initial block download stalling.
  * Remove IRC seeding support.
  * Performance tweaks.
  * Added testnet DNS seeds.

## Wallet compatibility/rescuing

  * Cases where wallets cannot be opened in another version/installation should be reduced.
  * -salvagewallet now works for encrypted wallets.

## Known Bugs

  * Entering the `getblocktemplate` or `getwork` RPC commands into the Bitcoin-Qt debug console will cause Bitcoin-Qt to crash. Run Bitcoin-Qt with the -server command-line option to workaround.

## Thanks to everybody who contributed to the 0.8.2 and 0.8.3 releases!

  * APerson241
  * Andrew Poelstra
  * Calvin Owens
  * Chuck LeDuc DÃ­az
  * Colin Dean
  * David Griffith
  * David Serrano
  * Eric Lombrozo
  * Gavin Andresen
  * Gregory Maxwell
  * Jeff Garzik
  * Jonas Schnelli
  * Larry Gilbert
  * Luke Dashjr
  * Matt Corallo
  * Michael Ford
  * Mike Hearn
  * Patrick Brown
  * Peter Todd
  * Philip Kaufmann
  * Pieter Wuille
  * Richard Schwab
  * Roman Mindalev
  * Scott Howard
  * Tariq Bashir
  * Warren Togami
  * Wladimir J. van der Laan
  * freewil
  * gladoscc
  * kjj2
  * mb300sd
  * super3

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
