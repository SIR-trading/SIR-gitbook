---
description: The Three-Token Economy and Business Model
---

# 💰 Economic Model

## The Three-Token Ecosystem

The SIR protocol operates through a synergistic three-token model, each serving distinct but interconnected roles:

**SIR Token: Governance & Value Capture**

* **Dividend Distribution:** Stake SIR to earn a share of protocol fees (WETH on Ethereum, WHYPE on HyperEVM, WETH on MegaETH)
* **Continuous Issuance:** 2.015 billion SIR per year, creating sustainable liquidity incentives
* **Future Governance:** Control treasury and direct reward allocations across vaults

**TEA Token: Liquidity Provision**

* **Liquidity Representation:** Mint TEA by depositing assets; burn to withdraw
* **Fee Structure:** 9% upfront deposit fee (retained as protocol-owned liquidity)
* **Revenue Streams:**
  * Primary: Trading fees from APE leverage positions
  * Secondary: SIR token rewards for selected vaults

**APE Token: Leverage Positions**

* **Position Management:** Minted when opening leverage, burned when closing
* **Fee Structure:** Substantial minting fee paid to LPers, scaling with leverage ratio (higher leverage = higher fee)
* **Revenue Generation:** Trading activity drives protocol fees distributed to stakeholders

## Business Model Architecture

The protocol's economic model can be understood through traditional business roles:

**Customers:** APE holders (leverage traders) who pay fees for leveraged positions. They are the primary revenue generators for the ecosystem.

**Service Providers:** TEA holders (liquidity providers) act as intermediaries, enabling leverage capacity. Greater TEA liquidity allows higher leverage potential, attracting more APE users.

**Stakeholders:** SIR holders capture value through dividends and governance rights, aligning their interests with protocol growth.

**Revenue Flow**

1. APE holders generate fees through leverage trading
2. Fees flow to TEA holders (90%) and SIR stakers (up to 10%)
3. SIR emissions incentivize TEA liquidity provision
4. Increased liquidity attracts more APE users, creating a growth flywheel

## Sustainable Tokenomics Design

**Why Constant Issuance?**

Unlike projects with capped supplies that front-load emissions, SIR maintains constant issuance for several strategic reasons:

**Long-term Viability:** High initial emissions followed by reduction creates unsustainable dynamics. As emissions decrease, new participants have less incentive to join, potentially leading to protocol forks or competitive disadvantages.

**Fair Opportunity:** Constant issuance ensures future liquidity providers (when TVL is higher) can still earn meaningful rewards, while early participants benefit from easier accumulation when liquidity is lower.

**Transparent Predictability:** Instead of teams selling tokens unpredictably to fund operations, SIR embeds liquidity incentives directly into the protocol in a transparent, permanent manner.

**The Best of Both Worlds**

For participants seeking to optimize their position:

* **Stake SIR:** Earn dividends from protocol fees
* **Provide Liquidity:** Earn SIR rewards to offset dilution
* **Do Both:** LP and stake earned SIR for maximum benefit (no dilution + dividends)

## Protocol-Owned Liquidity

SIR implements a groundbreaking approach where 9% of every TEA deposit becomes permanent protocol-owned liquidity (POL). This POL never withdraws and continuously earns fees, creating a growing foundation that reduces reliance on temporary incentives over time.

For detailed mechanics, benefits, and projections, see the dedicated [protocol-owned-liquidity.md](../liquidity-and-leverage/protocol-owned-liquidity.md "mention").

## Economic Alignment

**Incentive Structure**

The protocol aligns all participant incentives toward sustainable growth:

1. **APE Users:** Access leverage with predictable fees and deep liquidity
2. **TEA Holders:** Earn stable income from fees plus SIR rewards
3. **SIR Holders:** Capture protocol value through dividends and price appreciation
4. **Protocol Treasury:** Accumulates permanent liquidity for long-term resilience

**Mathematical Optimization**

Reward distribution follows economic contribution:

* Vaults receive SIR proportional to fees generated
* Maximum 10% fee redistribution ensures LPer profitability
* Quadratic constraint (√Σfi² ≤ 10%) optimizes allocation efficiency

This creates a self-balancing system where the most productive vaults naturally attract appropriate incentives, maximizing capital efficiency across the protocol.
