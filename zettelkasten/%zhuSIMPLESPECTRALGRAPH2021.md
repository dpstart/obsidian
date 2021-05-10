---
topics: #gnn #graphnets 
---

Simple Spectral Graph Convolution

Graph convolution method to avoid oversmoothing. Here, the authors propose a pectral-based graph convolution layer, called Simple Spectral Graph Convolution (S2GC), which is based on the Markov Diffusion Kernel (MDK). The authors show that S2GC is capable of aggregating k-hop neighbourhood information without oversmoothing.

The initial proposed layer has the form

![[Screenshot 2021-05-10 at 14.16.45.png]]

with $T$ !add hat being the normalized adjacency matrix with added self-loops.!

However, this formulation can still incur in oversmoothing. Thus, the authors incorporate the possibility to interpolate between self-information and neighbor aggregation:
[[Screenshot 2021-05-10 at 14.18.26.png]]

The model is evaluated on the tasks of text and node classification, as well as node clustering and community detection. In general, the results are competitive with previous models, but this new formulation appears to be able to combat oversmoothing as the receptive field increases.