---
description: A New DeFi Primitive for Holding Leverage
---

# 💡 Why SIR Matters

## The Missing Primitive

DeFi has produced a handful of genuine financial primitives — mechanisms so fundamental they become building blocks for everything else. AMMs let anyone provide liquidity. Flash loans enabled atomic arbitrage. Perpetuals brought leveraged exposure on-chain. Each was dismissed early and recognized late.

SIR is the first protocol that lets you **hold leveraged exposure indefinitely** without volatility decay, funding fees, or liquidation. That makes it something new: a vanilla leveraged token that actually works.

## Holding Leverage Is Practically Impossible

Every existing approach to leverage forces you into a tradeoff between cost, risk, and time:

| Approach | Volatility Decay | Ongoing Fees | Liquidation | Practical Hold Duration |
|----------|:---:|:---:|:---:|:---:|
| Margin Trading | — | Funding rates | Yes | Days to weeks |
| Leveraged ETFs/Tokens | Severe | Hidden (rebalancing) | No | Degrades over time |
| Perpetuals | — | Funding rates | Yes | Days to weeks |
| Options | Time decay | Premium | Expiration | Fixed term |
| **SIR** | **No** | **One-time mint fee** | **No** | **Unlimited** |

None of the traditional approaches let you say "I want 1.5x long ETH" and walk away for a year. SIR does.

## The Rebalancing Problem

To understand why SIR is different, you need to understand why every other leveraged token fails over time.

Traditional leveraged tokens (like the ones FTX offered, or leveraged ETFs in traditional finance) maintain their target leverage by **rebalancing daily**. When the underlying asset goes up, they buy more. When it goes down, they sell. This sounds reasonable — until you see what it does to your money.

Consider a hypothetical 3x leveraged token tracking an asset that goes up 10% one day and down 10% the next, repeatedly:

- **The underlying asset** oscillates but trends sideways
- **The 3x token** buys high and sells low on every rebalance, bleeding value with each cycle
- After enough cycles, the leveraged token has lost significant value even though the underlying is flat

This is volatility decay, and it's not a bug — it's a mathematical certainty of any rebalancing strategy. The more volatile the underlying, the faster the decay. In crypto, where 5-10% daily moves are routine, leveraged tokens can lose most of their value in weeks during choppy markets.

## What Makes SIR Different

SIR's leveraged tokens (APE) don't rebalance. Instead, they track a **power-law formula**:

$$
\text{Value} = x(1-f)\left(\frac{p'}{p}\right)^l
$$

Your return depends only on where the price ends up relative to where you entered — not the path it took to get there. This means:

- **No volatility decay** — sideways markets don't erode your position
- **Convex payoff** — you gain more on the upside than you lose on the downside
- **No liquidation** — your position can lose value but never goes to zero
- **No funding fees** — you pay once when you mint, then hold as long as you want

The tradeoff is an upfront minting fee (roughly equivalent to one year of funding on a perps position) and the fact that leverage is bounded by available liquidity. For the full math, see [Take on Leverage and Forget](take-on-leverage-and-forget.md).

## Real Utility

This isn't just a trading toy. Vanilla leveraged tokens unlock use cases that were previously impractical:

- **Long-term directional bets** — Bullish on ETH over the next year? Take 1.5x exposure and forget about it. No maintenance, no margin calls, no daily check-ins.
- **Capital-efficient hedging** — Hedge a portfolio position with less capital at risk than a full short would require.
- **Reduced anxiety** — No liquidation means no 3 AM margin calls. Your worst case is the minting fee, not your entire position.
- **Composability** — APE tokens are standard ERC-20s. They can be held, transferred, or integrated into other protocols like any other token.

## Multi-Chain

SIR is live on **Ethereum**, **HyperEVM**, and **MegaETH**, with the same core mechanics on each chain. See [Deployments](../deployments.md) for contract addresses across all chains.
