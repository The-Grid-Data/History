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
0.6.0

# Bitcoin-Qt version 0.6.0 released

30 March 2012

Bitcoin-Qt version 0.6.0 is now available for download at:
<http://sourceforge.net/projects/bitcoin/files/Bitcoin/bitcoin-0.6.0/>

This release includes more than 20 language localizations. More translations
are welcome; join the project at Transifex to help:
<https://www.transifex.net/projects/p/bitcoin/>

Please report bugs using the issue tracker at github:
<https://github.com/bitcoin/bitcoin/issues>

Project source code is hosted at github; we are no longer distributing .tar.gz
files here, you can get them directly from github:
<https://github.com/bitcoin/bitcoin/tarball/v0.6.0> # .tar.gz
<https://github.com/bitcoin/bitcoin/zipball/v0.6.0> # .zip

For Ubuntu users, there is a ppa maintained by Matt Corallo which you can add
to your system so that it will automatically keep bitcoin up-to-date. Just
type sudo apt-add-repository ppa:bitcoin/bitcoin in your terminal, then
install the bitcoin-qt package.

## KNOWN ISSUES

Shutting down while synchronizing with the network (downloading the
blockchain) can take more than a minute, because database writes are queued to
speed up download time.

## NEW FEATURES SINCE BITCOIN VERSION 0.5

Initial network synchronization should be much faster (one or two hours on a
typical machine instead of ten or more hours).

Backup Wallet menu option.

Bitcoin-Qt can display and save QR codes for sending and receiving addresses.

New context menu on addresses to copy/edit/delete them.

New Sign Message dialog that allows you to prove that you own a bitcoin
address by creating a digital signature.

New wallets created with this version will use 33-byte âcompressedâ public
keys instead of 65-byte public keys, resulting in smaller transactions and
less traffic on the bitcoin network. The shorter keys are already supported by
the network but wallet.dat files containing short keys are not compatible with
earlier versions of Bitcoin-Qt/bitcoind.

New command-line argument `-blocknotify=<command>` that will spawn a shell
process to run `<command>` when a new block is accepted.

New command-line argument -splash=0 to disable Bitcoin-Qtâs initial splash
screen

validateaddress JSON-RPC api command output includes two new fields for
addresses in the wallet: pubkey : hexadecimal public key iscompressed : true
if pubkey is a short 33-byte key

New JSON-RPC api commands for dumping/importing private keys from the wallet
(dumprivkey, importprivkey).

New JSON-RPC api command for getting information about blocks (getblock,
getblockhash).

New JSON-RPC api command (getmininginfo) for getting extra information related
to mining. The getinfo JSON-RPC command no longer includes mining-related
information (generate/genproclimit/hashespersec).

## NOTABLE CHANGES

BIP30 implemented (security fix for an attack involving duplicate âcoinbase
transactionsâ).

The -nolisten, -noupnp and -nodnsseed command-line options were renamed to
-listen, -upnp and -dnsseed, with a default value of 1. The old names are
still supported for compatibility (so specifying -nolisten is automatically
interpreted as -listen=0; every boolean argument can now be specified as
either -foo or -nofoo).

The -noirc command-line options was renamed to -irc, with a default value of
0. Run -irc=1 to get the old behavior.

Three fill-up-available-memory denial-of-service attacks were fixed.

## NOT YET IMPLEMENTED FEATURES

Support for clicking on bitcoin: URIs and opening/launching Bitcoin-Qt is
available only on Linux, and only if you configure your desktop to launch
Bitcoin-Qt. All platforms support dragging and dropping bitcoin: URIs onto the
Bitcoin-Qt window to start payment.

## PRELIMINARY SUPPORT FOR MULTISIGNATURE TRANSACTIONS

This release has preliminary support for multisignature transactionsâ
transactions that require authorization from more than one person or device
before they will be accepted by the bitcoin network.

Prior to this release, multisignature transactions were considered ânon-
standardâ and were ignored; with this release multisignature transactions
are considered standard and will start to be relayed and accepted into blocks.

It is expected that future releases of Bitcoin-Qt will support the creation of
multisignature transactions, once enough of the network has upgraded so
relaying and validating them is robust.

For this release, creation and testing of multisignature transactions is
limited to the bitcoin test network using the âaddmultisigaddressâ JSON-
RPC api call.

Short multisignature address support is included in this release, as specified
in BIP 13 and BIP 16.

Thanks to everybody who contributed to this release:

  * Alex B
  * Alistair Buxton
  * Chris Moore
  * Clark Gaebel
  * Daniel Folkinshteyn
  * Dylan Noblesmith
  * Forrest Voight
  * Gavin Andresen
  * Gregory Maxwell
  * Janne Pulkkinen
  * Joel Kaartinen
  * Lars Rasmusson
  * Luke Dashjr
  * Matt Corallo
  * Michael Ford
  * Michael Hendricks
  * Nick Bosma
  * Nils Schneider
  * Philip Kaufmann
  * Pierre Pronchery
  * Pieter Wuille
  * Rune K Svendsen
  * Wladimir J. van der Laan
  * coderrr
  * p2k
  * sje397

Special thanks to Sergio Lerner and Matt Corallo for bringing potential
denial-of-service attacks to our attention.

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

