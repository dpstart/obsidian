topics: #graphnets #transformers #graphtransformers

### Why

Original [[transformer]] from NLP operates on fully-connected graph -> Does not leverage sparse connectivity -> performrs poorly when topology is important + does not leverage edge features if available.

### How


#### Attention

Again, in NLP, a sentence fed to a transformers if treated as a fully-connected graph. This makes sense as we can't know a-priori what are the relevant interactions betweens tokens, and thus we give the network full freedom to discover them.  Clearly, adding these many degrees of freedom makes the network computationally inefficient. More speficially, quadratic in the input sequence length for the vanilla transformer. For working with sentenced this might be ok, but it's definitely not when working with arbitrary graph, which might reach million/billions of nodes. 

The solution here is to only compute attention score for nodes that are connected by an edge. Attention is multi-head.


#### Positional encodings

In NLP transformers, positional encodings are required in order to add positional information to the input tokens.
For graphs, however, encoding node positions is not trivial, as there is no natural ordering of the nodes. The authors here employ the Laplacian eigenvectors as positional encodings, as they contain both structural and positional information about the nodes (nearby nodes have similar positional features and farther nodes have dissimilar features).

An ablation is also performed using WL positional encodings from GraphBERT, and Laplcian PE work better.

#### Layer Norm -> Batch Norm
Empirically, batch normalization works better that layer normalization for all datasets evaluated.

#### Incorporate edge features
In this framework, the incorporation of edge features is very straighfroward. The edge features are first projectred to fixed-dimensional vector via a linear projection, and they are then pointwise-multiplied with the attention scores in the self-attention layers. This seems to be enough to inject edge feature information in the model.


### Results
The model is evaluated on three datasets:

* **ZINC**: dataset for graph regression. It's a molecular dataset, and the task is to preict molecular properties. The dataset containes edge attributes.
* **PATTERN**: dataset for node classification. The dataset is generated using the Stochastic Block Model ([[SBM]]), with the goal to classify nodes into two communities. There are no edge features.
* **CLUSTER**: dataset for node classification. This dataset is also generated using the SBM model, with the task to assign nodes to clusters. No edge features. 

* The model works better than [[GCN]] and [[GAT]]. Note that GAT also uses multi-head attention.
* The model performs closely with [[gatedgcn]] on ZINC, which has edge features. 

### What's next

* Efficient training on large graphs
* Application fo heterogeneous graphs