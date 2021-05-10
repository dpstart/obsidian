---
topics: #gnn #graphnets #paper
---




Framework for [[graph embedding]].

Embedding a graph typically requires some form of i) feature aggregation to produce node embeddings, followed coarsening or ii) graph pooling, and the final iii) classification step.

Methods for graph classification fail to scale. For example, kernel methods need to compute pairwise similarities between the graphs embeddings.

This approach employs optimal transport methods to measure the dissimilarity between the graph. There already existed similar approaches, but this one goes from quadratic to linear.
