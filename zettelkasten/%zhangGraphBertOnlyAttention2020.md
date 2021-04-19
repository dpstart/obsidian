topics: #graphnets #transformers #graphtransformers #graphbert

### Why

Overreliance of graphnets on links leads to issues such as *suspended animation* and *oversmoothing*. Moreover, it impedes strong parallelization within the graph, which becomes increasingly important as graphs grow larger.

This model doesn't uses link information, also allowing unsupervised pre-training and fine-tuning/transfer to different graph datasets.


### How

#### Linkless subgraph batching

GraphBERT works on linkless subgraph. That is, subgraphs are linked from the input graphs, and links batched, with the edges being completely ignored by the model. This allows strong parallelization across the subgraphs.

For sampling the subgraph, a *top-k intimacy* approach is used. More specifically, an intimiacy matrix **S** is computed, measuring some kind of relationship between nodes. After that, given a starting nodes, other nodes are added to the subgraph based on the relative intimacy. In the top-k setting, the *k* nodes which exhibit the highest intimiacy with the initial node are sampled. 

The intimacy matrix is defined based on the [[pagerank]] algorithm. 


#### Input embeddings

The nodes in the sampled subgraphs here a
#### Transformer encoder


### Results


### What's next
