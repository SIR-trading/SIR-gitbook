---
description: The Mechanics of Constant Leverage
---

# Liquidity and Leverage

Vault creation in SIR is open to anyone and is defined by three key parameters: the collateral token (COL), the debt token (DBT), and the leverage ratio ($$l$$). There are two types of users: gentlemen  (liquidity providers or LPers) and the apes (traders). Gentlemen mint TEA tokens by depositing collateral, earning substantial fees generated from the trading activities of the apes. Similarly, apes mint APE tokens, a leveraged COL/DBT token, by also depositing collateral. TEA tokens are ERC-1155, and APE tokens are ERC-20. The reserve of collateral in the vault, $$R$$, is always split between the gentlemen and the apes

$$
R=G+A.
$$

At any time a gentlemen can claim their part of $$G$$ proportionally to their TEA balance, and similarly the apes can claim their part of $$A$$.&#x20;

### Fees

Vaults feature a fee system that rewards the gentlemen with significant fees from the minting and burning of APE tokens. These fees vary by vault, increasing with the vault's leverage ratio. Although these fees are substantial, they allow apes to hold APE tokens without incurring any maintenance fees, regardless of the holding period. The fees for minting or burning APE tokens are on par with the costs of holding a margin position for approximately one year, striking a balance between potential returns and upfront costs. This structure aims to benefit liquidity providers and encourage long-term traders, while short-term traders may not see their speculative positions fully materialize, essentially contributing more to the ecosystem's finances through these initial fees.

## The Limits of Constant Leverage

Let's define $$p$$ as the current price of the collateral (COL) in terms of the debt token (DBT) units. For instance, if COL = ETH and DBT = USDC, then on April 4, 2024, $$p$$ equals 3,355 USDC/ETH. Ideally, the apes' claim on the reserve, $$A$$, adapts based on the power-law function of constant-leverage:

$$
A'=\left(\frac{p'}{p}\right)^{l−1}A,
$$

where $$A'$$ is the new value of the apes' reserve, $$p'$$ is the new price, $$p$$ is the original price, and $$l$$ is the leverage. This constant leverage regime is the preferred regime but it cannot, logically, be sustained for any price $$p'$$ since$$A'$$ can escalate indefinitely.

To maintain the leverage ratio $$l$$, an additional $$l-1$$ units of liquidity are required for every $$1$$ unit held by the apes. The saturation price, $$p_\textrm{sat}$$, signifies the threshold at which liquidity is fully utilized, i.e., when $$G=(l-1)A$$. Therefore, the vault can accommodate any price movement within the $$[0,p_\textrm{sat}]$$range without disrupting the constant leverage. Importantly, $$p_\textrm{sat}$$ is not static; it adjusts based on the $$G/A$$ ratio, reflecting changes in the gentlemen's liquidity versus the apes' positions. Specifically, $$p_\textrm{sat}$$ increases when gentlemen add liquidity or apes reduce their leveraged positions, and it decreases otherwise.

## The Saturation Zone

\
The saturation zone is initiated when the market price surpasses $$p_\textrm{sat}​$$, shifting away from the ideal constant leverage scenario to a liquidity-constrained state, where $$G<(l-1)A$$. Beyond $$p_\textrm{sat}​$$, the amount owed to the gentlemen denominated in debt token (DBT) becomes fixed:: $$D=G_\textrm{sat}p_\textrm{sat}$$, thereby fixing their reserve portion to

$$
G'=\frac{D}{p'}=\frac{p}{p'}G.
$$

In practical terms, if COL = ETH and DBT = USDC, in this regime the gentlemen's reserve value is calculated in USDC, while the apes benefit from the appreciation of ETH versus USDC. This mirrors a conventional margin long position with the initial leverage $$l$$. Similar to traditional margin trading, as the price continues to climb, the effective leverage ratio experienced by the apes diminishes.

&#x20;&#x20;

IT IS PERHAPS MISSING THE PART WHERE GENTLEMEN GET QUITE A NICE CUT OF FEES UPON MINTING/BURNING OF APE, THE HIGHER THE LEVERAGE THE HIGHER THE FEES PAID UPFRONT AND WHEN EXITING BY THE APES. THIS FEES ARE HIGHER THAN NORMAL BUT IT IS THE PRICE TO PAY BY THE APES TO REMAIN FEE-FREE WHILE HOLDING THEIR APE. THE FEES FOR MINTING/BURNING APE ARE A SIMILAR ORDER OF MAGNITUDE TO HOLDING A MARGIN POSITION FOR 1 YEAR.
