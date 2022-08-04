# 🦍 APE Token Basics

<mark style="background-color:blue;">APE tokens tracks the price of an underlying token with leverage.</mark> It turns out that if the leverage is

1. continuously-rebalanced-and-perfectly-constant, and
2. no funding/maintenance fees are charged,

then the price ($$q$$) follows the power-law

$$
\begin{equation}q=p^l,\end{equation}
$$

where

* $$p$$ is the price of the underlying asset, and&#x20;
* $$l$$ is the leverage ratio.

From the expression we can derive a few example curves for visualization purposes.

<img src="../../.gitbook/assets/file.drawing (6).svg" alt="APE price vs. its underlying asset price for different leverage ratios. Under normal conditions, the APE token never goes to 0 unless the underlying goes to 0." class="gitbook-drawing">

#### The Leverage Ratio

Before going into more details, let us first define the leverage ratio as

$$
\begin{equation}
l = \frac{\text{value of total assets}}{\text{equity}}= \frac{\text{value of total assets}}{\text{value of total assets}-\text{borrowed capital}}.
\end{equation}
$$

Usually, leveraged tokens or [leveraged ETFs attempt to maintain a constant leverage](https://www.investopedia.com/articles/exchangetradedfunds/07/leveraged-etf.asp#mntl-sc-block\_1-0-32) ($$l$$) by periodically adjusting their debt based on the value of total assets.

For example, [ETH2X-FLI](https://www.indexcoop.com/ethfli) tracks ETH/USD with 2x leverage, such that if the ETH price increases 5% in a day, then ETH2X-FLI increases 10% gain. So if ETH price increases, total assets increases as well, and the denominator increases faster than the numerator, lowering the leverage to less than 2. Therefore, ETH2X-FLI would borrow more to buy more ETH, and rebalance the leverage back to 2. Similarly, if the ETH price decreased, ETH2X-FLI sells ETH and pays off some of the debt.

#### How to Instantly Rebalance?

Instead of operating on large time intervals for rebalancing, <mark style="background-color:green;">APE tokens</mark> <mark style="background-color:green;"></mark><mark style="background-color:green;">**rebalance instantly**</mark> upon any price fluctuation. It turns out that if the leverage is always constant. From (1) the theoretical advantages of constant-leverage tokens, such as APE, are that

1. they cannot go to 0 (i.e., be liquidated) because $$q=0$$ only if $$p=0$$, and
2. the payout grows polynomially as the price increases.

{% hint style="info" %}
By mitigating the risk of liquidation and removing the funding fees, APE tokens will be the first leveraged tokens suitable for mid/long-term investing.&#x20;
{% endhint %}

While APE effectively behaves as an instantly rebalanced leveraged token, internally it works different to other leverage derivatives which need to continuously take on debt or pay it off by interacting with a lending platform like [Aave](https://aave.com/).

In SIR, the pool contract uses its own reserve of collateral to increase or decrease the value of the APE token according to formula (1). Liquidity is moved internally (without emitting actual transactions) between the different users in the pool: holders of TEA, holders of APE and liquidity providers (LPers). The pool can do it because the holders of TEA are effectively counter-trading the holders of APE; and the LPers are essentially holding a mixed bag of TEA and APE managed by the pool itself in exchange for protocol fees. More technical details in [leverage-rebalancing](../../the-protocol/leverage-rebalancing/ "mention").
