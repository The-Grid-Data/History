[![Website logo](https://archbee-image-
uploads.s3.amazonaws.com/1V4gfFTIaxtgPmnodv3E2/DhBhbHngHN0BOAIwdQOpo_logotype-
light.png)](https://sujiko.trade)

`Ctrl``K`

[🏃Getting Started](/)

🚀Perpetual Futures

[Funding Payments](/funding-payments)

[Trading Fees](/trading-fees)

[PNL Settlement](/pnl-settlement)

[Oracles](/oracles)

[🏦Liquidity Mechanism](/liquidity-mechanism)

[💱Flow Of Funds](/flow-of-funds)

[📒Listing & Delisting Process](/listing-and-delisting-process)

[👛Liquidity Providers](/liquidity-providers)

[📉Liquidations](/liquidations)

[⛓️Guardrails](/guardrails)

[🚧Risks](/risks)

🧑‍💻Developers

[📝SDK Documentation](/sdk-documentation)

[🕸️REST API](/rest-api)

[🤖Bots (Keeper & Trading)](/bots-keeper-and-trading)

[📖Terms of Use](/terms-of-use)

[🔅Disclaimer](/disclaimer)

[Docs powered by Archbee](https://www.archbee.com/?utm_campaign=hosted-
docs&utm_medium=referral&utm_source=docs.sujiko.trade)

# Liquidity Mechanism

13min

Sujiko uses a liquidity mechanism composed of a) a core hybrid virtual AMM
(vAMM), b) auction mechanism and c) limit orderbook.

## Hybrid Virtual AMM (vAMM)

A normal AMM has the same price for asks and bids with flat fee.

Sujiko, however, leverages a hybrid [vAMM](https://blog.perp.fi/a-deep-dive-
into-our-virtual-amm-vamm-40345c522eeb "vAMM") implementing the [constant
product algorithm](https://uniswapv3book.com/docs/introduction/constant-
function-market-maker/ "constant product algorithm") — allowing for better
market efficiency and risk management.

Our hybrid vAMM has configurable parameters such as initial/maintenance margin
ratio, minimum/maximum spread, initial reserves (referred to as terminal
reserves), liquidity depth, max fill reserve fraction, etc.

The base price, also known as reservation price, adjusts based on the current
oracle price. The bid/ask price quoted by the hybrid vAMM is equal to the
reservation price ± base_spread + f(inventory skew).

Each perpetual futures market on Sujiko includes tracking for:

  * Last 10 oracle values (lookback window for volatility dampening)

  * Mark TWAP - 1HR + Oracle TWAP - 1HR (used for funding)

  * Mark TWAP - 5min + Oracle TWAP - 5min (used to determine market health i.e. if mark price > 20% from TWAP)

Each hybrid vAMM of each perpetual futures market has an associated isolated
adjustments pool, funding rate pool, and insurance fund pool. The adjustments
pool is used to adjust the base price by rebalancing the pool through a repeg.
The funding rate pool is used to pay out/receive funding payments to/from
traders with positions.

The insurance fund pool is used to cover losses from liquidations. When a
position is liquidated, a liquidation penalty is incurred. This liquidation
penalty is added to the insurance fund pool.

A perpetuals futures market can enter a restricted mode if it is deemed
unhealthy. This can occur when a strong imbalance of longs and shorts exists
or the divergence between oracle and mark price exceeds a pre-defined limit of
20%. When a market enters restricted mode, there will be restrictions to order
fills, liquidations, and funding rate updates if they increase protocol risk.

## **Repeg Event**

A repeg event effectively keeps the funding rate within a range. The
cost/benefit of the repeg is the change in total liquidating cost of the net
position of the protocol. This is implemented using a scaling factor we call
m_mul:

Markdown

m_mul = p_oracle / p_mark  

m_mul = p_oracle / p_mark

﻿

The new hybrid vAMM mark price can be calculated using:

Markdown

p_newmark = m_mul * (y / x)  

p_newmark = m_mul * (y / x)

﻿

Where:

  * y = quote reserves

  * x = base reserves in the hybrid vAMM

The protocol will check if a repeg is required on any trade or after a funding
payment is made. If the divergence between oracle and mark price is greater
than 5% for more than 3 hours, a repeg event is triggered and the hybrid
vAMM’s mark price is reset to the oracle price. Each market’s dedicated
adjustments pool will cover any costs that arise from repeg events.

Repeg cost (difference between actual and terminal reserves).

peg cost| Direction| Use optimal peg| Revenue  
---|---|---|---  
0| Any| Yes| Yes  
> 0| Down| Yes| Yes  
< 0| Up| Yes| Yes  
budget > cost| Any| Yes| Yes  
ELSE| Any| No| No  
  
We can calculate a repeg cost using:

Markdown

(reserves_quote-reserves_terminalquote)*(peg_newmark - peg_multiplier)  

(reserves_quote-reserves_terminalquote)*(peg_newmark - peg_multiplier)

﻿

If there are enough funds in the pool, we will repeg when profitable or cost-
free.

## Auction Mechanism (Dutch Auctions)

To prevent [toxic orderflow](https://deepwaters.xyz/learn/toxic-order-flow
"toxic orderflow"), we’ve implemented an auction mechanism for taker orders
which applies to liquidation orders. The auction process mimics a small
settlement delay for taker orders (where the delay is t = 5s).

### **Parameters**

Each market order enters an individual auction that has three default
parameters:

Order direction| Buy| Sell  
---|---|---  
Start price| Oracle price| Oracle price  
End price| vAMM ask price| vAMM bid price  
Duration| 5 seconds| 5 seconds  
  
The auction is a Dutch-style regular auction where the price goes from best to
worst for the taker.

The auction ends up creating a price band per auction where the top of price
band = hybrid vAMM price and bottom of price band = oracle price (if market
order is buy direction and conversely if sell direction).

### Order Flow: Market Orders

  1. A trader submits a market order. On submission, the order is validated and broadcast to off-chain keepers.

  2. The market order is first attempted to be matched with any orders on Sujiko’s limit orderbook. If there are no matching orders or there is size remaining after matching against limit orders, the remaining size will be placed in a Dutch auction.

  3. The market order enters the Dutch auction with a start time, specific start price (oracle price), end price (hybrid vAMM quote price), and duration (fixed at 5s).

  4. Market makers can compete to fill the trader’s order at a price better than or equal to the current auction price.

  5. If no market maker fills the order within the duration or there is only a partial fill, the remaining order size will be filled by the hybrid vAMM. The hybrid vAMM may repeg and adjust its bid/ask quotes before settling the remaining size.

### Limitations Of Dutch Auctions

  * There can only be up to 32 auctions at one given time for a given market. Makers can enter any and as many auctions as they wish to.

  * Market orders can be partially filled based on slippage tolerance and available liquidity.

  * An auction can be cancelled midway by the initiating trader. This does not apply to any partially filled size.

  * The auction mechanism is isolated from the limit orderbook (i.e. orders posted for a specific auction will not appear on the limit orderbook during or after the auction).

## Limit Orderbook

Each perpetual futures market on Sujiko has an individual limit orderbook.

Sujiko’s limit orderbooks mimic central limit order books (CLOBs) through an
off-chain network of keepers.

Orders are kept in trader accounts on-chain. When a keeper starts up, it will
fetch on-chain orders and construct an in-memory orderbook where orders
include price, size, time/age. Keepers will sort orders by price, then age,
then size if two orders have matching age.

### Order Flow: Limit Orders

  1. Traders submit limit order as post-only. On submission, order is validated.

  2. Keepers listen to trader account changes and see new order. Order is added into in-memory orderbook.

  3. Next, 3 scenarios are possible:

    1. Hybrid vAMM price hits limit order price. Keeper network observes this and submits a settlement instruction (settling the limit order against the hybrid vAMM’s quoted price).

    2. A market order is submitted that matches the limit order. In this event, the limit order is filled up to the size of the market order. If the limit order is only partially filled, it remains on the limit orderbook with the remaining size.

    3. A limit order (taker, fill-or-kill) is submitted at the same price as the post-only limit order.

### Limitations Of Limit Orderbooks

  * Each trader can only have 64 total open orders across all markets.

  * Two post-only orders cannot be matched with each other.

  * Orders filled by the hybrid vAMM are not eligible for fee rebate.

  * There can be scenarios where an order is not filled due to degraded network conditions. The keeper network depends on transactions being processed successfully and if the network is degraded (e.g. network halt or low TPS) transactions may not confirm as expected.

## **Keeper Rewards**

Keepers will earn a portion of the fees generated through matched orders.

Traders can increase the likelihood of an order being filled by paying a
additional fee capped at 0.1 SOL. This fee is directly paid to the keeper for
matching the order.

Updated 25 Mar 2024

![Doc
contributor](https://lh3.googleusercontent.com/a/AGNmyxbDN5iT7VOjich934jqre3CmHU0G2wiJV0ERbBm=s96-c)

Did this page help you?

Yes

No

[PREVIOUSOracles](/oracles "Oracles")[NEXTFlow Of Funds](/flow-of-funds "Flow
Of Funds")

[Docs powered by Archbee](https://www.archbee.com/?utm_campaign=hosted-
docs&utm_medium=referral&utm_source=docs.sujiko.trade)

TABLE OF CONTENTS

Hybrid Virtual AMM (vAMM)

Repeg Event

Auction Mechanism (Dutch Auctions)

Parameters

Order Flow: Market Orders

Limitations Of Dutch Auctions

Limit Orderbook

Order Flow: Limit Orders

Limitations Of Limit Orderbooks

Keeper Rewards

[Docs powered by Archbee](https://www.archbee.com/?utm_campaign=hosted-
docs&utm_medium=referral&utm_source=docs.sujiko.trade)

Press space bar to start a drag. When dragging you can use the arrow keys to
move the item around and escape to cancel. Some screen readers may require you
to be in focus mode or to use your pass through key

Press space bar to start a drag. When dragging you can use the arrow keys to
move the item around and escape to cancel. Some screen readers may require you
to be in focus mode or to use your pass through key

Press space bar to start a drag. When dragging you can use the arrow keys to
move the item around and escape to cancel. Some screen readers may require you
to be in focus mode or to use your pass through key

