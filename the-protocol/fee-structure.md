# 🧾 Fee Structure

Fees are a critical part of any money lego. For instance, [Uniswap v3 only overtook Curve as primary DEX for stablecoin trading once it enable it's 0.01% fee tier](https://twitter.com/RyanWatkins\_/status/1483640421502885888). That is because LPers barely suffer from [impermanent loss](https://medium.com/coinmonks/understanding-impermanent-loss-9ac6795e5baa) in stablecoin-to-stablecoin pairs, and so they can accept much smaller trading comissions for their liquidity. However, it is clear that a 0% fee tier would not work because LPers would have no incentives. Choosing the right fee structure is a sensitive choice for any project. On the one hand, too large fees may discourage users, and on the other hand, too little fees may discourage LPers.

### SIR's Fee Model

A core value of SIR is that [no funding fees](../introduction/safer-leverage/#a-new-defi-primitive) are charged for holding TEA or APE. This is not the case of perpetual futures which charge a [funding rate](https://www.binance.com/en/blog/futures/a-beginners-guide-to-funding-rates-421499824684900382) which can easily erode anyone's position over the long-term. Instead, we implement a mechanism more akin to spot exchanges where a fee may be charged only when executing the trade. So in the case of SIR, a fee may be charged **upon minting or burning TEA/APE**.

#### LP Incentives

Fees are the lubricant of the SIR protocol. Fees are taken from gentlemen and apes and paid to LPers. Without fees, LPers would have no incentives to provide liquidity and the leverage would become [out of sync](leverage-rebalancing/price-stability-range.md).&#x20;

#### Free Pass

To keep the leverage in sync implies that we must have a perfect ratio between the apes' reserve ($$A$$) and the gentlemen reserve ($$G$$) exactly equal to $$G/A=l-1$$. In this perfect scenario, the LPers are in fact not needed. The larger the divergence, the more LP liquidity that is needed to keep the leverage in sync. Therefore, we would want the protocol to get as close as possible to the ideal ratio. To this end when $$G/A<l-1$$ no fees are charged for minting TEA (to encourage $$G$$ increases) and no fees are charged for burning APE (to encourage$$A$$ decreases); and similarly, when $$G/A>l-1$$ no fees are charged for burning TEA and minting APE. In summary,

<table><thead><tr><th></th><th data-type="select">Mint</th><th>Burn</th></tr></thead><tbody><tr><td>TEA <span data-gb-custom-inline data-tag="emoji" data-code="1f375">🍵</span></td><td></td><td><span class="math">G/A \leq l-1</span> ⇔ fee<br><span class="math">G/A>l-1</span> ⇔ no fee</td></tr><tr><td>APE <span data-gb-custom-inline data-tag="emoji" data-code="1f9a7">🦧</span></td><td></td><td>⇔ no fee<br> ⇔ fee</td></tr></tbody></table>

#### Fee Amount



To finely adjust, the fees will be left as a tunable parameter during the beta testing of SIR.

MENTION IT WILL BE A TUNABLE PARAMETER IN THE BETA PERIOD

CONDITION: NO FUNDING FEE

DISTRIBUTION OF THE FEES

FEE MECHANISM
