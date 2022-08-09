# Safer Leverage

## The Risks of Using Leverage

In a nutshell, leverage trading consists on taking on debt to purchase more of an asset. [Demand for leverage trading](https://finance.yahoo.com/news/ethereum-based-leverage-trading-protocol-162512422.html) continues to rise in crypto. Margin trading platforms lure new traders with the promise of higher potential gains, however, it also comes with substantial risks.

### Liquidation Risk

In margin trading and futures trading, a trader borrows some asset (usually USD) against his margin (e.g., ETH) to buy more of the same asset he is long. For instance, with 2x leverage on ETH/USD, a user borrows as much USD as his ETH is worth and buys more ETH, starting with twice as much ETH as he had.

On the one hand, if ETH price goes to infinity, he can basically pay his debt for free and ends up with 2x his initial capital in ETH. On the other hand if the ETH price is halved, his capital is worth exactly what he owes, and he is liquidated. I.e., he is forced to sell his ETH to pay back his debt, resulting in a **complete loss of his capital**.  In fact it is estimated that [95% of the traders lose money](https://cointelegraph.com/news/day-trading-bitcoin-why-95-of-traders-lose-money-and-fail).

{% hint style="danger" %}
The higher the leverage, the higher the likelihood of liquidation.
{% endhint %}

### Funding/Maintenance Fees

Contrary to spot trading, margin traders are charged funding fees since the borrow capital. This funding rate slowly erodes the trader's capital, making leveraged trading a losing proposition in the long-run.

### Volatility Decay

Another related type of financial product are leveraged ETFs. In TradFi, leverage ETFs are [Exchange Traded Funds](https://www.investopedia.com/terms/e/etf.asp) that take on some debt to increase exposure to the underlying asset(s):

> A [leveraged ETF](https://www.investopedia.com/terms/l/leveraged-etf.asp) seeks to return some multiples (e.g., 2× or 3×) on the return of the underlying investments. For instance, if the S\&P 500 rises 1%, a 2× leveraged S\&P 500 ETF will return 2% (and if the index falls by 1%, the ETF would lose 2%).

The difference between leveraged ETFs and margin trading is that the debt is rebalanced periodically (usually daily) to keep the leverage quasi-constant. As price goes up, the ETF takes on more debt; and as price declines it pays-off some of its debt. This creates and seemingly great product for the trader because for the same amount of leverage the possible pay-off is much larger, and it mitigates the risk of liquidation since the debt is paid-off before as price goes down.

<img src="../../.gitbook/assets/file.drawing (1) (1).svg" alt="Made up example of the effects of volatility decay on leveraged ETFs" class="gitbook-drawing">

However, leveraged ETFs are not as popular as one would expect because of a chronic shortcoming. When price trades in a range and the leverage is rebalanced up and down at the end of every day, the ETF suffers from [volatility decay](https://www.coingecko.com/buzz/part-1-introduction-to-crypto-leveraged-etf), slowly bleeding their money away. Coarsely speaking, what happens is that the leverage is decreased when price is about to rebound up, and increased when price is about to drop, which is **exactly the wrong strategy when using leverage**. See [Erina Azmi’s part 2 on leverage ETFs](https://www.coingecko.com/buzz/part-2-deep-dive-into-decentralized-leveraged-etfs) for a performance comparison of such products.

{% hint style="warning" %}
Volatility decay is specially noticeable when the price is range-bound, because the underlying asset's final price may end up the same, but the ETF's value will be lower.
{% endhint %}

### Counterparty Risk

Leverage trading in crypto occurs mostly in centralized exchanges like [Binance and FTX](https://coinmarketcap.com/rankings/exchanges/derivatives/). The traders must deposit their assets and trust that the exchange's security practices will stop any hacks or loss of funds. Unfortunately, crypto has a long history of hacks.&#x20;

{% embed url="https://www.hedgewithcrypto.com/cryptocurrency-exchange-hacks/" %}

## A New DeFi Primitive

SIR introduces a new primitive to mitigate or eliminate all these risks. For any pair of tokens (say TKNA and TKNB), a synthetic APE token can be created that tracks TKNA/TKNB with any leverage of choice. APE is a leveraged token with the following features:

| Feature                                                  | Description                                                                                                                                                                                                                                               | Problems Solved/Mitigated                      |
| -------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------- |
| Perfectly constant leverage                              | [Under certain liquidity and price conditions](../../the-protocol/leverage-rebalancing/price-stability-range.md), SIR will <mark style="background-color:green;">continuously and instantly rebalance the leverage</mark>, despite of price fluctuations. | <p>Liquidation risk<br>Volatility decay</p>    |
| No funding fees                                          | Fees are only charged upon minting or burning APE token. <mark style="background-color:blue;">No fees are charged while holding APE</mark>.                                                                                                               | Continuous loss of capital due to funding fees |
| No external dependances except for the Uniswap v3 oracle | SIR needs a price oracle and <mark style="background-color:purple;">Uniswap v3 is</mark> THE DEX (<mark style="background-color:purple;">trustless</mark> & highest volume).                                                                              | Counterparty risk                              |
| Tokenized leverage                                       | APE is a <mark style="background-color:orange;">fully-compliant ERC20 token</mark>. Therefore it can be transferred, held in a wallet just like any other regular ERC20, and used as collateral in other DeFi apps.                                       | Money Lego                                     |

In the next section we delve deeper into the mechanics of the APE token.
