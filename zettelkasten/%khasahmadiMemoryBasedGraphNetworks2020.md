Topics: #graphnets 

Introduction of a memory layer for join [[graph-representation-learning]] and graph coarsening that consists of a multi-head array of memory keys and a convolution operator to aggrgeate soft cluster assignments from different heads.

The memory layer does not explicitly require connectivity informaiton and unloinke GNNs relies on the global informationr ather than local topology. "Hence it does not struggle with [[oversmoothing]]".

Related work is mainly [[memory-augmented-neural-networks]], which utilize external memory to access past experiences.

[[graph-pooling]] can be defined in global of hierarchical manners.
In the first definiction, node representations are aggregated into a graph representation by a redout layer implement using some arithmetic operator such as sum or mean, or using set neural entworks. In the latter definiction, graphs are coarsened in each layer to capture the hierachical structure.

[[diffpool]] traubs two parallel GNNs to compute node representations and cluster assignments using a multi-ter loss including classification, link prediction, and entropy losses. [[mincut]] pool uses the minimum cut objective. [[topkpool]] computes node scores by learning projectionv ectors and dropping all the nodes expect the top scoring nodes. [[sagpool]] extends the topkpool by using graph convolution to take neighbor node feature into account.


### Method

#### Memory Layer


The memory layers is a parametric function that takes $n$ query vector of size $d$ and generates $n'$ query vector of size $d'$, with $n' < n$. Thus, the memory layer learng to jointly coarsen the input nodes, and transform thei features.