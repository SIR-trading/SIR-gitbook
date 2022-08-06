# 🔮 Trustless Oracle

As stated [by Chainlink](https://chain.link/education/blockchain-oracles),

> Blockchain oracles are entities that connect blockchains to external systems, thereby enabling smart contracts to execute based upon inputs and outputs from the real world.&#x20;

To [rebalance each pool](the-protocol/leverage-rebalancing/), the SIR protocols needs the price between the collateral token and debt token.&#x20;

#### The Uniswap V3 Oracle

SIR's hypothesis is that **any protocol can only be as trustless as its underlying layers of technology**. For this reason SIR uses the Uniswap v3 oracle which is, in our opinion, the most trustless on-chain price oracle for the following reasons:

* [x] <mark style="background-color:blue;">Purely on-chain.</mark>  Being on-chain implies that it is ran by smart contracts, and therefore it is fully auditable and ruled by its smart contracts.
* [x] <mark style="background-color:orange;">Immutable smart contracts.</mark> Contrary to many other money legos, all versions of Uniswap were launched with non-upgradable immutable contracts.
* [x] <mark style="background-color:purple;">Protected by economic incentives.</mark> Any divergence between the price of Uniswap v3 and any other exchange will be arbitraged for a profit, eliminating the price difference. The cost to manipulate the price is proportional to the liquidity of the traded pair.
* [x] <mark style="background-color:green;">Permissionless.</mark> Similar to a blockchain, a key part is that anyone can arbitrage the price between Uniswap v3 and any exchange.
* [x] <mark style="background-color:red;">Largest liquidity.</mark> Uniswap v3 is [the most liquid DEX](https://www.coingecko.com/en/dex) and among the top most liquid exchanges.

Uniswap v3 allows for the retrieval of a [time-weighted-averaged-price](https://en.wikipedia.org/wiki/Time-weighted\_average\_price).

{% hint style="warning" %}
Uniswap v3 is **not suitable for instant market prices** because they can be easily manipulated, for example, with the use of flash loans.&#x20;
{% endhint %}

The above shortcoming is whatsoever not a problem for SIR because a TWAP providers protection against sudden market volatility and mitigates the risk of liquidation.

{% hint style="warning" %}
Arguably, the biggest shortcoming of Uniswap v3 is that **it can only report prices of ERC20 tokens that exist on-chain**.
{% endhint %}

#### Weighted Logarithmic Price Mean&#x20;
