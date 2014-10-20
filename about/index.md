---
layout: page
title: Projects
tags: 
modified: 2014-08-08T20:53:07.573882-04:00
comments: true
image:
  feature: texture-feature-02.jpg
  credit: Texture Lovers
  creditlink: http://texturelovers.com
---

## Inference under Nonignorable Missingness in Longitudinal Studies

In clinical trials, it is common to intend collect data on a subject
$$\mathbf Y_i = (Y_{i1}, \ldots, Y_{iJ})$$ but, for various reasons, we only
observe $$Y_{ij}$$ at a subset of the intended collection times, with
$$R_{ij} = 1$$ or $$0$$ according as $$Y_{ij}$$ is observed or
not. The presence of missing data introduces two substantial
problems. 

1. For efficient inference, the values of $$Y_{ij}$$ for which
   $$R_{ij} = 0$$ must - in some sense - be imputed. Even if the
   missing data is missing at random, this is a hard problem in light
   of the curse of dimensionality. Most imputation based methods make
   quite strong parametric assumptions about the distribution of the
   missing data, such as multivariate normality.
2. When the missing data cannot reasonably be assumed to be missing at
   random, the distribution of $$p_\theta(\mathbf y_{mis} \mid \mathbf
   y_{obs}, \mathbf r)$$ is not nonparametrically identified. 

My research is primarily concerned with attempting to address both
issues in a Bayesian nonparametric or semiparametric fashion. To
address the first issue we place priors on the space of
$$p_\theta(\mathbf y_{obs}, \mathbf r)$$ which strike a compromise between
complexity and parsimony, but which otherwise makes no assumptions
about $$p_\theta(\mathbf y_{mis} \mid \mathbf y_{obs}, \mathbf r)$$. To
address the second issue, we embed the distribution of the missing
data in a semiparametric family which controls deviations of our model
from some baseline assumption, such as missing at random, indexed by a
completely unidentified sensitivity parameter $$\xi$$. In true Bayesian
fashion, an expert-prior may be elicited on this parameter to collate
inferences under different missing data assumptions.

## Empirical Bayes and Model Selection in Nonparametric Models

The choice of prior on hyperparameters in Bayesian nonparametric
problems can have a large influence on inferences. Often, researchers
place heuristically justified hierarchical priors to allow for
uncertainty in hyperparameters. This can be an effective strategy, but
then shifts the problem to the specification of the hyperprior. In
some problems the hyperprior must be informative, but it isn't always
easy to make sure that the hyperprior is properly calibrated to get
sensible inferences.

An alternative automatic method for addressing this problem is to
carry out hyperparameter optimization. This introduces it own set of
issues. The empirical Bayes approach optimizes the marginal likelihood
of the observed data to select hyperparameters.

Additionally, it may be questioned in certain (although not all)
problems whether a nonparametric model is required or if a more
parsimonious model would suffice. An example might be to test whether
a parametric assumption on the distribution of some random effects can
be justified. I develop some methods for comparing complicated
nonparametric models through Bayes factors and give computational
devices for doing so.
