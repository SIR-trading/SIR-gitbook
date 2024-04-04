# 🎩 SIR Token

### Governance Token

SIR is the governance token of the SIR protocol. It is a token-based voting DAO which controls the SIR treasury.

{% hint style="info" %}
The DAO has limited powers and it cannot change or tune the SIR protocol parameters.
{% endhint %}

The DAO's abilities are limited to:

1. Control of the liquidity mining program
2. Control of the treasury funds

### Liquidity Mining Rewards

LPers in selected pools receive 100% of SIR token emissions in exchange for giving up a small portion of their fees to the DAO treasury fund. The overall portion of fees paid by the protocol to the treasury amounts to 5% or less of the total collected fees. We expect this trade-off to be profitable for LPers.

{% hint style="info" %}
The DAO is in charge of selecting the pools receiving the SIR tokens. The selection can be changed any time.
{% endhint %}

{% hint style="info" %}
100% of SIR token emissions go to LPers&#x20;
{% endhint %}

The term "liquidity mining" usually refers to the concept that LPers are rewarded with some internal token in exchange for their liquidity. The main idea is that liquidity in the protocol can be further boosted by adding extra rewards in addition to the collected fees. This helps boost the following **positive feedback loop**: (1) As LP liquidity increases, [the pool's leverage ratio becomes more stable](broken-reference), which attracts mores users in search for safe leverage and trustless stablecoins. More usage increases the collected fees, which subsequently attracts more LPers, increasing LP liquidity, etcetera.

<img src="../.gitbook/assets/file.drawing (3).svg" alt="The fees&#x27; positive feedback loop" class="gitbook-drawing">

### Treasury Fund

The DAO treasury fund feeds from fees collected from the protocol. The token holders have the power to spend such funds as they see fit. However, not all pools contribute to the DAO treasury. In order for a pool to give some of its fees to the DAO, it must receive a piece of the SIR token emissions in return. More details in [sir-token.md](sir-token/sir-token.md "mention").

### Issuance

Most protocol tokens are limited in supply because they are usually more appealing in the eye of the buyer. This is not surprising given Bitcoin's idiosyncrasy. Unfortunately, programming a protocol token with large emissions at the beginning of its life, and small or no tail emissions, can be counterproductive to the protocol itself.

{% embed url="https://twitter.com/Fiskantes/status/1426906528276271106" %}

We want to incentivize early adoption AND the solidification of the protocol long-term. For this reason we choose a different issuance model:

{% hint style="info" %}
The SIR token will have **constant-rate of emission**, meaning the same amount of SIR will be emitted at any point in time.
{% endhint %}

A constant-emission allows early adopters to still profit from the lack of competition, while late adopters still profit despite the extra competition from the fact that the token usually enjoys a higher price.

{% hint style="info" %}
Even though constant-emission implies an infinite diluted supply, its **inflation tends towards zero**.
{% endhint %}

#### Premine

10% of the total supply in the first 3 years is reserved for contributors including developers, advisors, community managers, etcetera. They will receive their rewards at the same pace than the LPers, i.e., for every 9 SIR that are liquidity mined, 1 SIR will be minted for contributors.

### Community & Speculation Vehicle

Token incentives are in fact a new crypto primitive. Those who get rewarded with SIR tokens become economically aligned with the growth of the protocol, creating a powerful community that voluntarily spreads its love. If we were to draw parallels with [meat space](https://www.tokenfy.com/glossary/meatspace-crypto/), it is as if buyers of iPhones got Apple shares for their loyalty.

In addition, having a token attached to a protocol serves as speculation vehicle for those who are bullish on the protocol and want to bet on it. It is a win-win proposition because the protocol benefits from a higher token price, and the SIR token holders benefit from a well functioning protocol.

