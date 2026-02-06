---
description: 'APE: The Math Behind Holdable Leverage'
---

# 📈 Take on Leverage and Forget

APE is SIR's leveraged token designed to magnify returns through directional price exposure. Unlike conventional leveraged products that erode returns with time-based fees (e.g., daily funding costs or volatility decay), APE decouples profitability from holding duration. Gains and losses are determined exclusively by two factors: the ratio between entry and exit prices, and a single upfront fee.

### **The Formula**

Within the [convex zone](../liquidity-and-leverage/#the-limits-of-constant-leverage), APE's returns follow:

$$
\textrm{Exit value} = x(1-f)\left(\frac{p'}{p}\right)^l
$$

where&#x20;

* $$x$$ is the initial investment
* $$f$$ is the initial fee (e.g., ~9% for ^1.5, ~17% for ^2 — higher leverage means higher fee)
* $$p$$ is the entry price
* $$p'$$ is the exit price

#### Key Implications

* **Fixed Initial Fee**: A fixed fee is deducted upfront, meaning the traders experience an immediate loss on opening their position.
* **Convex Returns**: The exponent amplifies gains and losses non-linearly:
  * **Upside**: Profits accelerate faster than linear growth as prices rise.
  * **Downside**: Losses are mitigated compared to normal leverage, and the trader is never liquidated.
* **No Time Penalty**: Returns depend purely on price movement, not holding duration.

### Example Scenario

Assume an initial investment $$x=\$1000$$ in the pair `(ETH/USD)^1.5`, and the fee is $$f=9\%$$.

| Price Change | Calculation              | Gain Multiple | Exit Value | Net Return |
| ------------ | ------------------------ | ------------- | ---------- | ---------- |
| -50%         | $$0.91\cdot0.5^{1.5}$$  | 0.32x         | $322       | -68%       |
| -25%         | $$0.91\cdot0.75^{1.5}$$ | 0.59x         | $591       | -41%       |
| 0%           | $$0.91\cdot1^{1.5}$$    | 0.91x         | $910       | -9%        |
| +50%         | $$0.91\cdot1.5^{1.5}$$  | 1.67x         | $1,672     | +67%       |
| +100%        | $$0.91\cdot2^{1.5}$$    | 2.57x         | $2,574     | +157%      |
| +150%        | $$0.91\cdot2.5^{1.5}$$  | 3.60x         | $3,597     | +260%      |

#### **Critical Considerations**

1. **Liquidity Limits**: The power-law formula holds within the [convex zone](../liquidity-and-leverage/#the-limits-of-constant-leverage). Beyond the saturation price, where demand for leverage exceeds available LP liquidity, gains become path dependent and volatility decay can occur — similar to traditional leveraged tokens. The size of the convex zone depends on the ratio of LP inventory to trader notional. See [Liquidity and Leverage](../liquidity-and-leverage/) for details.
2. **Fee Structure**: The initial fee necessitates a minimum price recovery to breakeven. For example, to offset a 9% fee at ^1.5, the price must rise by ~7%.

### **Conclusion**

APE offers a unique balance of amplified upside and defined risk, making it a powerful tool for investors confident in directional price movements. By decoupling returns from time and focusing purely on price action, SIR ensures transparency and simplicity in profit generation — provided the vault operates within the convex zone.
