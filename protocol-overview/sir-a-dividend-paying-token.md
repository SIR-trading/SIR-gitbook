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

In SIR, select vaults are chosen to receive token emissions. LPers in these vaults earn SIR tokens in return for sacrificing a portion of their fees to SIR stakers, capped at 10% of the vault's total fees. For fairness, the compensation in SIR tokens is directly proportional to the percentage of fees relinquished. For instance, a vault forfeiting 10% of its fees receives twice as much SIR compared to one forfeiting 5%. As a result, the total fees redistributed as dividends by the protocol do not exceed 10% of the collected fees, aiming to make this arrangement beneficial for LPers.

### Constant Issuance Rate

Many protocol tokens opt for a limited supply to enhance their appeal among buyers, a trend influenced by Bitcoin's model. However, structuring a token with high initial emissions followed by reduced or negligible emissions over time can ultimately hinder the protocol's long-term viability as Fiskantes explains:

{% embed url="https://twitter.com/Fiskantes/status/1426906528276271106" %}

SIR's issuance will start as soon as the protocol launches, with its functions and mechanisms locked in. The token is emitted at a constant rate of **2015 million SIR per year** _ad infinitum_. Early holders benefit from generous rewards in a nascent ecosystem and the potential token appreciation. Later entrants benefit from the steady emission rate and higher valuation. To mitigate dilution LPers can keep their liquidity in the protocol.

### First 3 Years

During the first three years, 30% of SIR token emissions are diverted as follows:&#x20;

* <mark style="background-color:blue;">10% to</mark> <mark style="background-color:blue;"></mark><mark style="background-color:blue;">**pre-mainnet contributors**</mark>,
* <mark style="background-color:green;">10% reserved in a treasury for</mark> <mark style="background-color:green;"></mark><mark style="background-color:green;">**post-mainnet contributors**</mark>, and
* <mark style="background-color:red;">10% to</mark> <mark style="background-color:red;"></mark><mark style="background-color:red;">**investors**</mark>

Here, "contributors" broadly includes coders, testers, advisors, etc. After this period, all subsequent token emissions are directed to LPers.

## Vault Selection Process

The protocol incorporates a singular aspect that necessitates human decision-making: vault selection. Given the diversity of tokens used as collateral across vaults, accurately evaluating which vaults are the most economically significant (e.g., generating the highest fees or volume) via smart contract is challenging. This complexity arises partly because not all token pairs have corresponding Uniswap v3 pools to facilitate straightforward valuation.

To address this, the protocol empowers SIR token holders to vote on which vaults should be awarded SIR token rewards and determine their specific allocations. This decision-making process is facilitated through the SIR DAO, utilizing economic incentives to align the interests of SIR token holders, ensuring that the rewards distribution reflects the economic contribution of each vault.

Mathematically, the reward for vault $$i$$, denoted as $$r_i​$$, is set to be proportional to the fees it contributes, denoted as $$f_i​$$, according to the formula:

$$
r_i=\alpha f_i
$$

Here $$\alpha$$ is a constant, $$r_i$$ is measured in $$[\textrm{SIR/s}]$$, and $$f_i$$ is a percentage $$[\textrm{%}]$$. The aim is for vaults to receive SIR tokens in direct proportion to their fee contributions. For instance, if we have only two vaults where vault 1 generates $1M in fees and vault 2 generates $4M, they would receive rewards of 403M SIR/year and 1612M SIR/year, respectively, under an ideal allocation.

By implementing the constraint:

$$
\sqrt{\sum f_i^2} \leq 10\textrm{ [%]}
$$

it's mathematically demonstrable that the optimal economic allocation of SIR, as overseen by the SIR DAO, follows the proposed model. This strategy ensures that token distribution effectively matches the economic input of vaults, maximizing the protocol's overall efficiency and fairness.
