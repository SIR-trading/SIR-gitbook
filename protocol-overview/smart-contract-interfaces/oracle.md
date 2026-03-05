---
description: TWAP price oracle interface backed by Uniswap V3 / HyperSwap / Kumbaya.
---

# Price Oracle

The Oracle contract provides time-weighted average price (TWAP) feeds for all token pairs used by SIR Protocol. It interfaces with the chain's native Uniswap V3-style DEX and automatically selects the most liquid fee tier for each pair.

The Oracle is fully permissionless — anyone can initialize new token pairs or register new fee tiers.

{% hint style="warning" %}
**Chain differences:**

- **DEX backend:** Uniswap V3 (Ethereum) / HyperSwap (HyperEVM) / Kumbaya (MegaETH)
- **TWAP delta:** 5 minutes on Ethereum vs 1 minute on HyperEVM/MegaETH
- **Fee tier update cadence:** 23 hours on Ethereum vs 1 hour on HyperEVM/MegaETH
- **TWAP duration:** 30 minutes (same on all chains)
{% endhint %}

---

## `getPrice`

Returns the TWAP price for a collateral-debt token pair as a Q21.42 fixed-point tick value. This is a view function that does not modify state.

```solidity
function getPrice(
    address collateralToken,
    address debtToken
) external view returns (int64)
```

| Parameter | Type | Description |
|-----------|------|-------------|
| `collateralToken` | `address` | The collateral token address |
| `debtToken` | `address` | The debt token address |

**Returns:** `int64` — TWAP price as a Q21.42 fixed-point tick. The sign convention ensures the price represents collateral/debt.

> Reverts with `OracleNotInitialized` if the token pair has not been initialized.

---

## `updateOracleState`

Updates the oracle price for a token pair and stores it so subsequent calls in the same block don't need to query the DEX again. Also periodically checks if a better fee tier is available.

```solidity
function updateOracleState(
    address collateralToken,
    address debtToken
) external returns (int64 tickPriceX42, address uniswapPoolAddress)
```

| Parameter | Type | Description |
|-----------|------|-------------|
| `collateralToken` | `address` | The collateral token address |
| `debtToken` | `address` | The debt token address |

**Returns:**
- `tickPriceX42` — updated TWAP price (Q21.42 fixed point)
- `uniswapPoolAddress` — address of the DEX pool currently being used

> This function is called internally by the Vault during mints/burns. External callers (e.g., keepers) can call it to keep prices fresh.

---

## `initialize`

Initializes the oracle for a token pair. Permissionless — anyone can call it. Scans all known fee tiers to find the most liquid pool and sets up the TWAP.

```solidity
function initialize(address tokenA, address tokenB) external
```

| Parameter | Type | Description |
|-----------|------|-------------|
| `tokenA` | `address` | First token address |
| `tokenB` | `address` | Second token address (order does not matter) |

> No-op if already initialized (does not revert). Reverts with `NoUniswapPool` if no pool exists for any fee tier.

---

## `uniswapFeeTierOf`

Returns the fee tier currently being used as the oracle source for a token pair.

```solidity
function uniswapFeeTierOf(
    address tokenA,
    address tokenB
) external view returns (uint24)
```

| Parameter | Type | Description |
|-----------|------|-------------|
| `tokenA` | `address` | First token address |
| `tokenB` | `address` | Second token address (order does not matter) |

**Returns:** `uint24` — fee tier in hundredths of a basis point (e.g., `3000` = 0.30%).

---

## `getUniswapFeeTiers`

Returns all fee tiers known to the Oracle — the 4 default tiers plus any custom ones that have been registered.

```solidity
function getUniswapFeeTiers() public view returns (UniswapFeeTier[] memory)
```

**Returns:** Array of `UniswapFeeTier` structs:

```solidity
struct UniswapFeeTier {
    uint24 fee;          // Fee in hundredths of a bip (e.g., 3000 = 0.30%)
    int24 tickSpacing;   // Tick spacing for this fee tier
}
```

Default fee tiers: `100` (0.01%), `500` (0.05%), `3000` (0.30%), `10000` (1.00%).

---

## `newUniswapFeeTier`

Registers a new DEX fee tier so the Oracle can consider it when selecting the best pool. Permissionless — anyone can call it. The fee tier must exist in the DEX factory.

```solidity
function newUniswapFeeTier(uint24 fee) external
```

| Parameter | Type | Description |
|-----------|------|-------------|
| `fee` | `uint24` | The fee tier to register (must exist in the DEX factory) |

> Maximum of 9 total fee tiers (4 default + 5 custom). Reverts if the fee tier already exists or if the limit is reached.

---

## `state`

Returns the full oracle state for a token pair. Tokens must be provided in lexicographic order (`token0 < token1`).

```solidity
function state(
    address token0,
    address token1
) external view returns (OracleState memory)
```

| Parameter | Type | Description |
|-----------|------|-------------|
| `token0` | `address` | Lower address token |
| `token1` | `address` | Higher address token |

**Returns:** `OracleState`:

```solidity
struct OracleState {
    int64 tickPriceX42;           // Last stored price (Q21.42)
    uint40 timeStampPrice;        // Timestamp of last stored price
    uint8 indexFeeTier;           // Current fee tier index
    uint8 indexFeeTierProbeNext;  // Next fee tier to probe
    uint40 timeStampFeeTier;      // Last fee tier probe timestamp
    bool initialized;             // Whether the oracle is initialized
    UniswapFeeTier uniswapFeeTier; // Current fee tier details
}
```

---

## Constants

| Constant | Value | Description |
|----------|-------|-------------|
| `TWAP_DURATION` | 30 minutes | Duration of the TWAP window (all chains) |
| `UNISWAPV3_FACTORY` | varies | Address of the DEX factory |
| `POOL_INIT_CODE_HASH` | varies | Pool creation code hash for address computation |
