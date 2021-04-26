---
topics: #graphtransformers #heterographs #graphnets 
---

This stuff can handle very big heterpgraph, even with a temporal component.


# WHY

Working with [[heterographs]] requires using metapaths, which were usually handcrafter and so require domain knowledge plus don't transfer to different graphs.
Secondly, classical methods assume that different types of nodes/edges share the same feature and representation space, or keep non-sharing weights for either node type or edge type alone.

Their, they don't work with dynamic graphs, and they don't scale to huge graphs.



Metarelation: tuple containin:

* type of source node
* type of edge
* type of destination ndoe

# How

Given a sample heterosubgraph, all linked node pairs are extracted. The goal of the network is to aggregate information from source nodes to get a contextualized representation for the tarhet node. The process is decompoded into

* Heterogeneous mutual attention
	* Calculate mutual attention between source and target node. Each metarelation, however, has it's own set of projections for calculating the attention. 
	* Moreover, a weight matrix for the edge type is used in calculating the attention score
	* Moreover, a prior matrix is used to denote the general significance of each meta relation triplet.
* Heterogeneous message passing
	* Multi-head message by projectinf source nodes with linear projections according to the node type, and then multiply by a matrix that incorporate the edge dependency. Finally, all message heads are concatenated.
* Target-Specific aggregation
	* use attention vectors as the weight to average the messages. Then, apply final 
