# Similarity search on high-dimensional vectors - a literature review
This document covers works that focus on similarity search in high-dimensional vector spaces. 
While this also generalizes to time series data, the community hardly ever focuses on such data.
Rather, due to the popularity of neural networks and embeddings, the focus is on high-dimensional vectors and approximate nearest neighbor search (ANN).
For an overview of the works that combine both time series and vector search, see the respective literature review in the [both_search](/both_search/literature_review.md).

## Surveys
- [Matsui 23](/vector_search/graphbased_lecture/matsui23_lecture_summary.md): Theory and Applications of Graph-based Search
    - Lecture on graph-based similarity search algorithms like HNSW, NMSLIB, etc.
    - Part of a tutorial on neural search at CVPR 2023.
    - Summary
        - Problem: Graph-based algorithms solve Approximate Nearest Neighbor (ANN) search problems.
        - Levels of technology: Algorithms (e.g., HNSW), libraries (e.g., FAISS), services (i.e., VectorDB).
        - Algorithms: Old algorithms on the million-scale used either an index or compression followed by exhaustive search. New algorithms combine the two approaches. **Graph-based algorithm are current SOTA**.
        - Current state: SOTA has been stable for a few years: HNSW combined with compression through product quantization (PQ). Many algorithms are **in-memory**, but **disk-based** algorithms are getting more attention. While GPU support is available, it is not widely used.

- [Aumuller 23](/vector_search/survey/aumuller23_survey_summary.md): Survey on Vector Similarity Search Algorithms at billion-scale
    - Survey on vector similarity search algorithms
    - Part of a tutorial on neural search at CVPR 2023.
    - Summary
        - Benchmarking: Many algorithms are evaluated on the ANN-Benchmarks and in competitions at NeurIPS. Rules: 2h for index building + single-threaded search. Metrics: QPS over recall. 
        - Best algorithms: 
            - In-memory + high recall: graph-based algorithms. 
            - In-memory + low recall: inverted file-based indexes (IVF).
            - Disk-based + high recall: vector compression through product quantization (PQ) + graph-based algorithms.
            - Disk-based + low recall: inverted file-based indexes (IVF) + PQ.
        - Product quantization (PQ): Split the vector into subvectors and discretize each subvector by storing the id of the nearest centroid. I.e., k-means is run on each subvector space.

        


