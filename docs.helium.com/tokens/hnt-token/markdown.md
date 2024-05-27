Skip to main content

[![Helium Logo](/img/icons/logo_docs_black.svg)****](/)[Tokens](/tokens/hnt-
token)[Wallets](/wallets)[IoT Network](/iot)[Mobile Network](/mobile/5g-on-
helium)

More

  * [Network Architecture](/solana)
  * [Community Governance](/governance)
  * [Dev Blog](/devblog)
  * [Helium GitHub](https://github.com/helium)

Search```K`

  * [Helium Network Token](/tokens/hnt-token)
  * [IOT Network Token](/tokens/iot-token)
  * [MOBILE Network Token](/tokens/mobile-token)
  * [Data Credit](/tokens/data-credit)
  * [SOL Token](/tokens/sol-token)

On this page

# The Helium Network Token

![](/img/blockchain/heliumtoken.png)

The Helium Network Token (HNT) is the native cryptocurrency and protocol token
of the Helium Network.

The original Helium blockchain produced the first HNT on July 29th, 2019, on
block 93. There was no pre-mine of HNT before the launch of the Network. The
Helium network migrated to the Solana Blockchain on April 18, 2023.

The mint address for HNT is
[`hntyVP6YFm1Hg25TN9WGLqM12b8TQmcknKrdu1oxWux`](https://explorer.solana.com/address/hntyVP6YFm1Hg25TN9WGLqM12b8TQmcknKrdu1oxWux)
on the Solana blockchain.

Navigate to <https://explorer.helium.com/stats> for up-to-date information on
Network tokens.

## HNT Usage​

HNT serves the needs of the two primary parties in the Helium Ecosystem:

  1. **Hotspot Hosts and Operators**. Hosts are rewarded in network tokens like [IOT](/tokens/iot-token) or [MOBILE](/tokens/mobile-token) while deploying and maintaining network coverage. These network tokens are redeemable for HNT.
  2. **Enterprises and Developers use the Helium Network** to connect devices and build IoT applications. [Data Credits](/tokens/data-credit), which are a $USD-pegged utility token derived from HNT, [are used to pay transaction fees](/iot/transaction-fees) for wireless data transmissions on the Network.

## HNT Token Economic Concepts​

The Network uses three token economic concepts to ensure HNT supply is both
plentiful for usage needs and relatively scarce, with a known maximum.

Daily Net Emissions

### Max Supply​

The Network targeted the distribution of 5,000,000 HNT per month at launch.
Following the community approval of HIP-20, the Network uses a two-year
halving schedule, resulting in a maximum HNT supply of 223,000,000 HNT.

Year| Year Start| HNT at Year Start| Target HNT Emission  
---|---|---|---  
1| August 1st, 2019| 0| 60,000,000  
2| August 1st, 2020| 60,000,000| 60,000,000  
3| August 1st, 2021| 120,000,000| 30,000,000  
4| August 1st, 2022| 150,000,000| 30,000,000  
5| August 1st, 2023| 180,000,000| 15,000,000  
6| August 1st, 2024| 195,000,000| 15,000,000  
7| August 1st, 2025| 210,000,000| 7,500,000  
8| August 1st, 2026| 217,500,000| 7,500,000  
  
> The full token emission schedule can be viewed in the HNT section of this
> document: [Token Emissions as of Solana
> Migration](https://github.com/helium/HIP/blob/main/files/0077/token-
> emissions-as-of-solana-migration.pdf).

### Burn and Mint Economics​

[Data Credits](/tokens/data-credit) (DC) are a $USD-pegged utility token
derived from HNT and is used to pay fees on the Helium Network. DC is only
produced by burning HNT. This HNT to DC relationship is based on a design
commonly called a [burn and mint
equilibrium](https://multicoin.capital/2018/02/13/new-models-utility-tokens/)
and intends to allow for the supply of HNT to respond to network usage trends.

### Net Emissions​

As the halving schedule progresses, it is possible that the HNT minted per
epoch is not sufficiently divisible for data transfer rewards. Therefore, in
order to ensure that miners are incentivized to continue transmitting data and
ensure a healthy, robust network, the Net Emissions mechanism was instituted
in August 2021.

Net Emissions give the protocol enough HNT for rewards in perpetuity by
monitoring the number of HNT burned for DC in a given epoch and adding that to
the number of HNT to mint that epoch. Because HNT produced via Net Emissions
do not add to the total outstanding, they do not violate max supply. However,
to ensure that the deflationary pressure is still present, the Net Emission is
capped at 1% of the epoch emission.

For instance, in February 2024, the Net Emissions cap is 1,643.83561643 HNT
per epoch, and the up-to-date value can be verified [on
chain](https://explorer.solana.com/address/BQ3MCuTT5zVBhNfQ4SjMh3NPVhFy73MPV8rjfq5d1zie/anchor-
account).

If less than 1,643.83561643 HNT is burned for DC within an epoch, the full
amount burned will be re-minted and distributed into the subnetwork's Treasury
for that epoch. However, if more than 1,643.83561643 HNT is burned for DC
within a single epoch, any HNT burn for DC over 1,643.83561643 will be
permanently burned and removed from the max supply, while 1,643.83561643 being
re-minted and distributed to the subnetwork.

Review the [complete Net Emissions discussion in the
HIP](https://github.com/helium/HIP/blob/master/0020-hnt-max-supply.md#net-
emissions) for more information. Note that in HIP-20, the cap was 34.24 HNT
because the epoch was every 30 minutes at the time HIP-20 was written. The
current epoch is only 24 hour basis, yielding a cap of 1,643.83561643 HNT.

[Edit this page](https://github.com/helium/docs/edit/master/docs/tokens/hnt-
token.mdx)

[NextIOT Network Token](/tokens/iot-token)

  * HNT Usage
  * HNT Token Economic Concepts
    * Max Supply
    * Burn and Mint Economics
    * Net Emissions

Copyright © 2024 Helium Foundation

![](/static/images/brand-logo.svg)

[](/helium/embed/query/7417/visualization/21858)

