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

Let's define $$p$$ as the current price of the collateral (COL) in terms of the debt token (DBT) units. For instance, if COL = ETH and DBT = USDC, then on April 4, 2024, $$p$$ equals 3,355 USDC/ETH. Ideally, the apes' claim on the reserve, $$A$$, adapts based on the power-law function of constant-leverage:

$$
A'=\left(\frac{p'}{p}\right)^{l−1}A,
$$

where $$A'$$ is the new value of the apes' reserve, $$p'$$ is the new price, $$p$$ is the original price, and $$l$$ is the leverage. This constant leverage regime is the preferred regime but it cannot, logically, be sustained for any price $$p'$$ since$$A'$$ can escalate indefinitely.

To maintain the leverage ratio $$l$$, an additional $$l-1$$ units of liquidity are required for every $$1$$ unit held by the apes. The saturation price, $$p_\textrm{sat}$$, signifies the threshold at which liquidity is fully utilized, i.e., when $$G=(l-1)A$$. Therefore, the vault can accommodate any price movement within the $$[0,p_\textrm{sat}]$$range without disrupting the constant leverage. Importantly, $$p_\textrm{sat}$$ is not static; it adjusts based on the $$G/A$$ ratio, reflecting changes in the gentlemen's liquidity versus the apes' positions. Specifically, $$p_\textrm{sat}$$ increases when gentlemen add liquidity or apes reduce their leveraged positions, and it decreases otherwise.

## The Saturation Zone

\
The saturation zone is initiated when the market price exceeds the defined saturation price, $$p_\textrm{sat}​$$. This transition marks a shift from the ideal state of constant leverage to a scenario where the vault is constrained by the available liquidity, $$G<(l-1)A$$. As the price crosses the saturation price, the gentlemen's are owed a fixed amount in debt token (DBT): $$D=G_\textrm{sat}p_\textrm{sat}$$, and therefore their part of the reserve becomes

$$
G'=\frac{D}{p'}=\frac{p}{p'}G.
$$

For instance, if COL = ETH and DBT = USDC, then the gentlemen are owed a fixed amount in USDC and the apes capture the profit of the ETH bought with USDC appreciating. Essentially, it boils down to a traditional margin long position with initial leverage $$l$$. Just like in a margin long, as the price increases, the apes' leverage ratio decreases&#x20;

&#x20;&#x20;

IT IS PERHAPS MISSING THE PART WHERE GENTLEMEN GET QUITE A NICE CUT OF FEES UPON MINTING/BURNING OF APE, THE HIGHER THE LEVERAGE THE HIGHER THE FEES PAID UPFRONT AND WHEN EXITING BY THE APES. THIS FEES ARE HIGHER THAN NORMAL BUT IT IS THE PRICE TO PAY BY THE APES TO REMAIN FEE-FREE WHILE HOLDING THEIR APE.&#x20;
