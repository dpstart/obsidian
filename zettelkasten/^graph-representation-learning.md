Author: [[hamilton]]
Topics: [[graphs]] [[graphnets]]

# Traditional Approaces

## Graph Statistics and [[Kernel]] Methods (Node level)

Statistics/Features (from heurstics or domain knowledge) as input to ML classifier.

Typical statisics would be

#### Node degree 
$$deg_i = \sum_j A_{ij}$$

#### Node centrality 

such as [[eigenvector]] centrality, which also takes into account how important a node's neighbor are. This is defined recursively as being proportional to the average centrality of the neighbors:

$$e_i = \frac{1}{\lambda} \sum_j A_{ij}e_j$$

In vector form, with $e$ being the vector of node centralities, it can rewritten as

$$\lambda e = Ae$$ 
which is the standard eigenvector equation for the adjacency matrix. Morever, the vector that determines the centrality values is the one corresponding to the largest eigenvalues of $A$ (comed from wanting the centrality values to be positive)

How to interpret node centrality: likelihood that a node is visited on a random walk of infinite length on the graph.

#### Clustering coefficient

**proportions of closed triangles in a node's local neighborhood**

Calculated as: number of edges between neighbors of a node, divided by how many pairs of nodes are in the neighborhoo. A clustering coefficient of 1 implies that all of u's neighbors are also neighbors of each other.

So this measure is related to the number of triangles int he neighborhood. In general, one could count other motifs ot graphlets, and consider more complext structures such as cycles of particular length.


## Graph Level Features and Graph Kernels

#### Bag of nodes

Just aggregate node-level statistics. can miss important global properties of the graph.

#### The [[weisfeiler-lehman]] kernel

**iterative neighbor aggregation**
Idea: extract node-level features that contain more information that just their local ego graph.

Basic idea behing the WL algorithm:

1. Assign inital label $l^{(0)})(v)$ to each node. For most graphs, it cn be the node degree.
2. Iteratively assign a new label to each node by hashing the multiset of the current labels within the node's neighborhood.
3. After K iterations of re-labeling, each node labels summarizes he structure of it's K-hop neighborhood. It's then possible to compute histograms or other summary statistics over these labels as featue representation for the graph. The WL kernel is computed by measuring the difference between the resultant label sets for two graphs.


#### Graphlets and path-based methods

Identify a graph by the number of occurrences of a certain [[graphlet]]. Combinatorially difficult, but approximations exist. An alternative to enumerate all possible graphlets are path-based methods, where one examines the different kinds of *paths* that occur in a graph, like statistics on random ealks, shortest paths, etc.

### Neighborhood overlap detection

Statistical measures of neighborhood overlap between pairs of nodes, which tells us how much two nodes are related. One simple baseline is to simply count the number of neighbors that two nodes share.

Given a neighborhood overlap statistic, a strategy for edge prediction is to assume that the likelihood of an edge is proportional to the overlap.


#### Local overlap statistics

Functions of the number of common neighbors that two nodes share. Normalization is typically important, otherwise the measure would be biased towards predicting edges for nodes with high degrees.


#### Global overlap measures

Local approaches are limited as they only consider local neighborhoods. For example, count the number of paths of all lengths between a pair of nodes.


### [[Graph Laplacian]]

