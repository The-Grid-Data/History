[](https://www.binance.com/en-GB/)

Buy Crypto

  * [Buy Crypto via Bank CardGBPUse Bank Card to Buy Crypto](https://www.binance.com/en-GB/crypto/buy/GBP/BTC)
  * [Buy Crypto via P2PUse Peer-to-Peer to Buy Crypto](https://p2p.binance.com/en-GB/trade/all-payments/USDT?fiat=GBP)
  * [Buy Fan TokensBuy Fan Tokens](https://www.binance.com/en-GB/fan-token)
  * [Buy NFTsBuy Non-Fungible Tokens](https://www.binance.com/en-GB/nft/home)

Trade

  * [ConvertUse Convert to Trade Crypto](https://www.binance.com/en-GB/convert)
  * [Spot ExchangeUse Spot Exchange to Trade Crypto](https://www.binance.com/en-GB/markets/spot_margin-FIAT)
  * [Margin ExchangeUse Margin Exchange to Trade Crypto](https://www.binance.com/en-GB/trade?type=cross)
  * [Trading BotsUse Trading Bots to Trade Crypto](https://www.binance.com/en-GB/trading-bots)

[Earn](https://www.binance.com/en-GB/earn)

  * [Launch PlatformCryptoasset Token Launch Platform](https://launchpad.binance.com/en-GB)
  * [Auto-InvestCryptoasset Auto-Invest Platform](https://www.binance.com/en-GB/auto-invest/)

Support

  * [Submit Live ChatChat with Customer Support](https://www.binance.com/en-GB/chat)
  * [Support CentreAccess Support FAQ articles](https://www.binance.com/en-GB/support)
  * [Trading FeesView the trading fees](https://www.binance.com/en-GB/fee/trading)
  * [Trading RuleView the trading rules and limits](https://www.binance.com/en-GB/trade-rule)

[Log In](https://accounts.binance.com/en-
GB/login?loginChannel=&return_to=aHR0cHM6Ly93d3cuYmluYW5jZS5jb20vZW4tR0IvcHJvb2Ytb2YtcmVzZXJ2ZXM%3D)[Sign
Up](https://accounts.binance.com/en-
GB/register?registerChannel=&return_to=aHR0cHM6Ly93d3cuYmluYW5jZS5jb20vZW4tR0IvcHJvb2Ytb2YtcmVzZXJ2ZXM%3D)

# Proof of Reserves

Verify that Binance user assets are fully backed, at least 1:1. Please note
that the vast majority of Binance’s corporate holdings are stored in wallets
that do not form part of the proof-of-reserves calculations.

View Report

Audit Time

No results found.

Verification Mechanism:

Merkle Root Hash:

Download All Address

## What is Proof of Reserves (PoR)?

When we say Proof of Reserves, we are specifically referring to those assets
that we hold in custody for users. This means that we are showing evidence and
proof that Binance has funds that cover all of our users assets 1:1, as well
as some reserves.  
When a user deposits one Bitcoin, Binance's reserves increase by at least one
Bitcoin to ensure client funds are fully backed. It is important to note that
this does not include Binance’s corporate holdings, which are kept on a
completely separate ledger.  
What this means in actual terms is that Binance holds all user assets 1:1 (as
well as some reserves), we have zero debt in our capital structure and we have
made sure that we have an emergency fund (SAFU fund) for extreme cases.  
Read on to see more information on what we have built to allow people to check
their funds are safe with Binance.

Our commitment to our community remains the same as it has always been

Transparency

We will always be transparent with our users

Safety

The safety of our users funds is a priority for us

Protected

Your funds are protected

## Merkle Tree

What have we built?

In order to show that Binance has all user assets 1:1, we have built and
implemented the Merkle tree (shown below) to allow people to verify their
assets within the platform. Our goal is that every user will be able to verify
their asset holdings using their own generated Merkle hash/record ID. This way
people will be able to confirm that their funds are held 1:1 and they can have
it verified by a third-party audit agency.

What is a Merkle Tree?

A Merkle Tree is a cryptographic tool that enables the consolidation of large
amounts of data into a single hash. This single hash, called a Merkle Root,
acts as a cryptographic seal that “summarizes” all the inputted data.
Additionally, Merkle Trees give users the ability to verify specific contents
that were included within a particular set of “sealed” data. We use these
properties of Merkle Trees during our Proof of Reserves assessments to verify
individual user accounts are included within the liabilities report inspected
by the auditor.

## zk-SNARKs

What have we built?

By using a zk-SNARK, a crypto exchange can prove that all Merkle tree leaf
nodes’ balance sets (i.e., user account balances) contribute to the exchange’s
claimed total user asset balance. Each user can easily access their leaf node
as having been included in the process. For each user’s balance set (Merkle
tree leaf node), our circuit ensures that:

1\. A user’s asset balances are included in the calculation of the sum of the
total net user balances with Binance.

2\. The total net balance of the user is greater than or equal to zero.

3\. The change of Merkle tree root is valid (i.e., not using falsified
information) after updating a user’s information to the leaf node hash.

Here are some useful resources:
[blog](https://academy.binance.com/en/articles/improving-crypto-transparency-
with-zero-knowledge-proof), [technical specification](https://gusty-
radon-13b.notion.site/Proof-of-solvency-61414c3f7c1e46c5baec32b9491b2b3d) and
[our source code](https://github.com/binance/zkmerkle-proof-of-
solvency/blob/main/circuit/batch_create_user_circuit.go) for the circuit
(constraints) for implementation detail.

What is a zk-SNARK?

A [zk-SNARK](https://academy.binance.com/en/articles/zk-snarks-and-zk-starks-
explained) (Zero-Knowledge Succinct Non-Interactive Argument of Knowledge) is
a proof protocol that follows the zero-knowledge principles previously
outlined. With a [zk-SNARK](https://academy.binance.com/en/articles/zk-snarks-
and-zk-starks-explained), you can prove that you know the original hashed
value (discussed further below) without revealing what that value is. You can
also prove the validity of a
[transaction](https://academy.binance.com/en/glossary/transaction-id) without
revealing any information about the specific amounts, values, or addresses
involved.

## How it works

How can I verify my own transactions?

Log in to the Binance Website

-> Click on **“Wallet”**

-> Click on **“Verification”**

You will be able to find your Merkle Leaf and Record ID within the page.

Select the verification date you want to check. You will then find
confirmation of the verification type, your Record ID (specific to your
account and this particular verification), the assets that were covered, and
your asset balances at the time of the verification.

The Record ID/Merkle Leaf enables you to independently verify that your
account balance was included by the third-party auditor’s attestation report.

## Verification Process

We have two ways to produce verification reports, the first is the self-
verification method (combined with zk-SNARKS technical solutions) and the
second is third-party audits providing audit reports.

Zero-Knowledge ProofThird-Party Audit

1\. Verify Ownership of Address

For assets that are used to verify reserves, we must ensure that ownership of
the wallet belongs to Binance (including cold and hot wallet).

2\. Snapshot of User Balances

The snapshot value is calculated based on the asset holding within the
customer's account balances at the date and time of the snapshot.

3\. Generate zk-SNARKs Proof

We generate zk-SNARKs proof files for users so that each user can easily
access their leaf node, providing transparency for all users.

4\. Generation of Merkle Tree

We generate the underlying data block by linking the hashed UID and balance of
each user. We then generate a Merkle tree based upon all users' data. The
Merkle root will change if any account ID or balance in the leaf node changes.
Every user can verify whether their assets are included in the leaf node.

### Community

[](https://x.com/binanceuk)

Theme

Theme

### Company

  * [About Us](https://www.binance.com/en-GB/about)
  * [Inquiries](https://www.binance.com/en-GB/about#email)
  * [Careers](https://www.binance.com/en-GB/careers)
  * [Press](https://www.binance.com/en-GB/press)

### Support

  * [Support Center](https://www.binance.com/en-GB/support)
  * [24/7 Chat Support](https://www.binance.com/en-GB/chat?sourceEntry=4)
  * [Fees](https://www.binance.com/en-GB/fee/schedule)
  * [Trading Rules](https://www.binance.com/en-GB/trade-rule)

### Legal

  * [Terms](https://www.binance.com/en-GB/terms)
  * [Privacy Notice](https://www.binance.com/en-GB/about-legal/privacy-portal)

### Compliance

  * [Risk Warning](https://www.binance.com/en-GB/legal/risk-warning)
  * [Law Enforcement Request](https://www.binance.com/en-GB/support/law-enforcement)
  * [Licenses & Registrations](https://www.binance.com/en-GB/legal/licenses)

### Products

  * [Spot](https://www.binance.com/en-GB/markets/overview)
  * [OCBS](https://www.binance.com/en-GB/crypto)
  * [Convert](https://www.binance.com/en-GB/convert/GBP/BTC)
  * [NFT](https://www.binance.com/en-GB/nft/home)

Nest Services Limited, trading as Binance, is the entity ultimately
responsible for the Binance Services offered through the Platform.  
  
Trading cryptocurrencies involves significant risk and can result in the loss
of your capital. You should not invest more than you can afford to lose and
you should ensure that you fully understand the risks involved. Before
trading, please take into consideration your level of experience, investment
objectives, and seek independent financial advice if necessary. It is your
responsibility to ascertain whether you are permitted to use the services of
Binance based on the legal requirements in your country of residence. Neither
the firm nor investments in cryptoassets are regulated by the Financial
Conduct Authority, nor covered by the Financial Ombudsman Service or subject
to protection under the Financial Services Compensation Scheme. The
information on this site is not directed at residents of the United States,
Canada, Singapore, Japan, Korea, Australia, and New Zealand or any particular
country or jurisdiction where such distribution or use would be contrary to
local law or regulation.

Binance© 2024Cookie Preferences

