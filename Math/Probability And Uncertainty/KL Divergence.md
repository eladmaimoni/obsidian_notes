https://www.youtube.com/watch?v=q0AkK8aYbLY

$$\sum_i{P(y_i|x_i)}\,log\Bigg(\frac{P(y_i|x_i)}{Q(y_i|x_i)}\Bigg)$$
- $P$ is the true distribution (what our data says)
- $Q$ is the approximated distribution (what our model says)
- We treat the conditional probability as likelihood (function of $x_i$)
- We wish to maximize the likelihood of $y_i$ given $x_i$

### Intuitive Explanation of the KL divergence
- If our approximated model yields more likelihood for a certain $(x_i,y_i)$ pair, then the relevant element in the sum is negative - it means it is a better fit than the true distribution.
- If the approximated model yields less likelihood, then it contributes a positive number to the sum.
- The plain $P(y_i|x_i)$ can be treated as a weight coefficient when summing all possible examples in the dataset.



- We want to quantify:
  If we assume that the distribution is what our model says it is - $Q$, How close is it to the true distribution $P$?

### Requirements From Our Measure
- The measure should equal zero if the distributions are identical
- If the distribution are not equal for certain events, then it should contribute to the overall cost.
- If for certain event, the true distribution is larger $\frac {P(x)}{Q(x)} > 1$ then:
	- It should have a positive contribution to the overall cost (this is not what we want from our approximation)
- If for certain event, the approximated distribution is larger $\frac {P(x)}{Q(x)} < 1$ then:
	- It should reduce our total cost - it means that for this sample, the approximation 
	- it should have an equivalent (but opposite) contribution to the measure as the case where the approximation 
- Sample a sequence from the input space (all possible events)
- Do a weighted sum of $log{\frac {P(x)}{Q(x)}}$
- 
- A weighted sum
- ratio in one direction or another has the same effect in terms of quantification
- 
- We wish to measure how similar 2 distributions *P* and *Q* are.
- *P* is referred to as the 'true' distribution.
- The Algorithm:
  1. generate a sequence of all possible samples. 
  2. The probability of getting this samples with distribution Pr(observation | P) is $\prod_{i}{P(x_i)}$  
  3. The probability of getting this samples with distribution Pr(observation | Q) is $\prod_{i}{Q(x_i)}$  
  4. ask - do the 2 distributions assign the same probability to the sequence?

What Is the Questions?
Give a true distribution P, and an approximated distribution Q, 
What is the cost of assuming the distribution is Q when it is actually P?

If the true distribution is P, we want to quantify how close it is to assume that it is Q.


