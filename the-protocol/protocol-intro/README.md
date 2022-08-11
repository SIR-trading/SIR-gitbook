# ⚙ Protocol Intro

Analogously to Uniswap, the Factory contract allows anyone to instantiate new pools in the protocol. Each pool is identified by the following unique set of properties:

1. <mark style="background-color:blue;">Collateral token</mark> (COL) address
2. <mark style="background-color:green;">Debt token</mark> (DBT) address
3. <mark style="background-color:orange;">Leverage ratio</mark> ($$l$$)

{% hint style="danger" %}
There cannot exist two pools with the same set of parameters.
{% endhint %}

Each pool spawns a [TEA token](../../introduction/trustless-stablecoins/tea-token-basics.md) and an [APE token](../../introduction/safer-leverage/ape-token-basics.md) that are also unique and managed by the pool.&#x20;

### Two Types of Users

Definitions:

* We call holders of APE, **apes**, because apes never back off from a leveraged trade.
* We call holders of TEA , **gentlemen**, because gentlemen love stability.

The properties of the pool defined in the previous section determine the properties of the APE and TEA tokens associated with each pool.

* <mark style="background-color:yellow;">APE tracks the price of COL/DBT with constant leverage ratio</mark> $$l$$​
* TEA is pegged to DBT and backed by a COL reserve with collateralization factor $$r$$

{% hint style="info" %}
The leverage ratio of the APE token ($$l$$) and the collateralization factor of the TEA token ($$r$$) are connected by the formula in [Broken link](broken-reference "mention").
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
There is a 3rd type of user 🤵‍♀️, the liquidity providers (or LPers for short). Their token is called MAAM. More on it in [maam-token.md](../leverage-rebalancing/maam-token.md "mention").
{% endhint %}

### Minting / Burning

<mark style="background-color:green;">Minting</mark> :magic\_wand:: A user deposits the collateral token of the pool an gets TEA, APE or MAAM depending on what he wants.

<mark style="background-color:red;">Burning</mark> :fire:: A user burns TEA, APE or MAAM and instantly gets its value worth in collateral from the pool.

{% hint style="info" %}
The SIR protocol will always offer **instant liquidity**.
{% endhint %}

All three types of tokens, TEA, APE and MAAM, can be minted or burnt at any time. There are no bottlenecks that slow down withdrawals or deposits, or other-like functionalities like freezing.
