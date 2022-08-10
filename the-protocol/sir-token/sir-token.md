# ⛏ Automated Liquidity Mining

### Liquidity Mining Design

Contrary to [previous projects' liquidity mining](https://101blockchains.com/liquidity-mining/), **SIR's liquidity mining is part of the core protocol** and designed to last forever. The main reason is that we see it as a stabilizing force for the protocol, and not as a once-in-a-time ad-hoc program to benefit a few users for a short period of time. In addition, we want the SIR token to be as the SIR protocol: [immutable and trustless](../../).

#### Rewards Allocation

Assume pools are enumerated from $$1$$ to $$N$$. Let $$v_i \text{ [USD/day]}$$ be the revenue in fees made by pool $$i$$. Furthermore, let $$r_i \text{ [SIR/day]}$$ be the rewards received by pool $$i$$. <mark style="background-color:green;">Our goal is that each pool receives an amount of SIR tokens proportional to its revenue in fees</mark>:

$$
\begin{equation}
r_i = \beta\, v_i \;\forall i
\end{equation}
$$

for some constant $$\beta$$.

#### Fair Tax

Let $$c_i$$ be the % of fees taken by the DAO from pool $$i$$. For example if $$c_i=50$$, then 50% of all fees collected by pool $$i$$ would go to the DAO treasury. For the sake of fairness, <mark style="background-color:purple;">the % of fees taxed by the DAO from each pool should be proportional to the rewards it receives</mark>, i.e.,&#x20;

$$
\begin{equation}
c_i = \alpha\, r_i \;\forall i
\end{equation}
$$

for some constant $$\alpha$$. **This condition can be easily implemented via smart contract.**

Next, we analyze two different implementations of the proposed [rewards allocation](sir-token.md#rewards-allocation).

### Smart-Contract-Based Rewards Allocation

The naïve approach would be to hard code the rewards allocation into the smart contract. The problems are twofold:

1. It could be gamified/manipulated by a small group of LPers to maximize their own rewards
2. It is difficult to calculate $$v_i$$ for every pool because they use different collateral tokens

#### Manipulation Games

For example, a small group of LPers could create a new pool where they are the only LPers and wash trade APE and TEA to artificially increase the fee revenue. Since they are the LPers they would lose very little in fees and in exchange they would get most of the liquidity mining rewards.&#x20;

In another example, the LPers could also open a pool with a collateral token whose price is easy to manipulate because it is highly illiquid.

#### Heterogenous Tokens

Because pools can use arbitrary collateral tokens, which is the token the fees are paid on, it may be difficult to assest the fee

Evaluating every pool's fee revenue is hard because each pool has its own collateral token (the fees are paid in collateral token). To assess the fee revenue precisely would require some price conversion between all these tokens to a common token. However, this opens another can of worms.  How to get the price between any two tokens in a trustless manner? Uniswap does not have exchange pairs for every pair of tokens. What if the price is unreliable because it is obtained from a highly illiquid pool? The problems quickly stack up. &#x20;

### Incentive-Driven Rewards Allocation

As outlined in the previous section, a purely algorithmic solution is hard. Instead, we rely on a solution based on human discretion and economic incentives. The idea is simple, we let the DAO decide on the amount of fees subtracted from each pool.&#x20;

The only condition enforced by the protocol is that

$$
\begin{equation}
\sqrt{c_1^2+\cdots+c_N^2} \leq 5 \;[\%].
\end{equation}
$$

Because the fee allocation must be voted by the DAO, it is harder for a group of holders with a small stake to manipulate the outcome. From the DAO perspective, to maximize the treasury and consequently the SIR token price, the best strategy is to take fees from the pools generating the highest fees. In other words, the DAO is economically incentivized to

$$
\begin{equation}
\max c_1v_1+\cdots+c_Nv_N
\end{equation}
$$

where $$v_i$$ are the fees generated over some time period by the $$i$$-th pool (all denominated in the same currency). It turns out that the optimum solution to (2) subject to (1) is

$$
f_i= \beta \,v_i \;\forall i
$$

where $$\beta$$ is a constant.

{% hint style="info" %}
In summary, thanks to constraint (1), the DAO is economically incentivized to reward pools with an amount of SIR token proportional to their fee volume.
{% endhint %}
