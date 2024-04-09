---
description: Maximally Trustless Prices
---

# 🔮 Price Oracle

According to [Chainlink](https://chain.link/education/blockchain-oracles),

> Blockchain oracles are entities that connect blockchains to external systems, thereby enabling smart contracts to execute based upon inputs and outputs from the real world.

As evident in [liquidity-and-leverage](liquidity-and-leverage/ "mention"), for every vault, SIR requires accurate price data between the collateral and the debt token. SIR integrates the Uniswap v3 Oracle to ensure its price data is as trustless as possible. A wrapper contract around the Uniswap v3 oracle extends its functionality, enabling SIR to:

1. <mark style="background-color:blue;">Selecting the most liquid fee tier:</mark> When SIR retrieves the price for a particular token pair from Uniswap v3, it can fetch it from different [fee tiers](https://docs.uniswap.org/concepts/protocol/fees#pool-fees-tiers). These are Uniswap v3 pools with the same pair of tokens but different fee structure. SIR selects the fee tier with the highest liquidity—a figure directly provided by Uniswap v3. The premise here is that pools with more liquidity are less likely to be manipulated.
2. <mark style="background-color:green;">Autonomous TWAP management:</mark> SIR autonomously handles adjustments to the Time-Weighted Average Price (TWAP), ensuring it selects the most liquid fee tier for accurate pricing. Although SIR typically employs a 15-minute TWAP, it recognizes that not all Uniswap v3 pairs have their price buffers fully initialized. To address this, the system incrementally extends the TWAP duration each time a mint/burn transaction occurs. This gradual extension distributes the initialization cost of the price buffer among many users.
3. <mark style="background-color:red;">Defense against multi-block price manipulation:</mark> The shift from Proof of Work (PoW) to Proof of Stake (PoS) in Ethereum introduced [new attack surfaces for oracles](https://blog.uniswap.org/uniswap-v3-oracles). SIR addresses this risk by coupling its 15-minute TWAP with a price truncation mechanism. This strategy sets a cap on the maximum allowable price change per block, effectively neutralizing the impact of such attacks.

### The Uniswap V3 Oracle

SIR's hypothesis is that **any protocol can only be as trustless as its underlying layers of technology**. For this reason SIR uses the Uniswap v3 oracle which is, in our opinion, the most trustless on-chain price oracle for the following reasons:

* [x] Purely on-chain. Being on-chain implies that it is ran by smart contracts, and therefore it is fully auditable.
* [x] Immutable smart contracts. Contrary to many other money legos, all versions of Uniswap were launched with non-upgradable immutable contracts.
* [x] Protected by economic incentives. Any divergence between the price of Uniswap v3 and any other exchange will be arbitraged for a profit, eliminating the price difference. The cost to manipulate the price is proportional to the liquidity of the traded pair.
* [x] Permissionless. Similar to a blockchain, a key part is that anyone can arbitrage the price between Uniswap v3 and any exchange.
* [x] Largest liquidity. Uniswap v3 is [the most liquid DEX](https://www.coingecko.com/en/dex) and among the top most liquid exchanges.



