---
topics: #gnn #graphnets #paper
---




Framework for [[graph embedding]].

Embedding a graph typically requires some form of i) feature aggregation to produce node embeddings, followed coarsening or ii) graph pooling, and the final iii) classification step.

Methods for graph classification fail to scale. For example, kernel methods need to compute pairwise similarities between the graphs embeddings.

This approach employs optimal transport methods to measure the dissimilarity between the graph. There already existed similar approaches but, by providing a direct linear map to compute the Wasserstein embedding, this method is linear int he number of graph

The first step in this method is to produce node embeddings. This is done via a non-parametric diffusion process, with a final concatenation of the node representations across layers.