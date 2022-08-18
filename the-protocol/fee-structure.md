# 🧾 Fee Structure

A core value of SIR is that [**no funding fees**](../introduction/safer-leverage/#a-new-defi-primitive) are charged for holding TEA or APE. This is not the case of any other leveraged derivative. For instance, exchanges with [perpetual futures](https://en.wikipedia.org/wiki/Perpetual\_futures) charge a [funding rate](https://www.binance.com/en/blog/futures/a-beginners-guide-to-funding-rates-421499824684900382) which can easily erode anyone's position over the long-term. Instead, we implement a mechanism more akin to spot exchanges where a fee may be charged only when executing the trade. So in the case of SIR, **a fee is charged upon minting or burning TEA/APE**.

### Free Passes

To keep the leverage in sync without LPers implies that we must have a perfect ratio between the apes' reserve ($$A$$) and the gentlemen reserve ($$G$$) exactly equal to $$G/A=l-1$$. The larger the divergence, the more LP liquidity that is needed to keep the leverage in sync. Therefore, we would want the protocol to get as close as possible to the ideal ratio. To this end when $$G/A<l-1$$ no fees are charged for minting TEA (to encourage $$G$$ increases) and no fees are charged for burning APE (to encourage$$A$$ decreases); and similarly, when $$G/A>l-1$$ no fees are charged for burning TEA and minting APE. In summary,

|                                                             | $$G/A < l-1$$                                       | $$G/A > l-1$$                                       |
| ----------------------------------------------------------- | --------------------------------------------------- | --------------------------------------------------- |
| <mark style="color:green;">Mint</mark> 🪄 TEA :tea:         | <mark style="background-color:green;">no fee</mark> | <mark style="background-color:red;">fee</mark>      |
| <mark style="color:red;">Burn</mark> :fire: TEA :tea:       | <mark style="background-color:red;">fee</mark>      | <mark style="background-color:green;">no fee</mark> |
| <mark style="color:green;">Mint</mark> 🪄 APE :orangutan:   | <mark style="background-color:green;">no fee</mark> | <mark style="background-color:red;">fee</mark>      |
| <mark style="color:red;">Burn</mark> :fire: APE :orangutan: | <mark style="background-color:red;">fee</mark>      | <mark style="background-color:green;">no fee</mark> |

### Fee Mechanism

Apes and gentlemen live in symbiosis. Apes obtain their leverage from the collateral deposited by the gentlemen, and gentlemen's enjoy the benefits of a over-collateralized reserve thanks to the apes. Each type of user benefits from each other's liquidity. Specifically, in a pool with leverage ratio $$l$$, one unit of collateral in the ape reserve requires $$(l-1)$$ units of collateral in the gentlemen's reserve. So fees are charged proportionally to the amount of liquidity that is required, i.e.,

$$
\begin{align}
f_\text{ape} &= (l-1)f_\text{base} \\
f_\text{tea} &= (r-1)f_\text{base}
\end{align}
$$

where $$f_\text{base}$$ is the base fee and it is fixed. For example, for a user minting or burning APE by depositing or withdrawing $$x$$ collateral, he must pay a fee of $$f_\text{ape}\, x$$.

### Distribution

Fees are the lubricant of any money lego and SIR is no exception. The main recipient of the protocol fees are <mark style="background-color:purple;">LPers</mark> because they perform the critical task of [syncing the leverage](leverage-rebalancing/price-stability-range.md). However, depending on the pool, there are up to two other recipients.

| Fee Recipient            | Allocation for Pool w\o Liquidity Mining | Allocation for Pool with Liquidity Mining |
| ------------------------ | ---------------------------------------- | ----------------------------------------- |
| LPers                    | $$95\%$$                                 | $$(100-x)\%$$                             |
| Protocol Owned Liquidity | $$5\%$$                                  | $$5\%$$                                   |
| DAO                      | $$0\%$$                                  | $$x\%$$ where $$x\in(0,5]$$               |

[Protocol owned liquidity](leverage-rebalancing/protocol-owned-liquidity.md) (<mark style="background-color:orange;">POL</mark>) is virtually any LPer that is not controlled by anyone. Because it is not controlled by anyone, POL is like an extremely loyal LPer who will never withdraw its collateral.

Lastly, some selected pools will distribute a small variable part of their fees to the <mark style="background-color:green;">DAO</mark>. As a compensation for the loss of fees, those pools will be issued SIR token, making it some form of liquidity mining. More on this topic in [sir-token.md](sir-token.md "mention").

{% hint style="info" %}
LPers receive only the fees collected by the pool they are in. So naturally LPers will want to move to the pools with the most activity.
{% endhint %}
