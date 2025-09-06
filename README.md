# Approximate inference tutorial
This repo covers the main methods for performing approximate inference in Bayesian statistics. 

Contents:
1. Markov Chain Monte Carlo (MCMC)
2. Approximate Bayesian Computation (ABC)
3. Variational Inference (VI)
4. Sequential Monte Carlo (SMC)
5. Amortised Inference

# Why approximate?
Let's look at Bayes' rule:

\[
p(h \mid d) = \frac{p(d \mid h) \times p(h)}{p(d)}
\]

or:

\[
p(h \mid d) = \frac{p(d \mid h) \times p(h)}{\int p(d \mid h) \times p(h)\, dh}
\]

where

\[
p(d) = \int p(d \mid h) \times p(h)\, dh
\]

- \( p(h \mid d) \): The posterior; the probability of the hypothesis (e.g. that a parameter has a certain value) given the data  
- \( p(d \mid h) \): The likelihood of observing/generating the data given the hypothesis  
- \( p(h) \): The prior probability of the hypothesis  
- \( p(d) \): The probability of observing the data under all hypotheses  

---

**It is \( p(d) \) that makes this equation so difficult to solve in high dimensions (number of parameters to estimate).**

We are left in the following situation:

We have a distribution function

\[
p(x) = \frac{1}{nc} f(x)
\]

where \( f(x) \) is easy to compute but \( nc \), the normalising constant, is very hard.  
