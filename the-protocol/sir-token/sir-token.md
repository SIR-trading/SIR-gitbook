# ⛏️ Automated Liquidity Mining

### Liquidity Mining Design

Contrary to [previous projects' liquidity mining](https://101blockchains.com/liquidity-mining/), **SIR's liquidity mining is part of the core protocol** and designed to last forever. The main reason is that we see it as a stabilizing force for the protocol, and not as a once-in-a-time ad-hoc program to benefit a few users for a short period of time. In addition, we want the SIR token to be as the SIR protocol: [immutable and trustless](broken-reference).

#### Rewards Allocation

Assume pools are enumerated from $$1$$ to $$N$$. Let $$v_i \text{ [USD/day]}$$ be the revenue in fees made by pool $$i$$. Furthermore, let $$R\text{ [SIR/day]}$$ be the SIR token issuance, and let $$r_i \text{ [SIR/day]}$$ be the rewards received by pool $$i$$ such that $$r_1+\cdots+r_N=R$$. <mark style="background-color:green;">Our goal is that each pool receives an amount of SIR tokens proportional to its revenue in fees</mark>:

$$
\begin{equation}
r_i = \alpha\, v_i \;\forall i
\end{equation}
$$

where $$\alpha = R / (v_1+\cdots+v_N)$$ is a normalization constant. As explained in [the next section](sir-token.md#the-drawbacks-of-algorithmic-liquidity-mining) **this condition **<mark style="color:red;">**cannot**</mark>** be easily implemented via smart contract.**

#### Fair Tax

Let $$c_i$$ be the % of fees taken by the DAO from pool $$i$$. For example if $$c_i=50$$, then 50% of all fees collected by pool $$i$$ would go to the DAO treasury. For the sake of fairness, <mark style="background-color:purple;">the % of fees taxed by the DAO from each pool should be proportional to the rewards it receives</mark>, i.e.,&#x20;

$$
\begin{equation}
c_i = \beta\, r_i \;\forall i
\end{equation}
$$

for some constant $$\beta$$. **This condition can be **<mark style="color:green;">**easily**</mark>** implemented via smart contract.**

Next, we analyze two different implementations of the proposed [rewards allocation](sir-token.md#rewards-allocation).

### Smart-Contract-Based Rewards Allocation

The naïve approach would be to hard code the rewards allocation into the smart contract. The problems with this approach are twofold:

1. It could be gamified/manipulated by a small group of LPers to maximize their own rewards
2. It is difficult to calculate $$v_i$$ for every pool because they use different collateral tokens

#### Manipulation Games

For example, a small group of LPers could create a new pool where they are the only LPers and wash trade APE and TEA to artificially increase the fee revenue. Since they are the LPers they would lose very little in fees and in exchange they would get most of the liquidity mining rewards.&#x20;

In another example, the LPers could also open a pool with a collateral token whose price is easy to manipulate because it is highly illiquid.

#### Heterogenous Tokens

Evaluating every pool's fee revenue is hard because each pool has its own collateral token (the fees are paid in collateral token). To assess the fee revenue precisely would require some price conversion between all these tokens to a common token. However, this opens another can of worms.  How to get the price between any two tokens in a trustless manner? Uniswap does not have exchange pairs for every pair of tokens. What if the price is unreliable because it is obtained from a highly illiquid pool? The problems quickly stack up. &#x20;

### Incentive-Driven Rewards Allocation

As outlined in the previous section, a smart contract solution for achieving (1) is hard. Instead, we rely on a solution based on human discretion and economic incentives.&#x20;

We show next that by enforcing via smart contract that the fees taxed from each pool are subject to

$$
\begin{equation}
\sqrt{c_1^2+\cdots+c_N^2} \leq 5 \;[\%].
\end{equation}
$$

the DAO will be economically incentivized to allocate rewards as in (1).

#### Proof

The DAO's best interest is to maximize the treasury which will indirectly boost the SIR token price. Consequently, the DAO's optimum strategy is to tax the pools generating the highest fees. In other words, the DAO is economically incentivized to

$$
\begin{equation}
\max c_1v_1+\cdots+c_Nv_N
\end{equation}
$$

where $$v_i$$ is the fee revenue of pool $$i$$. It turns out that the optimum solution to (3) subject to (2) is

$$
\begin{equation}
c_i= \gamma\,v_i \;\forall i
\end{equation}
$$

where $$\gamma = 5 (v_1^2+\cdots+v_N^2)^{-1/2}$$ is a constant. Combining (3) and (2), we get (1).

{% hint style="info" %}
In summary, thanks to the constraint on the pool taxes in [#rewards-allocation](sir-token.md#rewards-allocation "mention"), the DAO is economically incentivized to reward pools with an amount of SIR token proportional to their fee revenue.
{% endhint %}
