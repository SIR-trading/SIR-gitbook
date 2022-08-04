---
description: Liquidity providers perform an essentially duty for the stability of the pool.
---

# ⚖ Pool Rebalancing

Expressing the formulas for the collateralization factor and leverage ratio [in the previous section](../apes-vs.-gentlemen.md) as a function of the price

$$
\begin{align} r_\text{eff}&=\frac{R}{T/p} \\
l_\text{eff}&=\frac{R}{R-T/p}
\end{align}
$$

we find out that if the price increases 📈, the collateralization factor increases 📈 and the leverage decreases 📉; and vice-versa. This is where the **liquidity providers (LPers)** step in to save the day.

### Leverage In Sync

<mark style="background-color:blue;">We say that _the leverage is in sync_ when $$l_\text{eff}=l$$ (or equivalently $$r_\text{eff}=r$$).</mark> 

{% hint style="info" %}
LPers are in charge of buying/selling TEA and APE  in order to keep the leverage synched.

In exchange for their services, **LPers get protocol fees**.
{% endhint %}

The following table outlines the actions taken by LPers upon price movements:

|                       Price Action                       |                       LPers' Reaction                       |
| :------------------------------------------------------: | :---------------------------------------------------------: |
| Price increases ➟ $$r_\text{eff}$$📈, $$l_\text{eff}$$📉 | Sell APE & buy TEA ➟ $$r_\text{eff}$$📉, $$l_\text{eff}$$📈 |
| Price decreases ➟ $$r_\text{eff}$$📉, $$l_\text{eff}$$📈 | Sell TEA & Buy APE ➟ $$r_\text{eff}$$📈, $$l_\text{eff}$$📉 |

{% hint style="info" %}
LPers do not actually buy/sell APE/TEA. It is taken cared automatically by the protocol.
{% endhint %}

{% hint style="info" %}
LPers do not actually hold APE & TEA themselves, instead **LPers hold a token called MAAM**. The protocol handles the rebalancing internally without the need for transactions.
{% endhint %}

LPers an sync the leverage down/up to a certain price point. If the price falls below or exceed the price stability range (PSR), then the leverage goes out of sync. [More about the PSR in the next section.](price-stability-range.md)

#### Example

In the flow chart below, a new pool is created by Alice with ETH as collateral, USDC as debt token and 1.25 as leverage ratio. From [#the-collateralization-factor](../protocol-intro.md#the-collateralization-factor "mention"), we get that $$r=5$$.

![Functional Flow Chart of SIR with 4 Pool Instances](<../../.gitbook/assets/SIR Protocol (2) (1).svg>)

Assume some activity has occurred since creation and the current state of the pool is $$A=4$$ and $$G=1$$. In addition, LPers own 2 ETH, which we denote as $$L=2$$. If we ignore the LPers, from (3) we get that $$l_\text{eff}=(4+1)/4=1.25$$, and it is in sync with the target leverage $$l_\text{eff}=l$$.

The LPers allocate 1,6 ETH and 0.4 ETH to the apes' and gentlemen's reserves, respectively, because in this way it does not alter the leverage:  $$l_\text{eff} = (5.6+1.4)/5.6=1.25$$. Life is good and the pool is well balanced 🥳.

{% hint style="info" %}
Holding a mixed bag of APE & TEA on a $$(r-1)$$-$$1$$-ratio, is equivalent to holding pure collateral.
{% endhint %}

Next, imagine the price of ETH increases by 25%. In this case less ETH is needed to cover the gentlemen's reserve: $$G=0.8$$, and consequently $$A=4.2$$. The effective leverage is now $$l_\text{eff}=(4.2+0.8)/4.2=1.19$$ and the pool has become out of sync, $$l_\text{eff}\neq l$$ 🙁.

The protocol trades some of the LPers' APE for TEA, so their 2 ETH is now split 1.4 ETH to the apes' reserve and 0.6 to the gentlemen's reserve. Then, $$l_\text{eff} = (5.6+1.4)/5.6=1.25$$, and the leverage is back in sync 🥳.



