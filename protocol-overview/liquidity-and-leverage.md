---
description: The Balance Between Gentlemen and Apes
---

# Liquidity and Leverage

SIR enables the permissionless and trustless creation of vaults, inviting participation from liquidity providers (LPers) and traders. Within these vaults, TEA and APE tokens are minted by depositing collateral. TEA tokens are issued to the gentlemen (LPers) for their liquidity contributions, and APE tokens, an ERC-20 leveraged token, are issued to traders who wish to long COL/DBT (apes). The reserve of collateral, $$R$$, is always split between the gentlemen and the apes

$$
R=G+A.
$$

At any time a gentlemen can claim their part of $$G$$ proportionally to their TEA balance, and similarly the apes can claim their part of $$A$$.&#x20;

## Two Zones of Operation

Let's define $$p$$ as the current price of the collateral (COL) in terms of the debt token (DBT) units. For instance, if the COL = ETH and DBT = USDC, then on April 4, 2024, $$p$$ equals 3,355 USDC/ETH. The system transitions between two operational zones based on $$p$$ and the saturation price, $$p_\textrm{sat}$$, which is fixed by the vault's state. The Power Zone, where the system ideally functions, is characterized by constant leverage and is in effect when $$p<p_\textrm{sat}$$.  Conversely, the Saturation Zone takes over when $$p\geq p_\textrm{sat}$$, where the leverage of the APE token decreases as price moves up, like in a traditional margin long. The saturation price, $$p_\textrm{sat}$$, is not static; it adjusts in response to the ratio of $$G/A$$—the gentlemen's liquidity to the apes' positions. Specifically, $$p_\textrm{sat}$$ rises when gentlemen add liquidity or apes reduce their leveraged positions.

## The Power Zone

The system operates into two distinct operational zones based on the current collateral (COL) price with respect to the debt token (DBT): the Power Zone and the Saturation Zone. The Power Zone, where SIR ideally operates, follows the principle that the apes' reserve, $$�A$$, adapts based on the power-law function $$�′=(�′/�)(�−1)�A′=(p′/p)(l−1)A$$, where $$�′A′$$ is the new value of the apes' reserve, $$�′p′$$ is the new price, $$�p$$ is the original price, and $$�l$$ is the leverage. This ensures the leverage remains constant, enhancing the benefits for the apes. Conversely.

## The Saturation Zone

The Saturation Zone is reached when prices escalate beyond the saturation point, leading to a shift where the gentlemen's reserves, represented by $$�G$$, are recalculated as $$����=(�−1)/�×�Gsat​=(l−1)/l×R$$ in terms of the total reserve $$�R$$, adjusting the distribution between the gentlemen and apes.

Fees are an essential part of the protocol, particularly for the gentlemen. They benefit from the fees generated when APE tokens are minted or burned—fees that escalate with higher leverage. These fees, borne by the apes, enable them to maintain their APE holdings without incurring ongoing charges. Although these fees are above average, they facilitate the maintenance of leverage in the Power Zone.

Transitioning between these zones ensures SIR remains balanced, focusing on equitable gains distribution and maintaining system integrity. This balance is crucial for managing the relationship between liquidity providers and leveraged trading participants effectively.

***

I THINK THE SUBTITLE SHOULD SAY SOMETHING ABOUT THE BALANCE BETWEEN GENTLEMEN AND APES

In SIR's ecosystem, vault creation is permissionless and trustless, aligning with the core principles of decentralized finance. This approach allows both liquidity providers (LPers) and users to participate without barriers. Within each vault, collateral is distributed between two roles: the gentlemen (LPers) and the apes. This distribution underpins the creation of two distinct tokens: TEA for the gentlemen, reflecting their liquidity providing position, and APE for the apes, an ERC-20 leveraged token designed for use both within and outside the SIR protocol. The APE token's value follows a power-law relative to the underlying asset, calculated as $$�=�(�−1)q=p(l−1)$$, ensuring that its value accurately reflects the intended leverage.

PERHAPS IMPORTANT TO MENTION THAT THE POWER-LAW IS THE IDEAL CONSTANT LEVERAGE FORMULA. ALSO POWER ZONE IS THE ZONE THE PROTOCOL WANTS VAULTS TO OPERATE IN. WITH SUFFICIENT LIQUIDITY WE SHOULD ALWAYS BE IN THE POWER ZONE, AND THAT IS WHY FEES ARE IMPORTANT. TOO LITTLE FEES AND WE FAIL TO MAINTAIN THE POWER ZONE AND TOO HIGH FEES AND NO FOLKS WILL MINT APE. SATURATION MODE IS A SUBOPTIMAL PLACE OF OPERATION WHERE APES STILL HAVE SOME LEVERAGE BUT LESS THAN WHAT THEY WISHED FOR.

The operational framework of SIR is structured around two zones: the Power Zone and the Saturation Zone, determined by the current price of the collateral relative to a predefined saturation price. In the Power Zone, the reserve for apes adjusts according to a constant-leverage power-law function, optimizing leverage effects. As the market price approaches the saturation point, the dynamics shift. The protocol transitions into the Saturation Zone, where the leverage model adapts, simulating a traditional margin position without further rebalancing.

This transition between zones is a critical aspect of SIR's design, ensuring that liquidity providers (the gentlemen) gradually shift their collateral to support the apes' leveraged positions. This mechanism is vital for maintaining the balance within the ecosystem, especially as it moves into the Saturation Zone, where the leverage stabilizes, and the focus shifts towards preserving the system's integrity and ensuring fair distribution of gains.

IT IS PERHAPS MISSING THE PART WHERE GENTLEMEN GET QUITE A NICE CUT OF FEES UPON MINTING/BURNING OF APE, THE HIGHER THE LEVERAGE THE HIGHER THE FEES PAID UPFRONT AND WHEN EXITING BY THE APES. THIS FEES ARE HIGHER THAN NORMAL BUT IT IS THE PRICE TO PAY BY THE APES TO REMAIN FEE-FREE WHILE HOLDING THEIR APE.&#x20;
