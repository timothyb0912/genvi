Requirements [WIP]
============
AKA: what precisely needs to be delivered from the project? I.e. a list of “features”:

The constructed software system must:
1. Take as inputs
    - Model object—subclass of nn.Module
    - Prior object (? Must further specify)
        - How to specify intractable prior in pyro? E.g. a prior that is itself composed of an un-normalized multiplication of densities
    - Guide object from Pyro (? Must further specify)
    - Data-based loss function (? Must further specify)
    - Divergence measure between prior and guide (? Must further specify)
    - PyTorch Dataset object
    - [In fit method] X, Y (or some dataset object)
2. Return as outputs:
    - Fitted parameter values for the guide
    - Whatever other info the user specified to capture as part of the training procedure. (? Must further specify)
    - Anything else? (? Must further specify; should look at the predecessor packages and what they return from their fit methods)
3. Implement the GVI theoretical framework, for theoretical support / justification.
4. Seamlessly integrate (what does this mean?) with PyTorch and Pyro
    - Have defined interfaces / classes that communicate with PyTorch and Pyro, e.g.
        - a very general compound loss class (to allow communication / compatibility with PyTorch)
            - that can be infinitely composed with other compound losses for maximum generality
            - A subclass of the compound loss that also inherits from Pyro ELBO so that we can have a surrogate ELBO that implements the GVI objective function. (For pyro compatibility)
            - A subclass of the compound loss that will be a compound divergence. Supports generality for users (e.g. using both an IPM loss and a KSD loss for the divergence between prior and guide). These objects will simply take in guides and priors.
            - A subclass of the compound loss that will be a compound data-loss. Again it supports generality for users
        - Package specific wrappers. / classes for the model, prior, guide, losses, and divergences so that we can perform some validity checking (e.g. making sure the specified losses work with the given model, for example a density based loss won’t work with an intractable model that only samples…)
5. Provide guidance for the user in the code itself in the form of
    - docstrings for all (public?) functions
    - aggressive/proactive input validation for all processes
    - Helpful and usefully specific error messages and exceptions
6. Allow for use in sci-kit learn pipelines by taking (X, Y) in a .fit() method.
7. Be able to incorporate the following potential / expected future changes:
    - Framework agnosticism (e.g. being built atop ignite instead of pytorch-lightning, etc.)
    - Basing losses and divergences off of [model, posterior_guide, observed data, prior, prior_guide].  This will allow for maximum generality / extreme fanciness, e.g
        - Un-normalized density as prior (e.g. “masking” / “priors on functionals” / “predicate exchange”) but no easy way to sample from the prior. Can combine with a prior_guide from which we can sample and use variational inference to make the prior_guide approximate the prior.
        - Differential Equation as prior encoding scientific knowledge. Same issue as above, can combine with a prior_guide from which we can sample (and possibly compute densities) and use variational inference to make the prior_guide approximate the prior.
        - Data-based prior processes such as the classical (i.e. of Dennison, Mallick, etc.) priors for decision trees.
    - (? Must further specify)
8. Be able to fail gracefully in the following ways:
    - (? Must further specify; I don’t even know what it means for the software to fail. Cannot instantiate the Trainer object? I should look at bugs filed with other framework packages like lightning/inferno/ignite/aorun/skorch/etc.)
9. Purposefully (and with written rationale) balance
    - Conflicting benefits that the software could be designed to maximize
        - flexibility vs usability (e.g removal of boilerplate increases usability and decreases flexibility)
    - project benefits vs costs
        - flexibility & usability vs producibility / maintainability (e.g. supporting particle variational inference for intractable priors and using those particles in a IPM loss with the guide samples, in a compound divergence with a typical KSD)
    - (? Must further specify)
10. Demonstrate correctness and general applicability on a variety of simulated and real-world test cases / case studies such as
    - Mean-field VI for MNL
    - Mean-field VI for MXL
    - Some GVI (e.g. particle optimization) for an arbitrary, somewhat complex model from published literature / Pyro examples
11. Be publicly accessible via:
    - PyPI and Anaconda for all operating systems
    - a project website with case studies / examples and tutorials that show the workflow and demonstrate package use
    - online documentation such as read-the-docs
12. So users can trust the software (and to save developer time and headache), have a test suite with
    - __% (high, full, etc.) code coverage
    - all types of tests deemed necessary
    - etc.
13. Not address the following topics / issues: they are non-goals
    - Demonstration of generalized variational inference being a good technique to use
        - No comparisons with MCMC
        - No comparisons on a wide variety of known posterior distributions of varying shapes and modalities
        - No comparisons vs other inference methods (e.g. Divergence variational inference where some non-KL-divergence between the standard bayesian posterior and the guide is used)
    - Demonstration of a complete workflow for bayesian variational inference, i.e.
        - prior predictive checks / calibration
        - simulation-based inference checking
        - inference
        - inference validation (i.e. estimation diagnostics)
        - model checking
        - model refinement
    - Routinizing evaluation of the fitted approximate posterior.
        - This project will only be concerned with routinizing model fitting.
        - Routinizing model evaluation is also important, and as such it deserves to be its own separate effort / project.
