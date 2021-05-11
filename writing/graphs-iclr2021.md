The field of geometric deep learning is booming, there's no way around it. And graph neural networks are the rockstars, sitting in the driver seat.

And graphs were clearly at the center of a lot of attention at ICLR 2021.
Not only thanks to [Michael Bronstein's amazing keynote speech on geometric deep learning](https://iclr.cc/virtual/2021/invited-talk/3717), but also thanks to a number of interesting papers ranging from theory, methods and applications.

In this post,  I will try to summarize what these papers were mainly about, what seem to be the current trends, and what we can expect from the future.


## Methods

### WASSERSTEIN EMBEDDING FOR GRAPH LEARNING

This paper is all about the development of a new framework for embedding entire graphs.
Graph embedding methods typically require several steps namely i) feature aggregation to produce node embeddings, following by some type of ii) graph coarsening or pooling, and a final iii) classification step.

However, current methods for grah classification fail to scale with the number of graphs in the dataset. As an example, kernel methods typically need to compute pairwise similarities between the graphs, which is computationally heavy when the dataset is large.

The approach proposed in the paper employs optimal transport methods to measure the dissimilarity between the graphs. Similar approaches already exist, but the authors here derive a direct linar map to compute the embedding, making the algorithm linear in the number of input graphs.

The first step in the process here is to produce the node embeddings, which is done via a simple non-parametric diffusion process. After that, the node representations across layers are concatenated to get the final representation.
These representations are then mapped to 

