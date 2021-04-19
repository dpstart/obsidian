topics: #graphnets #transformers #graphtransformers

### Why

Original [[transformer]] from NLP operates on fully-connected graph -> Does not leverage sparse connectivity -> performrs poorly when topology is important + does not leverage edge features if available.

### How


#### Attention

Again, in NLP, a sentence fed to a transformers if treated as a fully-connected graph. This makes sense as we can't know a-priori what are the relevant interactions betweens tokens, and thus we give the network full freedom to discover them.  Clearly, adding these many degrees of freedom makes the network computationally inefficient. More speficially, quadratic in the input sequence length for the vanilla transformer. For working with sentenced this might be ok, but it's definitely not when working with arbitrary graph, which might reach million/billions of nodes. 

The solution here is to only compute attention score for nodes that are connected by an edge. 


#### Positional encodings

In NLP transformers, positional encodings are required in order to add 


#### Layer Norm -> Batch Norm
#### Incorporate edge features

### Results

### What's next