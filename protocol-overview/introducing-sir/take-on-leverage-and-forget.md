# 📈 Take on Leverage and Forget

APE is SIR's leveraged token designed to magnify returns through directional price exposure, operating within predefined liquidity boundaries. Unlike conventional leveraged products that erode returns with time-based fees (e.g., daily funding costs or volatility decay), APE decouples profitability from holding duration. Gains and losses are determined exclusively by two factors: the ratio between entry and exit prices, and a single upfront fee.

This chapter breaks down the mechanics of APE’s profit potential using a clear mathematical model.

### **The Formula**

APE’s returns are calculated using the following formula:

$$
\textrm{Exit value} = x(1-f)\left(\frac{p'}{p}\right)^l
$$

where&#x20;

* $$x$$ is the initial investment
* $$f$$ is the initial fee, usually larger for higher leverage
* $$p$$ is the entry price
* $$p'$$ is the exit price

#### Key Implications

* **Fixed Initial Fee**: A fixed fee is deducted upfront, meaning the traders experience an immediate loss on opening their position.
* **Convex Returns**: The exponent  amplifies gains and losses non-linearly:
  * **Upside**: Profits accelerate faster than linear growth as prices rise.
  * **Downside**: Losses are mitigated compared to normal leverage, and the trader is never liquidated.
* **No Time Penalty**: Returns depend purely on price movement, not holding duration.

### Example Scenario

Assume an initial investment $$x=\$1000$$ in the pair `(ETH/USD)^1.5`, and the fee is $$f=24\%$$.

| Price Change	 | Calculation             | Gain Multiple | Exit Value | Net Return |
| ------------- | ----------------------- | ------------- | ---------- | ---------- |
| -50           | $$0.76\cdot0.5^{1.5}$$  | 0.27x         | $270       | -74%       |
| -25%          | $$0.76\cdot0.75^{1.5}$$ | 0.49x         | $490       | -51%       |
| 0%            | $$0.76\cdot1^{1.5}$$    | 0.76x         | $760       | -24%       |
| +50%          | $$0.76\cdot1.5^{1.5}$$  | 1.40x         | $1,400     | +40%       |
| +100%         | $$0.76\cdot2^{1.5}$$    | 2.15x         | $2.150     | +115%      |
| +150%         | $$0.76\cdot2.5^{1.5}$$  | 3x            | $3.000     | +200%      |

#### **Critical Considerations**

1. **Liquidity Limits**: APE operates within predefined liquidity bounds. Price movements beyond these limits will make the gains path dependent, and introduce our own version of _volatility decay_.
2. **Fee Structure**: The initial fee necessitates a minimum price recovery to breakeven. For example, to offset the 24% fee, the price must rise by \~32%.

### **Conclusion**

APE offers a unique balance of amplified upside and defined risk, making it a powerful tool for investors confident in directional price movements. By decoupling returns from time and focusing purely on price action, SIR ensures transparency and simplicity in profit generation—provided liquidity constraints are respected.
