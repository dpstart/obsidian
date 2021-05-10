---
topics: #gnn #graphnets #paper
---




Framework for [[graph embedding]].

Embedding a graph typically requires some form of i) feature aggregation to produce node embeddings, followed by coarsening or ii) graph pooling, and a final iii) classification step.

Methods for graph classification fail to scale. For example, kernel methods need to compute pairwise similarities between the graphs embeddings.

This approach employs optimal transport methods to measure the dissimilarity between the graph. There already existed similar approaches but, by providing a direct linear map to compute the Wasserstein embedding, this method is linear in the number of graph

The first step  is to produce node embeddings. This is done via a non-parametric diffusion process, with a final concatenation of the node representations across layers.
The embeddings are then mapped to  the final Wasserstein embeddings, where the l2 distance between the resulting vectors approximates the 2-Wasserstein distance.
These final representation can that be used in any kind of downstream classifier or kernel methods.

With this approach, the authors achieve SOTA or competitive results on obgb-molhiv for molecular property prediction and on several TUD benchmark datasets.
