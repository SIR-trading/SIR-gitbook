---
description: 'The Fine Print: What Could Go Wrong?'
---

# ⚠️ Security

The SIR protocol empowers leveraged trading and liquidity provision, but it's not without risks. While built on robust foundations, potential vulnerabilities might remain:

* **Smart Contract Bugs**: Despite being thoroughly audited by multiple independent security firms — see [Audits](audits.md) — undiscovered bugs or exploits in SIR's smart contracts could lead to fund losses. These might stem from complex logic in vault mechanics or leverage calculations that audits failed to catch, exposing users to rare but critical failures.

{% hint style="info" %}
This risk is mitigated by [our beta period and gradual transition to a fully decentralized protocol](beta-period.md), during which we can activate Emergency Mode or initiate a Shutdown to protect users if issues arise.
{% endhint %}

* **Third-Party Dependencies**: SIR relies on battle-tested on-chain DEXes for price data — Uniswap V3 on Ethereum, HyperSwap on HyperEVM, and Kumbaya on MegaETH. While these DEXes' established reliability minimizes concerns, any newly found vulnerability in their smart contracts could theoretically propagate to SIR, potentially disrupting operations or jeopardizing user funds. Though such risk is considered extremely low given the proven stability and track records of these platforms in the DeFi ecosystem.

Below, we outline risks specific to leverage users ("Apes") and liquidity providers ("LPers").

## Risks for Apes (Leverage Users)

Apes use SIR to take leveraged positions via vaults. These come with the following risks:

1. **Leverage Peg Breakdown**\
   If vaults reach [saturation](liquidity-and-leverage/) —where demand for leverage exceeds available liquidity— the target leverage ratio (e.g., `^2`) may falter. This can lead to reduced returns, and/or volatility decay.
2. **Volatility Decay in Saturation**\
   SIR eliminates volatility decay on a best-effort basis by maintaining constant leverage within the [convex zone](liquidity-and-leverage/#the-limits-of-constant-leverage). However, when a vault enters the [saturation zone](liquidity-and-leverage/#the-saturation-zone) — where LP liquidity is insufficient to maintain constant leverage — the same buy-high-sell-low rebalancing dynamic seen in traditional leveraged tokens can occur. The deeper into saturation, the more pronounced the decay. This risk is mitigated by the protocol's [self-balancing convexity loop](../introducing-sir/why-sir-matters.md#self-balancing-convexity), which incentivizes LP liquidity to keep the convex zone wide.

{% hint style="info" %}
SIR's convex payout structure means apes gain more on the upside and lose less on the downside compared to traditional perpetuals (_aka_ perps) or margin leverage — provided the vault operates within the convex zone.
{% endhint %}

## Risks for Liquidity Providers (LPers)

LPers supply capital to SIR's pools, earning fees from minting and burning. Their risks include:

1. **Low Activity and Fee Drought**\
   In periods of apathy, when apes aren't minting or burning, fee generation drops. This leaves LPers with idle capital and lower returns.

{% hint style="info" %}
However, [SIR's incentives](sir-a-dividend-paying-token/) to selected vaults can potentially offset this by providing a 2nd revenue stream.
{% endhint %}

2. **Impermanent Loss (IL)**\
   LPers may lose value compared to holding collateral assets when prices rise, but gain relative to holding debt tokens —and vice versa when prices fall. For unopinionated market participants, this dampens volatility rather than acting as a pure loss.
