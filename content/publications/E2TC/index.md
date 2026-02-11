---
abstract: We consider linear stochastic bandits where the set of actions is an
  ellipsoid.  We provide the first known minimax optimal algorithm for this
  problem.  We first derive a novel information-theoretic lower bound on the
  regret of any algorithm, which must be at least $\Omega(\min(d \sigma \sqrt{T}
  + d \|\theta\|_{A}, \|\theta\|_{A} T))$ where $d$ is the dimension, $T$ the
  time horizon, $\sigma^2$ the noise variance, $A$ a matrix defining the set of
  actions and $\theta$ the vector of unknown parameters. We then provide an
  algorithm whose regret matches this bound to a multiplicative universal
  constant.  The algorithm is non-classical in the sense that it is not
  optimistic, and it is not a sampling algorithm.  The main idea is to combine a
  novel sequential procedure to estimate $\|\theta\|_A$, followed by an
  explore-and-commit strategy informed by this estimate. The algorithm is highly
  computationally efficient, and a run requires only time $O(dT + d^2 \log(T/d)
  + d^3)$ and memory $O(d^2)$, in contrast with known optimistic algorithms,
  which are not implementable in polynomial time. We go beyond minimax
  optimality and show that our algorithm is locally asymptotically minimax
  optimal, a much stronger notion of optimality.  We further provide numerical
  experiments to illustrate our theoretical findings. The code to reproduce the
  experiments is available at
  \url{https://github.com/RaymZhang/LinearBanditsEllipsoidsMinimaxCOLT}. }
slides: ""
url_pdf: https://arxiv.org/abs/2502.17175
publication_types:
  - Comference Paper
authors:
  - me
  - Hédi Hadiji
  - Richard Combes
author_notes: []
publication: In *The Thirty Eighth Annual Conference on Learning Theory 2025*
summary: We show that the lower bound for Linear Bandit for ellipsoidal action
  set is $\Omega(\min(d \sigma \sqrt{T} + d \|\theta\|_{A}, \|\theta\|_{A} T))$
  and that for any algorithm hard problem for linear bandit are everywhere. We
  give a low complexity algorithm with mathching regret upperbound.
url_dataset: ""
url_project: ""
publication_short: In *COLT2025*
url_source: ""
url_video: ""
title: "Thompson Sampling For Combinatorial Bandits: Polynomial Regret and
  Mismatched Sampling Paradox"
doi: ""
featured: false
tags: []
projects: []
image:
  caption: ""
  focal_point: ""
  preview_only: false
  filename: featured.jpg
date: 2025-06-30T00:00:00.000Z
url_slides: ""
publishDate: 2024-12-01T00:00:00.000Z
url_poster: ""
url_code: https://github.com/RaymZhang/LinearBanditsEllipsoidsMinimaxCOLT
---


<!-- {{% callout note %}}
Click the *Cite* button above to demo the feature to enable visitors to import publication metadata into their reference management software.
{{% /callout %}}

{{% callout note %}}
Create your slides in Markdown - click the *Slides* button to check out the example.
{{% /callout %}}

Supplementary notes can be added here, including [code, math, and images](https://wowchemy.com/docs/writing-markdown-latex/). -->
