---
layout: post
title: "Dirichlet-Inconsistency"
modified:
categories: 
excerpt:
tags: []
css: style
image:
  feature:
date: 2015-01-01T15:56:50-05:00
---

In this post we will illustrate an example of inconsistency of the
Dirichlet process for the elementary problem of cumulative
distribution function estimation. My personal opinion is that this
example of inconsistency in a nonparametric Bayesian setting is easier
to grasp than the more complicated examples given in the seminal work
of Diaconis and Freedman (1986).

## Preliminaries on the Dirichlet Process

I begin by stating some facts about the Dirichlet process, which can
be skipped by those already familiar. First, recall the definition of
the Dirichlet process.

> ### Definition
> 
> A random measure $$P$$ on a measureable space
> $$(\mathscr X, \mathscr B)$$ is a Dirichlet process with
> concentration parameter $$\alpha > 0$$ and mean distribution $$H$$
> if for every partition $$A_1, \ldots, A_k$$ of $$\mathscr X$$, the
> vector $$(P(A_1), \ldots, P(A_k))$$ has a
> $$\operatorname{Dirichlet}(\alpha H(A_1), \ldots, \alpha
> H(A_k))$$. In this case, we will write $$P \sim \mathscr D(\alpha
> H)$$.

There are other ways to define the Dirichlet process which are
equivalent; that this definition is well-defined is suggested by an
appeal to the Kolmogorov Extension Theorem, although making this
strategy work is a little subtle.

More important than the definition above is the following *conjugacy*
property of the Dirichlet distribution. 

> ### Theorem 1
> Suppose we draw $$Y_1, \ldots, Y_n$$ iid from a
> Dirichlet process $$P \sim \mathscr D(\alpha H)$$. If
> $$Y_{n+1}$$ is also independently drawn from $$P$$ then the
> predictive distribution of $$Y_{n+1}$$ given $$Y_1, \ldots, Y_n$$ is
> given by
>
> $$\mathscr L(Y_{n+1} \mid Y_1, \ldots, Y_n) = \frac{\alpha H +
> \sum_{j = 1} ^ n \delta_{Y_{j}}}{\alpha + n}$$.
>
> This predicitve distribution is also the posterior mean of $$P$$ in
> the sense that the posterior distribution of $$P$$ is a Dirichlet
> process with base distribution given by this predictive distribution
> and concentration parameter $$\alpha + n$$.

Here $$\delta_y$$ denotes a point mass distribution at $$y$$ and
$$\mathscr L(A \mid B)$$ is the conditional distribution of the random
element $$A$$ given $$B$$. 

Hence, the Dirichlet process admits a very convenient conjugate
update! If I want to estimate a probability distribution $$P$$ in a
Bayesian manner I can specify a Dirichlet process prior and update my
prior beliefs about $$P$$ in a very straightforward manner. The prior
base distribution $$H$$ constitutes a prior guess of what the
distribution is, and $$\alpha > 0$$ plays the role of a "prior sample
size". Indeed, as $$\alpha \to 0$$, my prior sample size goes to $$0$$
and the estimate of the mean converges to the empirical distribution
$$\mathbb P_n$$. If I am very confident in my guess of the mean
distribution $$H$$ I may choose $$\alpha$$ large, while if I am not I
may choose $$\alpha$$ close to $$0$$ and "let the data speak for
itself." As $$n$$ tends to infinity, we see that the predictive
distribution approaches the empirical cdf, so that the Dirichlet
process 

Below are some draws from the Dirichlet process with $$H = \mathcal
N(0, 1)$$ and various values of $$\alpha$$, with the cdf of the
$$\mathcal N(0, 1)$$ distribution for comparison. First, we might
notice that the cdf of the Dirichlet processes possess jumps. That is
*the Dirichlet process places probability $$1$$ on discrete
distributions*. This is a little dissapointing, considering that we
often expect to encounter continuous distributions in practice. In
addition to this, we state some facts about the Dirichlet process
below.

> ### Facts About the Dirichlet Process
>
> Suppose $$P$$ has a $$\mathscr D(\alpha, H)$$ distribution. Then the
> following are true.
> 
> 1. $$P$$ is a discrete distribution.
> 2. While $$P$$ is discrete, there is a positive probability of
>     $$P$$ being arbitrarily close to any distribution $$F$$.
> 3. 

Property 2 above suggests that the Dirichlet process is a reasonable
model for a random distribution. 

## The Inconsistency

[INSERT DISTINCTION OF DENSITY ESTIMATION AND DISTRIBUTION ESTIMATION,
ALSO NEED TO INTRODUCE THE NOTION OF A TRUE VALUE OF THE CDF]

By far the most common useage of the Dirichlet process is in the
following, relatively unproblematic, case of *density
estimation*. Rather than being interested in $$P$$ itself, one assumes
that there exist latent $$\theta_i$$ drawn from $$P$$, and conditional
on $$\theta_i$$ one observes $$Y_i \sim \mathcal N(\theta_i,
\sigma^2)$$ for example. This induces a continuous distribution on the
$$Y_i$$, which is highly desireable, and bypasses the issues discussed
below.

Occasionally, however, one might be tempted to model the cdf of the
$$Y_i$$ directly with a Dirichlet process; again, this is
unproblematic. If my use case is *distribution function estimation*
then I might not be particularly troubled by the fact that draws of
$$P$$ are discrete; I only care about the cdf. It is easy to see that
as $$n \to \infty$$ that the Dirichlet distribution will behave
essentially as the empirical cdf, which is the gold standard for cdf
estimation.

Being good Bayesians, we may further want to model our uncertainty
about the parameters $$\alpha$$ and $$H$$, or otherwise try to make
the choice less "subjective." Perhaps I'd like to allow for the
possibility of $$P$$ being very close to $$H$$, or very far away from
$$H$$, with the degree of departure being learned from the data. Being
a prudent Bayesian, the casual user might decide to place a prior on
$$\alpha$$ and $$H$$. Both of these tactics sound reasonable, and are
done routinely in the case of density estimation. Placing a prior on
$$H$$ also tends to be unproblematic in the case of cdf
estimation. Where we run into problems is placing a prior on
$$\alpha$$ in the case of distribution estimation. To show this, we
need one more fact.

> ### Proposition 1
>
> Suppose I have collected data $$Y_1, \ldots, Y_n$$ from $$P$$, with
> $$P \sim \mathscr D(\alpha H)$$. Then the likelihood function of
>$$\alpha$$ is given by
> 
> $$L(\alpha) \propto \frac{\alpha^K \Gamma(\alpha)}
>                     {\Gamma(\alpha +n)},$$
>
> where $$K$$ denotes the number of unique values of the $$Y_1,
> \ldots, Y_n$$. 

What stands out about this proposition is the role of the number of
unique values $$Y_i$$ in the likelihood of 
