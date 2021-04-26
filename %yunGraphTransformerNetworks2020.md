---
topics: #graphnets #graphtransformers 
---

One limitation of most GNNs is that they assume the graph structure is fixed and homogeneous, since graph convolution is determined by the fixed graph structure -> a noisi graph with missing/spurious connections results in ineffective convolution with wrong neighbors on the graph.


Moreover, working with [[heterographs]] is not trivials.
Possibilities are:

* Ignore edge types and make the graph homogeneous.
* Manually design [[metapaths]] and 
