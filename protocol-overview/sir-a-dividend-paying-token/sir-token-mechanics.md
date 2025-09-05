---
description: How the SIR Token Works - Staking, Dividends, and Governance
---

# 🎩 SIR Token Mechanics

The SIR token serves as the protocol's value-capture mechanism and governance backbone, designed with sustainable economics and aligned incentives at its core.

## Core Functions

**1. Dividend Distribution**
SIR holders can stake their tokens to earn a share of protocol fees. All fees are converted to WETH through an [auction system](../token-auctions.md) and distributed to stakers, providing a direct claim on the protocol's revenue.

**2. Perpetual Liquidity Incentives**
Unlike temporary liquidity mining programs, SIR embeds token distribution directly into the protocol's immutable contracts. This ensures continuous, predictable rewards for liquidity providers without arbitrary end dates or governance votes.

**3. Future Governance**
Once the SIR DAO is established, token holders will govern:
- Vault selection and reward allocation for SIR emissions
- Treasury management

This creates a direct alignment: vaults generating the highest fees receive optimal reward allocation, maximizing value for all stakeholders.

## Staking Mechanics

**How Staking Works**
To earn protocol dividends, SIR holders must stake their tokens, temporarily removing them from circulation. Key features:
- **Flexible Operations:** Stake, unstake, and claim dividends at any time
- **WETH Dividends:** All protocol fees are converted to WETH via [auctions](../token-auctions.md) for consistent payouts
- **Pro-rata Distribution:** Rewards proportional to your staked share

**Anti-Exploitation Locking**
Staked SIR follows a progressive unlocking mechanism to prevent flash loan attacks:
- **Initial Lock:** 100% locked upon staking
- **Exponential Decay:** 30-day half-life unlocking schedule
  - Day 30: 50% unlocked
  - Day 60: 75% unlocked  
  - Day 90: 87.5% unlocked
- **Continuous Process:** Unlocking occurs every second, not in discrete steps

This design prevents short-term manipulation while maintaining long-term flexibility for genuine stakers.

## Token Issuance Model

**Constant Emission Rate**
SIR tokens are emitted at a fixed rate of **2.015 billion per year**, starting from zero supply at launch. This predictable, linear issuance continues indefinitely.

**Why Not Capped Supply?**
Many protocols follow Bitcoin's model with limited supply and decreasing emissions. However, as Fiskantes explains, front-loaded emissions create unsustainable dynamics:

{% embed url="https://twitter.com/Fiskantes/status/1426906528276271106" %}

Our constant issuance model ensures:
- **Early Participants:** Benefit from easier accumulation when liquidity is low
- **Future Participants:** Still receive meaningful rewards when TVL is higher
- **Sustainable Growth:** Avoid the "death spiral" of diminishing rewards
- **Mitigation Strategy:** LPers can retain positions to offset dilution through rewards

## Liquidity Mining Framework

**Permanent Integration**
Unlike temporary "liquidity mining" campaigns from DeFi Summer 2020, SIR embeds rewards directly into immutable smart contracts. This creates:
- **Predictable Incentives:** No arbitrary end dates or governance votes
- **Long-term Commitment:** Permanent support for protocol liquidity
- **Fair Distribution:** Rewards proportional to economic contribution

**Vault Reward Mechanism**
Selected vaults receive SIR emissions in exchange for sharing fees with stakers:
- **Fee Sharing Cap:** Maximum 10% of vault fees to SIR stakers
- **Proportional Rewards:** 10% fee share earns 2x the SIR of 5% share
- **Aligned Incentives:** Most productive vaults receive optimal rewards

## Governance & Vault Selection

**The Human Element**
While most protocol functions are automated, vault selection requires human judgment due to:
- **Token Diversity:** Various collateral types across vaults
- **Oracle Limitations:** Not all token pairs have Uniswap v3 pools
- **Economic Complexity:** Difficulty measuring true vault productivity on-chain

**DAO-Driven Optimization**
The SIR DAO will manage vault rewards through mathematical optimization:

**Reward Formula:**
$$r_i = \alpha f_i$$

Where:
- $$r_i$$ = Vault reward rate [SIR/s]
- $$f_i$$ = Fee contribution [%]
- $$\alpha$$ = Proportionality constant

**Optimization Constraint:**
$$\sqrt{\sum f_i^2} \leq 10\%$$

This ensures rewards match economic contribution while maintaining system sustainability.

**Example Allocation**
Two-vault scenario:
- Vault 1: $1M fees → 403M SIR/year (20%)
- Vault 2: $4M fees → 1,612M SIR/year (80%)

The mathematical framework guarantees fair, efficient capital allocation across all protocol vaults.