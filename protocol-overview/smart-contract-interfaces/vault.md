---
description: Main entry point for minting and burning the protocol's synthetic tokens.
---

# Vault

The Vault is the core contract of SIR Protocol. It uses a singleton architecture — all vaults live in a single contract. Users interact with the Vault to create new vaults, mint/burn APE and TEA tokens, and query vault state.

The Vault inherits from TEA (the ERC1155 LP token contract) and deploys APE contracts (ERC20 clones) for each vault.

{% hint style="warning" %}
**Chain differences:**

- **`mint()` lock parameter:** On MegaETH, `mint()` includes a `portionLockTime` parameter that lets LPers reduce their minting fee by locking TEA. On Ethereum and HyperEVM this parameter does not exist.
- **Native token:** Send ETH with `mint()` on Ethereum/MegaETH (WETH vaults), or HYPE on HyperEVM (WHYPE vaults). The contract auto-wraps the native token.
- **Swap callback:** Named `uniswapV3SwapCallback` on Ethereum/MegaETH, `hyperswapV3SwapCallback` on HyperEVM.
{% endhint %}

---

## `initialize`

Creates a new vault. Permissionless — anyone can call it. Deploys a new APE (ERC20) contract for the vault and initializes the Oracle for the token pair if needed. Reverts if the vault already exists.

```solidity
function initialize(VaultParameters memory vaultParams) external
```

| Parameter | Type | Description |
|-----------|------|-------------|
| `vaultParams` | `VaultParameters` | The debt token, collateral token, and leverage tier identifying the new vault |

> Each unique combination of `(debtToken, collateralToken, leverageTier)` creates a distinct vault with its own APE token.

---

## `mint`

Mints APE or TEA tokens by depositing collateral. Supports three deposit methods:
1. **Collateral token** — set `collateralToDepositMin = 0`
2. **Debt token** (auto-swapped via Uniswap/HyperSwap/Kumbaya) — set `collateralToDepositMin > 0` as slippage protection
3. **Native ETH/HYPE** — send value with the call (only for WETH/WHYPE vaults)

{% tabs %}
{% tab title="Ethereum / HyperEVM" %}
```solidity
function mint(
    bool isAPE,
    VaultParameters memory vaultParams,
    uint256 amountToDeposit,
    uint144 collateralToDepositMin,
    uint40 deadline
) external payable returns (uint256 amount)
```
{% endtab %}

{% tab title="MegaETH" %}
```solidity
function mint(
    bool isAPE,
    VaultParameters memory vaultParams,
    uint256 amountToDeposit,
    uint144 collateralToDepositMin,
    uint40 deadline,
    uint8 portionLockTime
) external payable returns (uint256 amount)
```
{% endtab %}
{% endtabs %}

| Parameter | Type | Description |
|-----------|------|-------------|
| `isAPE` | `bool` | `true` to mint APE, `false` to mint TEA |
| `vaultParams` | `VaultParameters` | The vault to mint into |
| `amountToDeposit` | `uint256` | Amount of collateral (or debt token if `collateralToDepositMin > 0`) to deposit. Ignored when sending native ETH/HYPE. |
| `collateralToDepositMin` | `uint144` | Set to `0` when depositing collateral directly. When depositing debt token, this is the minimum collateral to receive from the swap (slippage protection). |
| `deadline` | `uint40` | Transaction deadline timestamp. Set to `0` to disable. |
| `portionLockTime` | `uint8` | **MegaETH only.** `0` = full fee (no lock), `255` = no fee (full lock period). Ignored for APE mints. |

**Returns:** `uint256` — amount of APE or TEA tokens minted.

> When minting with native ETH/HYPE, `msg.value` overrides `amountToDeposit`. The contract wraps it to WETH/WHYPE automatically.

---

## `burn`

Burns APE or TEA tokens and returns collateral to the caller.

```solidity
function burn(
    bool isAPE,
    VaultParameters calldata vaultParams,
    uint256 amount,
    uint40 deadline
) external returns (uint144)
```

| Parameter | Type | Description |
|-----------|------|-------------|
| `isAPE` | `bool` | `true` to burn APE, `false` to burn TEA |
| `vaultParams` | `VaultParameters` | The vault to burn from |
| `amount` | `uint256` | Amount of APE or TEA tokens to burn |
| `deadline` | `uint40` | Transaction deadline timestamp. Set to `0` to disable. |

**Returns:** `uint144` — amount of collateral received.

> On MegaETH, burning TEA will revert with `TEALocked` if the caller's TEA position is still within its lock period.

---

## `getReserves`

Returns the current reserves of a vault — how much collateral belongs to APE holders vs TEA holders (LPs), and the current price.

```solidity
function getReserves(
    VaultParameters calldata vaultParams
) external view returns (Reserves memory)
```

| Parameter | Type | Description |
|-----------|------|-------------|
| `vaultParams` | `VaultParameters` | The vault to query |

**Returns:** `Reserves` — `(reserveApes, reserveLPers, tickPriceX42)`

---

## `vaultStates`

Returns the raw on-chain state of a vault.

```solidity
function vaultStates(
    VaultParameters calldata vaultParams
) external view returns (VaultState memory)
```

| Parameter | Type | Description |
|-----------|------|-------------|
| `vaultParams` | `VaultParameters` | The vault to query |

**Returns:** `VaultState` — `(reserve, tickPriceSatX42, vaultId)`

> Use `getReserves()` for the decomposed view (separate APE and LP reserves). Use `vaultStates()` to get the vault ID or raw storage values.

---

## `ORACLE`

Returns the current Oracle contract address. On MegaETH, this accounts for pending oracle changes with a time delay.

```solidity
function ORACLE() public view returns (Oracle)
```

**Returns:** The active `Oracle` contract address.

---

## `totalReserves`

Returns the total collateral balance across all vaults for a given token (excluding fees reserved for stakers).

```solidity
function totalReserves(address collateral) external view returns (uint256)
```

| Parameter | Type | Description |
|-----------|------|-------------|
| `collateral` | `address` | The collateral token address |

**Returns:** `uint256` — total collateral held.

---

## `APE_IMPLEMENTATION`

Returns the address of the APE implementation contract used for deploying clones.

```solidity
function APE_IMPLEMENTATION() external view returns (address)
```

**Returns:** The APE implementation address.
