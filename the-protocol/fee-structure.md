# 🧾 Fee Structure

A core value of SIR is that [**no funding fees**](../introduction/safer-leverage/#a-new-defi-primitive) are charged for holding TEA or APE. This is not the case of perpetual futures which charge a [funding rate](https://www.binance.com/en/blog/futures/a-beginners-guide-to-funding-rates-421499824684900382) which can easily erode anyone's position over the long-term. Instead, we implement a mechanism more akin to spot exchanges where a fee may be charged only when executing the trade. So in the case of SIR, **a fee may be charged upon minting or burning TEA/APE**.

#### Distribution

Fees are the lubricant of the SIR protocol. Fees are taken from gentlemen and apes and paid mainly to LPers. Without fees, LPers would have no incentives to provide liquidity and the leverage would become [out of sync](leverage-rebalancing/price-stability-range.md).

GO INTO MORE DETAILS

#### Free Passes

To keep the leverage in sync without LPers implies that we must have a perfect ratio between the apes' reserve ($$A$$) and the gentlemen reserve ($$G$$) exactly equal to $$G/A=l-1$$. The larger the divergence, the more LP liquidity that is needed to keep the leverage in sync. Therefore, we would want the protocol to get as close as possible to the ideal ratio. To this end when $$G/A<l-1$$ no fees are charged for minting TEA (to encourage $$G$$ increases) and no fees are charged for burning APE (to encourage$$A$$ decreases); and similarly, when $$G/A>l-1$$ no fees are charged for burning TEA and minting APE. In summary,

|                                                             | $$G/A < l-1$$                                       | $$G/A > l-1$$                                       |
| ----------------------------------------------------------- | --------------------------------------------------- | --------------------------------------------------- |
| <mark style="color:green;">Mint</mark> 🪄 TEA :tea:         | <mark style="background-color:green;">no fee</mark> | <mark style="background-color:red;">fee</mark>      |
| <mark style="color:red;">Burn</mark> :fire: TEA :tea:       | <mark style="background-color:red;">fee</mark>      | <mark style="background-color:green;">no fee</mark> |
| <mark style="color:green;">Mint</mark> 🪄 APE :orangutan:   | <mark style="background-color:green;">no fee</mark> | <mark style="background-color:red;">fee</mark>      |
| <mark style="color:red;">Burn</mark> :fire: APE :orangutan: | <mark style="background-color:red;">fee</mark>      | <mark style="background-color:green;">no fee</mark> |

#### Fee Mechanism

Apes and gentlemen live in symbiosis. Apes obtain their leverage from the collateral deposited by the gentlemen, and gentlemen's enjoy the benefits of a over-collateralized reserve thanks to the apes. Each type of user benefits from each other's liquidity. Specifically, in a pool with leverage ratio $$l$$, one unit of collateral in the ape reserve requires $$(l-1)$$ units of collateral in the gentlemen's reserve. So fees are charged proportionally to the amount of liquidity that is required, i.e.,

$$
\begin{align}
f_\text{ape} &= (l-1)f_\text{base} \\
f_\text{tea} &= (r-1)f_\text{base}
\end{align}
$$

where $$f_\text{base}$$ is the base fee and it is fixed. For example, for a user minting or burning APE by depositing or withdrawing $$x$$ collateral, he must pay a fee of $$f_\text{ape}\, x$$.

#### Beta Period

Fees are a critical part of any money lego. For instance, [Uniswap v3 only overtook Curve as primary DEX for stablecoin trading once it enable it's 0.01% fee tier](https://twitter.com/RyanWatkins\_/status/1483640421502885888). That is because LPers barely suffer from [impermanent loss](https://medium.com/coinmonks/understanding-impermanent-loss-9ac6795e5baa) in stablecoin-to-stablecoin pairs, and so they can accept much smaller trading comissions for their liquidity. However, it is clear that a 0% fee tier would not work because LPers would have no incentives. Choosing the right fee structure is a sensitive choice for any project. On the one hand, too large fees may discourage users, and on the other hand, too little fees may discourage LPers. So to finely adjust the fee value charged to users, the base fee value ($$f_\text{base}$$) will be tuned during the beta testing of SIR.
