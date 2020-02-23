Vision
======
AKA: At the highest level, how will this project solve its motivating problems, or put differently, what will be done in the project?

This project will provide a single, unambiguous, generically useful, and trivially extended / customizable API for conducting variational inference.

First, by building an inference framework around generalized variational inference (GVI), this project aims to be as generally useful as possible.
In particular, the use of various kernel divergences allows for theoretically justified variational inference in an essentially unlimited combination of models, priors, and approximate posterior distributions.

Second, to lower the barrier to entry for using variational inference, this project will offer a single, clearly defined process for setting up and using GVI in one’s problem.
We will do this by leveraging the generality and modularity of GVI itself.
Specifically, GVI provides for a single, common optimization objective with study-specific components (e.g. likelihoods, priors, variational approximating families, etc.).
We will build on this common objective by creating and re-using a single corresponding codebase that will be composed with user-supplied objects for the parts specific to the user's study.

Finally, this project will ensure flexibility by building on templates such as pytorch-lightning that have been praised and highly adopted for removing boilerplate but still allowing for user customization if desired.

This project will aim to mimic the practices of such pre-existing template projects as closely as possible.
