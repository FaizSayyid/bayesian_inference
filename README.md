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

![Bayes](https://latex.codecogs.com/svg.latex?p(h%7Cd)%20%3D%20%5Cfrac%7Bp(d%7Ch)p(h)%7D%7Bp(d)%7D)

expanding the denominator, we have:

![Bayes2](https://latex.codecogs.com/svg.latex?p(h%7Cd)%20%3D%20%5Cfrac%7Bp(d%7Ch)p(h)%7D%7B%5Cint%20p(d%7Ch)p(h)%5C%2Cdh%7D)

where

![evidence](https://latex.codecogs.com/svg.latex?p(d)%20%3D%20%5Cint%20p(d%7Ch)p(h)%5C%2Cdh)

---

- ![posterior](https://latex.codecogs.com/svg.latex?p(h%7Cd)) : The posterior; the probability of the hypothesis (e.g. that a parameter has a certain value) given the data  
- ![likelihood](https://latex.codecogs.com/svg.latex?p(d%7Ch)) : The likelihood of observing/generating the data given the hypothesis  
- ![prior](https://latex.codecogs.com/svg.latex?p(h)) : The prior probability of the hypothesis  
- ![marglike](https://latex.codecogs.com/svg.latex?p(d)) : The probability of observing the data under all hypotheses  

---

**It is ![p(d)](https://latex.codecogs.com/svg.latex?p(d)) that makes this equation so difficult to solve in high dimensions (number of parameters to estimate).**

We are left in the following situation:

We have a distribution function

![unnormalised](https://latex.codecogs.com/svg.latex?p(x)%20%3D%20%5Cfrac%7B1%7D%7Bnc%7D%20f(x))

where ![fx](https://latex.codecogs.com/svg.latex?f(x)) is easy to compute but ![nc](https://latex.codecogs.com/svg.latex?nc), the normalising constant, is very hard.  

