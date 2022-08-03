# ⚔ Apes vs. Gentlemen

Let $$R$$ be the total amount of collateral deposited in the pool, which we call **the reserve**. [The apes and the gentlemen](../protocol-intro.md#two-types-of-users) "compete" for the collateral in the reserve. Let $$A$$ be the collateral in the reserve allocated to APE, and let $$G$$ be the collateral in the reserve allocated to TEA; then

$$
\begin{equation}
R=A+G.
\end{equation}
$$

<mark style="background-color:green;">The gentlemen</mark>'s claim to a piece of the reserve is decided by the price of the collateral because the protocol must honor  1 TEA = 1 DBT (worth of collateral), i.e.,

$$
\begin{equation}
G=\frac{T}{p}.
\end{equation}
$$

Thus, <mark style="background-color:red;">the apes</mark> can claim the rest

$$
\begin{equation}
A=R-\frac{T}{p}.
\end{equation}
$$

Important to notice that, in the absence of deposits or withdrawals, $$R$$ and $$T$$ are fixed, but the price $$p$$ will oscillate.

### TEA's Collateralization Factor


### APE's Leverage Ratio

The apes' reserve's expression is exactly equivalent to a margin position with a loan of $$T$$ \[DBT] and initial margin $$A_0=R-T/p_0$$ \[COL] where $$p_0$$ is the starting price. If price increases then $A>A_0$, and if price decreases $A<A_0$. Thus, according to (1) in [ape-token-basics.md](../../introduction/safer-leverage/ape-token-basics.md "mention"), the leverage ratio of this position is

$$
\begin{equation}
l_\text{eff}=\frac{R}{A}=1+\frac{T}{pA}.
\end{equation}
$$