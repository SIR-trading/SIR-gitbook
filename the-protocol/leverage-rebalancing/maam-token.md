# 👒 MAAM Token

As explained in the previous sections, LPers hold a mix bag of TEA & APE managed by the protocol itself. Depending on the state of the pool, SIR will trade TEA for APE, or vice-versa, with the [goal to always keep the leverage in sync](price-stability-range.md). But LPers do not actually hold the TEA and APE tokens in their wallets. Instead, they are "wrapped" as a new token called MAAM. Just as TEA and APE, at any time

1. MAAM <mark style="background-color:red;">can be burnt</mark> to obtain collateral from the pool's reserve
2. MAAM <mark style="background-color:green;">can be minted</mark> by depositing collateral in the pool

### Rebasing Token

In exchange for depositing collateral, LPers get MAAM. Ideally, in the long-run LPers should outperform a pure collateral position  thanks to the fees taxed on the gentlemen and apes. For this reason MAAM is a rebasing token pegged to the collateral, i.e., 1 MAAM = 1 COL.
