# ↔ The Price Stability Range

If the price lies within the Price Stability Range (PSR), bounded below by $$p_\text{low}$$ and above by $$p_\text{high}$$, then **the leverage is in sync**, i.e., $$l_\text{eff}=l$$. The purpose of the LPers is to keep the price within the PSR and outside the two other possible zones of operation shown in the drawing below.

<img src="../../.gitbook/assets/file.drawing (5).svg" alt="" class="gitbook-drawing">

The 3 distinct price zones informally labelled as _heaven_, _limbo_ and _hell._ Some of the most important properties of these 3 regions are are summarized in the table below.

| Price Region                                                | Price                                | Leverage & Collateralization                                                                                                      | LPers                |
| ----------------------------------------------------------- | ------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------- | -------------------- |
| <mark style="background-color:yellow;">"upper limbo"</mark> | $$p > p_\text{high}$$                | $$l_\text{eff}<l$$, $$r_\text{eff}>r$$                                                                                            | 100% APE             |
| PSR <mark style="background-color:blue;">"heaven"</mark>    | $$p\in[p_\text{low},p_\text{high}]$$ | <p><strong>Leverage in sync</strong></p><p><span class="math">l_\text{eff}=l</span>, <span class="math">r_\text{eff}=r</span></p> | TEA & APE            |
| <mark style="background-color:yellow;">"lower limbo"</mark> | $$p\in[p_\text{liq},p_\text{low})$$  | $$l_\text{eff}>l$$, $$r_\text{eff}<r$$                                                                                            | 100% TEA             |
| <mark style="background-color:red;">"hell"</mark>           | $$p <p_\text{liq}$$                  | $$r_\text{eff}<1$$                                                                                                                | :warning: Liquidated |

__

While the price remains in the PSR, the APE token price enjoys the ideal convex payout equation described in [ape-token-basics.md](../../introduction/safer-leverage/ape-token-basics.md "mention").  Also the TEA token remains fully overcollateralized. This is the optimal mode of operation. Mathematically, $$p\in [p_\text{low},p_\text{high}]  \Longleftrightarrow l_\text{eff} = l$$.

When price falls below or shoots above the PSR, there is insufficient liquidity to maintain a proper reserve ratio between gentlemen and apes, and the leverage starts to fluctuate. Precisely, the leverage ratio increases below the PSR and decreases above the PSR. While APE fails to maintain a constant leverage, it still remains leveraged. **The APE payout curve becomes linear as that of a margin trade.** TEA still remains fully collateralized.

The hell zone defines a region where bad things occur. If price crosses the liquidation price ($$p_\text{liq}$$) the reserve becomes undercollateralized. Consequently, **apes and LPers are liquidated** :volcano:, and **gentlemen are slashed** until the value of all TEA matches the value of the reserve.

#### Price formulas

For readability we do not include the proofs of these formulas.

$$
\begin{align}
p_\text{high} &= p_\text{low} \left(\frac{R}{l \left.A\right|_{p=p_\text{low}}}\right)^{r-1} \\
p_\text{low} &= \frac{rT}{R}   \\
p_\text{liq} &= \frac{p_\text{low}}{r} \\
\end{align}
$$

### The Role of LPers

Without LPers, the PSR reduces to a single point $$p_\text{low}=p_\text{high}=(r-1)T/A$$, which is essentially the price at which the gentlemen and apes' reserves are in equilibrium and the leverage is in sync. Because price will fluctuate, it is practically impossible that the leverage can remain in sync without LPers. If LP liquidity is added, the ratio $$p_\text{high}/p_\text{low}$$ increases; and vice-versa.

Let $$\Delta L$$ be the increment or decrement in LP liquidity after minting or burning MAAM, respectively. The following table shows the effect of changes in LP liquidity.

|                  Price Afterwards |                              LPer Adds Liquidity                              |                            LPer Removes Liquidity                            |
| --------------------------------: | :---------------------------------------------------------------------------: | :--------------------------------------------------------------------------: |
|               $$p_\text{high}'=$$ |          $$p_\text{high} \left( 1+\frac{\Delta L}{R} \right)^{r-1}$$​         |          $$p_\text{high} \left( 1-\frac{\Delta L}{R} \right)^{r-1}$$         |
|                $$p_\text{low}'=$$ |           $$p_\text{low}  \left( 1+\frac{\Delta L}{R} \right)^{-1}$$          |          $$p_\text{low}  \left( 1-\frac{\Delta L}{R} \right)^{-1}$$          |
| $$p_\text{high}'/p_\text{low}'=$$ | $$\frac{p_\text{high}}{p_\text{low}} \left( 1+\frac{\Delta L}{R} \right)^r$$​ | $$\frac{p_\text{high}}{p_\text{low}} \left( 1-\frac{\Delta L}{R} \right)^r$$ |

From the table, we can infer that what matters is the amount of liquidity added/removed ($$\Delta L$$) relative to the current pool liquidity ($$R$$). In addition to the LP liquidity, a large collateralization factor ($$r$$) is also beneficial for increasing the PSR. This is due to the fact that a large $$r$$ implies a low leverage ratio, and therefore less liquidity is needed for the apes.

{% hint style="info" %}
It is easier for pools with a lower leverage ratio to stay in sync because their PSR is larger for the same amount of liquidity.&#x20;
{% endhint %}

### Protocol Owned Liquidity

Most of the fees are paid to LPers who after all perform the important task of synching the leverage ratio, such that. But 5% of all fees collected are diverged to the protocol which then acts as an LPer. The advantage of **protocol owned liquidity** over regular LPers**,** is that it **will never be withdrawn**. As the pool continues to exist we an only hope that protocol owned liquidity will grow as well increasing the stability of the pool.
