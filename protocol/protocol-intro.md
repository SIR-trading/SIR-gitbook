# ⚙ Protocol Intro

The Factory contract allows anyone to instantiate new pools in the protocol. Each pool is identified by the following unique set of properties:

1. <mark style="background-color:blue;">Collateral token</mark> (COL) address
2. <mark style="background-color:green;">Debt token</mark> (DBT) address
3. <mark style="background-color:orange;">Leverage ratio</mark> ($$l$$)

{% hint style="danger" %}
There cannot exist two pools with the same set of parameters.
{% endhint %}

Each pool spawns a [TEA token](../introduction/trustless-stablecoins/tea-token-basics.md) and an [APE token](../introduction/safer-leverage/ape-token-basics.md) that are also unique and managed by the pool. However, strictly speaking not any pair of tokens and leverage ratio can be selected for a pool.

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
The leverage ratio is artificially constrained by the SIR protocol to a set of discrete points:

$$\begin{equation}  l\in\left\{1+2^k : k\in \{-20,-19,\ldots,19,20\}\right\} \end{equation}$$,

which effectively \*limits\* the leverage to the range \[1.00000095367, 1,048,577].&#x20;
{% endhint %}

These are some extreme ludicrous minimum and maximum values which will most likely never be selected. The goal of offering a very wide range of values is to leave it up to the users to decide the best pool parameters.

{% hint style="info" %}
We denominate $$k$$, which ranges from -20 to 20, **the leverage tier**.
{% endhint %}

### Two Types of Users

Definitions:

* We call holders of APE, **apes**, because apes never back off from a leveraged trade.
* We call holders of TEA , **gentlemen**, because gentlemen love stability.

The properties of the pool defined in the previous section determine the properties of the APE and TEA tokens associated with each pool.

* <mark style="background-color:yellow;">APE tracks the price of COL/DBT with constant leverage ratio</mark> $$l$$​
* TEA is pegged to DBT and backed by a COL reserve with collateralization factor $$r$$

{% hint style="info" %}
The leverage ratio of the APE token ($$l$$) and the collateralization factor of the TEA token ($$r$$) are connected by the formula in [leverage-and-collateralization.md](apes-vs.-gentlemen/leverage-and-collateralization.md "mention").
{% endhint %}

To summarize,

|                   | APE 🦍   | TEA 🍵    |
| ----------------- | -------- | --------- |
| User label        | Ape      | Gentleman |
| Price             | COL/DBT  | DBT       |
| Leverage ratio    | $$l>1$$​ | 1 (none)  |
| Backed by         | COL      | COL       |
| Collateralization | N/A      | $$r>1$$​  |

{% hint style="info" %}
There is a 3rd type of user 🤵‍♀️, the liquidity providers (or LPers for short). Their token is called MAAM. More on it in [leverage-rebalancing](leverage-rebalancing/ "mention").
{% endhint %}

###
