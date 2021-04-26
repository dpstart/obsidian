---
topics: #graphnets #graphtransformers #heterographs
---

One limitation of most GNNs is that they assume the graph structure is fixed and homogeneous, since [[graph convolution]] is determined by the fixed graph structure -> a noisy graph with missing/spurious connections results in ineffective convolution with wrong neighbors on the graph.


Moreover, working with [[heterographs]] is not trivial.
Possibilities are:

* Ignore edge types and make the graph homogeneous.
* Manually design [[metapaths]] and go from hetero to homo with them.
	* Two-stage approach, requires handfcrafted metapaths for each problem. Accuracy can be dependent on choice of metapaths.

**Enter [[graph transformer networks]], which transforms a heterogeneous input graph into metapath graphs for each task and learn node representations on the graphs end-to-end.
**

Main challenge: metapaths can have arbitrary length and edge types.

## Method

Goal: generate new graph structures and learn node representations on the learned graph simultaneously.
The graph is not assumed to be given. GTN searches for new graph structures using multiple candidate adjacenty matrices to perform more effective graph convolutions and learn more powerful representations.


**Metapath**: a path on the heterogeneous graph connected with heterogeneous edges. It defines a composite relation between starting and ending nodes. The adj matrix of the metapath is the multiplications of the adjacenty matrices for each relation in the path.
An example of a metapath is the path AuthorPaperConference in a citation network.

The approach uses [[GCN]] learning nodes representations.

### Metapath generation
![[Screenshot 2021-04-26 at 10.19.39.png]]
1. Softly select two graph structures Q_1 and Q_2 from candidate adjacenty matrices.
	1. Apply 1x1 convolution to the tensor of adjaceny matrices. This reduces the dimensionality of the number of adj matrices. The filter is softmaxed so that the result is a weighted sum of the channels.
2. Learn a new graph structure by the composition of two relations. (multiplication of the adjancency matrices.)
	1. The resulting weighted combinations of the adjacenty matrices are combined via matrix multiplication to build the metapath. Each layers build a "two-degrees" metapath. Layers can be stacked for longer paths.
	2. Each additional layers increases the length of the path, but this is not always advisable. This, the identitry matrix is included in the set of adjacency matrices. In this way, the network can choose the length of the metapath up to L+1, with L being the number of stacked layers.

The 1x1 convolutions has C channels. this means that the result is actually still an adjacency tensor. Thus, graph convolution is applied using each of the matrices in the tensor, and the features are concatenated.
![[Screenshot 2021-04-26 at 10.19.28.png]]