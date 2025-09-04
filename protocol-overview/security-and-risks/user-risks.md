---
description: 'The Fine Print: What Could Go Wrong?'
---

# ⚠️ User Risks

The SIR protocol empowers leveraged trading and liquidity provision, but it's not without risks. While built on robust foundations, potential vulnerabilities might remain:

* **Smart Contract Bugs**: Despite our [thorough audit with Egis Security](https://github.com/Egis-Security/audits/blob/main/reports/SIR-Trading.pdf), undiscovered bugs or exploits in SIR's smart contracts could lead to fund losses. These might stem from complex logic in vault mechanics or leverage calculations that audits failed to catch, exposing users to rare but critical failures.

{% hint style="info" %}
This risk is mitigated by [our beta period and gradual transition to a fully decentralized protocol](beta-period.md), during which we can activate Emergency Mode or initiate a Shutdown to protect users if issues arise.
{% endhint %}

* **Third-Party Dependencies**: SIR relies solely on the battle-tested Uniswap V3 for accurate and secure price data. While Uniswap V3's established reliability minimizes concerns, any new found vulnerability in its smart contract could theoretically propagate to SIR, potentially disrupting operations or jeopardizing user funds. Though such risk is considered extremely low given Uniswap's proven stability and track record in the DeFi ecosystem.

Below, we outline risks specific to leverage users ("Apes") and liquidity providers ("LPers").

## Risks for Apes (Leverage Users)

Apes use SIR to take leveraged positions via vaults. These come with the following risks:

1. **Leverage Peg Breakdown**\
   If vaults reach [saturation](liquidity-and-leverage/) —where demand for leverage exceeds available liquidity— the target leverage ratio (e.g., `^2`) may falter. This can lead to reduced returns, and/or volatility decay.
2. **Volatility Amplification**\
   Like any leveraged product, SIR amplifies both gains and losses in volatile markets, increasing the chance of liquidation or collateral erosion.&#x20;

{% hint style="info" %}
However, SIR's convex payout structure means apes gain more on the upside and lose less on the downside compared to traditional perpetuals (_aka_ perps) or margin leverage.
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
