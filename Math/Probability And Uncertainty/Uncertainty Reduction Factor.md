- Given new information - by what factor did we increased our cetainty about the event?
- Example:
	- Given a distribution $P(X)$, What is the uncertainty that the event $X=x$ will occur?
	- The certainty that it will occur is $P(X=x)$.
	- If we KNOW that the event $X=x$ has occurred, our certainty is now $1$.
	- So we increased our certainty by a factor of $\frac {1}{P(X=x)}$ .
- The term uncertainty actually means certainty. URF measures how much we increased our certainty.  If we were to measure how much we reduced our uncertainty than it our be $\frac {0} {1-P(X=x)}$ 
-  URF - How much we increased our certainty (Not how much we reduced our uncertainty)
$$URF = \frac {\text{Increased Certainty}}{\text{Initial Certainty}}$$
### Amount of Information in an event
- Uncertainty Reduction Factor with respect to the maximal certainty $\frac {1}{p(x)}$ can be viewed as a measure of the information that a certain event has.
- An event with no information doesn't reduce the uncertainty (we are already certain).
- If a low probability event occurs, that holds more information than if something "exepected" occurs.

### KL divergence
KL divergence has roots in information theory, where it represents the amount of information lost when approximating one distribution with another. This is crucial in contexts like machine learning, where we often deal with models that approximate true data distributions. KL divergence quantifies the inefficiency of assuming that the model distribution is the true distribution.

Unlike symmetric measures (e.g., Euclidean distance), KL divergence is asymmetric. This property is meaningful because it differentiates between the "true" distribution $P$ and an approximation $Q$. In practical terms, $𝐷_{𝐾𝐿}(𝑃∥𝑄)$ represents the cost of assuming that the distribution is 𝑄 when it is actually 𝑃. This is not the same as $𝐷_{𝐾𝐿}(𝑄∥𝑃)$, which would measure the cost in the opposite assumption. This distinction is important in scenarios like variational inference in Bayesian statistics, where we want to minimize the divergence from the true distribution to our approximating family.

- Our examples $\{{x_i,y_i}\}$ depict some empirical distribution of the outputs $q(y)$ 
  it can be viewed as having probability 
- Our model may predict a certain probability distribution $p(y)$.
- The quantity $\frac {p(y)}{q(y)}$ Can depict f 

### Uncertainty And Cross Entropy Loss
- Our examples $\{{x_i,y_i}\}$ depict some empirical distribution of the outputs $q(y)$ 
- Our model may predict a certain probability distribution $p(y)$.
- If we strive to maximize $\frac {p(y)}{q(y)}$ it is as if our model 