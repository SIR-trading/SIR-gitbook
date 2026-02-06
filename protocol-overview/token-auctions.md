---
description: 'Streamlining Conversion: From Diverse Tokens to Dividends'
---

# 🏷️ Token Auctions

SIR accrues fees in various tokens, making direct distributions to [stakers](sir-a-dividend-paying-token/#staking) both gas-intensive and administratively complex. To streamline this, SIR utilizes an efficient auction system for converting all tokens into the chain's native wrapped token seamlessly.

### Auction Mechanics

Each week, an auction is open for every unique ERC-20 token (uniqueness determined by contract address). This auction, lasting one day, allows participants to place bids for the tokens. The process ensures that the highest bidder wins the tokens at the end of the auction, with immediate refunds issued to outbid participants. The process for claiming the auctioned tokens is open to anyone, facilitating the withdrawal to the auction winner.

### Chain-Specific Details

The auction mechanics are the same on every chain, with minor differences in bid currency and minimum bid increase:

| Chain | Bid Currency | Dividend Token | Min Bid Increase |
|-------|-------------|----------------|:---:|
| Ethereum | ETH | WETH | 1% |
| HyperEVM | HYPE | WHYPE | 5% |
| MegaETH | ETH | WETH | 5% |

### Incentives for Participants

This system presents opportunities for those interested in Maximal Extractable Value (MEV), often viewed negatively, and repurposes it into a positive mechanism for SIR. It facilitates the trustless conversion of any token into the dividend token, leveraging MEV for the protocol's advantage. While bids are placed in the chain's native token for simplicity, stakers receive their dividends in the wrapped version, marrying efficiency with ease of implementation.
