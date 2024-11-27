# Subsequence search on Multivariate time-series (MTS) - literature review

## Multivariate time series
- [Wang 14] Multivariate Time Series Similarity Searching
	- Similarity Search
	- Notes
		- Proposes new similarity measure based on weighted BORDA voting among dimension-wise similarities
		- Get k*-nn for every dimension, then aggregate with voting.
			- k* is larger than final k to make sure top-k is complete.
				- Not sure if correct still.
		- Use PCA as preprocessing step to make MTS dimensions uncorrelated
		- Pretty poor performance in classification evaluation
		- Gives good summary of relevant works in last 10 years
		- Ody: bullshit paper in bullshit conference.

- [Yang 04] A PCA-based Similarity Measure for Multivariate Time Series
	- Similarity Search
	- Notes
		- Proposes new similarity measure for MTS that effectively measures the *weighted sum of the angles* between the *Principal Components* of two MTW.
		- Sim name: **Eros**, Extended Frobenius norm
		- Lots of citations
		- Also has extension papers for indexing and kNN schemes

- [Yang 05] On the Stationarity of Multivariate Time Series for Correlation-Based Data Analysis
	- Notes
		- Argue for stationarity checks on the MTS before using correlation-based similarity measures on MTS like Eros.
		- Simply test stationarity of all timeseries, if the majority is non-stationary they stationarize data using first-order differencing (i.e. np.diff()).

- [Vlachos 06] Indexing Multi-Dimensional Time-Series with Support for Multiple Distance Measures
	- Similarity search
	- Euclidean distance, LCSS, DTW
	- Notes:
		- Provides good summary of pros and cons of Euclidean Distance and Dynamic Time Warping.
		- Suggests Longest Common Subsequence distance (LCSS), because it's 'robust and scalable'
		- Provides multivariate versions of the above distances.
			- Really weird recursive measures though.
		- Provides an index which supports all of those distances
			- Based on R-tree, so pretty *dependent on dimensionality*

- [Yoon 05] Feature Subset Selection and Feature Ranking for Multivariate Time Series 
	- Dimensionality reduction
	- Notes:
		- Presents a way to do feature selection on an MTS dataset based on PCA on each of the MTS.

- [Bagnall 18] The UEA multivariate time series classification archive, 2018
	- Datasets, MTS classification
	- Notes
		- Propose a new archive of benchmark datasets for MTS classification

- [Yekta 17] Generalizing DTW to the multi-dimensional case requires an adaptive approach
	- Notes
		- Argues and shows that not dependent DTW nor independent DTW outperforms the other.
		- Really good and understadable argumentation

- [Santoro 23] Higher-order organization of multivariate time series
	- Multivariate correlation analysis on multivariate time series (MTS)
	- Makes good case for multivariate correlation analysis.
	- Defines correlation on a group of vectors V as *the product of the values of V at a certain timestep t*, i.e., V[:, t].sum().
		- Consequently outputs a correlation graph for each timestep.

- [Yeh 17] Matrix Profile VI: Meaningful Multidimensional Motif Discovery
	- Motif discovery
	- Euclidean distance
	- Notes
		- Make a case for defining motifs not on all dimensions but on a subset -- all dimensions is too constraining, some dims can be noise.
		- Query: Given a MTS T^d and a maximum subset of dimensions k <= d, find all motifs.
		- Create matrix profile for each dimensions and perform some sorting and analysis rules on those to find k subset with lowest distance -> best motif.
			- In summary, again a loop over the matrix profile.

- [Frenzel 07] Partial Mutual Information for Coupling Analysis of Multivariate Time Series
	- Causal inference
	- Mutual information
	- Notes
		- Goal: Data-driven way of constructing Bayesian Network between *dimensions* of MTS.
		- Done through measuring *partial mutual information* I(X,Y | Z)
			- Measured through special k-means NN method of finding kNN value for each t, maximizing over dimensions.

- [Ghassempour 14] Clustering Multivariate Time Series Using Hidden Markov Models
	- Clustering
	- HMM-based distance
	- Notes
		- Cluster by building HMM for each MTS, and then using Kullback-Leibner divergence as distance between HMM. 

- [Ruiz 20] The great multivariate time series classification bake off: a review and experimental evaluation of recent algorithmic advances
	- Classification
	- Survey
	- Notes
		- Provides an overview of the current algorithms for MTSC
			- Dependent
				- kNN with multivariate DTW measure of [Yekta 17].
				- Generalized random shapelet forest
					- Building a decision tree based on the discovered shapelets in a MTS.
				- WEASEL + MUSE
					- Extract 'Words' over the MTS (and its derivatives)
					- Then do Logistic regression with words as input
				- ROCKET
					- Random convolution kernel transform
					- Uses convolutions to extract temporal patterns from each dimension in the MTS, and uses that as input for logistic regression.
			- Independent
				- Ensemble of classifiers per dimension.
		- ROCKET was the best
		- Clearly explain the added complexity of multiple dimensions for classification.
			- *"The core additional complexity for MTSC is that discriminatory features may be in the interactions between dimensions, not just in the autocorrelation within an individual series."*
		- Use MTS dataset archive of [Bagnall 18].

- [Shifaz 23] Elastic similarity and distance measures for multivariate time series
	- Survey
	- Notes
		- Proposes multivariate versions of 7 univariate (elastic) distance measures
			- Measures include multiple variants of
				- Euclidean distance
				- DTW
				- LCSS
				- Edit distance with real penalty
				- Move-Split-merge
				- Time warp edit
				- Elastic Ensemble
			- Discriminates between *dependent* and *independent* distance extensions
				- Independent is p-norm of dimension-wise distances (i.e. sum column-wise distances)
				- Dependent is p-norm of sample-wise distances (i.e. sum row-wise distances)
					- Significantly different from our definition
		- Evaluate through classification
			- No one measure outperforms the others
			- Argues for ensemble methods
		- Good survey structure
			- Good terminology
			- Summarize univariate and multivariate classification methods

- [Salarpour 18] An Empirical Comparison of Distance Measures for Multivariate Time Series Clustering
	- Survey
	- Notes
		- Compares 12 measures through clustering
			- Edit dista/neural_search/survey/
				- TWED
				- Move-Split-Merge
			- Geometry-based measures	
				- Hausdorff
				- Frechet
				- Symmetric Segment Path
			- Differentia-based measures
				- Derivative DTW
				- CIDTW
		- Evaluation shows that measures are equivalent, which is weird

- [Li 19] Feature Representation and Similarity Measure Based on Covariance Sequence for Multivariate Time Series
	- Notes
		- Discussed Dimensionality reduction methods to reduce the variable-dimensionality of MTS
		- Argues again using Euclidean on PCA components as they are produced from different transformations
			- Suggests method to solve this
		- Poorly written paper at bad conference

- [Shen 16] A Novel Similarity Measure Model for Multivariate Time Series Based on LMNN and DTW
	- Notes
		- Present a new MTS similarity measure based on metric learning and DTW
			- Learns the optimal projection for differentiating classes with DTW distance 
			- I.e., perfect mapping s.t. kNN classification under DTW-D is optimal.
		- Evaluation
			- Classification
			- Compare to other metric-learning distances, DTW-D and Euclidean distance

- [Banko 12] Correlation based dynamic time warping of multivariate time series
	- Idea
		- Combines PCA Similarity Factor with DTW
			- "The main goal of this paper is to construct a dissimilarity measure which deals with the changes in the correlation structure of the variables as 	ﬂexible as DTW allows."
		- Segments the MTS to account for evolving correlation patterns, e.g., due to process transitions
	- References/cites several case studies of PCA Similarity Factor
	- Poorly written paper and conference

- [Yu 19] A fast LSH-based similarity search method for multivariate time series
	- Similarity search
	- DTW-D
	- Fixed query length
	- Notes
		- Create LSH technique to index MTS on DTW -- hash multiple variants of a query point to query candidate MTS.
			- Hashing based on random projections DIMENSION-WISE, instead of classical time-wise mannor.
				-> This makes it **unusable for variying dimensions**.
			- Candidate if enough LSH bands have collisions.
			- Decide LSH-parameters based on pre- statistical analysis of dataset.
		- Good summary of univariate time series algorithm methods, and how they can(not) be extended to MTS.
		- Really well written paper, can borrow notation technique.

- [Yu 23] PSEUDo: Interactive Pattern Search in Multivariate Time Series with Locality-Sensitive Hashing and Relevance Feedback
		- Similarity search
		- Learned distance
		- Fixed query length
		- Notes
			- Similar to [Yu 19], index MTS based on random projections *dimension-wise*, instead of on time dimensions.
			- Do not prove why this way of indexing returns similar MTS, but fix this by asking feedback from user, and using that to learn similarity.
				- Effectively similarity learning.
				- Means that things have to be re-indexed **every loop**.

- [Bhaduri 10] Fast and Flexible Multivariate Time Series Subsequence Search
	- MTS Subsequence search
	- Ad-hoc matching of variables
	- Threshold query
	- Allows **fixed** time lags between variables (i.e., query and d should have the same lag among variables)
	- Two solutions
		- List based search
		- R*-tree based search
	- Notes
		- Very good related work, can be used as summary

## Univariate time series
- [Palpanas 20] Evolution of a Data Series Index
	- Survey of iSAX family of indexes
	- Notes
		- Addresses how iSAX index was extended considering challenges like bulk loading (iSAX2+), adaptive indexing (ADS), parallelism (ParIS), distribution (MESSI), and variable-length query answering (ULISSE).
		- Important: Coconut family of indexes is currently SOTA for both indexing and querying.
			- Uses sortable iSAX representations to build the index bottom-up in a balanced way.
			- Parallisable
			- Outperforms DSTree and ADS.
		- Future research directions include
			- Unified indexes combining features like progressive queries, approximate answers, and variable-length support.
			- Sequence Management System (i.e., a DBMS for time series data)

- [Shieh 08] iSAX: Indexing and Mining Terabyte sized time series
	- Similarity search (whole search)
	- Euclidean distance
	- kNN & Range search
	- **Only normalized data**
	- Notes
		- Indexing method based on SAX representation of time series
		- SAX representation;
			- PAA + discretization to symbols (i.e., bitstrings)
			- PAA of varying cardinality
			- Segments (x-axis breaks) are parameter, breakpoints (y-axis breaks) are pre-defined (!!)
		- iSAX index;
			- Hierarchical index where each node increases the cardinality (i.e., resolution) of one of the PAA segments.
			- Distance between node and index is lower-bounded through the PAA representations.
				- Can bound the distance between two representations of different cardinality by 'filling in' the missing values for the lower-cardinality representation using a 'best-case' approach.
			- Index is built by iteratively adding time series to the index, and splitting nodes when they reach a certain size.

- [Camerra 14] iSAX2+: Beyond one billion time series: indexing and mining very large time series collections with iSAX2
	- Similarity search (whole search)
	- Euclidean distance
	- kNN & Range search
	- **Only normalized data**
	- Notes
		- Adaptation to iSAX with faster indexing time
		- Optimizations:
			- Bulk loading algorithm that minimizes IOs
			- New split strategy to make tree more balanced; split the PAA segment that is most likely to result in a 50-50 split, rather than a round-robin strategy (as done in iSAX).

- [Linardi 18] ULISSE: ULtra compact Index for Variable-Length Similarity SEarch in Data Series
	- Subsequence search
	- Variable query length
	- Euclidean distance, claims to work on DTW as well
	- Normalized and unnormalized subsequences
	- kNN
	- Notes
		- Argue that indexing all possible subsequences of length \in [l_min, l_max] for all data points is incredibly inefficient.
		- Possible subsequences are
			1) Given a length l, there are n-l+1 possible shifts.
			2) There are l_max - l_min + 1 possible lengths.
		- Solution;
			1. Given a subsequence of length l_max, its PAA will also cover the PAA of subsets of that sequence down to length l_min -> only compute the PAA of subsequences of length l_max (solves problem 2).
			2. Capture many different shifts/offsets by computing *envelopes* over the PAA segments of the subsequences (solves problem 1).
			3. Then, index those envelopes and match to correct length ad-hoc.
		- How to enable normalization?
			- Observation 1. does not hold when considering normalized subsequences.
			- Solution; don't represent all smaller series by the PAA of the larger series (named *master series* in the paper), but instead store the PAA values of all (normalized) series of length l_min to l_max for each possible shift.
			- I.e., as a result, given a timeseries T, for each offset o \in [0, n-l_min], you get a set of PAA representations of size l_max - l_min + 1.
			- Envelopes per PAA segment are now derived over all possible subsequences rather than just the master series.


- [Rakthanmanon 12] Searching and Mining Trillions of Time Series Subsequences under Dynamic Time Warping
	- Pattern matching
	- DTW
	- Fixed query length
	- Notes
		- Claim that variable query length cannot be indexed
		- DO NOT do any indexing -- simply do sequential search over the DB with a large list of optimizations. 

- [Djebour 23] Variable-Size Segmentation for Time Series Representation
	- Similarity search
	- Euclidean distance
	- Notes
		- Provide an adaptive way of defining the segments before discretizing with (i)SAX, based on entropy or sum of absolute errors.
			- I.e., instead of fixed segment lengths, segments are smaller for periods of higher variance, and longer for stable periods.
		- Segment definition is *global* (i.e., dataset-wide though), so you assume that all ts have some common trend.


