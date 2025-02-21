---
hidden: true
---

# 📈 Profit Potential

\
One of the defining features of SIR’s APE is its ability to amplify returns based on market movements while operating within liquidity limits.

Unlike traditional leveraged products, APE eliminates time-based penalties (e.g., funding fees or decay), ensuring your gains or losses depend solely on price action and a one-time fee. This chapter breaks down the mechanics of APE’s profit potential using a clear mathematical model.

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
* **No Time Penalty**: Returns depend purely on price movement, not holding duration. (In reality there are conditions which breaks this and returns become path dependent, but more on this [liquidity-and-leverage](../liquidity-and-leverage/ "mention"))

### Example Scenario

Assume an initial investment $$x=\$1000$$ in the pair `(ETH/USD)^1.5`, and the fee is $$f=24\%$$.

<table><thead><tr><th>Price Change	</th><th>Calculation</th><th>Gain Multiple</th><th data-type="number">Exit Value</th><th data-type="number">Net Return</th></tr></thead><tbody><tr><td>-50</td><td></td><td>NaN</td><td>23</td><td>null</td></tr><tr><td>-25%</td><td>NaN</td><td>NaN</td><td>null</td><td>null</td></tr><tr><td>0%</td><td>NaN</td><td>NaN</td><td>null</td><td>null</td></tr><tr><td>+50%</td><td></td><td></td><td>null</td><td>null</td></tr></tbody></table>
