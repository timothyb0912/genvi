Who?
===
A collaborative, online, open-source effort. I.e., as many of us who choose to be involved.

What?
====
A python package for straightforward and easy variational inference (VI) with arbitrary combinations of models and variational approximating families.

      Pytorch           —>    Pyro
        |                      |
        \/                     \/
    Pytorch-lightning    —>    GenVI


Where?
=====
Via the internet

When?
====
In January (planning) and February (execution)?

Why?
===
- To help enable bayesian estimation of models only dreamed of previously. E.g.
    - Discrete choice models with non-parametric error distributions (e.g. neural network generator for the error distribution)
    - Fancy decision tree based models (e.g. heterogeneity across individuals in whether a node is a leaf-node)
- To help enable and routinize bayesian estimation of all models, especially those models most frequently used today.


How
===
- Implement generalized variational inference (GVI) in Python to enable bayesian inference in arbitrary models.
- Build on top of Pyro to make GVI computationally possible.
- Build on top of Pytorch via existing frameworks (e.g. pytorch lightning) to make setup for GVI straightforward, boilerplate-free, and minimally standardized (to support reproducibility and collaboration).
