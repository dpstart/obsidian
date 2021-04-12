Topics: #graphnets 

Introduction of a memory layer for join [[graph-representation-learning]] and graph coarsening that consists of a multi-head array of memory keys and a convolution operator to aggrgeate soft cluster assignments from different heads.

The memory layer does not explicitly require connectivity informaiton and unloinke GNNs relies on the global informationr ather than local topology. "Hence it does not struggle with [[oversmoothing]]".

Related work is mainly [[memory-augmented-neural-networks]], which utilize external memory to access past experiences.