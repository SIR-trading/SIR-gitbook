# ⚔ Apes vs. Gentlemen

Let $$R$$ be the total amount of collateral deposited in the pool, which we call **the reserve**. [The apes and the gentlemen](../protocol-intro.md#two-types-of-users) "compete" for the collateral in the reserve. Let $$A$$ be the collateral in the reserve allocated to APE, and let $$G$$ be the collateral in the reserve allocated to TEA; then

$$
\begin{equation} R=A+G. \end{equation}
$$

<mark style="background-color:green;">The gentlemen</mark>'s claim to a piece of the reserve is decided by the price of the collateral because the protocol must honor 1 TEA = 1 DBT (worth of collateral), i.e.,

$$
\begin{equation} G=\frac{T}{p}. \end{equation}
$$

Thus, <mark style="background-color:red;">the apes</mark> can claim the rest

$$
\begin{equation} A=R-\frac{T}{p}. \end{equation}
$$

Important to notice that, in the absence of deposits or withdrawals, $$R$$ and $$T$$ are fixed, but the price $$p$$ will oscillate.

#### TEA's Collateralization Factor

Gentlemen's have a claim on $$G$$, a smaller piece of the reserve $$R$$. The fact that the total reserve is larger than the gentlemen's reserve ($$R>G$$) allows the TEA token to withstand fluctuations in the price of the collateral. The real-time collateralization factor is simply

$$
\begin{equation} 
r_\text{eff}=\frac{R}{G}=1+\frac{Ap}{T}.
\end{equation}
$$

It fluctuates with the state of the pool, and is different from the targeted prescribed pool collateralization factor, $$r$$.

#### APE's Leverage Ratio

The apes' reserve expression (3) is exactly equivalent to a margin position with a loan of $$T$$ \[DBT] and initial margin $$A_0=R-T/p_0$$ \[COL] where $$p_0$$ is the starting price. If price increases then $$A>A_0$$, and if price decreases $$A<A_0$$. Thus, according to (1) in [ape-token-basics.md](../../introduction/safer-leverage/ape-token-basics.md "mention"), the real-time leverage ratio of this position is

$$
\begin{equation} l_\text{eff}=\frac{R}{A}=1+\frac{T}{pA}, \end{equation}
$$

which fluctuates with the state of the pool, and is different from the targeted prescribed pool leverage ratio, $$l$$.

#### The Connection Between Collateralization & Leverage

From the expressions above it is clear that the collateralization factor and the leverage ratio are two sides of the same coin:

$$
\begin{equation} 
(r_\text{eff}-1)(l_\text{eff}-1)=1.
\end{equation}
$$
