**Gaussian similarity search - literature review**

- [Dong 15] Top-k Similarity Search over Gaussian Distributions Based on KL-Divergence
	- Search on *non-correlated* Gaussian distributions
		- Argue that compared to general Gaussians, non-correlated reduces parameters, storage and compute.
	- Use *KL-divergence*
	- Exploit the properties of  KL-div for uncorrelation Gaussians. These do not hold for general Gaussians.

- [Dong 17] k-Expected Nearest Neighbor Search over Gaussian Objects
	- Tries to measure 'probabilistic location information' through so-called *expected distance*
		- Expected distance is essentially the distance between two probabilistic objects (i.e. points with stochastic loations).
		This is computed through $$igr ||x - q||^2 * p(x) dx$$
		- It is unrelated to KL-divergence
		- Needs importance sampling to be estimated.
	- Do efficient search through bounding the expected distance, and using R-tree.

- [Bohm 06] The Gauss-Tree: Efficient Object Identification in Databases of Probabilistic Feature Vectors
	- Models vectors/time series as probabilistic points by *adding a standard deviation to each observation*. Then, computes distances using conditional probabilities.
		- Mind that this is a multivariate Gaussian, but an uncorrelated one, as the covariance matrix is diagonal.

- [Charbuillet 10] A fast algorithm for music search by similarity in large databases based on modified Symetrized Kullback Leibler Divergence
	- Consider *full-covariance* Gaussian distributions
	- Turn KL-divergence into true metric and then use M-tree to prune
		- Transformation is done through TG-modifier
	- Also show a method to make a semi-metric into a metric -- could be very interesting for CD-general 
		- See more in [T. Skopal. Uniﬁed framework for fast exact and approximate search in dissimilarity spaces. ACM Transactions on Database Systems (TODS), 32(4):29, 2007].
	- Not very good performance -- max 10x improvement compared to sequential scan with some precision loss.

- [Mesejo-Leon 18] Approximate Nearest Neighbor Search for the Kullback-Leibler divergence (thesis)
	- Do not necessarily focus on gaussians
		- Use histograms of distributions
	- Analyzes 3 methods for ANNS with Kullback Leibler Divergence (as specialization of Bregman divergence)
		- Bregman Ball tree
		- LSH
		- Inverted Index
	- Inverted index performed the best
	- All seems a bit hacky
		- Read again for better understanding of their Gaussian definition

- [Zhang 09] Similarity Search on Bregman Divergence: Towards Non-Metric Indexing
	- Supports *any distribution*
		- Use the normalized histogram
		- Univariate distributios
	- Uses *Bregman divergence*
	- Improves on Bregman Ball tree
	- Expands the original space by adding a value to each vector that is a function if all the previous values, i.e. x = [x0, ..., xn] -> [x0, ..., xn, f(x)]
		- For KL-div, f(x) = xlog(x)
		- Show that this can be used in R-tree and VA file

## Notes
- Discussion with ChatGPT on the difference between KL-div on standard multivariate normal distributions and simply comparing covariance matrices with Frob-norm
	- https://chat.openai.com/share/dddcbfb8-9a91-4f52-bf03-b5e0b8179771

## Reading list

- D. Schnitzer, A. Flexer, G. Widmer, and A. Linz. A ﬁlter and-reﬁne indexing method for fast similarity search in millions of music tracks. In 10th International Society for Music Information Retrieval Conference (ISMIR), Kobe, Japan, 2009.

- Bishop, C.M.: Pattern Recognition and Machine Learning, Springer (2006).