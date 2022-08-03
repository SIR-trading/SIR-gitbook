# ↔ Price Stability Range

The SIR protocol operates optimally when the price falls within the Price Stability Range (PSR) bounded below by $$p_\text{low}$$ and above by $$p_\text{high}$$. LPers' purpose is to keep the price within the PSR, because there are two other possible zones of operation as shown in the drawing below.

<img src="../../.gitbook/assets/file.drawing (10).svg" alt="" class="gitbook-drawing">

The 3 distinct price zones informally labelled as _heaven_, _limbo_ and _hell._

1. <mark style="background-color:blue;">"Heaven"</mark> (PSR): While the price remains in the PSR, the APE token price enjoys the ideal convex payout equation described in XXXXX (PLACE WHERE THE APE PRICE EQUATION).  Also the TEA token remains fully overcollateralized. This is the optimal mode of operation. We say the **leverage is in sync** because the actual leverage matches the pool's targeted leverage. Mathematically, $$p\in [p_\text{low},p_\text{high}]  \Longleftrightarrow l_\text{eff} = l$$.
2. <mark style="background-color:purple;">"Limbo"</mark>: When price falls below or shoots above the PSR, there is insufficient liquidity to maintain a proper reserve ratio between gentlemen and apes, and the leverage starts to fluctuate. Precisely, the leverage ratio increases below the PSR and decreases above the PSR. While **APE fails to maintain its target leverage**, it is still leveraged; and TEA remains fully collateralized.
3. <mark style="background-color:red;">"Hell"</mark>: This is the no-go zone. If price crosses the liquidation price ($$p_\text{liq}$$) the reserve becomes undercollateralized. Consequently, **apes and LPers are liquidated** :volcano:, and **gentlemen are slashed** such that the value of all TEA equals the value of the reserve.

Keep in mind that the 3 price tags in the figure change their values as a function of the pool's state and parameters. So as TEA/APE/MAAM is minted/burnt, their values keep changing, and in fact in their exact formulas are:

$$
\begin{align}
p_\text{high} &= p_\text{low} \left(\frac{R}{l \left.A\right|_{p=p_\text{low}}}\right)^{r-1} \\
p_\text{low} &= rT/R   \\
p_\text{liq} &= \frac{p_\text{low}}{r} \\
\end{align}
$$

### LPers and PSR

Without LPers, the PSR reduces to a single point $$p_\text{low}=p_\text{high}=(r-1)T/A$$ which is essentially the price at which the gentlemen and apes' reserves have a $$1$$-to-$$(r-1)$$ ratio. Because price will fluctuate, it is practically impossible that the leverage can remain in sync without LPers. If LP liquidity is added, the ratio $$p_\text{high}/p_\text{low}$$ increases; and vice-versa.

Let $$\Delta R$$ be the increment or decrement in LP liquidity after minting or burning MAAM, respectively. The following table shows the effect of changes in LP liquidity.

|                  Price Afterwards |                              LPer Adds Liquidity                              |                            LPer Removes Liquidity                            |
| --------------------------------: | :---------------------------------------------------------------------------: | :--------------------------------------------------------------------------: |
|               $$p_\text{high}'=$$ |          $$p_\text{high} \left( 1+\frac{\Delta R}{R} \right)^{r-1}$$​         |          $$p_\text{high} \left( 1-\frac{\Delta R}{R} \right)^{r-1}$$         |
|                $$p_\text{low}'=$$ |           $$p_\text{low}  \left( 1+\frac{\Delta R}{R} \right)^{-1}$$          |          $$p_\text{low}  \left( 1-\frac{\Delta R}{R} \right)^{-1}$$          |
| $$p_\text{high}'/p_\text{low}'=$$ | $$\frac{p_\text{high}}{p_\text{low}} \left( 1+\frac{\Delta R}{R} \right)^r$$​ | $$\frac{p_\text{high}}{p_\text{low}} \left( 1-\frac{\Delta R}{R} \right)^r$$ |

From the table, we can infer that what matters is the amount of liquidity added/removed ($$\Delta R$$) with respect to the current pool liquidity ($$R$$). In addition to the LP liquidity, a large collateralization factor ($$r$$) is also beneficial for increasing the PSR. This is due to the fact that a large $$r$$ implies a low leverage ratio, and therefore less liquidity is needed for the apes.

{% hint style="info" %}
It is more likely for pools with a lower leverage ratio to stay in sync.&#x20;
{% endhint %}
