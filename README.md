---
description: A New DeFi Protocol for Safer Leverage
---

# 👋 Introducing SIR

SIR is a DeFi protocol designed to address the key challenges of leveraged trading, such as volatility decay and liquidation risks, making it safer for long-term investing. SIR is live on **Ethereum**, **HyperEVM**, and **MegaETH**. Here's how SIR stands out:

* **Volatility Decay Elimination:** Unlike traditional leveraged ETFs, or other leveraged tokens like Squeeth, that lose value in stagnant markets due to [volatility decay](https://www.afrugaldoctor.com/home/volatility-decay-dont-hold-leveraged-etfs-long-term), SIR ensures that its leveraged tokens maintain their value over time. This is achieved by tracking the value of the leveraged token according to its theoretical power-law formula which eliminates the need for external transactions for rebalancing.

<figure><img src=".gitbook/assets/image (1).png" alt=""><figcaption><p>On May 2022 the price of ETH was the same than in the beginning of the chart, but Squeeth had already lost a fair chunk of value.</p></figcaption></figure>

* **No Funding Fees for Holding Positions:** SIR differentiates itself by not charging any funding fees while you hold a leveraged position. Fees are only applied when minting or burning leveraged tokens, reducing the cost of maintaining long-term positions.
* **Trustless Leveraged Trading:** SIR prioritizes being maximally trustless, a cornerstone for becoming a fundamental DeFi building block. It achieves this by utilizing on-chain price oracles (Uniswap V3 on Ethereum, HyperSwap on HyperEVM, Kumbaya on MegaETH) and thanks to its non-upgradable contracts and immutable parameters.
* **Permissionless Vault Creation:** Echoing the ethos of platforms like Uniswap, which democratize the creation and trading of tokens, SIR brings this philosophy into the leveraged trading space. It allows users to create vaults without needing permission, with each vault defined by its collateral token (COL), debt token (DBT), and leverage $$l$$. This setup enables the leveraged token to accurately track the price of COL/DBT with the chosen leverage $$l$$, providing unparalleled flexibility.

SIR is designed for investors looking for small, long-term compounding leverage, in a maximally trustless setting. By only charging fees on token minting and burning, and addressing the issue of volatility decay internally, SIR offers a more efficient and safer way to engage in leveraged trading in the crypto space.

To understand why this matters and how SIR compares to every other form of leverage, see [Why SIR Matters](protocol-overview/introducing-sir/why-sir-matters.md).

{% hint style="success" %}
Following the [March 2025 exploit](protocol-overview/exploit-and-relaunch.md), SIR was rebuilt and relaunched after completing [four independent security audits](protocol-overview/security-and-risks/audits.md).
{% endhint %}
