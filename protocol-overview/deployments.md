# 🌐 Deployments

SIR is deployed on three chains. The core protocol contracts are identical across all deployments — the same Vault, Oracle, and token mechanics — configured for each chain's native DEX and tokens.

---

## Ethereum

| | |
|---|---|
| **Chain ID** | 1 |
| **Native Token** | ETH |
| **SIR Token** | SIR |
| **DEX** | Uniswap V3 |
| **Block Explorer** | [etherscan.io](https://etherscan.io) |

| Contract | Address |
|----------|---------|
| [Vault.sol](https://github.com/SIR-trading/Core/blob/master/src/Vault.sol) | [`0x7Dad75dD36dE234C937C105e652B6E50d68b0309`](https://etherscan.io/address/0x7Dad75dD36dE234C937C105e652B6E50d68b0309) |
| [SIR.sol](https://github.com/SIR-trading/Core/blob/master/src/SIR.sol) | [`0x4Da4fb565Dcd5D5C5dB495205c109bA983A8ABa2`](https://etherscan.io/address/0x4Da4fb565Dcd5D5C5dB495205c109bA983A8ABa2) |
| [Oracle.sol](https://github.com/SIR-trading/Core/blob/master/src/Oracle.sol) | [`0xeD89aF5E62965C45956A0125a5d078218228497A`](https://etherscan.io/address/0xeD89aF5E62965C45956A0125a5d078218228497A) |
| [SystemControl.sol](https://github.com/SIR-trading/Core/blob/master/src/SystemControl.sol) | [`0xbbb9BafB8E41f081fFa064b697bBeffd1a5B52F4`](https://etherscan.io/address/0xbbb9BafB8E41f081fFa064b697bBeffd1a5B52F4) |
| [Contributors.sol](https://github.com/SIR-trading/Core/blob/master/src/Contributors.sol) | [`0xca5d6c55e249a9add07a2440eccfe16f56572cb5`](https://etherscan.io/address/0xca5d6c55e249a9add07a2440eccfe16f56572cb5) |
| [Assistant.sol](https://github.com/SIR-trading/Periphery/blob/main/src/Assistant.sol) | [`0xff14f91285580AEd3733c0B1F3C8b6d04804c5ec`](https://etherscan.io/address/0xff14f91285580AEd3733c0B1F3C8b6d04804c5ec) |

**Uniswap V3 Factory:** [`0x1F98431c8aD98523631AE4a59f267346ea31F984`](https://etherscan.io/address/0x1F98431c8aD98523631AE4a59f267346ea31F984)

---

## HyperEVM

| | |
|---|---|
| **Chain ID** | 999 |
| **Native Token** | HYPE |
| **SIR Token** | HyperSIR |
| **DEX** | HyperSwap |
| **Block Explorer** | [hyperevmscan.io](https://hyperevmscan.io) |

| Contract | Address |
|----------|---------|
| [Vault.sol](https://github.com/SIR-trading/Core/blob/master/src/Vault.sol) | [`0x4a35e7448Dad9cAc6B3e529050B5a6Ee56A0eDF0`](https://hyperevmscan.io/address/0x4a35e7448Dad9cAc6B3e529050B5a6Ee56A0eDF0) |
| [SIR.sol](https://github.com/SIR-trading/Core/blob/master/src/SIR.sol) (HyperSIR) | [`0xA06D0c5a8ADb7134903CA13D1FC0641731E2B766`](https://hyperevmscan.io/address/0xA06D0c5a8ADb7134903CA13D1FC0641731E2B766) |
| [Oracle.sol](https://github.com/SIR-trading/Core/blob/master/src/Oracle.sol) | [`0x2Ab530127a40a832B3e9AD2F0eC6Cdfee17542E0`](https://hyperevmscan.io/address/0x2Ab530127a40a832B3e9AD2F0eC6Cdfee17542E0) |
| [SystemControl.sol](https://github.com/SIR-trading/Core/blob/master/src/SystemControl.sol) | [`0xaAD7A78da51Fa53b50d17f4dA47ae0A042301C93`](https://hyperevmscan.io/address/0xaAD7A78da51Fa53b50d17f4dA47ae0A042301C93) |
| [Contributors.sol](https://github.com/SIR-trading/Core/blob/master/src/Contributors.sol) | [`0xDCd0d8bb7F54010b745Aee52eFf95eA246078A94`](https://hyperevmscan.io/address/0xDCd0d8bb7F54010b745Aee52eFf95eA246078A94) |
| [Assistant.sol](https://github.com/SIR-trading/Periphery/blob/main/src/Assistant.sol) | [`0x7d987b986FbA5e0A4247649A2334Bb2D4029656c`](https://hyperevmscan.io/address/0x7d987b986FbA5e0A4247649A2334Bb2D4029656c) |

**HyperSwap Factory:** [`0xB1c0fa0B789320044A6F623cFe5eBda9562602E3`](https://hyperevmscan.io/address/0xB1c0fa0B789320044A6F623cFe5eBda9562602E3)

---

## MegaETH

| | |
|---|---|
| **Chain ID** | 4326 |
| **Native Token** | ETH |
| **SIR Token** | MegaSIR |
| **DEX** | Kumbaya |
| **Block Explorer** | [megaeth.blockscout.com](https://megaeth.blockscout.com) |

| Contract | Address |
|----------|---------|
| [Vault.sol](https://github.com/SIR-trading/Core/blob/master/src/Vault.sol) | [`0x8d694D1b369BdE5B274Ad643fEdD74f836E88543`](https://megaeth.blockscout.com/address/0x8d694D1b369BdE5B274Ad643fEdD74f836E88543) |
| [SIR.sol](https://github.com/SIR-trading/Core/blob/master/src/SIR.sol) (MegaSIR) | [`0x9367A0c482703d8d9bda995B03f8E71056a72500`](https://megaeth.blockscout.com/address/0x9367A0c482703d8d9bda995B03f8E71056a72500) |
| [Oracle.sol](https://github.com/SIR-trading/Core/blob/master/src/Oracle.sol) | [`0x4edF071a7dEe52fBE663DF7873994725ba91Cdc7`](https://megaeth.blockscout.com/address/0x4edF071a7dEe52fBE663DF7873994725ba91Cdc7) |
| [SystemControl.sol](https://github.com/SIR-trading/Core/blob/master/src/SystemControl.sol) | [`0x549618c8E4b74f9eB319e459698b2CaF53dA0453`](https://megaeth.blockscout.com/address/0x549618c8E4b74f9eB319e459698b2CaF53dA0453) |
| [Contributors.sol](https://github.com/SIR-trading/Core/blob/master/src/Contributors.sol) | [`0x686748764c5C7Aa06FEc784E60D14b650bF79129`](https://megaeth.blockscout.com/address/0x686748764c5C7Aa06FEc784E60D14b650bF79129) |
| [Assistant.sol](https://github.com/SIR-trading/Periphery/blob/main/src/Assistant.sol) | [`0xB91AE2c8365FD45030abA84a4666C4dB074E53E7`](https://megaeth.blockscout.com/address/0xB91AE2c8365FD45030abA84a4666C4dB074E53E7) |

**Kumbaya Factory:** [`0x68b34591f662508076927803c567Cc8006988a09`](https://megaeth.blockscout.com/address/0x68b34591f662508076927803c567Cc8006988a09)

{% hint style="info" %}
LP positions on MegaETH have a lock period. Plan your liquidity provision accordingly.
{% endhint %}
