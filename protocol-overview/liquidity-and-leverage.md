---
description: The Mechanics of Constant Leverage
---

# Liquidity and Leverage

SIR enables the permissionless and trustless creation of vaults, inviting participation from liquidity providers (LPers) and traders. Within these vaults, TEA and APE tokens are minted by depositing collateral. TEA tokens are issued to the gentlemen (LPers) for their liquidity contributions, and APE tokens, an ERC-20 leveraged token, are issued to traders who wish to long COL/DBT (apes). The reserve of collateral, $$R$$, is always split between the gentlemen and the apes

$$
R=G+A.
$$

At any time a gentlemen can claim their part of $$G$$ proportionally to their TEA balance, and similarly the apes can claim their part of $$A$$.&#x20;

## The Limits of Constant Leverage

Let's define $$p$$ as the current price of the collateral (COL) in terms of the debt token (DBT) units. For instance, if the COL = ETH and DBT = USDC, then on April 4, 2024, $$p$$ equals 3,355 USDC/ETH. Ideally, the apes' claim on the reserve, $$A$$, adapts based on the power-law function of constant-leverage:

$$
A'=A\left(\frac{p'}{p}\right)^{l−1},
$$

where $$A'$$ is the new value of the apes' reserve, $$p'$$ is the new price, $$p$$ is the original price, and $$l$$ is the leverage. This is the optimal regime we want to operate in, but obviously from the formula it is not sustainable for any price because $$A'$$ goes to infinity.

In order to sustain the leverage ratio $$l$$, there must be $$l-1$$ units of extra liquidity. The saturation price, $$p_\textrm{sat}$$, is defined as the price where all liquidity is exhausted, i.e.,  $$G=(l-1)A$$. The vault can sustain any price fluctuation within the range $$[0,p_\textrm{sat}]$$without the constant leverage breaking down. The saturation price, $$p_\textrm{sat}$$, is not static; it adjusts in response to the ratio of $$G/A$$—the gentlemen's liquidity to the apes' positions. Specifically, $$p_\textrm{sat}$$ rises when gentlemen add liquidity or apes reduce their leveraged positions, and vice versa.

## The Saturation Zone

\
The saturation zone is initiated when the market price exceeds the defined saturation price, $$p_\textrm{sat}​$$. This transition marks a shift from the ideal state of constant leverage to a scenario where the vault is constrained by the available liquidity. Just like opening a margin long in a centralized exchange, the apes' leverage ratio decreases as the price increases beyond $$p_\textrm{sat}​$$. The gentlemen sold all their COL for DBT, so if $$G_\textrm{sat}$$ was the gentlemen's liquidity at $$p_\textrm{sat}$$ worth $$D_\textrm{sat}=G_\textrm{sat}p_\textrm{sat}$$ in units of DBT

&#x20;&#x20;

IT IS PERHAPS MISSING THE PART WHERE GENTLEMEN GET QUITE A NICE CUT OF FEES UPON MINTING/BURNING OF APE, THE HIGHER THE LEVERAGE THE HIGHER THE FEES PAID UPFRONT AND WHEN EXITING BY THE APES. THIS FEES ARE HIGHER THAN NORMAL BUT IT IS THE PRICE TO PAY BY THE APES TO REMAIN FEE-FREE WHILE HOLDING THEIR APE.&#x20;
