---
topics: #graphnets #gnn #iclr2021
---


#  LEARNING PARAMETRISED GRAPH SHIFT OPERATORS

This paper provides and analysis for graph shift operators (GSO)* in graph learning, as well as a strategy for learning parametrized shift operators on graph. 

The parametrization is achieved in the following way:
![[Screenshot 2021-05-11 at 16.07.26.png]]
where $D_a$ is the degre matrix,  and $A_a$ is the adjacency matrix with self-loops.

Depending on the parameters values, one can retrieve commonly used graph shift operators, as shown in the following table:

[[Screenshot 2021-05-11 at 16.08.26.png]]

The authors then show how to include this new parametrized GSO in common GNN architectures.

The exposition continues with a brief theoretical analysis, where for example it is shown that the parametrized GSO has real eigenvalues and eigenvectors, making it feasible to use in exhisting spectral network analysis frameworks where this property is required. Some other bounds useful for numerical stability are derived in the paper.

