Topics: #graphvae #graph-generartive

Graphs are hard to generate because of their discrete structure. Learning in a step-by-step, kinda autoregressive way requires discrete decisions, like for [[graphrnn]].

Solution: output a probabilistic, fully-connected graph of a predefined maximum size -> the existance of node/edges is a bernoulli variable. Nodes and edges attributes are multinomial variables.(I feel already like this is gonna be inefficient for big graphs). 

**Note**: continuos attributes are not considered. One could use gaussian RV.

Existence of nodes and edges is modeled as independent random variables.![[graphvae.png]]

Yes so the maximum size is very small, up to the order of tens.


Tensors used: 
* Adjacency matrix, containes node and edges probs.
* Edge attribute tensor, class probabilities for the edges.
* Node attribute matrix, class probabilities for nodes 


How do we do recontruction loss? It's hard for graphs, since they are permutation invariant -> Use approximate [[graph-matching]] algorithm.

