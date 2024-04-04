# 🔮 Trustless Oracle

As stated [by Chainlink](https://chain.link/education/blockchain-oracles),

> Blockchain oracles are entities that connect blockchains to external systems, thereby enabling smart contracts to execute based upon inputs and outputs from the real world.

To [rebalance each pool](broken-reference), the SIR protocols needs the price between the collateral token and debt token.

### The Uniswap V3 Oracle

SIR's hypothesis is that **any protocol can only be as trustless as its underlying layers of technology**. For this reason SIR uses the Uniswap v3 oracle which is, in our opinion, the most trustless on-chain price oracle for the following reasons:

* [x] <mark style="background-color:blue;">Purely on-chain.</mark> Being on-chain implies that it is ran by smart contracts, and therefore it is fully auditable and ruled by its smart contracts.
* [x] <mark style="background-color:orange;">Immutable smart contracts.</mark> Contrary to many other money legos, all versions of Uniswap were launched with non-upgradable immutable contracts.
* [x] <mark style="background-color:purple;">Protected by economic incentives.</mark> Any divergence between the price of Uniswap v3 and any other exchange will be arbitraged for a profit, eliminating the price difference. The cost to manipulate the price is proportional to the liquidity of the traded pair.
* [x] <mark style="background-color:green;">Permissionless.</mark> Similar to a blockchain, a key part is that anyone can arbitrage the price between Uniswap v3 and any exchange.
* [x] <mark style="background-color:red;">Largest liquidity.</mark> Uniswap v3 is [the most liquid DEX](https://www.coingecko.com/en/dex) and among the top most liquid exchanges.

Uniswap v3 allows for the retrieval of a [time-weighted-averaged-price](https://en.wikipedia.org/wiki/Time-weighted\_average\_price) (TWAP).

{% hint style="warning" %}
Uniswap v3 is **not suitable for instant market prices** because they can be easily manipulated, for example, with the use of flash loans.
{% endhint %}

The above shortcoming is not a problem for SIR because a TWAP provides protection against sudden market volatility and mitigates the risk of liquidation.

{% hint style="warning" %}
Arguably, the biggest shortcoming of Uniswap v3 is that **it can only report prices of ERC20 tokens that exist on-chain**.
{% endhint %}

### Weighted Geometric Price Mean

Contrary to standard TWAP where the average across time is a simple arithmetic mean, Uniswap v3 ouputs the [time-weighted-**geometric**-mean](https://twitter.com/danrobinson/status/1455237045568348163?lang=en) (gmTWAP). This is more of a technical consideration and for all practical purposes is very similar to standard TWAP.

When SIR retrieves the price for a particular token pair from Uniswap v3, it retrieves it from all the existing [pool fee tiers](https://docs.uniswap.org/protocol/concepts/V3-overview/fees#pool-fees-tiers). These are Unsiwap v3 pools with the same pair of tokens but different fee structure. SIR weights the gmTWAP of all pool fee tiers by their liquidity (which is a also metric output by Uniswap v3). The premise here is that pools with more liquidity should have a bigger impact on the oracle price.
