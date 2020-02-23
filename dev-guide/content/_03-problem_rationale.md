Project Rationale
=================
AKA: why work on this problem now?

The problems motivating this project are not new.

It is indeed very old news that bayesian inference is (often) harder than frequentist inference since integration (on which bayesian inference is based) is harder than differentiation (on which frequentist inference is based).

What has changed to make this problem ideal for addressing now is the following.

Circa 2016 and onwards, the Python programming language gained access to automatic differentiation as a generically usable tool.

This came because of open-source projects such as Tensorflow, PyTorch, Autograd, JAX, and others.

In 2018 those automatic differentiation tools were put to use in the Pyro library for probabilistic programming. This allowed arbitrary probabilistic and statistical models to be expressed in python and to automatically make available the derivatives of their associated probability density and probability mass functions.

Lastly, in 2019 the world saw
1. the release and immediate large community adoption of pytorch-lightning which aims to provide a straightforward and consistent process for building models in PyTorch, and
2. the ArXiv release of generalized variational inference (GVI).
    1. GVI (together with various kernel-based divergences of the last 10 - 12 years) provides a theoretical basis for a computational implementation of a single, composable approach to variational inference for arbitrary study setups.

All in all, it is only since December 2019 that all of the tools existed that are needed to make bayesian inference easy for anyone to perform in python.

Given that December was only a couple of weeks ago, it’s a great time for this project as very few others are likely to be working on it yet, and all of our research and industry efforts would immediately benefit from such a tool.

We will all benefit from
- Increased productivity and lower barriers to entry as we remove the guesswork in setting up a study for use with variational inference.
- Greater levels of reproducibility and collaboration as it becomes easier to share, understand, and repeat standardized workflows.
