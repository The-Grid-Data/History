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
0.13.0

# Bitcoin Core version 0.13.0 released

23 August 2016

ALL TOPICS

  * Compatibility
  * Notable changes
    * Database cache memory increased
    * bitcoin-cli: arguments privacy
    * C++11 and Python 3
    * Linux ARM builds
    * Compact Block support (BIP 152)
    * Hierarchical Deterministic Key Generation
    * Segregated Witness
    * Mining transaction selection (âChild Pays For Parentâ)
    * Reindexing changes
    * Removal of internal miner
    * New bytespersigop implementation
    * Low-level P2P changes
    * Low-level RPC changes
    * Low-level ZMQ changes
  * 0.13.0 Change log \- {:.} RPC and other APIs \- {:.} Block and transaction handling \- {:.} P2P protocol and network code \- {:.} Build system \- {:.} GUI \- {:.} Wallet \- {:.} Tests and QA \- {:.} Mining \- {:.} Documentation and miscellaneous
  * Credits

Bitcoin Core version 0.13.0 is now available from:

<https://bitcoin.org/bin/bitcoin-core-0.13.0/>

This is a new major version release, including new features, various bugfixes
and performance improvements, as well as updated translations.

Please report bugs using the issue tracker at github:

<https://github.com/bitcoin/bitcoin/issues>

To receive security and update notifications, please subscribe to:

<https://bitcoincore.org/en/list/announcements/join/>

# Compatibility

Microsoft ended support for Windows XP on [April 8th,
2014](https://www.microsoft.com/en-us/WindowsForBusiness/end-of-xp-support),
an OS initially released in 2001. This means that not even critical security
updates will be released anymore. Without security updates, using a bitcoin
wallet on a XP machine is irresponsible at least.

In addition to that, with 0.12.x there have been varied reports of Bitcoin
Core randomly crashing on Windows XP. It is [not
clear](https://github.com/bitcoin/bitcoin/issues/7681#issuecomment-217439891)
what the source of these crashes is, but it is likely that upstream libraries
such as Qt are no longer being tested on XP.

We do not have time nor resources to provide support for an OS that is end-of-
life. From 0.13.0 on, Windows XP is no longer supported. Users are suggested
to upgrade to a newer verion of Windows, or install an alternative OS that is
supported.

No attempt is made to prevent installing or running the software on Windows
XP, you can still do so at your own risk, but do not expect it to work: do not
report issues about Windows XP to the issue tracker.

# Notable changes

## Database cache memory increased

As a result of growth of the UTXO set, performance with the prior default
database cache of 100 MiB has suffered. For this reason the default was
changed to 300 MiB in this release.

For nodes on low-memory systems, the database cache can be changed back to 100
MiB (or to another value) by either:

  * Adding `dbcache=100` in bitcoin.conf
  * Changing it in the GUI under `Options â Size of database cache`

Note that the database cache setting has the most performance impact during
initial sync of a node, and when catching up after downtime.

## bitcoin-cli: arguments privacy

The RPC command line client gained a new argument, `-stdin` to read extra
arguments from standard input, one per line until EOF/Ctrl-D. For example:

    
    
    $ src/bitcoin-cli -stdin walletpassphrase
    mysecretcode
    120
    ..... press Ctrl-D here to end input
    $
    

It is recommended to use this for sensitive information such as wallet
passphrases, as command-line arguments can usually be read from the process
table by any user on the system.

## C++11 and Python 3

Various code modernizations have been done. The Bitcoin Core code base has
started using C++11. This means that a C++11-capable compiler is now needed
for building. Effectively this means GCC 4.7 or higher, or Clang 3.3 or
higher.

When cross-compiling for a target that doesnât have C++11 libraries,
configure with `./configure --enable-glibc-back-compat ... LDFLAGS=-static-
libstdc++`.

For running the functional tests in `qa/rpc-tests`, Python3.4 or higher is now
required.

## Linux ARM builds

Due to popular request, Linux ARM builds have been added to the uploaded
executables.

The following extra files can be found in the download directory or torrent:

  * `bitcoin-${VERSION}-arm-linux-gnueabihf.tar.gz`: Linux binaries for the most common 32-bit ARM architecture.
  * `bitcoin-${VERSION}-aarch64-linux-gnu.tar.gz`: Linux binaries for the most common 64-bit ARM architecture.

ARM builds are still experimental. If you have problems on a certain device or
Linux distribution combination please report them on the bug tracker, it may
be possible to resolve them.

Note that Android is not considered ARM Linux in this context. The executables
are not expected to work out of the box on Android.

## Compact Block support (BIP 152)

Support for block relay using the Compact Blocks protocol has been implemented
in PR 8068.

The primary goal is reducing the bandwidth spikes at relay time, though in
many cases it also reduces propagation delay. It is automatically enabled
between compatible peers. [BIP
152](https://github.com/bitcoin/bips/blob/master/bip-0152.mediawiki)

As a side-effect, ordinary non-mining nodes will download and upload blocks
faster if those blocks were produced by miners using similar transaction
filtering policies. This means that a miner who produces a block with many
transactions discouraged by your node will be relayed slower than one with
only transactions already in your memory pool. The overall effect of such
relay differences on the network may result in blocks which include widely-
discouraged transactions losing a stale block race, and therefore miners may
wish to configure their node to take common relay policies into consideration.

## Hierarchical Deterministic Key Generation

Newly created wallets will use hierarchical deterministic key generation
according to BIP32 (keypath m/0â/0â/kâ). Existing wallets will still use
traditional key generation.

Backups of HD wallets, regardless of when they have been created, can
therefore be used to re-generate all possible private keys, even the ones
which havenât already been generated during the time of the backup.
**Attention:** Encrypting the wallet will create a new seed which requires a
new backup!

Wallet dumps (created using the `dumpwallet` RPC) will contain the
deterministic seed. This is expected to allow future versions to import the
seed and all associated funds, but this is not yet implemented.

HD key generation for new wallets can be disabled by `-usehd=0`. Keep in mind
that this flag only has affect on newly created wallets. You canât disable
HD key generation once you have created a HD wallet.

There is no distinction between internal (change) and external keys.

HD wallets are incompatible with older versions of Bitcoin Core.

[Pull request](https://github.com/bitcoin/bitcoin/pull/8035/files), [BIP
32](https://github.com/bitcoin/bips/blob/master/bip-0032.mediawiki)

## Segregated Witness

The code preparations for Segregated Witness (âsegwitâ), as described in
[BIP 141](https://github.com/bitcoin/bips/blob/master/bip-0141.mediawiki),
[BIP 143](https://github.com/bitcoin/bips/blob/master/bip-0143.mediawiki),
[BIP 144](https://github.com/bitcoin/bips/blob/master/bip-0144.mediawiki), and
[BIP 145](https://github.com/bitcoin/bips/blob/master/bip-0145.mediawiki) are
finished and included in this release. However, BIP 141 does not yet specify
activation parameters on mainnet, and so this release does not support segwit
use on mainnet. Testnet use is supported, and after BIP 141 is updated with
proposed parameters, a future release of Bitcoin Core is expected that
implements those parameters for mainnet.

Furthermore, because segwit activation is not yet specified for mainnet,
version 0.13.0 will behave similarly as other pre-segwit releases even after a
future activation of BIP 141 on the network. Upgrading from 0.13.0 will be
required in order to utilize segwit-related features on mainnet (such as
signal BIP 141 activation, mine segwit blocks, fully validate segwit blocks,
relay segwit blocks to other segwit nodes, and use segwit transactions in the
wallet, etc).

## Mining transaction selection (âChild Pays For Parentâ)

The mining transaction selection algorithm has been replaced with an algorithm
that selects transactions based on their feerate inclusive of unconfirmed
ancestor transactions. This means that a low-fee transaction can become more
likely to be selected if a high-fee transaction that spends its outputs is
relayed.

With this change, the `-blockminsize` command line option has been removed.

The command line option `-blockmaxsize` remains an option to specify the
maximum number of serialized bytes in a generated block. In addition, the new
command line option `-blockmaxweight` has been added, which specifies the
maximum âblock weightâ of a generated block, as defined by [BIP 141
(Segregated Witness)]
(https://github.com/bitcoin/bips/blob/master/bip-0141.mediawiki).

In preparation for Segregated Witness, the mining algorithm has been modified
to optimize transaction selection for a given block weight, rather than a
given number of serialized bytes in a block. In this release, transaction
selection is unaffected by this distinction (as BIP 141 activation is not
supported on mainnet in this release, see above), but in future releases and
after BIP 141 activation, these calculations would be expected to differ.

For optimal runtime performance, miners using this release should specify
`-blockmaxweight` on the command line, and not specify `-blockmaxsize`.
Additionally (or only) specifying `-blockmaxsize`, or relying on default
settings for both, may result in performance degradation, as the logic to
support `-blockmaxsize` performs additional computation to ensure that
constraint is met. (Note that for mainnet, in this release, the equivalent
parameter for `-blockmaxweight` would be four times the desired
`-blockmaxsize`. See [BIP 141]
(https://github.com/bitcoin/bips/blob/master/bip-0141.mediawiki) for
additional details.)

In the future, the `-blockmaxsize` option may be removed, as block creation is
no longer optimized for this metric. Feedback is requested on whether to
deprecate or keep this command line option in future releases.

## Reindexing changes

In earlier versions, reindexing did validation while reading through the block
files on disk. These two have now been split up, so that all blocks are known
before validation starts. This was necessary to make certain optimizations
that are available during normal synchronizations also available during
reindexing.

The two phases are distinct in the Bitcoin-Qt GUI. During the first one,
âReindexing blocks on diskâ is shown. During the second (slower) one,
âProcessing blocks on diskâ is shown.

It is possible to only redo validation now, without rebuilding the block
index, using the command line option `-reindex-chainstate` (in addition to
`-reindex` which does both). This new option is useful when the blocks on disk
are assumed to be fine, but the chainstate is still corrupted. It is also
useful for benchmarks.

## Removal of internal miner

As CPU mining has been useless for a long time, the internal miner has been
removed in this release, and replaced with a simpler implementation for the
test framework.

The overall result of this is that `setgenerate` RPC call has been removed, as
well as the `-gen` and `-genproclimit` command-line options.

For testing, the `generate` call can still be used to mine a block, and a new
RPC call `generatetoaddress` has been added to mine to a specific address.
This works with wallet disabled.

## New bytespersigop implementation

The former implementation of the bytespersigop filter accidentally broke bare
multisig (which is meant to be controlled by the `permitbaremultisig` option),
since the consensus protocol always counts these older transaction forms as 20
sigops for backwards compatibility. Simply fixing this bug by counting more
accurately would have reintroduced a vulnerability. It has therefore been
replaced with a new implementation that rather than filter such transactions,
instead treats them (for fee purposes only) as if they were in fact the size
of a transaction actually using all 20 sigops.

## Low-level P2P changes

  * The optional new p2p message âfeefilterâ is implemented and the protocol version is bumped to 70013. Upon receiving a feefilter message from a peer, a node will not send invs for any transactions which do not meet the filter feerate. [BIP 133](https://github.com/bitcoin/bips/blob/master/bip-0133.mediawiki)

  * The P2P alert system has been removed in PR [#7692](https://github.com/bitcoin/bitcoin/pull/7692) and the `alert` P2P message is no longer supported.

  * The transaction relay mechanism used to relay one quarter of all transactions instantly, while queueing up the rest and sending them out in batch. As this resulted in chains of dependent transactions being reordered, it systematically hurt transaction relay. The relay code was redesigned in PRs <a href=âhttps://github.com/bitcoin/bitcoin/pull/7840â>#7840</a> and [#8082](https://github.com/bitcoin/bitcoin/pull/8082), and now always batches transactions announcements while also sorting them according to dependency order. This significantly reduces orphan transactions. To compensate for the removal of instant relay, the frequency of batch sending was doubled for outgoing peers.

  * Since PR [#7840](https://github.com/bitcoin/bitcoin/pull/7840) the BIP35 `mempool` command is also subject to batch processing. Also the `mempool` message is no longer handled for non-whitelisted peers when `NODE_BLOOM` is disabled through `-peerbloomfilters=0`.

  * The maximum size of orphan transactions that are kept in memory until their ancestors arrive has been raised in PR [#8179](https://github.com/bitcoin/bitcoin/pull/8179) from 5000 to 99999 bytes. They are now also removed from memory when they are included in a block, conflict with a block, and time out after 20 minutes.

  * We respond at most once to a getaddr request during the lifetime of a connection since PR [#7856](https://github.com/bitcoin/bitcoin/pull/7856).

  * Connections to peers who have recently been the first one to give us a valid new block or transaction are protected from disconnections since PR [#8084](https://github.com/bitcoin/bitcoin/pull/8084).

## Low-level RPC changes

  * RPC calls have been added to output detailed statistics for individual mempool entries, as well as to calculate the in-mempool ancestors or descendants of a transaction: see `getmempoolentry`, `getmempoolancestors`, `getmempooldescendants`.

  * `gettxoutsetinfo` UTXO hash (`hash_serialized`) has changed. There was a divergence between 32-bit and 64-bit platforms, and the txids were missing in the hashed data. This has been fixed, but this means that the output will be different than from previous versions.

  * Full UTF-8 support in the RPC API. Non-ASCII characters in, for example, wallet labels have always been malformed because they werenât taken into account properly in JSON RPC processing. This is no longer the case. This also affects the GUI debug console.

  * Asm script outputs replacements for OP_NOP2 and OP_NOP3

    * OP_NOP2 has been renamed to OP_CHECKLOCKTIMEVERIFY by [BIP 65](https://github.com/bitcoin/bips/blob/master/bip-0065.mediawiki)

    * OP_NOP3 has been renamed to OP_CHECKSEQUENCEVERIFY by [BIP 112](https://github.com/bitcoin/bips/blob/master/bip-0112.mediawiki)

    * The following outputs are affected by this change:

      * RPC `getrawtransaction` (in verbose mode)
      * RPC `decoderawtransaction`
      * RPC `decodescript`
      * REST `/rest/tx/` (JSON format)
      * REST `/rest/block/` (JSON format when including extended tx details)
      * `bitcoin-tx -json`
  * The sorting of the output of the `getrawmempool` output has changed.

  * New RPC commands: `generatetoaddress`, `importprunedfunds`, `removeprunedfunds`, `signmessagewithprivkey`, `getmempoolancestors`, `getmempooldescendants`, `getmempoolentry`, `createwitnessaddress`, `addwitnessaddress`.

  * Removed RPC commands: `setgenerate`, `getgenerate`.

  * New options were added to `fundrawtransaction`: `includeWatching`, `changeAddress`, `changePosition` and `feeRate`.

## Low-level ZMQ changes

  * Each ZMQ notification now contains an up-counting sequence number that allows listeners to detect lost notifications. The sequence number is always the last element in a multi-part ZMQ notification and therefore backward compatible. Each message type has its own counter. PR #[7762](https://github.com/bitcoin/bitcoin/pull/7762).

# 0.13.0 Change log

Detailed release notes follow. This overview includes changes that affect
behavior, not code moves, refactors and string updates. For convenience in
locating the code changes and accompanying discussion, both the pull request
and git merge commit are mentioned.

### RPC and other APIs

  * [#7156](https://github.com/bitcoin/bitcoin/pull/7156) [`9ee02cf`](https://github.com/bitcoin/bitcoin/commit/9ee02cf) Remove cs_main lock from `createrawtransaction` (laanwj)
  * [#7326](https://github.com/bitcoin/bitcoin/pull/7326) [`2cd004b`](https://github.com/bitcoin/bitcoin/commit/2cd004b) Fix typo, wrong information in gettxout help text (paveljanik)
  * [#7222](https://github.com/bitcoin/bitcoin/pull/7222) [`82429d0`](https://github.com/bitcoin/bitcoin/commit/82429d0) Indicate which transactions are signaling opt-in RBF (sdaftuar)
  * [#7480](https://github.com/bitcoin/bitcoin/pull/7480) [`b49a623`](https://github.com/bitcoin/bitcoin/commit/b49a623) Changed getnetworkhps value to double to avoid overflow (instagibbs)
  * [#7550](https://github.com/bitcoin/bitcoin/pull/7550) [`8b958ab`](https://github.com/bitcoin/bitcoin/commit/8b958ab) Input-from-stdin mode for bitcoin-cli (laanwj)
  * [#7670](https://github.com/bitcoin/bitcoin/pull/7670) [`c9a1265`](https://github.com/bitcoin/bitcoin/commit/c9a1265) Use cached block hash in blockToJSON() (rat4)
  * [#7726](https://github.com/bitcoin/bitcoin/pull/7726) [`9af69fa`](https://github.com/bitcoin/bitcoin/commit/9af69fa) Correct importaddress help reference to importpubkey (CypherGrue)
  * [#7766](https://github.com/bitcoin/bitcoin/pull/7766) [`16555b6`](https://github.com/bitcoin/bitcoin/commit/16555b6) Register calls where they are defined (laanwj)
  * [#7797](https://github.com/bitcoin/bitcoin/pull/7797) [`e662a76`](https://github.com/bitcoin/bitcoin/commit/e662a76) Fix generatetoaddress failing to parse address (mruddy)
  * [#7774](https://github.com/bitcoin/bitcoin/pull/7774) [`916b15a`](https://github.com/bitcoin/bitcoin/commit/916b15a) Add versionHex in getblock and getblockheader JSON results (mruddy)
  * [#7863](https://github.com/bitcoin/bitcoin/pull/7863) [`72c54e3`](https://github.com/bitcoin/bitcoin/commit/72c54e3) Getblockchaininfo: make bip9_softforks an object, not an array (rustyrussell)
  * [#7842](https://github.com/bitcoin/bitcoin/pull/7842) [`d97101e`](https://github.com/bitcoin/bitcoin/commit/d97101e) Do not print minping time in getpeerinfo when no ping received yet (paveljanik)
  * [#7518](https://github.com/bitcoin/bitcoin/pull/7518) [`be14ca5`](https://github.com/bitcoin/bitcoin/commit/be14ca5) Add multiple options to fundrawtransaction (promag)
  * [#7756](https://github.com/bitcoin/bitcoin/pull/7756) [`9e47fce`](https://github.com/bitcoin/bitcoin/commit/9e47fce) Add cursor to iterate over utxo set, use this in `gettxoutsetinfo` (laanwj)
  * [#7848](https://github.com/bitcoin/bitcoin/pull/7848) [`88616d2`](https://github.com/bitcoin/bitcoin/commit/88616d2) Divergence between 32- and 64-bit when hashing >4GB affects `gettxoutsetinfo` (laanwj)
  * [#7827](https://github.com/bitcoin/bitcoin/pull/7827) [`4205ad7`](https://github.com/bitcoin/bitcoin/commit/4205ad7) Speed up `getchaintips` (mrbandrews)
  * [#7762](https://github.com/bitcoin/bitcoin/pull/7762) [`a1eb344`](https://github.com/bitcoin/bitcoin/commit/a1eb344) Append a message sequence number to every ZMQ notification (jonasschnelli)
  * [#7688](https://github.com/bitcoin/bitcoin/pull/7688) [`46880ed`](https://github.com/bitcoin/bitcoin/commit/46880ed) List solvability in listunspent output and improve help (sipa)
  * [#7926](https://github.com/bitcoin/bitcoin/pull/7926) [`5725807`](https://github.com/bitcoin/bitcoin/commit/5725807) Push back `getaddednodeinfo` dead value (instagibbs)
  * [#7953](https://github.com/bitcoin/bitcoin/pull/7953) [`0630353`](https://github.com/bitcoin/bitcoin/commit/0630353) Create `signmessagewithprivkey` rpc (achow101)
  * [#8049](https://github.com/bitcoin/bitcoin/pull/8049) [`c028c7b`](https://github.com/bitcoin/bitcoin/commit/c028c7b) Expose information on whether transaction relay is enabled in `getnetworkinfo` (laanwj)
  * [#7967](https://github.com/bitcoin/bitcoin/pull/7967) [`8c1e49b`](https://github.com/bitcoin/bitcoin/commit/8c1e49b) Add feerate option to `fundrawtransaction` (jonasschnelli)
  * [#8118](https://github.com/bitcoin/bitcoin/pull/8118) [`9b6a48c`](https://github.com/bitcoin/bitcoin/commit/9b6a48c) Reduce unnecessary hashing in `signrawtransaction` (jonasnick)
  * [#7957](https://github.com/bitcoin/bitcoin/pull/7957) [`79004d4`](https://github.com/bitcoin/bitcoin/commit/79004d4) Add support for transaction sequence number (jonasschnelli)
  * [#8153](https://github.com/bitcoin/bitcoin/pull/8153) [`75ec320`](https://github.com/bitcoin/bitcoin/commit/75ec320) `fundrawtransaction` feeRate: Use BTC/kB (MarcoFalke)
  * [#7292](https://github.com/bitcoin/bitcoin/pull/7292) [`7ce9ac5`](https://github.com/bitcoin/bitcoin/commit/7ce9ac5) Expose ancestor/descendant information over RPC (sdaftuar)
  * [#8171](https://github.com/bitcoin/bitcoin/pull/8171) [`62fcf27`](https://github.com/bitcoin/bitcoin/commit/62fcf27) Fix createrawtx sequence number unsigned int parsing (jonasschnelli)
  * [#7892](https://github.com/bitcoin/bitcoin/pull/7892) [`9c3d0fa`](https://github.com/bitcoin/bitcoin/commit/9c3d0fa) Add full UTF-8 support to RPC (laanwj)
  * [#8317](https://github.com/bitcoin/bitcoin/pull/8317) [`304eff3`](https://github.com/bitcoin/bitcoin/commit/304eff3) Donât use floating point in rpcwallet (MarcoFalke)
  * [#8258](https://github.com/bitcoin/bitcoin/pull/8258) [`5a06ebb`](https://github.com/bitcoin/bitcoin/commit/5a06ebb) Hide softfork in `getblockchaininfo` if timeout is 0 (jl2012)
  * [#8244](https://github.com/bitcoin/bitcoin/pull/8244) [`1922e5a`](https://github.com/bitcoin/bitcoin/commit/1922e5a) Remove unnecessary LOCK(cs_main) in getrawmempool (dcousens)

### Block and transaction handling

  * [#7056](https://github.com/bitcoin/bitcoin/pull/7056) [`6a07208`](https://github.com/bitcoin/bitcoin/commit/6a07208) Save last db read (morcos)
  * [#6842](https://github.com/bitcoin/bitcoin/pull/6842) [`0192806`](https://github.com/bitcoin/bitcoin/commit/0192806) Limitfreerelay edge case bugfix (ptschip)
  * [#7084](https://github.com/bitcoin/bitcoin/pull/7084) [`11d74f6`](https://github.com/bitcoin/bitcoin/commit/11d74f6) Replace maxFeeRate of 10000*minRelayTxFee with maxTxFee in mempool (MarcoFalke)
  * [#7539](https://github.com/bitcoin/bitcoin/pull/7539) [`9f33dba`](https://github.com/bitcoin/bitcoin/commit/9f33dba) Add tags to mempoolâs mapTx indices (sdaftuar)
  * [#7592](https://github.com/bitcoin/bitcoin/pull/7592) [`26a2a72`](https://github.com/bitcoin/bitcoin/commit/26a2a72) Re-remove ERROR logging for mempool rejects (laanwj)
  * [#7187](https://github.com/bitcoin/bitcoin/pull/7187) [`14d6324`](https://github.com/bitcoin/bitcoin/commit/14d6324) Keep reorgs fast for SequenceLocks checks (morcos)
  * [#7594](https://github.com/bitcoin/bitcoin/pull/7594) [`01f4267`](https://github.com/bitcoin/bitcoin/commit/01f4267) Mempool: Add tracking of ancestor packages (sdaftuar)
  * [#7904](https://github.com/bitcoin/bitcoin/pull/7904) [`fc9e334`](https://github.com/bitcoin/bitcoin/commit/fc9e334) Txdb: Fix assert crash in new UTXO set cursor (laanwj)
  * [#7927](https://github.com/bitcoin/bitcoin/pull/7927) [`f9c2ac7`](https://github.com/bitcoin/bitcoin/commit/f9c2ac7) Minor changes to dbwrapper to simplify support for other databases (laanwj)
  * [#7933](https://github.com/bitcoin/bitcoin/pull/7933) [`e26b620`](https://github.com/bitcoin/bitcoin/commit/e26b620) Fix OOM when deserializing UTXO entries with invalid length (sipa)
  * [#8020](https://github.com/bitcoin/bitcoin/pull/8020) [`5e374f7`](https://github.com/bitcoin/bitcoin/commit/5e374f7) Use SipHash-2-4 for various non-cryptographic hashes (sipa)
  * [#8076](https://github.com/bitcoin/bitcoin/pull/8076) [`d720980`](https://github.com/bitcoin/bitcoin/commit/d720980) VerifyDB: donât check blocks that have been pruned (sdaftuar)
  * [#8080](https://github.com/bitcoin/bitcoin/pull/8080) [`862fd24`](https://github.com/bitcoin/bitcoin/commit/862fd24) Do not use mempool for GETDATA for tx accepted after the last mempool req (gmaxwell)
  * [#7997](https://github.com/bitcoin/bitcoin/pull/7997) [`a82f033`](https://github.com/bitcoin/bitcoin/commit/a82f033) Replace mapNextTx with slimmer setSpends (kazcw)
  * [#8220](https://github.com/bitcoin/bitcoin/pull/8220) [`1f86d64`](https://github.com/bitcoin/bitcoin/commit/1f86d64) Stop trimming when mapTx is empty (sipa)
  * [#8273](https://github.com/bitcoin/bitcoin/pull/8273) [`396f9d6`](https://github.com/bitcoin/bitcoin/commit/396f9d6) Bump `-dbcache` default to 300MiB (laanwj)
  * [#7225](https://github.com/bitcoin/bitcoin/pull/7225) [`eb33179`](https://github.com/bitcoin/bitcoin/commit/eb33179) Eliminate unnecessary call to CheckBlock (sdaftuar)
  * [#7907](https://github.com/bitcoin/bitcoin/pull/7907) [`006cdf6`](https://github.com/bitcoin/bitcoin/commit/006cdf6) Optimize and Cleanup CScript::FindAndDelete (pstratem)
  * [#7917](https://github.com/bitcoin/bitcoin/pull/7917) [`239d419`](https://github.com/bitcoin/bitcoin/commit/239d419) Optimize reindex (sipa)
  * [#7763](https://github.com/bitcoin/bitcoin/pull/7763) [`3081fb9`](https://github.com/bitcoin/bitcoin/commit/3081fb9) Put hex-encoded version in UpdateTip (sipa)
  * [#8149](https://github.com/bitcoin/bitcoin/pull/8149) [`d612837`](https://github.com/bitcoin/bitcoin/commit/d612837) Testnet-only segregated witness (sipa)
  * [#8305](https://github.com/bitcoin/bitcoin/pull/8305) [`3730393`](https://github.com/bitcoin/bitcoin/commit/3730393) Improve handling of unconnecting headers (sdaftuar)
  * [#8363](https://github.com/bitcoin/bitcoin/pull/8363) [`fca1a41`](https://github.com/bitcoin/bitcoin/commit/fca1a41) Rename âblock costâ to âblock weightâ (sdaftuar)
  * [#8381](https://github.com/bitcoin/bitcoin/pull/8381) [`f84ee3d`](https://github.com/bitcoin/bitcoin/commit/f84ee3d) Make witness v0 outputs non-standard (jl2012)
  * [#8364](https://github.com/bitcoin/bitcoin/pull/8364) [`3f65ba2`](https://github.com/bitcoin/bitcoin/commit/3f65ba2) Treat high-sigop transactions as larger rather than rejecting them (sipa)

### P2P protocol and network code

  * [#6589](https://github.com/bitcoin/bitcoin/pull/6589) [`dc0305d`](https://github.com/bitcoin/bitcoin/commit/dc0305d) Log bytes recv/sent per command (jonasschnelli)
  * [#7164](https://github.com/bitcoin/bitcoin/pull/7164) [`3b43cad`](https://github.com/bitcoin/bitcoin/commit/3b43cad) Do not download transactions during initial blockchain sync (ptschip)
  * [#7458](https://github.com/bitcoin/bitcoin/pull/7458) [`898fedf`](https://github.com/bitcoin/bitcoin/commit/898fedf) peers.dat, banlist.dat recreated when missing (kirkalx)
  * [#7637](https://github.com/bitcoin/bitcoin/pull/7637) [`3da5d1b`](https://github.com/bitcoin/bitcoin/commit/3da5d1b) Fix memleak in TorController (laanwj, jonasschnelli)
  * [#7553](https://github.com/bitcoin/bitcoin/pull/7553) [`9f14e5a`](https://github.com/bitcoin/bitcoin/commit/9f14e5a) Remove vfReachable and modify IsReachable to only use vfLimited (pstratem)
  * [#7708](https://github.com/bitcoin/bitcoin/pull/7708) [`9426632`](https://github.com/bitcoin/bitcoin/commit/9426632) De-neuter NODE_BLOOM (pstratem)
  * [#7692](https://github.com/bitcoin/bitcoin/pull/7692) [`29b2be6`](https://github.com/bitcoin/bitcoin/commit/29b2be6) Remove P2P alert system (btcdrak)
  * [#7542](https://github.com/bitcoin/bitcoin/pull/7542) [`c946a15`](https://github.com/bitcoin/bitcoin/commit/c946a15) Implement âfeefilterâ P2P message (morcos)
  * [#7573](https://github.com/bitcoin/bitcoin/pull/7573) [`352fd57`](https://github.com/bitcoin/bitcoin/commit/352fd57) Add `-maxtimeadjustment` command line option (mruddy)
  * [#7570](https://github.com/bitcoin/bitcoin/pull/7570) [`232592a`](https://github.com/bitcoin/bitcoin/commit/232592a) Add IPv6 Link-Local Address Support (mruddy)
  * [#7874](https://github.com/bitcoin/bitcoin/pull/7874) [`e6a4d48`](https://github.com/bitcoin/bitcoin/commit/e6a4d48) Improve AlreadyHave (morcos)
  * [#7856](https://github.com/bitcoin/bitcoin/pull/7856) [`64e71b3`](https://github.com/bitcoin/bitcoin/commit/64e71b3) Only send one GetAddr response per connection (gmaxwell)
  * [#7868](https://github.com/bitcoin/bitcoin/pull/7868) [`7daa3ad`](https://github.com/bitcoin/bitcoin/commit/7daa3ad) Split DNS resolving functionality out of net structures (theuni)
  * [#7919](https://github.com/bitcoin/bitcoin/pull/7919) [`7617682`](https://github.com/bitcoin/bitcoin/commit/7617682) Fix headers announcements edge case (sdaftuar)
  * [#7514](https://github.com/bitcoin/bitcoin/pull/7514) [`d9594bf`](https://github.com/bitcoin/bitcoin/commit/d9594bf) Fix IsInitialBlockDownload for testnet (jmacwhyte)
  * [#7959](https://github.com/bitcoin/bitcoin/pull/7959) [`03cf6e8`](https://github.com/bitcoin/bitcoin/commit/03cf6e8) fix race that could fail to persist a ban (kazcw)
  * [#7840](https://github.com/bitcoin/bitcoin/pull/7840) [`3b9a0bf`](https://github.com/bitcoin/bitcoin/commit/3b9a0bf) Several performance and privacy improvements to inv/mempool handling (sipa)
  * [#8011](https://github.com/bitcoin/bitcoin/pull/8011) [`65aecda`](https://github.com/bitcoin/bitcoin/commit/65aecda) Donât run ThreadMessageHandler at lowered priority (kazcw)
  * [#7696](https://github.com/bitcoin/bitcoin/pull/7696) [`5c3f8dd`](https://github.com/bitcoin/bitcoin/commit/5c3f8dd) Fix de-serialization bug where AddrMan is left corrupted (EthanHeilman)
  * [#7932](https://github.com/bitcoin/bitcoin/pull/7932) [`ed749bd`](https://github.com/bitcoin/bitcoin/commit/ed749bd) CAddrMan::Deserialize handle corrupt serializations better (pstratem)
  * [#7906](https://github.com/bitcoin/bitcoin/pull/7906) [`83121cc`](https://github.com/bitcoin/bitcoin/commit/83121cc) Prerequisites for p2p encapsulation changes (theuni)
  * [#8033](https://github.com/bitcoin/bitcoin/pull/8033) [`18436d8`](https://github.com/bitcoin/bitcoin/commit/18436d8) Fix Socks5() connect failures to be less noisy and less unnecessarily scary (wtogami)
  * [#8082](https://github.com/bitcoin/bitcoin/pull/8082) [`01d8359`](https://github.com/bitcoin/bitcoin/commit/01d8359) Defer inserting into maprelay until just before relaying (gmaxwell)
  * [#7960](https://github.com/bitcoin/bitcoin/pull/7960) [`6a22373`](https://github.com/bitcoin/bitcoin/commit/6a22373) Only use AddInventoryKnown for transactions (sdaftuar)
  * [#8078](https://github.com/bitcoin/bitcoin/pull/8078) [`2156fa2`](https://github.com/bitcoin/bitcoin/commit/2156fa2) Disable the mempool P2P command when bloom filters disabled (petertodd)
  * [#8065](https://github.com/bitcoin/bitcoin/pull/8065) [`67c91f8`](https://github.com/bitcoin/bitcoin/commit/67c91f8) Addrman offline attempts (gmaxwell)
  * [#7703](https://github.com/bitcoin/bitcoin/pull/7703) [`761cddb`](https://github.com/bitcoin/bitcoin/commit/761cddb) Tor: Change auth order to only use password auth if -torpassword (laanwj)
  * [#8083](https://github.com/bitcoin/bitcoin/pull/8083) [`cd0c513`](https://github.com/bitcoin/bitcoin/commit/cd0c513) Add support for dnsseeds with option to filter by servicebits (jonasschnelli)
  * [#8173](https://github.com/bitcoin/bitcoin/pull/8173) [`4286f43`](https://github.com/bitcoin/bitcoin/commit/4286f43) Use SipHash for node eviction (sipa)
  * [#8154](https://github.com/bitcoin/bitcoin/pull/8154) [`1445835`](https://github.com/bitcoin/bitcoin/commit/1445835) Drop vAddrToSend after sending big addr message (kazcw)
  * [#7749](https://github.com/bitcoin/bitcoin/pull/7749) [`be9711e`](https://github.com/bitcoin/bitcoin/commit/be9711e) Enforce expected outbound services (sipa)
  * [#8208](https://github.com/bitcoin/bitcoin/pull/8208) [`0a64777`](https://github.com/bitcoin/bitcoin/commit/0a64777) Do not set extra flags for unfiltered DNS seed results (sipa)
  * [#8084](https://github.com/bitcoin/bitcoin/pull/8084) [`e4bb4a8`](https://github.com/bitcoin/bitcoin/commit/e4bb4a8) Add recently accepted blocks and txn to AttemptToEvictConnection (gmaxwell)
  * [#8113](https://github.com/bitcoin/bitcoin/pull/8113) [`3f89a53`](https://github.com/bitcoin/bitcoin/commit/3f89a53) Rework addnode behaviour (sipa)
  * [#8179](https://github.com/bitcoin/bitcoin/pull/8179) [`94ab58b`](https://github.com/bitcoin/bitcoin/commit/94ab58b) Evict orphans which are included or precluded by accepted blocks (gmaxwell)
  * [#8068](https://github.com/bitcoin/bitcoin/pull/8068) [`e9d76a1`](https://github.com/bitcoin/bitcoin/commit/e9d76a1) Compact Blocks (TheBlueMatt)
  * [#8204](https://github.com/bitcoin/bitcoin/pull/8204) [`0833894`](https://github.com/bitcoin/bitcoin/commit/0833894) Update petertoddâs testnet seed (petertodd)
  * [#8247](https://github.com/bitcoin/bitcoin/pull/8247) [`5cd35d3`](https://github.com/bitcoin/bitcoin/commit/5cd35d3) Mark my dnsseed as supporting filtering (sipa)
  * [#8275](https://github.com/bitcoin/bitcoin/pull/8275) [`042c323`](https://github.com/bitcoin/bitcoin/commit/042c323) Remove bad chain alert partition check (btcdrak)
  * [#8271](https://github.com/bitcoin/bitcoin/pull/8271) [`1bc9c80`](https://github.com/bitcoin/bitcoin/commit/1bc9c80) Do not send witnesses in cmpctblock (sipa)
  * [#8312](https://github.com/bitcoin/bitcoin/pull/8312) [`ca40ef6`](https://github.com/bitcoin/bitcoin/commit/ca40ef6) Fix mempool DoS vulnerability from malleated transactions (sdaftuar)
  * [#7180](https://github.com/bitcoin/bitcoin/pull/7180) [`16ccb74`](https://github.com/bitcoin/bitcoin/commit/16ccb74) Account for `sendheaders` `verack` messages (laanwj)
  * [#8102](https://github.com/bitcoin/bitcoin/pull/8102) [`425278d`](https://github.com/bitcoin/bitcoin/commit/425278d) Bugfix: use global ::fRelayTxes instead of CNode in version send (sipa)
  * [#8408](https://github.com/bitcoin/bitcoin/pull/8408) [`b7e2011`](https://github.com/bitcoin/bitcoin/commit/b7e2011) Prevent fingerprinting, disk-DoS with compact blocks (sdaftuar)

### Build system

  * [#7302](https://github.com/bitcoin/bitcoin/pull/7302) [`41f1a3e`](https://github.com/bitcoin/bitcoin/commit/41f1a3e) C++11 build/runtime fixes (theuni)
  * [#7322](https://github.com/bitcoin/bitcoin/pull/7322) [`fd9356b`](https://github.com/bitcoin/bitcoin/commit/fd9356b) c++11: add scoped enum fallbacks to CPPFLAGS rather than defining them locally (theuni)
  * [#7441](https://github.com/bitcoin/bitcoin/pull/7441) [`a6771fc`](https://github.com/bitcoin/bitcoin/commit/a6771fc) Use Debian 8.3 in gitian build guide (fanquake)
  * [#7349](https://github.com/bitcoin/bitcoin/pull/7349) [`152a821`](https://github.com/bitcoin/bitcoin/commit/152a821) Build against system UniValue when available (luke-jr)
  * [#7520](https://github.com/bitcoin/bitcoin/pull/7520) [`621940e`](https://github.com/bitcoin/bitcoin/commit/621940e) LibreSSL doesnât define OPENSSL_VERSION, use LIBRESSL_VERSION_TEXT instead (paveljanik)
  * [#7528](https://github.com/bitcoin/bitcoin/pull/7528) [`9b9bfce`](https://github.com/bitcoin/bitcoin/commit/9b9bfce) autogen.sh: warn about needing autoconf if autoreconf is not found (knocte)
  * [#7504](https://github.com/bitcoin/bitcoin/pull/7504) [`19324cf`](https://github.com/bitcoin/bitcoin/commit/19324cf) Crystal clean make clean (paveljanik)
  * [#7619](https://github.com/bitcoin/bitcoin/pull/7619) [`18b3f1b`](https://github.com/bitcoin/bitcoin/commit/18b3f1b) Add missing sudo entry in gitian VM setup (btcdrak)
  * [#7616](https://github.com/bitcoin/bitcoin/pull/7616) [`639ec58`](https://github.com/bitcoin/bitcoin/commit/639ec58) [depends] Delete unused patches (MarcoFalke)
  * [#7658](https://github.com/bitcoin/bitcoin/pull/7658) [`c15eb28`](https://github.com/bitcoin/bitcoin/commit/c15eb28) Add curl to Gitian setup instructions (btcdrak)
  * [#7710](https://github.com/bitcoin/bitcoin/pull/7710) [`909b72b`](https://github.com/bitcoin/bitcoin/commit/909b72b) [Depends] Bump miniupnpc and config.guess+sub (fanquake)
  * [#7723](https://github.com/bitcoin/bitcoin/pull/7723) [`5131005`](https://github.com/bitcoin/bitcoin/commit/5131005) build: python 3 compatibility (laanwj)
  * [#7477](https://github.com/bitcoin/bitcoin/pull/7477) [`28ad4d9`](https://github.com/bitcoin/bitcoin/commit/28ad4d9) Fix quoting of copyright holders in configure.ac (domob1812)
  * [#7711](https://github.com/bitcoin/bitcoin/pull/7711) [`a67bc5e`](https://github.com/bitcoin/bitcoin/commit/a67bc5e) [build-aux] Update Boost & check macros to latest serials (fanquake)
  * [#7788](https://github.com/bitcoin/bitcoin/pull/7788) [`4dc1b3a`](https://github.com/bitcoin/bitcoin/commit/4dc1b3a) Use relative paths instead of absolute paths in protoc calls (paveljanik)
  * [#7809](https://github.com/bitcoin/bitcoin/pull/7809) [`bbd210d`](https://github.com/bitcoin/bitcoin/commit/bbd210d) depends: some base fixes/changes (theuni)
  * [#7603](https://github.com/bitcoin/bitcoin/pull/7603) [`73fc922`](https://github.com/bitcoin/bitcoin/commit/73fc922) Build System: Use PACKAGE_TARNAME in NSIS script (JeremyRand)
  * [#7905](https://github.com/bitcoin/bitcoin/pull/7905) [`187186b`](https://github.com/bitcoin/bitcoin/commit/187186b) test: move accounting_tests and rpc_wallet_tests to wallet/test (laanwj)
  * [#7911](https://github.com/bitcoin/bitcoin/pull/7911) [`351abf9`](https://github.com/bitcoin/bitcoin/commit/351abf9) leveldb: integrate leveldb into our buildsystem (theuni)
  * [#7944](https://github.com/bitcoin/bitcoin/pull/7944) [`a407807`](https://github.com/bitcoin/bitcoin/commit/a407807) Re-instate TARGET_OS=linux in configure.ac. Removed by 351abf9e035 (randy-waterhouse)
  * [#7920](https://github.com/bitcoin/bitcoin/pull/7920) [`c3e3cfb`](https://github.com/bitcoin/bitcoin/commit/c3e3cfb) Switch Travis to Trusty (theuni)
  * [#7954](https://github.com/bitcoin/bitcoin/pull/7954) [`08b37c5`](https://github.com/bitcoin/bitcoin/commit/08b37c5) build: quiet annoying warnings without adding new ones (theuni)
  * [#7165](https://github.com/bitcoin/bitcoin/pull/7165) [`06162f1`](https://github.com/bitcoin/bitcoin/commit/06162f1) build: Enable C++11 in build, require C++11 compiler (laanwj)
  * [#7982](https://github.com/bitcoin/bitcoin/pull/7982) [`559fbae`](https://github.com/bitcoin/bitcoin/commit/559fbae) build: No need to check for leveldb atomics (theuni)
  * [#8002](https://github.com/bitcoin/bitcoin/pull/8002) [`f9b4582`](https://github.com/bitcoin/bitcoin/commit/f9b4582) [depends] Add -stdlib=libc++ to darwin CXX flags (fanquake)
  * [#7993](https://github.com/bitcoin/bitcoin/pull/7993) [`6a034ed`](https://github.com/bitcoin/bitcoin/commit/6a034ed) [depends] Bump Freetype, ccache, ZeroMQ, miniupnpc, expat (fanquake)
  * [#8167](https://github.com/bitcoin/bitcoin/pull/8167) [`19ea173`](https://github.com/bitcoin/bitcoin/commit/19ea173) Ship debug tarballs/zips with debug symbols (theuni)
  * [#8175](https://github.com/bitcoin/bitcoin/pull/8175) [`f0299d8`](https://github.com/bitcoin/bitcoin/commit/f0299d8) Add âdisable-bench to config flags for windows (laanwj)
  * [#7283](https://github.com/bitcoin/bitcoin/pull/7283) [`fd9881a`](https://github.com/bitcoin/bitcoin/commit/fd9881a) [gitian] Default reference_datetime to commit author date (MarcoFalke)
  * [#8181](https://github.com/bitcoin/bitcoin/pull/8181) [`9201ce8`](https://github.com/bitcoin/bitcoin/commit/9201ce8) Get rid of `CLIENT_DATE` (laanwj)
  * [#8133](https://github.com/bitcoin/bitcoin/pull/8133) [`fde0ac4`](https://github.com/bitcoin/bitcoin/commit/fde0ac4) Finish up out-of-tree changes (theuni)
  * [#8188](https://github.com/bitcoin/bitcoin/pull/8188) [`65a9d7d`](https://github.com/bitcoin/bitcoin/commit/65a9d7d) Add armhf/aarch64 gitian builds (theuni)
  * [#8194](https://github.com/bitcoin/bitcoin/pull/8194) [`cca1c8c`](https://github.com/bitcoin/bitcoin/commit/cca1c8c) [gitian] set correct PATH for wrappers (MarcoFalke)
  * [#8198](https://github.com/bitcoin/bitcoin/pull/8198) [`5201614`](https://github.com/bitcoin/bitcoin/commit/5201614) Sync ax_pthread with upstream draft4 (fanquake)
  * [#8210](https://github.com/bitcoin/bitcoin/pull/8210) [`12a541e`](https://github.com/bitcoin/bitcoin/commit/12a541e) [Qt] Bump to Qt5.6.1 (jonasschnelli)
  * [#8285](https://github.com/bitcoin/bitcoin/pull/8285) [`da50997`](https://github.com/bitcoin/bitcoin/commit/da50997) windows: Add testnet link to installer (laanwj)
  * [#8304](https://github.com/bitcoin/bitcoin/pull/8304) [`0cca2fe`](https://github.com/bitcoin/bitcoin/commit/0cca2fe) [travis] Update SDK_URL (MarcoFalke)
  * [#8310](https://github.com/bitcoin/bitcoin/pull/8310) [`6ae20df`](https://github.com/bitcoin/bitcoin/commit/6ae20df) Require boost for bench (theuni)
  * [#8315](https://github.com/bitcoin/bitcoin/pull/8315) [`2e51590`](https://github.com/bitcoin/bitcoin/commit/2e51590) Donât require sudo for Linux (theuni)
  * [#8314](https://github.com/bitcoin/bitcoin/pull/8314) [`67caef6`](https://github.com/bitcoin/bitcoin/commit/67caef6) Fix pkg-config issues for 0.13 (theuni)
  * [#8373](https://github.com/bitcoin/bitcoin/pull/8373) [`1fe7f40`](https://github.com/bitcoin/bitcoin/commit/1fe7f40) Fix OSX non-deterministic dmg (theuni)
  * [#8358](https://github.com/bitcoin/bitcoin/pull/8358) [`cfd1280`](https://github.com/bitcoin/bitcoin/commit/cfd1280) Gbuild: Set memory explicitly (default is too low) (MarcoFalke)

### GUI

  * [#7154](https://github.com/bitcoin/bitcoin/pull/7154) [`00b4b8d`](https://github.com/bitcoin/bitcoin/commit/00b4b8d) Add InMempool() info to transaction details (jonasschnelli)
  * [#7068](https://github.com/bitcoin/bitcoin/pull/7068) [`5f3c670`](https://github.com/bitcoin/bitcoin/commit/5f3c670) [RPC-Tests] add simple way to run rpc test over QT clients (jonasschnelli)
  * [#7218](https://github.com/bitcoin/bitcoin/pull/7218) [`a1c185b`](https://github.com/bitcoin/bitcoin/commit/a1c185b) Fix misleading translation (MarcoFalke)
  * [#7214](https://github.com/bitcoin/bitcoin/pull/7214) [`be9a9a3`](https://github.com/bitcoin/bitcoin/commit/be9a9a3) qt5: Use the fixed font the system recommends (MarcoFalke)
  * [#7256](https://github.com/bitcoin/bitcoin/pull/7256) [`08ab906`](https://github.com/bitcoin/bitcoin/commit/08ab906) Add note to coin control dialog QT5 workaround (fanquake)
  * [#7255](https://github.com/bitcoin/bitcoin/pull/7255) [`e289807`](https://github.com/bitcoin/bitcoin/commit/e289807) Replace some instances of formatWithUnit with formatHtmlWithUnit (fanquake)
  * [#7317](https://github.com/bitcoin/bitcoin/pull/7317) [`3b57e9c`](https://github.com/bitcoin/bitcoin/commit/3b57e9c) Fix RPCTimerInterface ordering issue (jonasschnelli)
  * [#7327](https://github.com/bitcoin/bitcoin/pull/7327) [`c079d79`](https://github.com/bitcoin/bitcoin/commit/c079d79) Transaction View: LastMonth calculation fixed (crowning-)
  * [#7334](https://github.com/bitcoin/bitcoin/pull/7334) [`e1060c5`](https://github.com/bitcoin/bitcoin/commit/e1060c5) coincontrol workaround is still needed in qt5.4 (fixed in qt5.5) (MarcoFalke)
  * [#7383](https://github.com/bitcoin/bitcoin/pull/7383) [`ae2db67`](https://github.com/bitcoin/bitcoin/commit/ae2db67) Rename âamountâ to ârequested amountâ in receive coins table (jonasschnelli)
  * [#7396](https://github.com/bitcoin/bitcoin/pull/7396) [`cdcbc59`](https://github.com/bitcoin/bitcoin/commit/cdcbc59) Add option to increase/decrease font size in the console window (jonasschnelli)
  * [#7437](https://github.com/bitcoin/bitcoin/pull/7437) [`9645218`](https://github.com/bitcoin/bitcoin/commit/9645218) Disable tab navigation for peers tables (Kefkius)
  * [#7604](https://github.com/bitcoin/bitcoin/pull/7604) [`354b03d`](https://github.com/bitcoin/bitcoin/commit/354b03d) build: Remove spurious dollar sign. Fixes [#7189](https://github.com/bitcoin/bitcoin/pull/7189) (dooglus)
  * [#7605](https://github.com/bitcoin/bitcoin/pull/7605) [`7f001bd`](https://github.com/bitcoin/bitcoin/commit/7f001bd) Remove openssl info from init/log and from Qt debug window (jonasschnelli)
  * [#7628](https://github.com/bitcoin/bitcoin/pull/7628) [`87d6562`](https://github.com/bitcoin/bitcoin/commit/87d6562) Add âcopy full transaction detailsâ option (ericshawlinux)
  * [#7613](https://github.com/bitcoin/bitcoin/pull/7613) [`3798e5d`](https://github.com/bitcoin/bitcoin/commit/3798e5d) Add autocomplete to bitcoin-qtâs console window (GamerSg)
  * [#7668](https://github.com/bitcoin/bitcoin/pull/7668) [`b24266c`](https://github.com/bitcoin/bitcoin/commit/b24266c) Fix history deletion bug after font size change (achow101)
  * [#7680](https://github.com/bitcoin/bitcoin/pull/7680) [`41d2dfa`](https://github.com/bitcoin/bitcoin/commit/41d2dfa) Remove reflection from `about` icon (laanwj)
  * [#7686](https://github.com/bitcoin/bitcoin/pull/7686) [`f034bce`](https://github.com/bitcoin/bitcoin/commit/f034bce) Remove 0-fee from send dialog (MarcoFalke)
  * [#7506](https://github.com/bitcoin/bitcoin/pull/7506) [`b88e0b0`](https://github.com/bitcoin/bitcoin/commit/b88e0b0) Use CCoinControl selection in CWallet::FundTransaction (promag)
  * [#7732](https://github.com/bitcoin/bitcoin/pull/7732) [`0b98dd7`](https://github.com/bitcoin/bitcoin/commit/0b98dd7) Debug window: replace âBuild dateâ with âDatadirâ (jonasschnelli)
  * [#7761](https://github.com/bitcoin/bitcoin/pull/7761) [`60db51d`](https://github.com/bitcoin/bitcoin/commit/60db51d) remove trailing output-index from transaction-id (jonasschnelli)
  * [#7772](https://github.com/bitcoin/bitcoin/pull/7772) [`6383268`](https://github.com/bitcoin/bitcoin/commit/6383268) Clear the input line after activating autocomplete (paveljanik)
  * [#7925](https://github.com/bitcoin/bitcoin/pull/7925) [`f604bf6`](https://github.com/bitcoin/bitcoin/commit/f604bf6) Fix out-of-tree GUI builds (laanwj)
  * [#7939](https://github.com/bitcoin/bitcoin/pull/7939) [`574ddc6`](https://github.com/bitcoin/bitcoin/commit/574ddc6) Make it possible to show details for multiple transactions (laanwj)
  * [#8012](https://github.com/bitcoin/bitcoin/pull/8012) [`b33824b`](https://github.com/bitcoin/bitcoin/commit/b33824b) Delay user confirmation of send (Tyler-Hardin)
  * [#8006](https://github.com/bitcoin/bitcoin/pull/8006) [`7c8558d`](https://github.com/bitcoin/bitcoin/commit/7c8558d) Add option to disable the system tray icon (Tyler-Hardin)
  * [#8046](https://github.com/bitcoin/bitcoin/pull/8046) [`169d379`](https://github.com/bitcoin/bitcoin/commit/169d379) Fix Cmd-Q / Menu Quit shutdown on OSX (jonasschnelli)
  * [#8042](https://github.com/bitcoin/bitcoin/pull/8042) [`6929711`](https://github.com/bitcoin/bitcoin/commit/6929711) Donât allow to open the debug window during splashscreen & verification state (jonasschnelli)
  * [#8014](https://github.com/bitcoin/bitcoin/pull/8014) [`77b49ac`](https://github.com/bitcoin/bitcoin/commit/77b49ac) Sort transactions by date (Tyler-Hardin)
  * [#8073](https://github.com/bitcoin/bitcoin/pull/8073) [`eb2f6f7`](https://github.com/bitcoin/bitcoin/commit/eb2f6f7) askpassphrasedialog: Clear pass fields on accept (rat4)
  * [#8129](https://github.com/bitcoin/bitcoin/pull/8129) [`ee1533e`](https://github.com/bitcoin/bitcoin/commit/ee1533e) Fix RPC console auto completer (UdjinM6)
  * [#7636](https://github.com/bitcoin/bitcoin/pull/7636) [`fb0ac48`](https://github.com/bitcoin/bitcoin/commit/fb0ac48) Add bitcoin address label to request payment QR code (makevoid)
  * [#8231](https://github.com/bitcoin/bitcoin/pull/8231) [`760a6c7`](https://github.com/bitcoin/bitcoin/commit/760a6c7) Fix a bug where the SplashScreen will not be hidden during startup (jonasschnelli)
  * [#8256](https://github.com/bitcoin/bitcoin/pull/8256) [`af2421c`](https://github.com/bitcoin/bitcoin/commit/af2421c) BUG: bitcoin-qt crash (fsb4000)
  * [#8257](https://github.com/bitcoin/bitcoin/pull/8257) [`ff03c50`](https://github.com/bitcoin/bitcoin/commit/ff03c50) Do not ask a UI question from bitcoind (sipa)
  * [#8288](https://github.com/bitcoin/bitcoin/pull/8288) [`91abb77`](https://github.com/bitcoin/bitcoin/commit/91abb77) Network-specific example address (laanwj)
  * [#7707](https://github.com/bitcoin/bitcoin/pull/7707) [`a914968`](https://github.com/bitcoin/bitcoin/commit/a914968) UI support for abandoned transactions (jonasschnelli)
  * [#8207](https://github.com/bitcoin/bitcoin/pull/8207) [`f7a403b`](https://github.com/bitcoin/bitcoin/commit/f7a403b) Add a link to the Bitcoin-Core repository and website to the About Dialog (MarcoFalke)
  * [#8281](https://github.com/bitcoin/bitcoin/pull/8281) [`6a87eb0`](https://github.com/bitcoin/bitcoin/commit/6a87eb0) Remove client name from debug window (laanwj)
  * [#8407](https://github.com/bitcoin/bitcoin/pull/8407) [`45eba4b`](https://github.com/bitcoin/bitcoin/commit/45eba4b) Add dbcache migration path (jonasschnelli)

### Wallet

  * [#7262](https://github.com/bitcoin/bitcoin/pull/7262) [`fc08994`](https://github.com/bitcoin/bitcoin/commit/fc08994) Reduce inefficiency of GetAccountAddress() (dooglus)
  * [#7537](https://github.com/bitcoin/bitcoin/pull/7537) [`78e81b0`](https://github.com/bitcoin/bitcoin/commit/78e81b0) Warn on unexpected EOF while salvaging wallet (laanwj)
  * [#7521](https://github.com/bitcoin/bitcoin/pull/7521) [`3368895`](https://github.com/bitcoin/bitcoin/commit/3368895) Donât resend wallet txs that arenât in our own mempool (morcos)
  * [#7576](https://github.com/bitcoin/bitcoin/pull/7576) [`86a1ec5`](https://github.com/bitcoin/bitcoin/commit/86a1ec5) Move wallet help string creation to CWallet (jonasschnelli)
  * [#7577](https://github.com/bitcoin/bitcoin/pull/7577) [`5b3b5a7`](https://github.com/bitcoin/bitcoin/commit/5b3b5a7) Move âload wallet phaseâ to CWallet (jonasschnelli)
  * [#7608](https://github.com/bitcoin/bitcoin/pull/7608) [`0735c0c`](https://github.com/bitcoin/bitcoin/commit/0735c0c) Move hardcoded file name out of log messages (MarcoFalke)
  * [#7649](https://github.com/bitcoin/bitcoin/pull/7649) [`4900641`](https://github.com/bitcoin/bitcoin/commit/4900641) Prevent multiple calls to CWallet::AvailableCoins (promag)
  * [#7646](https://github.com/bitcoin/bitcoin/pull/7646) [`e5c3511`](https://github.com/bitcoin/bitcoin/commit/e5c3511) Fix lockunspent help message (promag)
  * [#7558](https://github.com/bitcoin/bitcoin/pull/7558) [`b35a591`](https://github.com/bitcoin/bitcoin/commit/b35a591) Add import/removeprunedfunds rpc call (instagibbs)
  * [#6215](https://github.com/bitcoin/bitcoin/pull/6215) [`48c5adf`](https://github.com/bitcoin/bitcoin/commit/48c5adf) add bip32 pub key serialization (jonasschnelli)
  * [#7913](https://github.com/bitcoin/bitcoin/pull/7913) [`bafd075`](https://github.com/bitcoin/bitcoin/commit/bafd075) Fix for incorrect locking in GetPubKey() (keystore.cpp) (yurizhykin)
  * [#8036](https://github.com/bitcoin/bitcoin/pull/8036) [`41138f9`](https://github.com/bitcoin/bitcoin/commit/41138f9) init: Move berkeleydb version reporting to wallet (laanwj)
  * [#8028](https://github.com/bitcoin/bitcoin/pull/8028) [`373b50d`](https://github.com/bitcoin/bitcoin/commit/373b50d) Fix insanity of CWalletDB::WriteTx and CWalletTx::WriteToDisk (pstratem)
  * [#8061](https://github.com/bitcoin/bitcoin/pull/8061) [`f6b7df3`](https://github.com/bitcoin/bitcoin/commit/f6b7df3) Improve Wallet encapsulation (pstratem)
  * [#7891](https://github.com/bitcoin/bitcoin/pull/7891) [`950be19`](https://github.com/bitcoin/bitcoin/commit/950be19) Always require OS randomness when generating secret keys (sipa)
  * [#7689](https://github.com/bitcoin/bitcoin/pull/7689) [`b89ef13`](https://github.com/bitcoin/bitcoin/commit/b89ef13) Replace OpenSSL AES with ctaes-based version (sipa)
  * [#7825](https://github.com/bitcoin/bitcoin/pull/7825) [`f972b04`](https://github.com/bitcoin/bitcoin/commit/f972b04) Prevent multiple calls to ExtractDestination (pedrobranco)
  * [#8137](https://github.com/bitcoin/bitcoin/pull/8137) [`243ac0c`](https://github.com/bitcoin/bitcoin/commit/243ac0c) Improve CWallet API with new AccountMove function (pstratem)
  * [#8142](https://github.com/bitcoin/bitcoin/pull/8142) [`52c3f34`](https://github.com/bitcoin/bitcoin/commit/52c3f34) Improve CWallet API with new GetAccountPubkey function (pstratem)
  * [#8035](https://github.com/bitcoin/bitcoin/pull/8035) [`b67a472`](https://github.com/bitcoin/bitcoin/commit/b67a472) Add simplest BIP32/deterministic key generation implementation (jonasschnelli)
  * [#7687](https://github.com/bitcoin/bitcoin/pull/7687) [`a6ddb19`](https://github.com/bitcoin/bitcoin/commit/a6ddb19) Stop treating importaddressâed scripts as change (sipa)
  * [#8298](https://github.com/bitcoin/bitcoin/pull/8298) [`aef3811`](https://github.com/bitcoin/bitcoin/commit/aef3811) wallet: Revert input selection post-pruning (laanwj)
  * [#8324](https://github.com/bitcoin/bitcoin/pull/8324) [`bc94b87`](https://github.com/bitcoin/bitcoin/commit/bc94b87) Keep HD seed during salvagewallet (jonasschnelli)
  * [#8323](https://github.com/bitcoin/bitcoin/pull/8323) [`238300b`](https://github.com/bitcoin/bitcoin/commit/238300b) Add HD keypath to CKeyMetadata, report metadata in validateaddress (jonasschnelli)
  * [#8367](https://github.com/bitcoin/bitcoin/pull/8367) [`3b38a6a`](https://github.com/bitcoin/bitcoin/commit/3b38a6a) Ensure <0.13 clients canât open HD wallets (jonasschnelli)
  * [#8378](https://github.com/bitcoin/bitcoin/pull/8378) [`ebea651`](https://github.com/bitcoin/bitcoin/commit/ebea651) Move SetMinVersion for FEATURE_HD to SetHDMasterKey (pstratem)
  * [#8390](https://github.com/bitcoin/bitcoin/pull/8390) [`73adfe3`](https://github.com/bitcoin/bitcoin/commit/73adfe3) Correct hdmasterkeyid/masterkeyid name confusion (jonasschnelli)
  * [#8206](https://github.com/bitcoin/bitcoin/pull/8206) [`18b8ee1`](https://github.com/bitcoin/bitcoin/commit/18b8ee1) Add HD xpriv to dumpwallet (jonasschnelli)
  * [#8389](https://github.com/bitcoin/bitcoin/pull/8389) [`c3c82c4`](https://github.com/bitcoin/bitcoin/commit/c3c82c4) Create a new HD seed after encrypting the wallet (jonasschnelli)

### Tests and QA

  * [#7320](https://github.com/bitcoin/bitcoin/pull/7320) [`d3dfc6d`](https://github.com/bitcoin/bitcoin/commit/d3dfc6d) Test walletpassphrase timeout (MarcoFalke)
  * [#7208](https://github.com/bitcoin/bitcoin/pull/7208) [`47c5ed1`](https://github.com/bitcoin/bitcoin/commit/47c5ed1) Make max tip age an option instead of chainparam (laanwj)
  * [#7372](https://github.com/bitcoin/bitcoin/pull/7372) [`21376af`](https://github.com/bitcoin/bitcoin/commit/21376af) Trivial: [qa] wallet: Print maintenance (MarcoFalke)
  * [#7280](https://github.com/bitcoin/bitcoin/pull/7280) [`668906f`](https://github.com/bitcoin/bitcoin/commit/668906f) [travis] Fail when documentation is outdated (MarcoFalke)
  * [#7177](https://github.com/bitcoin/bitcoin/pull/7177) [`93b0576`](https://github.com/bitcoin/bitcoin/commit/93b0576) [qa] Change default block priority size to 0 (MarcoFalke)
  * [#7236](https://github.com/bitcoin/bitcoin/pull/7236) [`02676c5`](https://github.com/bitcoin/bitcoin/commit/02676c5) Use createrawtx locktime parm in txn_clone (dgenr8)
  * [#7212](https://github.com/bitcoin/bitcoin/pull/7212) [`326ffed`](https://github.com/bitcoin/bitcoin/commit/326ffed) Adds unittests for CAddrMan and CAddrinfo, removes source of non-determinism (EthanHeilman)
  * [#7490](https://github.com/bitcoin/bitcoin/pull/7490) [`d007511`](https://github.com/bitcoin/bitcoin/commit/d007511) tests: Remove May15 test (laanwj)
  * [#7531](https://github.com/bitcoin/bitcoin/pull/7531) [`18cb2d5`](https://github.com/bitcoin/bitcoin/commit/18cb2d5) Add bip68-sequence.py to extended rpc tests (btcdrak)
  * [#7536](https://github.com/bitcoin/bitcoin/pull/7536) [`ce5fc02`](https://github.com/bitcoin/bitcoin/commit/ce5fc02) test: test leading spaces for ParseHex (laanwj)
  * [#7620](https://github.com/bitcoin/bitcoin/pull/7620) [`1b68de3`](https://github.com/bitcoin/bitcoin/commit/1b68de3) [travis] Only run check-doc.py once (MarcoFalke)
  * [#7455](https://github.com/bitcoin/bitcoin/pull/7455) [`7f96671`](https://github.com/bitcoin/bitcoin/commit/7f96671) [travis] Exit early when check-doc.py fails (MarcoFalke)
  * [#7667](https://github.com/bitcoin/bitcoin/pull/7667) [`56d2c4e`](https://github.com/bitcoin/bitcoin/commit/56d2c4e) Move GetTempPath() to testutil (musalbas)
  * [#7517](https://github.com/bitcoin/bitcoin/pull/7517) [`f1ca891`](https://github.com/bitcoin/bitcoin/commit/f1ca891) test: script_error checking in script_invalid tests (laanwj)
  * [#7684](https://github.com/bitcoin/bitcoin/pull/7684) [`3d0dfdb`](https://github.com/bitcoin/bitcoin/commit/3d0dfdb) Extend tests (MarcoFalke)
  * [#7697](https://github.com/bitcoin/bitcoin/pull/7697) [`622fe6c`](https://github.com/bitcoin/bitcoin/commit/622fe6c) Tests: make prioritise_transaction.py more robust (sdaftuar)
  * [#7709](https://github.com/bitcoin/bitcoin/pull/7709) [`efde86b`](https://github.com/bitcoin/bitcoin/commit/efde86b) Tests: fix missing import in mempool_packages (sdaftuar)
  * [#7702](https://github.com/bitcoin/bitcoin/pull/7702) [`29e1131`](https://github.com/bitcoin/bitcoin/commit/29e1131) Add tests verifychain, lockunspent, getbalance, listsinceblock (MarcoFalke)
  * [#7720](https://github.com/bitcoin/bitcoin/pull/7720) [`3b4324b`](https://github.com/bitcoin/bitcoin/commit/3b4324b) rpc-test: Normalize assert() (MarcoFalke)
  * [#7757](https://github.com/bitcoin/bitcoin/pull/7757) [`26794d4`](https://github.com/bitcoin/bitcoin/commit/26794d4) wallet: Wait for reindex to catch up (MarcoFalke)
  * [#7764](https://github.com/bitcoin/bitcoin/pull/7764) [`a65b36c`](https://github.com/bitcoin/bitcoin/commit/a65b36c) Donât run pruning.py twice (MarcoFalke)
  * [#7773](https://github.com/bitcoin/bitcoin/pull/7773) [`7c80e72`](https://github.com/bitcoin/bitcoin/commit/7c80e72) Fix comments in tests (btcdrak)
  * [#7489](https://github.com/bitcoin/bitcoin/pull/7489) [`e9723cb`](https://github.com/bitcoin/bitcoin/commit/e9723cb) tests: Make proxy_test work on travis servers without IPv6 (laanwj)
  * [#7801](https://github.com/bitcoin/bitcoin/pull/7801) [`70ac71b`](https://github.com/bitcoin/bitcoin/commit/70ac71b) Remove misleading âerrorString syntaxâ (MarcoFalke)
  * [#7803](https://github.com/bitcoin/bitcoin/pull/7803) [`401c65c`](https://github.com/bitcoin/bitcoin/commit/401c65c) maxblocksinflight: Actually enable test (MarcoFalke)
  * [#7802](https://github.com/bitcoin/bitcoin/pull/7802) [`3bc71e1`](https://github.com/bitcoin/bitcoin/commit/3bc71e1) httpbasics: Actually test second connection (MarcoFalke)
  * [#7849](https://github.com/bitcoin/bitcoin/pull/7849) [`ab8586e`](https://github.com/bitcoin/bitcoin/commit/ab8586e) tests: add varints_bitpatterns test (laanwj)
  * [#7846](https://github.com/bitcoin/bitcoin/pull/7846) [`491171f`](https://github.com/bitcoin/bitcoin/commit/491171f) Clean up lockorder data of destroyed mutexes (sipa)
  * [#7853](https://github.com/bitcoin/bitcoin/pull/7853) [`6ef5e00`](https://github.com/bitcoin/bitcoin/commit/6ef5e00) py2: Unfiddle strings into bytes explicitly (MarcoFalke)
  * [#7878](https://github.com/bitcoin/bitcoin/pull/7878) [`53adc83`](https://github.com/bitcoin/bitcoin/commit/53adc83) [test] bctest.py: Revert faa41ee (MarcoFalke)
  * [#7798](https://github.com/bitcoin/bitcoin/pull/7798) [`cabba24`](https://github.com/bitcoin/bitcoin/commit/cabba24) [travis] Print the commit which was evaluated (MarcoFalke)
  * [#7833](https://github.com/bitcoin/bitcoin/pull/7833) [`b1bf511`](https://github.com/bitcoin/bitcoin/commit/b1bf511) tests: Check Content-Type header returned from RPC server (laanwj)
  * [#7851](https://github.com/bitcoin/bitcoin/pull/7851) [`fa9d86f`](https://github.com/bitcoin/bitcoin/commit/fa9d86f) pull-tester: Donât mute zmq ImportError (MarcoFalke)
  * [#7822](https://github.com/bitcoin/bitcoin/pull/7822) [`0e6fd5e`](https://github.com/bitcoin/bitcoin/commit/0e6fd5e) Add listunspent() test for spendable/unspendable UTXO (jpdffonseca)
  * [#7912](https://github.com/bitcoin/bitcoin/pull/7912) [`59ad568`](https://github.com/bitcoin/bitcoin/commit/59ad568) Tests: Fix deserialization of reject messages (sdaftuar)
  * [#7941](https://github.com/bitcoin/bitcoin/pull/7941) [`0ea3941`](https://github.com/bitcoin/bitcoin/commit/0ea3941) Fixing comment in script_test.json test case (Christewart)
  * [#7807](https://github.com/bitcoin/bitcoin/pull/7807) [`0ad1041`](https://github.com/bitcoin/bitcoin/commit/0ad1041) Fixed miner test values, gave constants for less error-prone values (instagibbs)
  * [#7980](https://github.com/bitcoin/bitcoin/pull/7980) [`88b77c7`](https://github.com/bitcoin/bitcoin/commit/88b77c7) Smartfees: Properly use ordered dict (MarcoFalke)
  * [#7814](https://github.com/bitcoin/bitcoin/pull/7814) [`77b637f`](https://github.com/bitcoin/bitcoin/commit/77b637f) Switch to py3 (MarcoFalke)
  * [#8030](https://github.com/bitcoin/bitcoin/pull/8030) [`409a8a1`](https://github.com/bitcoin/bitcoin/commit/409a8a1) Revert fatal-ness of missing python-zmq (laanwj)
  * [#8018](https://github.com/bitcoin/bitcoin/pull/8018) [`3e90fe6`](https://github.com/bitcoin/bitcoin/commit/3e90fe6) Autofind rpc tests âsrcdir (jonasschnelli)
  * [#8016](https://github.com/bitcoin/bitcoin/pull/8016) [`5767e80`](https://github.com/bitcoin/bitcoin/commit/5767e80) Fix multithread CScheduler and reenable test (paveljanik)
  * [#7972](https://github.com/bitcoin/bitcoin/pull/7972) [`423ca30`](https://github.com/bitcoin/bitcoin/commit/423ca30) pull-tester: Run rpc test in parallel (MarcoFalke)
  * [#8039](https://github.com/bitcoin/bitcoin/pull/8039) [`69b3a6d`](https://github.com/bitcoin/bitcoin/commit/69b3a6d) Bench: Add crypto hash benchmarks (laanwj)
  * [#8041](https://github.com/bitcoin/bitcoin/pull/8041) [`5b736dd`](https://github.com/bitcoin/bitcoin/commit/5b736dd) Fix bip9-softforks blockstore issue (MarcoFalke)
  * [#7994](https://github.com/bitcoin/bitcoin/pull/7994) [`1f01443`](https://github.com/bitcoin/bitcoin/commit/1f01443) Add op csv tests to script_tests.json (Christewart)
  * [#8038](https://github.com/bitcoin/bitcoin/pull/8038) [`e2bf830`](https://github.com/bitcoin/bitcoin/commit/e2bf830) Various minor fixes (MarcoFalke)
  * [#8072](https://github.com/bitcoin/bitcoin/pull/8072) [`1b87e5b`](https://github.com/bitcoin/bitcoin/commit/1b87e5b) Travis: âmake checkâ in parallel and verbose (theuni)
  * [#8056](https://github.com/bitcoin/bitcoin/pull/8056) [`8844ef1`](https://github.com/bitcoin/bitcoin/commit/8844ef1) Remove hardcoded â4 nodesâ from test_framework (MarcoFalke)
  * [#8047](https://github.com/bitcoin/bitcoin/pull/8047) [`37f9a1f`](https://github.com/bitcoin/bitcoin/commit/37f9a1f) Test_framework: Set wait-timeout for bitcoind procs (MarcoFalke)
  * [#8095](https://github.com/bitcoin/bitcoin/pull/8095) [`6700cc9`](https://github.com/bitcoin/bitcoin/commit/6700cc9) Test framework: only cleanup on successful test runs (sdaftuar)
  * [#8098](https://github.com/bitcoin/bitcoin/pull/8098) [`06bd4f6`](https://github.com/bitcoin/bitcoin/commit/06bd4f6) Test_framework: Append portseed to tmpdir (MarcoFalke)
  * [#8104](https://github.com/bitcoin/bitcoin/pull/8104) [`6ff2c8d`](https://github.com/bitcoin/bitcoin/commit/6ff2c8d) Add timeout to sync_blocks() and sync_mempools() (sdaftuar)
  * [#8111](https://github.com/bitcoin/bitcoin/pull/8111) [`61b8684`](https://github.com/bitcoin/bitcoin/commit/61b8684) Benchmark SipHash (sipa)
  * [#8107](https://github.com/bitcoin/bitcoin/pull/8107) [`52b803e`](https://github.com/bitcoin/bitcoin/commit/52b803e) Bench: Added base58 encoding/decoding benchmarks (yurizhykin)
  * [#8115](https://github.com/bitcoin/bitcoin/pull/8115) [`0026e0e`](https://github.com/bitcoin/bitcoin/commit/0026e0e) Avoid integer division in the benchmark inner-most loop (gmaxwell)
  * [#8090](https://github.com/bitcoin/bitcoin/pull/8090) [`a2df115`](https://github.com/bitcoin/bitcoin/commit/a2df115) Adding P2SH(p2pkh) script test case (Christewart)
  * [#7992](https://github.com/bitcoin/bitcoin/pull/7992) [`ec45cc5`](https://github.com/bitcoin/bitcoin/commit/ec45cc5) Extend [#7956](https://github.com/bitcoin/bitcoin/pull/7956) with one more test (TheBlueMatt)
  * [#8139](https://github.com/bitcoin/bitcoin/pull/8139) [`ae5575b`](https://github.com/bitcoin/bitcoin/commit/ae5575b) Fix interrupted HTTP RPC connection workaround for Python 3.5+ (sipa)
  * [#8164](https://github.com/bitcoin/bitcoin/pull/8164) [`0f24eaf`](https://github.com/bitcoin/bitcoin/commit/0f24eaf) [Bitcoin-Tx] fix missing test fixtures, fix 32bit atoi issue (jonasschnelli)
  * [#8166](https://github.com/bitcoin/bitcoin/pull/8166) [`0b5279f`](https://github.com/bitcoin/bitcoin/commit/0b5279f) Src/test: Do not shadow local variables (paveljanik)
  * [#8141](https://github.com/bitcoin/bitcoin/pull/8141) [`44c1b1c`](https://github.com/bitcoin/bitcoin/commit/44c1b1c) Continuing port of java comparison tool (mrbandrews)
  * [#8201](https://github.com/bitcoin/bitcoin/pull/8201) [`36b7400`](https://github.com/bitcoin/bitcoin/commit/36b7400) fundrawtransaction: Fix race, assert amounts (MarcoFalke)
  * [#8214](https://github.com/bitcoin/bitcoin/pull/8214) [`ed2cd59`](https://github.com/bitcoin/bitcoin/commit/ed2cd59) Mininode: fail on send_message instead of silent return (MarcoFalke)
  * [#8215](https://github.com/bitcoin/bitcoin/pull/8215) [`a072d1a`](https://github.com/bitcoin/bitcoin/commit/a072d1a) Donât use floating point in wallet tests (MarcoFalke)
  * [#8066](https://github.com/bitcoin/bitcoin/pull/8066) [`65c2058`](https://github.com/bitcoin/bitcoin/commit/65c2058) Test_framework: Use different rpc_auth_pair for each node (MarcoFalke)
  * [#8216](https://github.com/bitcoin/bitcoin/pull/8216) [`0d41d70`](https://github.com/bitcoin/bitcoin/commit/0d41d70) Assert âchangePosition out of boundsâ (MarcoFalke)
  * [#8222](https://github.com/bitcoin/bitcoin/pull/8222) [`961893f`](https://github.com/bitcoin/bitcoin/commit/961893f) Enable mempool consistency checks in unit tests (sipa)
  * [#7751](https://github.com/bitcoin/bitcoin/pull/7751) [`84370d5`](https://github.com/bitcoin/bitcoin/commit/84370d5) test_framework: python3.4 authproxy compat (laanwj)
  * [#7744](https://github.com/bitcoin/bitcoin/pull/7744) [`d8e862a`](https://github.com/bitcoin/bitcoin/commit/d8e862a) test_framework: detect failure of bitcoind startup (laanwj)
  * [#8280](https://github.com/bitcoin/bitcoin/pull/8280) [`115735d`](https://github.com/bitcoin/bitcoin/commit/115735d) Increase sync_blocks() timeouts in pruning.py (MarcoFalke)
  * [#8340](https://github.com/bitcoin/bitcoin/pull/8340) [`af9b7a9`](https://github.com/bitcoin/bitcoin/commit/af9b7a9) Solve trivial merge conflict in p2p-segwit.py (MarcoFalke)
  * [#8067](https://github.com/bitcoin/bitcoin/pull/8067) [`3e4cf8f`](https://github.com/bitcoin/bitcoin/commit/3e4cf8f) Travis: use slim generic image, and some fixups (theuni)
  * [#7951](https://github.com/bitcoin/bitcoin/pull/7951) [`5c7df70`](https://github.com/bitcoin/bitcoin/commit/5c7df70) Test_framework: Properly print exception (MarcoFalke)
  * [#8070](https://github.com/bitcoin/bitcoin/pull/8070) [`7771aa5`](https://github.com/bitcoin/bitcoin/commit/7771aa5) Remove non-determinism which is breaking net_tests [#8069](https://github.com/bitcoin/bitcoin/pull/8069) (EthanHeilman)
  * [#8309](https://github.com/bitcoin/bitcoin/pull/8309) [`bb2646a`](https://github.com/bitcoin/bitcoin/commit/bb2646a) Add wallet-hd test (MarcoFalke)
  * [#8444](https://github.com/bitcoin/bitcoin/pull/8444) [`cd0910b`](https://github.com/bitcoin/bitcoin/commit/cd0910b) Fix p2p-feefilter.py for changed tx relay behavior (sdaftuar)

### Mining

  * [#7507](https://github.com/bitcoin/bitcoin/pull/7507) [`11c7699`](https://github.com/bitcoin/bitcoin/commit/11c7699) Remove internal miner (Leviathn)
  * [#7663](https://github.com/bitcoin/bitcoin/pull/7663) [`c87f51e`](https://github.com/bitcoin/bitcoin/commit/c87f51e) Make the generate RPC call function for non-regtest (sipa)
  * [#7671](https://github.com/bitcoin/bitcoin/pull/7671) [`e2ebd25`](https://github.com/bitcoin/bitcoin/commit/e2ebd25) Add generatetoaddress RPC to mine to an address (achow101)
  * [#7935](https://github.com/bitcoin/bitcoin/pull/7935) [`66ed450`](https://github.com/bitcoin/bitcoin/commit/66ed450) Versionbits: GBT support (luke-jr)
  * [#7600](https://github.com/bitcoin/bitcoin/pull/7600) [`66db2d6`](https://github.com/bitcoin/bitcoin/commit/66db2d6) Select transactions using feerate-with-ancestors (sdaftuar)
  * [#8295](https://github.com/bitcoin/bitcoin/pull/8295) [`f5660d3`](https://github.com/bitcoin/bitcoin/commit/f5660d3) Mining-related fixups for 0.13.0 (sdaftuar)
  * [#7796](https://github.com/bitcoin/bitcoin/pull/7796) [`536b75e`](https://github.com/bitcoin/bitcoin/commit/536b75e) Add support for negative fee rates, fixes `prioritizetransaction` (MarcoFalke)
  * [#8362](https://github.com/bitcoin/bitcoin/pull/8362) [`86edc20`](https://github.com/bitcoin/bitcoin/commit/86edc20) Scale legacy sigop count in CreateNewBlock (sdaftuar)
  * [#8489](https://github.com/bitcoin/bitcoin/pull/8489) [`8b0eee6`](https://github.com/bitcoin/bitcoin/commit/8b0eee6) Bugfix: Use pre-BIP141 sigops until segwit activates (GBT) (luke-jr)

### Documentation and miscellaneous

  * [#7423](https://github.com/bitcoin/bitcoin/pull/7423) [`69e2a40`](https://github.com/bitcoin/bitcoin/commit/69e2a40) Add example for building with constrained resources (jarret)
  * [#8254](https://github.com/bitcoin/bitcoin/pull/8254) [`c2c69ed`](https://github.com/bitcoin/bitcoin/commit/c2c69ed) Add OSX ZMQ requirement to QA readme (fanquake)
  * [#8203](https://github.com/bitcoin/bitcoin/pull/8203) [`377d131`](https://github.com/bitcoin/bitcoin/commit/377d131) Clarify documentation for running a tor node (nathaniel-mahieu)
  * [#7428](https://github.com/bitcoin/bitcoin/pull/7428) [`4b12266`](https://github.com/bitcoin/bitcoin/commit/4b12266) Add example for listing ./configure flags (nathaniel-mahieu)
  * [#7847](https://github.com/bitcoin/bitcoin/pull/7847) [`3eae681`](https://github.com/bitcoin/bitcoin/commit/3eae681) Add arch linux build example (mruddy)
  * [#7968](https://github.com/bitcoin/bitcoin/pull/7968) [`ff69aaf`](https://github.com/bitcoin/bitcoin/commit/ff69aaf) Fedora build requirements (wtogami)
  * [#8013](https://github.com/bitcoin/bitcoin/pull/8013) [`fbedc09`](https://github.com/bitcoin/bitcoin/commit/fbedc09) Fedora build requirements, add gcc-c++ and fix typo (wtogami)
  * [#8009](https://github.com/bitcoin/bitcoin/pull/8009) [`fbd8478`](https://github.com/bitcoin/bitcoin/commit/fbd8478) Fixed invalid example paths in gitian-building.md (JeremyRand)
  * [#8240](https://github.com/bitcoin/bitcoin/pull/8240) [`63fbdbc`](https://github.com/bitcoin/bitcoin/commit/63fbdbc) Mention Windows XP end of support in release notes (laanwj)
  * [#8303](https://github.com/bitcoin/bitcoin/pull/8303) [`5077d2c`](https://github.com/bitcoin/bitcoin/commit/5077d2c) Update bips.md for CSV softfork (fanquake)
  * [#7789](https://github.com/bitcoin/bitcoin/pull/7789) [`e0b3e19`](https://github.com/bitcoin/bitcoin/commit/e0b3e19) Add note about using the Qt official binary installer (paveljanik)
  * [#7791](https://github.com/bitcoin/bitcoin/pull/7791) [`e30a5b0`](https://github.com/bitcoin/bitcoin/commit/e30a5b0) Change Precise to Trusty in gitian-building.md (JeremyRand)
  * [#7838](https://github.com/bitcoin/bitcoin/pull/7838) [`8bb5d3d`](https://github.com/bitcoin/bitcoin/commit/8bb5d3d) Update gitian build guide to debian 8.4.0 (fanquake)
  * [#7855](https://github.com/bitcoin/bitcoin/pull/7855) [`b778e59`](https://github.com/bitcoin/bitcoin/commit/b778e59) Replace precise with trusty (MarcoFalke)
  * [#7975](https://github.com/bitcoin/bitcoin/pull/7975) [`fc23fee`](https://github.com/bitcoin/bitcoin/commit/fc23fee) Update bitcoin-core GitHub links (MarcoFalke)
  * [#8034](https://github.com/bitcoin/bitcoin/pull/8034) [`e3a8207`](https://github.com/bitcoin/bitcoin/commit/e3a8207) Add basic git squash workflow (fanquake)
  * [#7813](https://github.com/bitcoin/bitcoin/pull/7813) [`214ec0b`](https://github.com/bitcoin/bitcoin/commit/214ec0b) Update port in tor.md (MarcoFalke)
  * [#8193](https://github.com/bitcoin/bitcoin/pull/8193) [`37c9830`](https://github.com/bitcoin/bitcoin/commit/37c9830) Use Debian 8.5 in the gitian-build guide (fanquake)
  * [#8261](https://github.com/bitcoin/bitcoin/pull/8261) [`3685e0c`](https://github.com/bitcoin/bitcoin/commit/3685e0c) Clarify help for `getblockchaininfo` (paveljanik)
  * [#7185](https://github.com/bitcoin/bitcoin/pull/7185) [`ea0f5a2`](https://github.com/bitcoin/bitcoin/commit/ea0f5a2) Note that reviewers should mention the id of the commits they reviewed (pstratem)
  * [#7290](https://github.com/bitcoin/bitcoin/pull/7290) [`c851d8d`](https://github.com/bitcoin/bitcoin/commit/c851d8d) [init] Add missing help for args (MarcoFalke)
  * [#7281](https://github.com/bitcoin/bitcoin/pull/7281) [`f9fd4c2`](https://github.com/bitcoin/bitcoin/commit/f9fd4c2) Improve CheckInputs() comment about sig verification (petertodd)
  * [#7417](https://github.com/bitcoin/bitcoin/pull/7417) [`1e06bab`](https://github.com/bitcoin/bitcoin/commit/1e06bab) Minor improvements to the release process (PRabahy)
  * [#7444](https://github.com/bitcoin/bitcoin/pull/7444) [`4cdbd42`](https://github.com/bitcoin/bitcoin/commit/4cdbd42) Improve block validity/ConnectBlock() comments (petertodd)
  * [#7527](https://github.com/bitcoin/bitcoin/pull/7527) [`db2e1c0`](https://github.com/bitcoin/bitcoin/commit/db2e1c0) Fix and cleanup listreceivedbyX documentation (instagibbs)
  * [#7541](https://github.com/bitcoin/bitcoin/pull/7541) [`b6e00af`](https://github.com/bitcoin/bitcoin/commit/b6e00af) Clarify description of blockindex (pinheadmz)
  * [#7590](https://github.com/bitcoin/bitcoin/pull/7590) [`f06af57`](https://github.com/bitcoin/bitcoin/commit/f06af57) Improving wording related to Boost library requirements [updated] (jonathancross)
  * [#7635](https://github.com/bitcoin/bitcoin/pull/7635) [`0fa88ef`](https://github.com/bitcoin/bitcoin/commit/0fa88ef) Add dependency info to test docs (elliotolds)
  * [#7609](https://github.com/bitcoin/bitcoin/pull/7609) [`3ba07bd`](https://github.com/bitcoin/bitcoin/commit/3ba07bd) RPM spec file project (AliceWonderMiscreations)
  * [#7850](https://github.com/bitcoin/bitcoin/pull/7850) [`229a17c`](https://github.com/bitcoin/bitcoin/commit/229a17c) Removed call to `TryCreateDirectory` from `GetDefaultDataDir` in `src/util.cpp` (alexreg)
  * [#7888](https://github.com/bitcoin/bitcoin/pull/7888) [`ec870e1`](https://github.com/bitcoin/bitcoin/commit/ec870e1) Prevector: fix 2 bugs in currently unreached code paths (kazcw)
  * [#7922](https://github.com/bitcoin/bitcoin/pull/7922) [`90653bc`](https://github.com/bitcoin/bitcoin/commit/90653bc) CBase58Data::SetString: cleanse the full vector (kazcw)
  * [#7881](https://github.com/bitcoin/bitcoin/pull/7881) [`c4e8390`](https://github.com/bitcoin/bitcoin/commit/c4e8390) Update release process (laanwj)
  * [#7952](https://github.com/bitcoin/bitcoin/pull/7952) [`a9c8b74`](https://github.com/bitcoin/bitcoin/commit/a9c8b74) Log invalid block hash to make debugging easier (paveljanik)
  * [#7974](https://github.com/bitcoin/bitcoin/pull/7974) [`8206835`](https://github.com/bitcoin/bitcoin/commit/8206835) More comments on the design of AttemptToEvictConnection (gmaxwell)
  * [#7795](https://github.com/bitcoin/bitcoin/pull/7795) [`47a7cfb`](https://github.com/bitcoin/bitcoin/commit/47a7cfb) UpdateTip: log only one line at most per block (laanwj)
  * [#8110](https://github.com/bitcoin/bitcoin/pull/8110) [`e7e25ea`](https://github.com/bitcoin/bitcoin/commit/e7e25ea) Add benchmarking notes (fanquake)
  * [#8121](https://github.com/bitcoin/bitcoin/pull/8121) [`58f0c92`](https://github.com/bitcoin/bitcoin/commit/58f0c92) Update implemented BIPs list (fanquake)
  * [#8029](https://github.com/bitcoin/bitcoin/pull/8029) [`58725ba`](https://github.com/bitcoin/bitcoin/commit/58725ba) Simplify OS X build notes (fanquake)
  * [#8143](https://github.com/bitcoin/bitcoin/pull/8143) [`d46b8b5`](https://github.com/bitcoin/bitcoin/commit/d46b8b5) comment nit: miners donât vote (instagibbs)
  * [#8136](https://github.com/bitcoin/bitcoin/pull/8136) [`22e0b35`](https://github.com/bitcoin/bitcoin/commit/22e0b35) Log/report in 10% steps during VerifyDB (jonasschnelli)
  * [#8168](https://github.com/bitcoin/bitcoin/pull/8168) [`d366185`](https://github.com/bitcoin/bitcoin/commit/d366185) util: Add ParseUInt32 and ParseUInt64 (laanwj)
  * [#8178](https://github.com/bitcoin/bitcoin/pull/8178) [`f7b1bfc`](https://github.com/bitcoin/bitcoin/commit/f7b1bfc) Add git and github tips and tricks to developer notes (sipa)
  * [#8177](https://github.com/bitcoin/bitcoin/pull/8177) [`67db011`](https://github.com/bitcoin/bitcoin/commit/67db011) developer notes: updates for C++11 (kazcw)
  * [#8229](https://github.com/bitcoin/bitcoin/pull/8229) [`8ccdac1`](https://github.com/bitcoin/bitcoin/commit/8ccdac1) [Doc] Update OS X build notes for 10.11 SDK (fanquake)
  * [#8233](https://github.com/bitcoin/bitcoin/pull/8233) [`9f1807a`](https://github.com/bitcoin/bitcoin/commit/9f1807a) Mention Linux ARM executables in release process and notes (laanwj)
  * [#7540](https://github.com/bitcoin/bitcoin/pull/7540) [`ff46dd4`](https://github.com/bitcoin/bitcoin/commit/ff46dd4) Rename OP_NOP3 to OP_CHECKSEQUENCEVERIFY (btcdrak)
  * [#8289](https://github.com/bitcoin/bitcoin/pull/8289) [`26316ff`](https://github.com/bitcoin/bitcoin/commit/26316ff) bash-completion: Adapt for 0.12 and 0.13 (roques)
  * [#7453](https://github.com/bitcoin/bitcoin/pull/7453) [`3dc3149`](https://github.com/bitcoin/bitcoin/commit/3dc3149) Missing patches from 0.12 (MarcoFalke)
  * [#7113](https://github.com/bitcoin/bitcoin/pull/7113) [`54a550b`](https://github.com/bitcoin/bitcoin/commit/54a550b) Switch to a more efficient rolling Bloom filter (sipa)
  * [#7257](https://github.com/bitcoin/bitcoin/pull/7257) [`de9e5ea`](https://github.com/bitcoin/bitcoin/commit/de9e5ea) Combine common error strings for different options so translations can be shared and reused (luke-jr)
  * [#7304](https://github.com/bitcoin/bitcoin/pull/7304) [`b8f485c`](https://github.com/bitcoin/bitcoin/commit/b8f485c) [contrib] Add clang-format-diff.py (MarcoFalke)
  * [#7378](https://github.com/bitcoin/bitcoin/pull/7378) [`e6f97ef`](https://github.com/bitcoin/bitcoin/commit/e6f97ef) devtools: replace github-merge with python version (laanwj)
  * [#7395](https://github.com/bitcoin/bitcoin/pull/7395) [`0893705`](https://github.com/bitcoin/bitcoin/commit/0893705) devtools: show pull and commit information in github-merge (laanwj)
  * [#7402](https://github.com/bitcoin/bitcoin/pull/7402) [`6a5932b`](https://github.com/bitcoin/bitcoin/commit/6a5932b) devtools: github-merge get toplevel dir without extra whitespace (achow101)
  * [#7425](https://github.com/bitcoin/bitcoin/pull/7425) [`20a408c`](https://github.com/bitcoin/bitcoin/commit/20a408c) devtools: Fix utf-8 support in messages for github-merge (laanwj)
  * [#7632](https://github.com/bitcoin/bitcoin/pull/7632) [`409f843`](https://github.com/bitcoin/bitcoin/commit/409f843) Delete outdated test-patches reference (Lewuathe)
  * [#7662](https://github.com/bitcoin/bitcoin/pull/7662) [`386f438`](https://github.com/bitcoin/bitcoin/commit/386f438) remove unused NOBLKS_VERSION_{START,END} constants (rat4)
  * [#7737](https://github.com/bitcoin/bitcoin/pull/7737) [`aa0d2b2`](https://github.com/bitcoin/bitcoin/commit/aa0d2b2) devtools: make github-merge.py use py3 (laanwj)
  * [#7781](https://github.com/bitcoin/bitcoin/pull/7781) [`55db5f0`](https://github.com/bitcoin/bitcoin/commit/55db5f0) devtools: Auto-set branch to merge to in github-merge (laanwj)
  * [#7934](https://github.com/bitcoin/bitcoin/pull/7934) [`f17032f`](https://github.com/bitcoin/bitcoin/commit/f17032f) Improve rolling bloom filter performance and benchmark (sipa)
  * [#8004](https://github.com/bitcoin/bitcoin/pull/8004) [`2efe38b`](https://github.com/bitcoin/bitcoin/commit/2efe38b) signal handling: fReopenDebugLog and fRequestShutdown should be type sig_atomic_t (catilac)
  * [#7713](https://github.com/bitcoin/bitcoin/pull/7713) [`f6598df`](https://github.com/bitcoin/bitcoin/commit/f6598df) Fixes for verify-commits script (petertodd)
  * [#8412](https://github.com/bitcoin/bitcoin/pull/8412) [`8360d5b`](https://github.com/bitcoin/bitcoin/commit/8360d5b) libconsensus: Expose a flag for BIP112 (jtimon)

# Credits

Thanks to everyone who directly contributed to this release:

  * 21E14
  * accraze
  * Adam Brown
  * Alexander Regueiro
  * Alex Morcos
  * Alfie John
  * Alice Wonder
  * AlSzacrel
  * Andrew Chow
  * AndrÃ©s G. Aragoneses
  * Bob McElrath
  * BtcDrak
  * calebogden
  * CÃ©dric FÃ©lizard
  * Chirag DavÃ©
  * Chris Moore
  * Chris Stewart
  * Christian von Roques
  * Chris Wheeler
  * Cory Fields
  * crowning-
  * Daniel Cousens
  * Daniel Kraft
  * Denis Lukianov
  * Elias Rohrer
  * Elliot Olds
  * Eric Shaw
  * error10
  * Ethan Heilman
  * face
  * fanquake
  * Francesco âmakevoidâ Canessa
  * fsb4000
  * Gavin Andresen
  * gladoscc
  * Gregory Maxwell
  * Gregory Sanders
  * instagibbs
  * James OâBeirne
  * Jannes Faber
  * Jarret Dyrbye
  * Jeremy Rand
  * jloughry
  * jmacwhyte
  * Joao Fonseca
  * Johnson Lau
  * Jonas Nick
  * Jonas Schnelli
  * Jonathan Cross
  * JoÃ£o Barbosa
  * Jorge TimÃ³n
  * Kaz Wesley
  * Kefkius
  * kirkalx
  * Krzysztof Jurewicz
  * Leviathn
  * lewuathe
  * Luke Dashjr
  * Luv Khemani
  * Marcel KrÃ¼ger
  * Marco Falke
  * Mark Friedenbach
  * Matt
  * Matt Bogosian
  * Matt Corallo
  * Matthew English
  * Matthew Zipkin
  * mb300sd
  * Mitchell Cash
  * mrbandrews
  * mruddy
  * Murch
  * Mustafa
  * Nathaniel Mahieu
  * Nicolas Dorier
  * Patrick Strateman
  * Paul Rabahy
  * paveljanik
  * Pavel JanÃ­k
  * Pavel Vasin
  * Pedro Branco
  * Peter Todd
  * Philip Kaufmann
  * Pieter Wuille
  * Prayag Verma
  * ptschip
  * Puru
  * randy-waterhouse
  * R E Broadley
  * Rusty Russell
  * Suhas Daftuar
  * Suriyaa Kudo
  * TheLazieR Yip
  * Thomas Kerin
  * Tom Harding
  * Tyler Hardin
  * UdjinM6
  * Warren Togami
  * Will Binns
  * Wladimir J. van der Laan
  * Yuri Zhykin

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
