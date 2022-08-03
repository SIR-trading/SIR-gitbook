# ⚖ Leverage Rebalancing

From the above formula, if the price increases 📈, the leverage decreases 📉; and vice-versa. This is where the **liquidity providers (LPers)** step in to save the day.

|             Price Action             |             LPers' Reaction             |
| :----------------------------------: | :-------------------------------------: |
| Price increases ➟ $$l_\text{eff}$$📉 | Sell APE & buy TEA ➟ $$l_\text{eff}$$📈 |
| Price decreases ➟ $$l_\text{eff}$$📈 | Sell TEA & Buy APE ➟ $$l_\text{eff}$$📉 |

In exchange for rebalancing the leverage, LPers get the fees collected by the protocol.

{% hint style="info" %}
The buying and selling of APE & TEA owned by the LPers is done automatically at the protocol level without their interaction.
{% endhint %}

{% hint style="info" %}
Rather than holding a mixed position of APE & TEA in their wallets, which shall be rebased at every block by the protocol, LPers hold their own token. This token called MAAM is a pro-rata claim on the underlying collateral.&#x20;
{% endhint %}

In reality LPers hold MAAM (not APE & TEA), but it is still a good metaphor for understanding how it works.

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

{% hint style="info" %}
This example is only for illustration purposes. In reality the protocol rebalances the leverage instantly, not in large price jumps.
{% endhint %}



