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
25.0

# Bitcoin Core 25.0

# 25.0 Release Notes

Bitcoin Core version 25.0 is now available from:

<https://bitcoin.org/bin/bitcoin-core-25.0/>

This release includes new features, various bug fixes and performance
improvements, as well as updated translations.

Please report bugs using the issue tracker at GitHub:

<https://github.com/bitcoin/bitcoin/issues>

To receive security and update notifications, please subscribe to:

<https://bitcoincore.org/en/list/announcements/join/>

# How to Upgrade

If you are running an older version, shut it down. Wait until it has
completely shut down (which might take a few minutes in some cases), then run
the installer (on Windows) or just copy over `/Applications/Bitcoin-Qt` (on
macOS) or `bitcoind`/`bitcoin-qt` (on Linux).

Upgrading directly from a version of Bitcoin Core that has reached its EOL is
possible, but it might take some time if the data directory needs to be
migrated. Old wallet versions of Bitcoin Core are generally supported.

# Compatibility

Bitcoin Core is supported and extensively tested on operating systems using
the Linux kernel, macOS 10.15+, and Windows 7 and newer. Bitcoin Core should
also work on most other Unix-like systems but is not as frequently tested on
them. It is not recommended to use Bitcoin Core on unsupported systems.

# Notable changes

## P2P and network changes

  * Transactions of non-witness size 65 bytes and above are now allowed by mempool and relay policy. This is to better reflect the actual afforded protections against CVE-2017-12842 and open up additional use-cases of smaller transaction sizes. ([#26265](https://github.com/bitcoin/bitcoin/pull/26265))

## New RPCs

  * The scanblocks RPC returns the relevant blockhashes from a set of descriptors by scanning all blockfilters in the given range. It can be used in combination with the getblockheader and rescanblockchain RPCs to achieve fast wallet rescans. Note that this functionality can only be used if a compact block filter index (-blockfilterindex=1) has been constructed by the node. ([#23549](https://github.com/bitcoin/bitcoin/pull/23549))

## Updated RPCs

  * All JSON-RPC methods accept a new [named parameter](https://github.com/bitcoin/bitcoin/blob/master/doc/JSON-RPC-interface.md#parameter-passing) called `args` that can contain positional parameter values. This is a convenience to allow some parameter values to be passed by name without having to name every value. The python test framework and `bitcoin-cli` tool both take advantage of this, so for example:

    
    
    bitcoin-cli -named createwallet wallet_name=mywallet load_on_startup=1
    

Can now be shortened to:

    
    
    bitcoin-cli -named createwallet mywallet load_on_startup=1
    

  * The `verifychain` RPC will now return `false` if the checks didnât fail, but couldnât be completed at the desired depth and level. This could be due to missing data while pruning, due to an insufficient dbcache or due to the node being shutdown before the call could finish. ([#25574](https://github.com/bitcoin/bitcoin/pull/25574))

  * `sendrawtransaction` has a new, optional argument, `maxburnamount` with a default value of `0`. Any transaction containing an unspendable output with a value greater than `maxburnamount` will not be submitted. At present, the outputs deemed unspendable are those with scripts that begin with an `OP_RETURN` code (known as âdatacarriersâ), scripts that exceed the maximum script size, and scripts that contain invalid opcodes.

  * The `testmempoolaccept` RPC now returns 2 additional results within the âfeesâ result: âeffective-feerateâ is the feerate including fees and sizes of transactions validated together if package validation was used, and also includes any modified fees from prioritisetransaction. The âeffective-includesâ result lists the wtxids of transactions whose modified fees and sizes were used in the effective-feerate ([#26646](https://github.com/bitcoin/bitcoin/pull/26646)).

  * `decodescript` may now infer a Miniscript descriptor under P2WSH context if it is not lacking information. ([#27037](https://github.com/bitcoin/bitcoin/pull/27037))

  * `finalizepsbt` is now able to finalize a transaction with inputs spending Miniscript-compatible P2WSH scripts. ([#24149](https://github.com/bitcoin/bitcoin/pull/24149))

Changes to wallet related RPCs can be found in the Wallet section below.

## Build System

  * The `--enable-upnp-default` and `--enable-natpmp-default` options have been removed. If you want to use port mapping, you can configure it using a .conf file, or by passing the relevant options at runtime. ([#26896](https://github.com/bitcoin/bitcoin/pull/26896))

## Updated settings

  * If the `-checkblocks` or `-checklevel` options are explicitly provided by the user, but the verification checks cannot be completed due to an insufficient dbcache, Bitcoin Core will now return an error at startup. ([#25574](https://github.com/bitcoin/bitcoin/pull/25574))

  * Ports specified in `-port` and `-rpcport` options are now validated at startup. Values that previously worked and were considered valid can now result in errors. ([#22087](https://github.com/bitcoin/bitcoin/pull/22087))

  * Setting `-blocksonly` will now reduce the maximum mempool memory to 5MB (users may still use `-maxmempool` to override). Previously, the default 300MB would be used, leading to unexpected memory usage for users running with `-blocksonly` expecting it to eliminate mempool memory usage.

As unused mempool memory is shared with dbcache, this also reduces the dbcache
size for users running with `-blocksonly`, potentially impacting performance.

  * Setting `-maxconnections=0` will now disable `-dnsseed` and `-listen` (users may still set them to override).

Changes to GUI or wallet related settings can be found in the GUI or Wallet
section below.

## New settings

  * The `shutdownnotify` option is used to specify a command to execute synchronously before Bitcoin Core has begun its shutdown sequence. ([#23395](https://github.com/bitcoin/bitcoin/pull/23395))

## Wallet

  * The `minconf` option, which allows a user to specify the minimum number of confirmations a UTXO being spent has, and the `maxconf` option, which allows specifying the maximum number of confirmations, have been added to the following RPCs in [#25375](https://github.com/bitcoin/bitcoin/pull/25375): 
    * `fundrawtransaction`
    * `send`
    * `walletcreatefundedpsbt`
    * `sendall`
  * Added a new `next_index` field in the response in `listdescriptors` to have the same format as `importdescriptors` ([#26194](https://github.com/bitcoin/bitcoin/pull/26194))

  * RPC `listunspent` now has a new argument `include_immature_coinbase` to include coinbase UTXOs that donât meet the minimum spendability depth requirement (which before were silently skipped). ([#25730](https://github.com/bitcoin/bitcoin/pull/25730))

  * Rescans for descriptor wallets are now significantly faster if compact block filters (BIP158) are available. Since those are not constructed by default, the configuration option â-blockfilterindex=1â has to be provided to take advantage of the optimization. This improves the performance of the RPC calls `rescanblockchain`, `importdescriptors` and `restorewallet`. ([#25957](https://github.com/bitcoin/bitcoin/pull/25957))

  * RPC `unloadwallet` now fails if a rescan is in progress. ([#26618](https://github.com/bitcoin/bitcoin/pull/26618))

  * Wallet passphrases may now contain null characters. Prior to this change, only characters up to the first null character were recognized and accepted. ([#27068](https://github.com/bitcoin/bitcoin/pull/27068))

  * Address Purposes strings are now restricted to the currently known values of âsendâ, âreceiveâ, and ârefundâ. Wallets that have unrecognized purpose strings will have loading warnings, and the `listlabels` RPC will raise an error if an unrecognized purpose is requested. ([#27217](https://github.com/bitcoin/bitcoin/pull/27217))

  * In the `createwallet`, `loadwallet`, `unloadwallet`, and `restorewallet` RPCs, the âwarningâ string field is deprecated in favor of a âwarningsâ field that returns a JSON array of strings to better handle multiple warning messages and for consistency with other wallet RPCs. The âwarningâ field will be fully removed from these RPCs in v26. It can be temporarily re-enabled during the deprecation period by launching bitcoind with the configuration option `-deprecatedrpc=walletwarningfield`. ([#27279](https://github.com/bitcoin/bitcoin/pull/27279))

  * Descriptor wallets can now spend coins sent to P2WSH Miniscript descriptors. ([#24149](https://github.com/bitcoin/bitcoin/pull/24149))

## GUI changes

  * The âMask valuesâ is a persistent option now. (gui[#701](https://github.com/bitcoin/bitcoin/pull/701))
  * The âMask valuesâ option affects the âTransactionâ view now, in addition to the âOverviewâ one. (gui[#708](https://github.com/bitcoin/bitcoin/pull/708))

## REST

  * A new `/rest/deploymentinfo` endpoint has been added for fetching various state info regarding deployments of consensus changes. ([#25412](https://github.com/bitcoin/bitcoin/pull/25412))

## Binary verification

  * The binary verification script has been updated. In previous releases it would verify that the binaries had been signed with a single ârelease keyâ. In this release and moving forward it will verify that the binaries are signed by a _threshold of trusted keys_. For more details and examples, see: https://github.com/bitcoin/bitcoin/blob/master/contrib/verify-binaries/README.md ([#27358](https://github.com/bitcoin/bitcoin/pull/27358))

# Low-level changes

## RPC

  * The JSON-RPC server now rejects requests where a parameter is specified multiple times with the same name, instead of silently overwriting earlier parameter values with later ones. ([#26628](https://github.com/bitcoin/bitcoin/pull/26628))
  * RPC `listsinceblock` now accepts an optional `label` argument to fetch incoming transactions having the specified label. ([#25934](https://github.com/bitcoin/bitcoin/pull/25934))
  * Previously `setban`, `addpeeraddress`, `walletcreatefundedpsbt`, methods allowed non-boolean and non-null values to be passed as boolean parameters. Any string, number, array, or object value that was passed would be treated as false. After this change, passing any value except `true`, `false`, or `null` now triggers a JSON value is not of expected type error. ([#26213](https://github.com/bitcoin/bitcoin/pull/26213))

# Credits

Thanks to everyone who directly contributed to this release:

  * 0xb10c
  * 721217.xyz
  * @RandyMcMillan
  * amadeuszpawlik
  * Amiti Uttarwar
  * Andrew Chow
  * Andrew Toth
  * Anthony Towns
  * Antoine Poinsot
  * AurÃ¨le OulÃ¨s
  * Ben Woosley
  * Bitcoin Hodler
  * brunoerg
  * Bushstar
  * Carl Dong
  * Chris Geihsler
  * Cory Fields
  * David Gumberg
  * dergoegge
  * Dhruv Mehta
  * Dimitris Tsapakidis
  * dougEfish
  * Douglas Chimento
  * ekzyis
  * Elichai Turkel
  * Ethan Heilman
  * Fabian Jahr
  * FractalEncrypt
  * furszy
  * Gleb Naumenko
  * glozow
  * Greg Sanders
  * Hennadii Stepanov
  * hernanmarino
  * ishaanam
  * ismaelsadeeq
  * James OâBeirne
  * jdjkelly@gmail.com
  * Jeff Ruane
  * Jeffrey Czyz
  * Jeremy Rubin
  * Jesse Barton
  * JoÃ£o Barbosa
  * JoaoAJMatos
  * John Moffett
  * Jon Atack
  * Jonas Schnelli
  * jonatack
  * Joshua Kelly
  * josibake
  * Juan Pablo Civile
  * kdmukai
  * klementtan
  * Kolby ML
  * kouloumos
  * Kristaps Kaupe
  * laanwj
  * Larry Ruane
  * Leonardo Araujo
  * Leonardo Lazzaro
  * Luke Dashjr
  * MacroFake
  * MarcoFalke
  * Martin Leitner-Ankerl
  * Martin Zumsande
  * Matt Whitlock
  * Matthew Zipkin
  * Michael Ford
  * Miles Liu
  * mruddy
  * Murray Nesbitt
  * muxator
  * omahs
  * pablomartin4btc
  * Pasta
  * Pieter Wuille
  * Pttn
  * Randall Naar
  * Riahiamirreza
  * roconnor-blockstream
  * Russell OâConnor
  * Ryan Ofsky
  * S3RK
  * Sebastian Falbesoner
  * Seibart Nedor
  * sinetek
  * Sjors Provoost
  * Skuli Dulfari
  * SomberNight
  * Stacie Waleyko
  * stickies-v
  * stratospher
  * Suhas Daftuar
  * Suriyaa Sundararuban
  * TheCharlatan
  * Vasil Dimov
  * Vasil Stoyanov
  * virtu
  * w0xlt
  * willcl-ark
  * yancy
  * Yusuf Sahin HAMZA

As well as to everyone that helped with translations on
[Transifex](https://www.transifex.com/bitcoin/bitcoin/).

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

