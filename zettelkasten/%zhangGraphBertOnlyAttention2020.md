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

The nodes in the sampled subgraphs here are ordered according to the intimacy value with the initial node. After this ios done, the input vectors are first embedded in a feature vecor. After that, three separate embeddings are fused into the represantion, in order to add positional and structural information about the graph, as the model is trained without any edge information and wouldn't otherwise be able to exploit the graph structure.

##### Weisfeiler-Lehman Absolute Role Embedding

The Weisfeiler-Lehman ([[WL]]) algorithms is a procedure originally developed to solve the [[graph isomorphism]] problem. That is, decide whether two graphs have the same structure. To do so, the algorithms assings label to nodes based on their structural role in the graph data.

For GraphBERT, the WL labels are computed for each nodes, and based on that, a positional embedding is computed based on the reciped from the original transformer:


#####  Intimacy based Relative Positional Embedding

The WL encoding captures global nodes structural information. Contrarily, the intimacy-based encoding allows to extract local information in the sampled subgraph based on the order of the node list (recall that nodes represantions are sorted by intimacy score.)
##### Hop based Relative Distance Embedding

#### Transformer encoder


### Results


### What's next
