---
description: Maximally Trustless Prices
---

# 🔮 Price Oracle

As stated [by Chainlink](https://chain.link/education/blockchain-oracles),

> Blockchain oracles are entities that connect blockchains to external systems, thereby enabling smart contracts to execute based upon inputs and outputs from the real world.

As evident in [liquidity-and-leverage.md](liquidity-and-leverage.md "mention"), for every vault, SIR needs to know the price between the collateral and the debt token. SIR integrates the Uniswap v3 Oracle to ensure its price data is as trustless as possible. SIR implements a wrapper contract around the Uniswap v3 oracle that adds the following functionalities:

1. Selecting the most liquid fee tier: When SIR retrieves the price for a particular token pair from Uniswap v3, it retrieves it from all the existing [pool fee tiers](https://docs.uniswap.org/protocol/concepts/V3-overview/fees#pool-fees-tiers). These are Unsiwap v3 pools with the same pair of tokens but different fee structure. SIR then picks the fee tier which has the largest liquidity (which is a also metric output by Uniswap v3). The premise here is that pools with more liquidity are less likely to be manipulated.
2. The oracle proxy takes care automatically of increasing the TWAP if necessary, and selecting the most liquid fee tier. SIR uses a 15-min TWAP but not all Uniswap v3 pairs may have their price buffer fully initialized. Every time a gentlemen or ape mints/burns, the TWAP is marginally increased in length, so that the cost of initializing its buffer is spread.
3. Defen against multi-block price manipulation attacks. As explained in this blog post by Uniswap, the transition of Ethereum from PoW to PoS brought a new type of possible oracle attack. In combination with the 15-min TWAP, SIR also implements a price truncation mechanism. Essentially the maximum price change per block is capped, thus canceling the effect of the attack.

## The Uniswap V3 Oracle

SIR's hypothesis is that **any protocol can only be as trustless as its underlying layers of technology**. For this reason SIR uses the Uniswap v3 oracle which is, in our opinion, the most trustless on-chain price oracle for the following reasons:

* [x] <mark style="background-color:blue;">Purely on-chain.</mark> Being on-chain implies that it is ran by smart contracts, and therefore it is fully auditable.
* [x] <mark style="background-color:orange;">Immutable smart contracts.</mark> Contrary to many other money legos, all versions of Uniswap were launched with non-upgradable immutable contracts.
* [x] <mark style="background-color:purple;">Protected by economic incentives.</mark> Any divergence between the price of Uniswap v3 and any other exchange will be arbitraged for a profit, eliminating the price difference. The cost to manipulate the price is proportional to the liquidity of the traded pair.
* [x] <mark style="background-color:green;">Permissionless.</mark> Similar to a blockchain, a key part is that anyone can arbitrage the price between Uniswap v3 and any exchange.
* [x] <mark style="background-color:red;">Largest liquidity.</mark> Uniswap v3 is [the most liquid DEX](https://www.coingecko.com/en/dex) and among the top most liquid exchanges.



