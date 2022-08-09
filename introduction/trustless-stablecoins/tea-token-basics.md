# 🍵 TEA Token

TEA tokens are pegged to other tokens/assets, i.e., they track their price. A prominent example are stablecoins which are usually pegged to USD, such as USDC, USDT or DAI. Another good example are [Synths](https://synthetix.io/synths) pegged to other coins. Each TEA token is managed by a pool contract. At the creation of the pool, the creator specifies 3 parameters that define TEA:

1. <mark style="background-color:green;">**Debt token**</mark>: The token to which TEA is pegged
2. <mark style="background-color:blue;">**Collateral token**</mark>: The token used as collateral
3. <mark style="background-color:orange;">**The collateralization factor**</mark> ($$r$$)

These parameters will remain fixed forever. Only way to get TEA with different parameters is to create a new flavor of TEA. Each TEA will have its own contract and own users.

The basic idea of TEA is simple: the total supply of TEA ($$T$$) should be backed up by $$r$$ times its value in collateral, i.e.,

$$
\begin{equation}r T = p R\end{equation}
$$

where $$p$$ is the price of the collateral (in debt token) and $$R$$ is the supply of the collateral reserve.​

<img src="../../.gitbook/assets/file.drawing (7).svg" alt="" class="gitbook-drawing">

Anyone can create a TEA token with any choice of parameters, but most likely, only those with reasonable parameters will thrive. If the collateralization factor is too low compared to the volatility, then TEA may risk becoming undercollateralized. Contrarily, if the collateralization factor is too high, the economic incentives to keep the reserve full may be insufficient.&#x20;

{% hint style="info" %}
Some possible applications of TEA are

1. trustless decentralized stablecoins
2. exposure to the price of other tokens without their smart contract logic flaws (e.g. [Circle freezing Tornado Cash USDC balances](https://cointelegraph.com/news/circle-freezes-blacklisted-tornado-cash-smart-contract-addresses))
{% endhint %}
