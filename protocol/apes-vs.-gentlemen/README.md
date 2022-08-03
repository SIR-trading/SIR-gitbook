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
