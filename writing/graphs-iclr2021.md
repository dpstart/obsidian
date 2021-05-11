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
These representations are then mapped to the Wasserstein embeddings, with the idea that the L2 distance between the resulting vectors approximates the 2-Wasserstein distance.

These final representation can that be used in any kind of downstream classifier or kernel methods.

With this approach, the authors achieve SOTA or competitive results on obgb-molhiv for molecular property prediction and on several TUD benchmark datasets

### Simple Spectral Graph Convolution

Another graph convolution method to combat oversmoothing, derived from spectral principles.

Here, the authors propose a pectral-based graph convolution layer, called Simple Spectral Graph Convolution (S2GC), which is based on the Markov Diffusion Kernel (MDK). The authors show that S2GC is capable of aggregating k-hop neighbourhood information without oversmoothing.

The initial proposed layer has the form
![[Screenshot 2021-05-10 at 14.16.45.png]]

with $\hat{T}$ being the normalized adjacency matrix with added self-loops.

However, this formulation can still incur in oversmoothing. Thus, the authors incorporate the possibility to interpolate between self-information and neighbor aggregation:
[[Screenshot 2021-05-10 at 14.18.26.png]]

The model is evaluated on the tasks of text and node classification, as well as node clustering and community detection. In general, the results are competitive with previous models, but this new formulation appears to be able to combat oversmoothing as the receptive field increases.

It is also showed in the paper that  the proposed filter, by design, will give the highest weight to the closest neighborhood of a node, and that the model can incorporate larger receptive fields without undermining contributions of smaller receptive fields, which might be the reason why this model doesn't suffer from oversmoothing.

### ADAPTIVE UNIVERSAL GENERALIZED PAGERANK GRAPH NEURAL NETWORK


The goal here is to build a model that can adapt to both homophily and heterophily settings, and combat oversmoothing. The proposed approach incorporated the generalized page rank (GPR) algorithm in Graph Neural Networks (GNNs)

Simply put, the GPR algorithm assigns scores to nodes in a graph that are then used for clustering purposes.

 The GPR + GNN process is as follows:
![[Screenshot 2021-05-10 at 15.05.45.png]]

Here, the initial node representation is derived by a neural network $f_{\theta}$.
After that, the typical graph diffusion is performed using the symmetric adjacency matrix in order to get representations that aggregate information from 1 to k-hop neighborhoods.
To ge the final representations, the hidden representaions from 1 to k are summeds and weighted by values $\gamma_k$. These weights are trained jointly with $f_{\theta}$.

As the authors point out, the weights  $\gamma_k$ give th emodel  the ability to adaptively control the contribution of each propagation step and adjust it to the node label pattern, thus adapting to both homophily and etherophily settings. 

Moreover, oversmoothing should be combated by the model assigning less weight to large-step propagation steps whenever they are not beneficial in the training procedure.


### HOW TO FIND YOUR FRIENDLY NEIGHBORHOOD: GRAPH ATTENTION DESIGN WITH SELF-SUPERVISION

The paper is an exploration of attention in graph neural networks. Moreover, the authors propose to use attention-based, self-supervised link-prediction as an auxiliary task when doing node classification.

Apparently, there is room to improve self-attention mechanism in graph neural networks, as for example GATs have typically showed performance improvements, but the improvements are not consistent across dataset, and it's even clear what graph attention actually learns.

Let's recall that the GAT's attention comes in the form of $a^T[Wh_i||Wh_j]$. In addition to this, the authors investigate dot-product attention, which is in the form $(Wh_i) * (Wh_j)$.

In the proposed self-supervision framework, the attention is based as to predict the presence/absence of edge between node pairs. In essece, it's an auxiliary link prediction task. Here, the authors explore 4 different attention mechanisms: the original one from GAT, dot product attention, scaled dot product, and a mix of dot product and GAT attention.

The final loss is the combination of the cross-entropy on the node labels (for the node classification task), and the self-supervised grapha ttention losses, plus an L2 penalty term.

Given this framework, the authors pose some research question, which I'll summarize here.

1. **Does graph attention learn label agreement?** The authors here seem to think that, due to oversmoothing in GAT, if an edge exists between nodes with different labels, that it will be hard to distinguish them. Thus, they postulate that ideal attention should give all the weights to label-agreed neighbors. In their experiments, they show that GAT attention learns label-agreement better that dot-product.
2. **Is graph attention predictive for edge presence?** On the link predictiont ask, dot-product attention consistently outperforms GAT attention. 
3. **Which graph attention should we use for given graphs?** The hypothesis here is that different attention mechanisms have will have different abilities to model graphs under various homophily and average degree. Here, the best performing model in low-homphily settings employs scaled dot-product attention with self-supervision, showing that self-supervision can be useful. However, when homphily and average degree are high enough, there is no difference in performance between all the models, including a vanilla GCN.

All of the experiments done so fare were done using synthetic dataset, as they allow for controlling several graph properties. However, the authors show that the design choice generalize to many real-world datasets.

