---
description: Function-level reference for integrating with SIR Protocol contracts.
---

# Contract Interfaces

This section documents the public and external functions of SIR Protocol's core contracts. It is intended for developers building on top of the protocol — bots, aggregators, frontends, and other integrations.

For deployed contract addresses, see [Deployments](../deployments.md).

{% hint style="info" %}
The core contracts are deployed on **Ethereum**, **HyperEVM**, and **MegaETH**. Function signatures are nearly identical across chains, but there are meaningful differences noted on each page. Always verify against the deployment you are targeting.
{% endhint %}

<!-- ## Contract Architecture

```
┌─────────────────────────────────────────────────┐
│                    Vault                         │
│  Main entry point: mint / burn APE & TEA tokens  │
│  Singleton — all vaults live in one contract     │
├─────────────────────────────────────────────────┤
│  Inherits: TEA (ERC1155 LP tokens)              │
│  Deploys:  APE (ERC20 clone per vault)          │
│  Reads:    Oracle (TWAP price feed)             │
└──────────────┬──────────────────┬───────────────┘
               │                  │
       ┌───────▼───────┐  ┌──────▼──────┐
       │   TEA (ERC1155) │  │  APE (ERC20) │
       │ One token ID   │  │ One contract │
       │ per vault      │  │ per vault    │
       └───────────────┘  └─────────────┘

┌─────────────────────────────────────────────────┐
│              SIR Token (ERC20)                   │
│  Inherits: Staker                               │
│  Handles: SIR minting, staking, dividends,      │
│           fee auctions                          │
└─────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────┐
│                   Oracle                         │
│  TWAP price feed backed by Uniswap V3 /         │
│  HyperSwap / Kumbaya pools                      │
└─────────────────────────────────────────────────┘
``` -->

## Contract Pages

| Contract | Description |
|----------|-------------|
| [Vault](vault.md) | Main entry point for minting and burning APE/TEA tokens |
| [SIR & Staking](sir-and-staking.md) | SIR token, staking for dividends, reward claiming, and fee auctions |
| [Price Oracle](oracle.md) | TWAP price feed interface |
| [TEA & APE Tokens](tea-and-ape.md) | LP token (ERC1155) and leveraged token (ERC20) interfaces |

## Key Structs

These structs appear throughout the contract interfaces.

### `VaultParameters`

Identifies a specific vault. Used as input to most Vault functions.

```solidity
struct VaultParameters {
    address debtToken;
    address collateralToken;
    int8 leverageTier;       // Range: -2 to +2
}
```

### `Reserves`

Collateral reserves held by a vault, returned by `getReserves()`.

```solidity
struct Reserves {
    uint144 reserveApes;     // Collateral belonging to APE holders
    uint144 reserveLPers;    // Collateral belonging to TEA holders (LPs)
    int64 tickPriceX42;      // Current price in Q21.42 fixed point
}
```

### `VaultState`

On-chain storage representation of a vault's state.

```solidity
struct VaultState {
    uint144 reserve;          // Total reserve (reserveApes + reserveLPers)
    int64 tickPriceSatX42;    // Saturation price in Q21.42 fixed point
    uint48 vaultId;           // Unique vault identifier
}
```

### `Fees`

Fee breakdown returned during mint/burn operations.

```solidity
struct Fees {
    uint144 collateralInOrWithdrawn;   // Net collateral deposited or withdrawn
    uint144 collateralFeeToStakers;    // Fee portion sent to SIR stakers
    uint144 collateralFeeToLPers;      // Fee portion sent to LPers / POL
}
```

### `Auction`

State of a fee auction.

```solidity
struct Auction {
    address bidder;    // Current highest bidder
    uint96 bid;        // Current highest bid amount
    uint40 startTime;  // Auction start timestamp
}
```
