## Approximate inference tutorial
This repo covers the main methods for performing approximate inference in Bayesian statistics. 

Contents:
1. Markov Chain Monte Carlo (MCMC)
2. Approximate Bayesian Computation (ABC)
3. Variational Inference (VI)
4. Sequential Monte Carlo (SMC)
5. Amortised Inference

## Why approximate?
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

where ![fx](https://latex.codecogs.com/svg.latex?f(x)) is easy to compute but ![nc](https://latex.codecogs.com/svg.latex?nc), the normalising constant, is very hard. Because it is so hard to compute exactly in most complicated (non-conjugate) models we instead approximate it.

## Why do we need to compute the evidence?


Because if we want to work out the probability of a particular outcome, we need to normalize by the **total probability of the data under all possible hypotheses**.  

In the finite/discrete case this looks like the familiar formula we learned in school:

![prob](https://latex.codecogs.com/svg.latex?%5Ctext%7Bprobability%7D%20%3D%20%5Cfrac%7B%5Ctext%7Bweight%20of%20the%20ways%20the%20thing%20can%20happen%7D%7D%7B%5Ctext%7Btotal%20weight%20of%20all%20possible%20ways%20it%20could%20happen%7D%7D)

In Bayesian inference the same principle applies, but instead of *counting* outcomes, we **sum or integrate over hypotheses**, weighting each by its prior plausibility and the likelihood of the data under it:

![evidence](https://latex.codecogs.com/svg.latex?p(d)%20%3D%20%5Cint%20p(d%7Ch)%5C%2C%20p(h)%5C%2C%20dh)

This term ensures that the posterior ![posterior](https://latex.codecogs.com/svg.latex?p(h%7Cd)) is a proper probability distribution (i.e. integrates to 1).

**All of the methods covered in this tutorial repo are ways of avoiding having to compute evidence term in its entireity** 


## A sketch to demonstrate how hard computing the evidence can be:
