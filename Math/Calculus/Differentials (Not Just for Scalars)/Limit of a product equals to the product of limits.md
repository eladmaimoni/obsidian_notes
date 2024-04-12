assume $\lim_{x \rightarrow c}f(x) = K$ and $lim_{x \rightarrow c}g(x) = L$ 

$$
\lim_{x \rightarrow c}f(x)g(x) = \lim_{x \rightarrow c}\lbrack(f(x) - K)(g(x) - L) + Kg(x) + Lf(x) + KL\rbrack= \lim_{x \rightarrow c}[(f(x) - K)(g(x) - L)] + KL   
$$

We can now show that the term $\lim_{x \rightarrow c}[(f(x) - K)(g(x) - L)]$ evaluates to 0.
we need to find $\delta$ such that:

$$
\|(f(x) - K)(g(x) - L)\|=\|f(x)-K\|\|g(x)-L\|<\epsilon
$$

We can choose such $\delta$ such that both $f(x) - K$ and $g(x)-L$ are actually smaller then $\sqrt{\epsilon}$ and hence ...