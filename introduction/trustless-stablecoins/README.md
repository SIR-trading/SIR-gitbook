# Trustless Stablecoins

Stablecoins are tokens pegged to some form of fiat, usually the US dollar. More generally, pegged tokens are tokens pegged 1-to-1 to the price of other tokens. The main advantage of stable tokens is that they allow holders to gain on-chain price exposure to other assets without some of their pitfalls. As an example a token pegged to USDC is also stablecoin pegged to USD but without the potential risk of balance freeze by [Circle](https://www.circle.com/en/usdc).

### The Quest for a Trustless Stablecoin

Creating a truly trustless stablecoin is the holy grail of DeFi because it would allow

* a <mark style="background-color:blue;">stable unit of exchange</mark>&#x20;
* while remaining <mark style="background-color:green;">censorship-resistant</mark>.

Next, we discuss the most important properties.

#### Collateralization

Every stablecoin must be backed by some sort of collateral that helps defend its value.&#x20;

{% hint style="info" %}
So far any attempt to create a non-collateralized stablecoin has failed (e.g., [Empty Set Dollar or Basis Cash](https://blog.hubbleprotocol.io/stablecoin-cemetery/)) and seems implausible to work in the long-term.
{% endhint %}

Nonetheless, some stablecoins that are under-collateralized (akin to fractional reserve banking) have managed to survive such as [Frax](https://frax.finance/), even though the risk of bank-run is always looming. Terra, and its UST stablecoin, was the most recent fiasco of an under-collateralized stablecoin that fell into a death spiral, causing the market cap to shrink from $37B to less than $100M in the span of 1 week.

Most top stablecoins, such as USDT, USDC and DAI, are in fact over-collateralized. USDT, which is the #1 stablecoin by market cap, is fully collateralized by a [mix of US treasuries and commercial paper](https://tether.to/en/understanding-tethers-peg-and-reserves/). USDC is backed by auditable reserves of USD cash and US treasuries, and DAI is backed by mix of crypto assets (including USDC!).&#x20;

Contrary to USDT and USDC which are backed by USD-like collateral off-chain, DAI must be over-collateralized ([139% at the time of this writing](https://daistats.com/)) because some of the collateral is volatile. This is a drawback of any trustless stablecoin because there does not exist a USD-like derivative that is fully decentralized and on-chain.&#x20;

#### Type of Collateral

Stablecoins issued by centralized entities are often backed by cash or treasuries. Usually only selected parties can redeem the stablecoin for an equivalent amount of collateral, creating an arbitrage opportunity that stabilizes the peg of the stablecoin.

Other stablecoins, such as DAI, use a plethora of crypto assets as collateral. However, because of their volatility, they are suboptimal and usually require some degree of over-collateralization. In general, the less volatile the better.

Regardless, truly trustless stablecoins must consequently employ fully decentralized crypto assets as collateral. It is generally accepted that the most trustless crypto assets are L1 blockchain native coins such as BTC and ETH. Other blockchains' native coins are usually not considered as trustless because their blockchains fail to be sufficiently decentralized.&#x20;

#### Liquidity

By liquidity we can mean the global liquidity of the collateral. For instance, cash is extremely liquid. But it also can refer to the maximum amount of stablecoin that is redeemedable in a period of time for collateral, i.e., existence of a bottleneck for _cashing out_ the stablecoin.

An interesting case example is Fei which is backed by DAI. While technically DAI is very liquid because it can be redeemed at any time for collateral. On the other hand [Fei has implemented _bottlenecks_ at the protocol level](https://docs.tribedao.xyz/docs/protocol/Mechanism/PegStabilityModule) to discourage redeeming Fei for DAI in large amounts. For instance, they can charge a fee for redeeming effectively lowering the price of Fei or simply freeze conersion.

#### Oracle

Stablecoins backed by collateral types different than fiat/fiat-derivatives need an oracle that informs them of the price between the stablecoin unit and the collateral. For example, in MakerDAO  (the protocol generating DAI) if the collateral price falls below the liquidation price, the collateral is auctioned in exchange for DAI. Passing information from the real world to the blockchain in a trustless manner is known as [the oracle problem](https://cointelegraph.com/magazine/2021/12/30/can-blockchain-solve-its-oracle-problem) and remains unsolved.

For the particular case of passing prices, Uniswap v2 and v3 can actually be considered trustless oracles because they have no off-chain components. But they have a couple of shortcomings: (1) they can only inform about prices of tokens that exist on-chain, and (2) they are not suitable for instant market prices because they could be easily manipulated.

#### Immutability

A particular weak spots of practically all stablecoins is that they incorporate some type of governance or upgradability into their smart contracts. This means in practice that some of the protocol parameters, or even the entire smart contracts, can be changed upon the decision of a DAO in the best case scenario or a single individual in the worst case scenario.

For instance, USDT and USDC have admin control over their smart contracts understandably and can freeze transactions among other features. DAI transfers cannot be censored, but they its DAO has the power to change a lot of parameters in the protocol, including accepted collateral types. In fact it had its [fair bit of controversy](https://cointelegraph.com/news/as-the-old-dai-shuts-down-maker-must-deal-with-centralized-collateral-risk), in particular when it moved from being purely backed by ETH to accepting other types of less trustless collaterals.

#### Peg

The quality of a stablecoin is also defined by its stability, obviously. For example, [RAI](https://reflexer.finance/) is a an interesting "stablecoin" design in the sense that it is trustless by many of the properties described above. But it is not pegged hardly to the USD and, instead, it tries to even supply and demand by changing its _redemption price_, which can lead to substantial price oscillations with respect to USD.

### Permissionless Creation of Pegged Tokens

Just like Uniswap unleashed a new wave of trading pairs in 2020 thanks to its permissionless nature. SIR seeks to unleash a new wave of pegged tokens, which are denominated with the symbol TEA.&#x20;

Anyone can spin a stable token (1) pegged to _any_ digital asset and, (2) backed by some collateral of choice (3) with a user-defined collateralization ratio. We call minters of TEA tokens, gentlemen, because gentlemen love stability.

![](../../.gitbook/assets/oprah\_meme.jpg)

Our TEA pegged tokens have several strengths listed in the table below:

| Feature                  | Description                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| ------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Over-collateralized      | <p>The creator of each TEA chooses the target collateralization ratio.</p><p></p><p>A design feature of the protocol is that <mark style="background-color:blue;">the reserve must always be over-collateralized</mark>. In the event that the reserve cannot be maintained over-collateralized, gentlemen will be slashed pro-rata.</p>                                                                                                          |
| Any collateral of choice | The creator of each TEA chooses the token to be used as collateral. Its imagination is the limit.                                                                                                                                                                                                                                                                                                                                                 |
| Always redeemable        | The protocol is designed such that <mark style="background-color:orange;">TEA is always redeemable</mark> for its equivalent value in collateral. This will ensure that that the peg does not break.                                                                                                                                                                                                                                              |
| Trustless oracle         | <mark style="background-color:red;">Uniswap v3 is</mark> the price oracle of SIR because it is <mark style="background-color:red;">the only trustless and sufficiently decentralized on-chain oracle.</mark>                                                                                                                                                                                                                                      |
| No governance            | <mark style="background-color:purple;">The contracts are immutable and cannot be upgraded or tuned</mark>. An exception is made during the beta period where a couple of admin features will be left on. During the beta, the team will have the capacity to change the fees charged by the protocol in order to fine tune it. The team will also have the capacity to freeze deposits (not withdrawals) to rescue the users in case of hack/bug. |
| Pegged to anything       | TEA is pegged to the token chosen by the creator.                                                                                                                                                                                                                                                                                                                                                                                                 |
