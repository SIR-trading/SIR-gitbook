# ⚙ Protocol Design

Analogously to Uniswap, the Factory contract allows anyone to instantiate new pools in the protocol. Each pool has three unique features:

1. It uses a specific token as <mark style="background-color:blue;">collateral</mark> (COL)
2. Its debts is denominated in <mark style="background-color:green;">debt token</mark> (DBT)
3. It operates at a specific <mark style="background-color:orange;">leverage ratio</mark> ($$l$$)

{% hint style="danger" %}
There do not exist two pools with the same set of parameters.
{% endhint %}

COL and DBT can be any ERC-20 tokens that are traded in a Uniswap v3 pair. In addition each pool produces two unique tokens: [TEA ](../../introduction/trustless-stablecoins/tea-token-basics.md)and [APE](../../introduction/safer-leverage/ape-token-basics.md).

## Three Different Types of Users

Now, let's meet the users of our system:

* **Apes** - These are people who hold APE tokens. They are risk-takers who aren't scared of a little leverage. APE tokens' value follows the price of COL/DBT at a constant leverage ratio and is backed by COL.
* **Gentlemen** - These are the holders of TEA tokens. They enjoy stability. TEA is pegged to the value of DBT, and it's backed by a reserve of COL.
* **Liquidity Providers** - They're a special breed of users who contribute to the pool and get a unique token, called MAAM, in return.&#x20;

So, how do users get these tokens? It's a process called minting and burning.

:magic\_wand: <mark style="background-color:green;">Minting</mark> is like making a deposit. A user deposits the collateral token (COL) into the pool, and in return, they receive TEA, APE, or MAAM tokens.

:fire: <mark style="background-color:red;">Burning</mark> is like making a withdrawal. A user gives back their TEA, APE, or MAAM tokens, and in return, they receive the equivalent value in collateral (COL) from the pool.

{% hint style="info" %}
The SIR protocol promises **instant liquidity**, meaning you can mint or burn tokens anytime you want. There's no wait time for withdrawals or deposits, or other functionalities like freezing.
{% endhint %}

### Comparison Between APE and TEA

* <mark style="background-color:yellow;">APE tracks the price of COL/DBT with constant leverage ratio</mark> $$l$$​
* TEA is pegged to DBT and backed by a COL reserve with collateralization factor $$r$$

{% hint style="info" %}
The leverage ratio of the APE token ($$l$$) and the collateralization factor of the TEA token ($$r$$) are connected by the formula in [https://github.com/SIR-trading/SIR-white\_paper/blob/main/Whitepaper.pdf](https://github.com/SIR-trading/SIR-white\_paper/blob/main/Whitepaper.pdf "mention").
{% endhint %}

To summarize,

<table><thead><tr><th width="197.33333333333331"></th><th>APE 🦍</th><th>TEA 🍵</th></tr></thead><tbody><tr><td>User label</td><td>Ape</td><td>Gentleman</td></tr><tr><td>Price</td><td>COL/DBT</td><td>DBT</td></tr><tr><td>Leverage ratio</td><td><span class="math">l>1</span>​</td><td>1 (none)</td></tr><tr><td>Backed by</td><td>COL</td><td>COL</td></tr><tr><td>Collateralization</td><td>N/A</td><td><span class="math">r>1</span>​</td></tr></tbody></table>

###
