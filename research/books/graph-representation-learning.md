Author: [[hamilton]]
Topics: [[graphs]] [[graphnets]]

# Traditional Approaces

## Graph Statistics and [[Kernel]] Methods

Statistics/Features (from heurstics or domain knowledge) as input to ML classifier.

Typical statisics would be

#### Node degree 
$$deg_i = \sum_j A_{ij}$$

#### Node centrality 

such as [[eigenvector]] centrality, which also takes into account how important a node's neighbor are. This is defined recursively as being proportional to the average centrality of the neighbors:

$$e_i = \frac{1}{\lambda} \sum_j A_{ij}e_j$$

In vector form, with $e$ being the vector of node centralities, it can rewritten as

$$\lambda e = Ae$$ 
which is the standard eigenvector equation for the adjacency matrix. Morever, the vector that determines the centrality values is the one corresponding to the largest eigenvalues of $A$.

How to interpret node centrality: likelihood that a node is visited on a random walk of infinite length on the graph.

#### Clustering coefficient

