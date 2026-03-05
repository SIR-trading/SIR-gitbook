---
description: LP token (ERC1155) and leveraged token (ERC20) interfaces.
---

# TEA & APE Tokens

SIR Protocol uses two token types to represent positions:

- **TEA** — an ERC1155 token representing LP positions. One token ID per vault, all managed by the Vault contract.
- **APE** — a standard ERC20 token representing leveraged positions. One contract per vault, deployed as a minimal clone.

Minting and burning of both tokens happens through the [Vault](vault.md) contract. The interfaces below cover transfers, approvals, and queries.

{% hint style="info" %}
**Chain differences — token naming:**

- Ethereum: TEA-{id} / APE-{id}
- HyperEVM: HyperTEA{id} / HyperAPE-{id}
- MegaETH: MegaTEA{id} / MegaAPE-{id}
{% endhint %}

---

## TEA (ERC1155 LP Token)

TEA is managed by the Vault contract (which inherits from TEA). Each vault has a unique token ID equal to its `vaultId`.

### `balanceOf`

Returns the TEA balance of an account in a specific vault.

```solidity
function balanceOf(address account, uint256 vaultId) public view returns (uint256)
```

| Parameter | Type | Description |
|-----------|------|-------------|
| `account` | `address` | The account to query |
| `vaultId` | `uint256` | The vault (token ID) to query |

---

### `balanceOfBatch`

Returns TEA balances for multiple account/vault pairs in a single call.

```solidity
function balanceOfBatch(
    address[] calldata owners,
    uint256[] calldata vaultIds
) external view returns (uint256[] memory)
```

| Parameter | Type | Description |
|-----------|------|-------------|
| `owners` | `address[]` | Array of accounts |
| `vaultIds` | `uint256[]` | Array of vault IDs (must match `owners` length) |

---

### `totalSupply`

Returns the total supply of TEA for a specific vault.

```solidity
function totalSupply(uint256 vaultId) external view returns (uint256)
```

| Parameter | Type | Description |
|-----------|------|-------------|
| `vaultId` | `uint256` | The vault to query |

---

### `lockEnd`

Returns the timestamp when a user's TEA position in a vault becomes unlocked. Returns `0` if never locked.

```solidity
function lockEnd(address account, uint256 vaultId) external view returns (uint40)
```

| Parameter | Type | Description |
|-----------|------|-------------|
| `account` | `address` | The account to query |
| `vaultId` | `uint256` | The vault to query |

{% hint style="info" %}
Lock functionality is only active on MegaETH, where LPers can choose to lock TEA during minting to reduce the LP fee. On Ethereum and HyperEVM this always returns `0`.
{% endhint %}

---

### `paramsById`

Returns the vault parameters for a given vault ID.

```solidity
function paramsById(uint48 vaultId) external view returns (VaultParameters memory)
```

| Parameter | Type | Description |
|-----------|------|-------------|
| `vaultId` | `uint48` | The vault ID |

**Returns:** `VaultParameters` — `(debtToken, collateralToken, leverageTier)`.

---

### `numberOfVaults`

Returns the total number of vaults that have been created.

```solidity
function numberOfVaults() external view returns (uint48)
```

---

### `uri`

Returns the ERC1155 metadata URI for a vault. Returns a `data:` URL encoding a JSON object with name, symbol, decimals, chain ID, token addresses, leverage tier, and total supply.

```solidity
function uri(uint256 vaultId) external view returns (string memory)
```

| Parameter | Type | Description |
|-----------|------|-------------|
| `vaultId` | `uint256` | The vault to query |

---

### `supportsInterface`

ERC165 interface detection. Returns `true` for ERC165, ERC1155, and ERC1155MetadataURI.

```solidity
function supportsInterface(bytes4 interfaceId) external pure returns (bool)
```

---

### `safeTransferFrom`

Transfers TEA from one account to another.

```solidity
function safeTransferFrom(
    address from,
    address to,
    uint256 vaultId,
    uint256 amount,
    bytes calldata data
) external
```

| Parameter | Type | Description |
|-----------|------|-------------|
| `from` | `address` | Sender address |
| `to` | `address` | Recipient address |
| `vaultId` | `uint256` | The vault (token ID) |
| `amount` | `uint256` | Amount of TEA to transfer |
| `data` | `bytes` | Additional data for `onERC1155Received` callback |

> On MegaETH, transfers will revert with `TransferToLowerLockEnd` if the sender's lock end timestamp exceeds the recipient's. This prevents circumventing lock periods by transferring to an unlocked wallet.

---

### `safeBatchTransferFrom`

Batch transfers TEA across multiple vaults.

```solidity
function safeBatchTransferFrom(
    address from,
    address to,
    uint256[] calldata vaultIds,
    uint256[] calldata amounts,
    bytes calldata data
) external
```

| Parameter | Type | Description |
|-----------|------|-------------|
| `from` | `address` | Sender address |
| `to` | `address` | Recipient address |
| `vaultIds` | `uint256[]` | Array of vault IDs |
| `amounts` | `uint256[]` | Array of amounts (must match `vaultIds` length) |
| `data` | `bytes` | Additional data for `onERC1155BatchReceived` callback |

---

### `setApprovalForAll`

Grants or revokes operator approval for all TEA transfers.

```solidity
function setApprovalForAll(address operator, bool approved) external
```

| Parameter | Type | Description |
|-----------|------|-------------|
| `operator` | `address` | The operator address |
| `approved` | `bool` | Whether to approve or revoke |

---

### `isApprovedForAll`

Checks if an operator is approved for all TEA transfers on behalf of an account.

```solidity
function isApprovedForAll(address account, address operator) public view returns (bool)
```

---

## APE (ERC20 Leveraged Token)

Each vault has its own APE contract deployed as a minimal clone. APE tokens represent leveraged positions and are standard ERC20 tokens with EIP-2612 permit support.

### `leverageTier`

Returns the leverage tier for this APE token (stored as an immutable argument in the clone).

```solidity
function leverageTier() public pure returns (int8)
```

**Returns:** `int8` — leverage tier from `-2` to `+2`.

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

### Standard ERC20

APE implements the full ERC20 interface plus EIP-2612 permit:

| Function | Signature |
|----------|-----------|
| `name` | `name() returns (string)` |
| `symbol` | `symbol() returns (string)` |
| `decimals` | `decimals() returns (uint8)` |
| `totalSupply` | `totalSupply() returns (uint256)` |
| `balanceOf` | `balanceOf(address account) returns (uint256)` |
| `transfer` | `transfer(address to, uint256 amount) returns (bool)` |
| `transferFrom` | `transferFrom(address from, address to, uint256 amount) returns (bool)` |
| `approve` | `approve(address spender, uint256 amount) returns (bool)` |
| `increaseAllowance` | `increaseAllowance(address spender, uint256 amount) returns (bool)` |
| `decreaseAllowance` | `decreaseAllowance(address spender, uint256 amount) returns (bool)` |
| `allowance` | `allowance(address owner, address spender) returns (uint256)` |
| `permit` | `permit(address owner, address spender, uint256 value, uint256 deadline, uint8 v, bytes32 r, bytes32 s)` |

> APE decimals match the collateral token's decimals. Transfers to `address(0)` are not permitted.
