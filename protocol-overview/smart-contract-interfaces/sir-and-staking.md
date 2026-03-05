---
description: SIR token, staking for dividends, reward minting, and fee auctions.
---

# SIR & Staking

The SIR contract is the protocol's ERC-20 governance and reward token. It inherits from Staker, which handles staking, dividend distribution, and fee auctions. SIR stakers receive dividends from protocol trading fees.

{% hint style="warning" %}
**Chain differences:**

- **Token name:** SIR (Ethereum) / HyperSIR (HyperEVM) / MegaSIR (MegaETH)
- **Dividends paid in:** WETH (Ethereum/MegaETH) or WHYPE (HyperEVM), distributed as native ETH/HYPE
- **`bid()` payability:** `payable` on HyperEVM and MegaETH (supports native token bidding); not payable on Ethereum
- **Bid threshold:** Must be >1% higher on Ethereum, >5% higher on HyperEVM/MegaETH
{% endhint %}

---

## Staking & Dividends

### `stake`

Stakes SIR tokens to earn dividends from protocol fees. Newly staked SIR is locked and unlocks gradually — after 30 days, half of the staked amount is unlocked.

```solidity
function stake(uint80 amount) public
```

| Parameter | Type | Description |
|-----------|------|-------------|
| `amount` | `uint80` | Amount of SIR to stake |

---

### `unstake`

Unstakes SIR tokens. Only unlocked stake can be unstaked. Reverts with `InsufficientUnlockedStake` if `amount` exceeds unlocked balance.

```solidity
function unstake(uint80 amount) public
```

| Parameter | Type | Description |
|-----------|------|-------------|
| `amount` | `uint80` | Amount of SIR to unstake |

---

### `claim`

Claims accumulated dividends (ETH on Ethereum/MegaETH, HYPE on HyperEVM). Reverts with `NoDividends` if there is nothing to claim.

```solidity
function claim() public returns (uint96 dividends)
```

**Returns:** `uint96` — amount of native token dividends received.

---

### `unstakeAndClaim`

Convenience function that unstakes SIR and claims dividends in a single transaction.

```solidity
function unstakeAndClaim(uint80 amount) external returns (uint96 dividends)
```

| Parameter | Type | Description |
|-----------|------|-------------|
| `amount` | `uint80` | Amount of SIR to unstake |

**Returns:** `uint96` — amount of dividends received.

---

### `stakeOf`

Returns the unlocked and locked stake breakdown for a staker. Locked stake unlocks gradually with a 30-day half-life.

```solidity
function stakeOf(address staker) external view returns (uint80 unlockedStake, uint80 lockedStake)
```

| Parameter | Type | Description |
|-----------|------|-------------|
| `staker` | `address` | Address to query |

**Returns:** `(unlockedStake, lockedStake)` — breakdown of the staker's position.

---

### `unclaimedDividends`

Returns the amount of unclaimed dividends for a staker.

```solidity
function unclaimedDividends(address staker) external view returns (uint96)
```

| Parameter | Type | Description |
|-----------|------|-------------|
| `staker` | `address` | Address to query |

**Returns:** `uint96` — unclaimed dividend amount (in WETH/WHYPE).

---

## SIR Reward Minting

### `lperMint`

Claims SIR rewards earned by providing liquidity (TEA) in a specific vault.

```solidity
function lperMint(uint256 vaultId) public returns (uint80 rewards)
```

| Parameter | Type | Description |
|-----------|------|-------------|
| `vaultId` | `uint256` | The vault ID to claim rewards from |

**Returns:** `uint80` — amount of SIR minted.

---

### `lperMintAndStake`

Claims SIR rewards from a vault and immediately stakes them in a single transaction.

```solidity
function lperMintAndStake(uint256 vaultId) external returns (uint80 rewards)
```

| Parameter | Type | Description |
|-----------|------|-------------|
| `vaultId` | `uint256` | The vault ID to claim rewards from |

**Returns:** `uint80` — amount of SIR minted and staked.

---

### `contributorMint`

Claims SIR rewards for pre-mainnet contributors based on their allocation. Only available during the first 3 years.

```solidity
function contributorMint() public returns (uint80 rewards)
```

**Returns:** `uint80` — amount of SIR minted.

---

### `contributorMintAndStake`

Claims contributor SIR rewards and immediately stakes them.

```solidity
function contributorMintAndStake() external returns (uint80 rewards)
```

**Returns:** `uint80` — amount of SIR minted and staked.

---

### `contributorUnclaimedSIR`

Returns the amount of unclaimed SIR for a contributor.

```solidity
function contributorUnclaimedSIR(address contributor) public view returns (uint80)
```

| Parameter | Type | Description |
|-----------|------|-------------|
| `contributor` | `address` | Address to query |

**Returns:** `uint80` — unclaimed SIR amount.

---

## Fee Auctions

Protocol fees collected in various tokens are auctioned off for WETH/WHYPE, which is then distributed as dividends to stakers.

### `collectFeesAndStartAuction`

Collects accumulated fees from the Vault for a given token and starts a new auction. If the token is WETH/WHYPE, fees are distributed directly as dividends without an auction.

```solidity
function collectFeesAndStartAuction(address token) external returns (uint256 totalFees)
```

| Parameter | Type | Description |
|-----------|------|-------------|
| `token` | `address` | The fee token to collect and auction |

**Returns:** `uint256` — total fees collected.

> Reverts with `NewAuctionCannotStartYet` if the cooldown from the previous auction hasn't elapsed. Reverts with `NoFeesCollected` if there are no fees to collect.

---

### `bid`

Places a bid on an active fee auction. The bid must exceed the current highest bid by a minimum threshold.

{% tabs %}
{% tab title="Ethereum" %}
```solidity
function bid(address token, uint96 amount) external
```

Bid must be >1% higher than the current winning bid. Bidders must approve WETH spending beforehand.
{% endtab %}

{% tab title="HyperEVM / MegaETH" %}
```solidity
function bid(address token, uint96 amount) external payable
```

Bid must be >5% higher than the current winning bid. Send native ETH/HYPE with the call (auto-wraps), or approve WETH/WHYPE and pass `amount`.
{% endtab %}
{% endtabs %}

| Parameter | Type | Description |
|-----------|------|-------------|
| `token` | `address` | The token being auctioned |
| `amount` | `uint96` | Bid amount in WETH/WHYPE (ignored if `msg.value > 0` on HyperEVM/MegaETH) |

> The same bidder can increase their bid by calling `bid()` again — amounts are additive. Previous bidders are automatically refunded.

---

### `getAuctionLot`

Called by the auction winner after the auction ends to claim the auctioned tokens.

```solidity
function getAuctionLot(address token, address beneficiary) external
```

| Parameter | Type | Description |
|-----------|------|-------------|
| `token` | `address` | The token that was auctioned |
| `beneficiary` | `address` | Address to receive the tokens. Set to `address(0)` to send to the bidder's own address. |

> Reverts with `AuctionIsNotOver` if called before the auction ends, or `NotTheAuctionWinner` if the caller is not the winning bidder.

---

### `auctions`

Returns the current auction state for a token.

```solidity
function auctions(address token) external view returns (Auction memory)
```

| Parameter | Type | Description |
|-----------|------|-------------|
| `token` | `address` | The token to query |

**Returns:** `Auction` — `(bidder, bid, startTime)`.

---

## View / Constants

### `ISSUANCE_RATE`

Returns the global SIR issuance rate (tokens minted per second across all recipients).

```solidity
function ISSUANCE_RATE() external pure returns (uint72)
```

---

### `LP_ISSUANCE_FIRST_3_YEARS`

Returns the SIR issuance rate allocated to LPers during the first 3 years.

```solidity
function LP_ISSUANCE_FIRST_3_YEARS() external pure returns (uint72)
```

---

### `supply`

Returns the current supply of transferable (unstaked) SIR.

```solidity
function supply() external view returns (uint256)
```

---

### `totalSupply`

Returns the total supply of SIR (staked + unstaked, but excluding unclaimed).

```solidity
function totalSupply() external view returns (uint256)
```

---

### `maxTotalSupply`

Returns the maximum total supply as if all SIR tokens had been claimed (staked + unstaked + unclaimed from LPers and contributors).

```solidity
function maxTotalSupply() external view returns (uint256)
```

---

### `DOMAIN_SEPARATOR`

Returns the EIP-712 domain separator for permit signatures.

```solidity
function DOMAIN_SEPARATOR() public view returns (bytes32)
```

---

### `nonces`

Returns the current permit nonce for an address (EIP-2612).

```solidity
function nonces(address owner) external view returns (uint256)
```

---

## Standard ERC-20

The SIR token implements standard ERC-20 functions:

| Function | Signature |
|----------|-----------|
| `balanceOf` | `balanceOf(address account) returns (uint256)` |
| `transfer` | `transfer(address to, uint256 amount) returns (bool)` |
| `transferFrom` | `transferFrom(address from, address to, uint256 amount) returns (bool)` |
| `approve` | `approve(address spender, uint256 amount) returns (bool)` |
| `allowance` | `allowance(address owner, address spender) returns (uint256)` |
| `permit` | `permit(address owner, address spender, uint256 value, uint256 deadline, uint8 v, bytes32 r, bytes32 s)` |

> SIR uses 12 decimals (`SystemConstants.SIR_DECIMALS`). Transfers to `address(0)` or to the staking vault address are not permitted.
