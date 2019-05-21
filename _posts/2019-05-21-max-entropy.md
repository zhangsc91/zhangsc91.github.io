---
layout: post
title: Maximum Entropy -- how not to assume more than what you know
comments: true
---

Here's a great [intro article](https://kconrad.math.uconn.edu/blurbs/analysis/entropypost.pdf) by Keith Conrad. The [Wikipedia article](https://en.wikipedia.org/wiki/Maximum_entropy_probability_distribution) also has a nice table of maximum entropy distributions.

* Take this six-sided die. Now guess which number you will roll next.
* For inevitable things that will happen sooner or later, such as food decaying or atoms going bad, how likely will it happen in relation to an average expiration date?
* If a probability distributions on the real line has mean $\mu$ and standard deviation $\sigma$, what distribution comes to mind?

Given some constraints, for example, the possible outcomes, mean or variance, there are many possible probability distributions. When you don't know much, the best guess is the one that assume the least extra information. (In rock-paper-scissors, if you assume your opponent prefers rock, so you play paper more often, you will be extra punishable than playing neutral. Nash equilibrium!) Lack of information is measure by entropy: 
* for a discrete distribution where outcome $x$ has probability $p(x)$, $ H(p) = -\sum_x p(x) \log (x) $,
* for a continuous distribution with probability density $p(x)$, $ H(p) = -\int_x p(x) \log (x) dx $.

It's best to answer a vague question with honest ignorance. Or as Confucius said, 
>"To know what you know and what you do not know, that is true knowledge".

## Uniform distribution

Back to the opening questions. Given a six-sided die, without knowing anything other than there are 6 possible outcomes, the uniform distribution precisely maximizes $-\sum_i p_i \log p_i$, so indeed it is great place to start, even though we know unfair die is a thing. 

You can solve this maximization problem on 6 variables $p_1,\cdots, p_6$, with the constraint $\sum_i p_i =1$, using Lagrange multiplier for example. Doing this quick calculation will help you understand the rest of the post better!

By the way, the minimum entropy (0) happens when you know for sure that you will get a fixed roll, you cheater. You can make sense of "$0 \log 0$" using L'Hospital's rule.

## Exponential distribution

The maximum entropy probability distribution on $(0, \infty)$ with mean $\tau$ is the exponential distribution Exp($\lambda$): $ p(x) = \lambda e^{-\lambda x}$ where $\lambda=1/\tau$.

Derivation sketch: we want to
* maximize $ -\int_0^\infty p(x) \log p(x) dx $
* with constraints 
  * $ \int_0^\infty p(x) dx = 1 $, and
  * $ \int_0^\infty x p(x) dx = \mu $
  
Here we are maximizing over all functions $p(x)$ satisfying the constraints, so this is an infinite dimensional, variational problem. If at each $x$, we change $p(x)$ by the amount $(\delta p)(x)$, we still want the constraints to hold for the new $p+\delta p$. If $p$ indeed maximizes entropy, then with any such $\delta p$, the change in entropy should be like 0.

Applying "$\delta$" to the two constraints, we require:
* $ \int_0^\infty \delta p dx = 0$
* $ \int_0^\infty x\delta p dx = 0$

Applying "$\delta$" to the entropy, we want:
* $ -\int_0^\infty (\delta p \log p+ \frac{p(x)}{p(x)}\delta p )dx = -\int_0^\infty \delta p \log p dx =0. $

For this to work across all $ \delta p $ under the 2 constraints, $\log p = ax+b$, i.e. $p = Ce^{ax}$. Then the mean calculation and normalization will yield 

$$ p(x) = \frac{1}{\tau} e^{-x/\tau}. $$

Indeed, Exp stands for "expiration".

## Gaussian distribution

The maximum entropy probability distribution on $\mathbb{R}$ with mean $\mu$ and variance $\sigma^2$ is indeed the Gaussian/normal distribution with the same mean and variance, $\mathcal{N}(\mu, \sigma^2)$: 

$$ p(x) = \frac{1}{\sqrt{2\pi}\sigma}\exp\left(-\frac{(x-\mu)^2}{2\sigma^2}\right). $$ 

This fact generalizes to higher dimensions: The maximum entropy probability distribution on $\mathbb{R}^d$ with mean $\mu\in \mathbb{R}^d$ and ($d\times d$ symmetric) co-variance matrix $\Sigma$ is the multivariate normal distribution $\mathcal{N}(\mu, \Sigma)$:

$$p(x) = \frac{1}{(2\pi)^{d/2}(\det(\Sigma))^{1/2}}\exp\left(-\frac{1}{2}(x-\mu)^T \Sigma^{-1} (x-\mu)\right).$$

I used to think that normal distribution is everywhere because of Central Limit Theorem, which says that
> If $X_1, X_2, \cdots$ is a sequence of i.i.d. random variables, each with expectation $\mu$ and variance $\sigma^2$, then the random variable $Z_n=\frac{\sum_{i=1}^n X_i}{\sqrt{n}}$ converges in distribution to $\mathcal{N}(\mu, \sigma^2)$.

($\sqrt{n}$ instead of simply taking average so that the random variable is normalized to have the same variance.) In fact, [this paper](http://www.ams.org/journals/jams/2004-17-04/S0894-0347-04-00459-X/home.html) shows that as $n$ increases, the entropy of $Z_n$ increases monotonically to that of the normal distribution. 

Now I like the maximum entropy explanation better, because it is not assuming that a normal distribution comes from some average of a large ensemble.

Speaking of the average of a large ensemble, and entropy...

## Statistical mechanics

One of the cornerstones of statistical mechanics, Boltzman distribution, can be derived from 2 assumptions: known expected energy, and maximum entropy.

Suppose a system ("canonical ensemble") has countably many different states, each with energy levels $E_1< E_2<\cdots$. The expected energy of the system is $E$, which hopefully is between $E_1$ and $E_\infty$. we want to estimate the probability $p_i$ that the system is in the $i$-th state. 

Assuming nothing else, this becomes a constrained optimization problem, with countably many variables $p_i$:

* Maximize entropy $ H(p)= -\sum_{i=1}^\infty p_i \log p_i $
* under the constraints 
  - $ \mathbb{E}(E_i)= \sum_{i=1}^\infty p_i E_i = E$, and
  - $ \sum_{i=1} p_i = 1$.
  
For the second constraint, we just need to normalize $p_i$ in the end. With only 1 constraint, we use Lagrange multiplier to impose that the 2 (infinite dimensional) gradients differ only by a constant scaler of $\beta$:

$$ \frac{-p_i/p_i-\log p_i}{E_i} = \beta $$

So $ p_i = e^{-\beta E_i -1} \propto e^{-\beta E_i}$. 

Normalize in order for probabilities to sum up to 1: $ p_i = \frac{e^{-\beta E_i}}{Z}$, where 

$$Z=\sum_{i=1}^\infty e^{-\beta E_i}$$ 

is so important it has a name, partition function.

You should have 2 objections: we are not using the given average energy $E$, and also $Z$ as an infinite sum is unsatisfying. CS-minded people might also have suspicion that 1) Boltzman distribution looks like softmax, 2) softmax fits in an exponential family, and 3) in exponential family, there's something called log-partition function. In the next post, I will spell out all the missing links, and explain that indeed log-partition function is log of partition function $Z$, plus more crazy connections!