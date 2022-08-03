# 💳 Apes' Leverage Ratio

This is exactly equivalent to a margin position with a loan of $$T$$ \[DBT] and initial margin $$A_0=R-T/p_0$$ \[COL] where $$p_0$$ is the starting price. According to (1) in [ape-token-basics.md](../../introduction/safer-leverage/ape-token-basics.md "mention"), the leverage ratio of this position is

$$
\begin{equation}
l_\text{eff}=\frac{R}{A}=\frac{R}{R-T/p}.
\end{equation}
$$

Notice that the the only variable parameter as a function of price is $$A$$, not $$R$$ and $$T$$. Here, $$l_\text{eff}$$ is used to distinguish the true oscillating leverage ratio from the fixed leverage ratio ($$l$$) targeted by the pool.&#x20;

{% hint style="warning" %}
The effective leverage ratio ($$l_\text{eff}$$) fluctuates with the price, and therefore it will diverge from the pool's target leverage ratio ($$l$$) if left untouched.
{% endhint %}

In combination with (2) and (3) in [#the-collateralization-factor](../protocol-intro.md#the-collateralization-factor "mention"), we get the following insightful variations of (1):

$$
\begin{align}
R &= l_\text{eff} A \\
R &= r_\text{eff} G \\
A &= (r_\text{eff}-1)G \\
G &= (l_\text{eff}-1)A
\end{align}
$$

which outline the parallelisms between the leverage ratio and the collateralization factor.

