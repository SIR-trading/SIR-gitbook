# ↔️ The Price Stability Range

If the price lies within the Price Stability Range (PSR), bounded below by $$p_\text{low}$$ and above by $$p_\text{high}$$, then **the leverage is in sync**, i.e., $$l_\text{eff}=l$$. The purpose of the LPers is to keep the price within the PSR and outside the two other possible zones of operation shown in the drawing below.

<img src="../../.gitbook/assets/file.drawing (5).svg" alt="" class="gitbook-drawing">

The 3 distinct price zones informally labelled as _heaven_, _limbo_ and _hell._ Some of the most important properties of these 3 regions are are summarized in the table below.

<table><thead><tr><th width="164">Price Region</th><th width="162.33333333333331">Price</th><th width="188.96603946764574">Leverage &#x26; Collateralization</th><th>LPers</th></tr></thead><tbody><tr><td><mark style="background-color:yellow;">"upper limbo"</mark></td><td><span class="math">p > p_\text{high}</span></td><td><span class="math">l_\text{eff}&#x3C;l</span>, <span class="math">r_\text{eff}>r</span></td><td>100% APE</td></tr><tr><td>PSR <mark style="background-color:blue;">"heaven"</mark></td><td><span class="math">p\in[p_\text{low},p_\text{high}]</span></td><td><p><strong>Leverage in sync</strong></p><p><span class="math">l_\text{eff}=l</span>, <span class="math">r_\text{eff}=r</span></p></td><td>TEA &#x26; APE</td></tr><tr><td><mark style="background-color:yellow;">"lower limbo"</mark></td><td><span class="math">p\in[p_\text{liq},p_\text{low})</span></td><td><span class="math">l_\text{eff}>l</span>, <span class="math">r_\text{eff}&#x3C;r</span></td><td>100% TEA</td></tr><tr><td><mark style="background-color:red;">"hell"</mark></td><td><span class="math">p &#x3C;p_\text{liq}</span></td><td><span class="math">r_\text{eff}&#x3C;1</span></td><td><span data-gb-custom-inline data-tag="emoji" data-code="26a0">⚠️</span> Liquidated</td></tr></tbody></table>



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

<table><thead><tr><th width="200.33333333333331" align="right">Price Afterwards</th><th align="center">LPer Adds Liquidity</th><th align="center">LPer Removes Liquidity</th></tr></thead><tbody><tr><td align="right"><span class="math">p_\text{high}'=</span></td><td align="center"><span class="math">p_\text{high} \left( 1+\frac{\Delta L}{R} \right)^{r-1}</span>​</td><td align="center"><span class="math">p_\text{high} \left( 1-\frac{\Delta L}{R} \right)^{r-1}</span></td></tr><tr><td align="right"><span class="math">p_\text{low}'=</span></td><td align="center"><span class="math">p_\text{low}  \left( 1+\frac{\Delta L}{R} \right)^{-1}</span></td><td align="center"><span class="math">p_\text{low}  \left( 1-\frac{\Delta L}{R} \right)^{-1}</span></td></tr><tr><td align="right"><span class="math">p_\text{high}'/p_\text{low}'=</span></td><td align="center"><span class="math">\frac{p_\text{high}}{p_\text{low}} \left( 1+\frac{\Delta L}{R} \right)^r</span>​</td><td align="center"><span class="math">\frac{p_\text{high}}{p_\text{low}} \left( 1-\frac{\Delta L}{R} \right)^r</span></td></tr></tbody></table>

From the table, we can infer that what matters is the amount of liquidity added/removed ($$\Delta L$$) relative to the current pool liquidity ($$R$$). In addition to the LP liquidity, a large collateralization factor ($$r$$) is also beneficial for increasing the PSR. This is due to the fact that a large $$r$$ implies a low leverage ratio, and therefore less liquidity is needed for the apes.

{% hint style="info" %}
It is easier for pools with a lower leverage ratio to stay in sync because their PSR is larger for the same amount of liquidity.&#x20;
{% endhint %}
