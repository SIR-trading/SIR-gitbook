# 🚧 Constraints on Pool Parameters

#### Token Constraints

The collateral and debt tokens must satisfy some mild constraints:

{% hint style="success" %}
COL and DBT must comply with the [ERC20 standard](https://ethereum.org/en/developers/docs/standards/tokens/erc-20/).
{% endhint %}

In addition, because SIR relies on the Uniswap v3 oracle:

{% hint style="success" %}
COL and DBT must be traded directly in one Uniswap v3 pool. When the tokens trade in more than one [fee tier](https://docs.uniswap.org/protocol/concepts/V3-overview/fees#pool-fees-tiers) in Uniswap v3, SIR performs a price geometric mean weighted by liquidity.
{% endhint %}

#### Leverage Ratio Discrete Set

To avoid the fractionalization of liquidity across pools, the leverage ratio can also not just be any real number. Imagine there were was a pool with leverage ratio 1.5 and another pool with all parameters equal but leverage ratio 1.51, they would effectively be the same pool and split the liquidity.

{% hint style="success" %}
The leverage ratio is artificially constrained by the SIR protocol to a set of discrete points: $$\begin{equation}  l\in\left\{1+2^k : k\in \mathbb{Z}\right\} \end{equation}$$.
{% endhint %}

The goal of offering a very wide range of values is to leave it up to the users to decide the best pool parameters.

{% hint style="info" %}
We denominate $$k$$, **the leverage tier**.
{% endhint %}
