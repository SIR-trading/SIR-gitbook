# 🧪 Beta Period

After launch, SIR will remain in beta for several months. During this period a multisig formed by developers and advisors will have a few admin rights for the safety of the protocol.

:cold\_face: <mark style="background-color:blue;">Permission to freeze minting.</mark> So that in case of a critical bug users can be stopped from minting and depositing more capital. On the other hand, withdrawals will never be halted even during the beta period.

:control\_knobs: <mark style="background-color:green;">Permission to adjust the</mark> [<mark style="background-color:green;">base fee</mark>](fee-structure.md#fee-mechanism)<mark style="background-color:green;">.</mark> Fees are a critical part of any money lego. For instance, [Uniswap v3 only overtook Curve as primary DEX for stablecoin trading once it enable it's 0.01% fee tier](https://twitter.com/RyanWatkins\_/status/1483640421502885888). That is because LPers barely suffer from [impermanent loss](https://medium.com/coinmonks/understanding-impermanent-loss-9ac6795e5baa) in stablecoin-to-stablecoin pairs, and so they can accept much smaller trading commissions for their liquidity. However, it is clear that a 0% fee tier would not work because LPers would have no incentives. Choosing the right fee structure is a sensitive choice for any project. On the one hand, too large fees may discourage users, and on the other hand, too little fees may discourage LPers. So to finely adjust the fee value charged to users, the base fee value ($$f_\text{base}$$) will be tuned during the beta testing of SIR.

:hourglass\_flowing\_sand: <mark style="background-color:orange;">Permission to tune TWAP period.</mark> It is unclear&#x20;
