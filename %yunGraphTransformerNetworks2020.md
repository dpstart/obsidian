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
