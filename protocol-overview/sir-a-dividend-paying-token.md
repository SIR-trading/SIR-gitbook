---
description: An Immutable Token with Real Utility
---

# 🎩 SIR: A Dividend-Paying Token

SIR is not only the protocol but also its native token and it plays a multifaceted role:

* **A Speculative Vehicle:** The SIR token offers holders a claim on the protocol's fees, establishing strong fundamentals for the token and positioning it as a prime vehicle for speculation on the protocol's success.
* **Liquidity Mining Embedded in the Protocol:** SIR tokens are distributed to liquidity providers (LPers) as an incentive to enhance liquidity within key, selected vaults, starting from the protocol's launch and continuing indefinitely. While the allocation of rewards across vaults can be adjusted, this mechanism is integrated into the protocol's core contracts, ensuring its permanence and ongoing support for liquidity.
* **Governance and Reward Allocation:** The SIR DAO, powered by SIR holders, has the unique role of deciding which vaults are rewarded with SIR issuance in exchange for a portion of their fees. This setup aligns the interests of SIR holders with the protocol's success, as best vaults to allocated rewards are also those that generate the highest fees.

## **Liquidity Mining as a Core Feature**

The concept of "liquidity mining" gained prominence during the [DeFi summer of 2020](https://medium.com/@lily\_trangpham/the-formation-of-defi-summer-2020-conditions-for-a-new-defi-summer-a419d53d0d31), offering an innovative way to boost protocol liquidity by rewarding LPers with protocol tokens. Unlike temporary initiatives, SIR integrates liquidity mining as a permanent feature within its core contracts, ensuring its ongoing operation without an end date.

In SIR, select vaults are chosen to receive token emissions. LPers in these vaults earn SIR tokens in return for sacrificing a portion of their fees to SIR stakers, capped at 10% of the vault's total fees. The compensation in SIR tokens is directly proportional to the percentage of fees relinquished. For instance, a vault forfeiting 10% of its fees receives twice as much SIR compared to one forfeiting 5%. As a result, the total fees redistributed as dividends by the protocol do not exceed 10% of the collected fees, aiming to make this arrangement beneficial for LPers.

### Constant Issuance Rate

Many protocol tokens opt for a limited supply to enhance their appeal among buyers, a trend influenced by Bitcoin's model. However, structuring a token with high initial emissions followed by reduced or negligible emissions over time can ultimately hinder the protocol's long-term viability as Fiskantes explains:

{% embed url="https://twitter.com/Fiskantes/status/1426906528276271106" %}

SIR's issuance will start as soon as the protocol launches, with its functions and mechanisms locked in. The token is emitted at a constant rate of **2015 million SIR per year** _ad infinitum_. Early holders benefit from generous rewards in a nascent ecosystem and the potential token appreciation. Later entrants benefit from the steady emission rate and higher valuation. To mitigate dilution LPers can keep their liquidity in the protocol.

### First 3 Years

During the first three years, 30% of SIR token emissions are diverted as follows: 10% to pre-mainnet contributors, 10% reserved in a treasury for post-mainnet contributors, and 10% to investors. Here, "contributors" broadly includes coders, testers, advisors, etc. After this period, all subsequent token emissions are directed to LPers.

## Minimal Governance

There is only 1 aspect of the protocol that requires human input. Because vaults use different tokens as collateral, there is no simple way to compute at the smart contract level which vaults generate the most amount of fees, have the highest volume, or any other interesting economic metric. Thus, a fully automated smart contract-based approach to selecting the vaults receiving SIR rewards could easily fail. Using Uniswap v3 as price oracle is also extremely complicated because there are no pools for every single pair of tokens.

The solution to this it let SIR token holders vote on the vaults that receive SIR token rewards and their allocations. The idea here is to have use economic incentives to align SIR token holders. As we said before, mathematically, the amount of rewards by vault $$i$$, $$r_i$$, is proportional to the amount of fees it forfeited, $$t_i$$:

$$
r_i=\alpha f_i
$$

&#x20;where $$\alpha$$ is a constant. The units of $$r_i$$ are $$[\textrm{SIR/s}]$$ and $$f_i$$ is a percentage $$[\textrm{%}]$$. The only mathematical constraint enforced by the protocol is
