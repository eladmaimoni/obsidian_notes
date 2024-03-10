
We say that $f$ tends to $b$ if for every $\epsilon$ (as small as we want) there is always a $\delta$ so such that if $x$ is within a ball $B(c, \delta)$, then $f(x)$ is within a ball $B(b, \epsilon)$.

$$
\lim_{x\rightarrow c}(f(x)) = b
$$

### Why does the definition implies that $f$ tends to $b$ as $x$ tends to $c$?
- the definition does not state anything on how close $x$ has to be to $c$
- it only states that no matter how small we choose $\epsilon$, we can always find a $\delta$-Ball around the input $c$ that contains only values that will lead us closer than $\epsilon$ to $b$.

Lets think about **What happens to $x$ when we look a smaller and smaller $\epsilon$ around the limit.
- assume we start with some $\epsilon_1$, then we have our $\delta$-ball around the input.
- let's decide to take the maximal $\delta$ we can for this $\epsilon_1$: $\delta_{1-max}$
- if we now require a smaller $\epsilon$:  $\epsilon_2 < \epsilon_1$ than there is one important thing we can say about the new $\delta_{2-max}$:
	- it cannot be larger then the previous $\delta_{max}$ because otherwise our previously chosen $\delta_{max}$ could have been larger.
	- So it must be that $\delta_{2-max} \leq \delta_{1-max}$  
- So we have basicllay 2 options when we require a smaller $\epsilon$:
	- the behavior around $c$ stays the same, so we can leave our $\delta$ as is and decrease $\epsilon$ as much as we want. This is what will happen with constant functions.
	- $\delta$ will get smaller and smaller - tend to $c$ as we further restrict the ball around the output.