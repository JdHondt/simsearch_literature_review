**Hidden markov models for MTS** -- review

1. Computing the log-likehoods for MTS with a subset of the dimensions that an HMM was 'trained' on
	- Given the HMM uses multivariate gaussian to model the emissions probabilities, log-likelihood for a given (subset) MTS can be computed by only using the means and covariances relevant to that MTS (so a subset of the total covariance matrix).
	- This is equal to marginalizing the full distribution to only the relevant dimensions (See book of Kevin Murphy [link](https://probml.github.io/pml-book/).

	- Need good way of normalizing likelihoods between subset dimensions (i.e. the ll of MTS with 3 vs MTS with 2 dims)

	- This whole method could even be made simpler; could just compute the KL-divergence between multivariate gaussians. 

2. Estimating KL-div with method from Ghassempour paper results in one-shot encoding when translating log-likehoods to probabilities. 
	- Name of their approach is *self-normalized importance sampling* (also in Murphy's book).
		- Very hard to follow (ask Tim)

	- Called the *importance weighting/sampling problem*
		- See [this paper](https://digitalassets.lib.berkeley.edu/sdtr/ucb/text/696.pdf)
		
	- Monte-carlo sampling approach would in theory be better, but probably requires an extreme amount of samples to get to good estimated performance, given that the dimensionality of the distribution modeled by the HMMs is very high.