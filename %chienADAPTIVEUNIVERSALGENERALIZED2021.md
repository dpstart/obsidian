---
topics: #gnn #graphnets 
---

 

ADAPTIVE UNIVERSAL GENERALIZED PAGERANK GRAPH NEURAL NETWORK


The goal is to build a model that can adapt to both homophily and heterophily settings, and combat oversmoothing. The proposed approach incorporated the generalized page rank (GPR) algorithm in Graph Neural Networks (GNNs).

Simply put, the GPR algorithm assigns scores to nodes in a graph that are then used for clustering purposes.

 The GPR + GNN process is as follows:
![[Screenshot 2021-05-10 at 15.05.45.png]]

Here, the initial node representation is derived by a neural network $f_{\theta}$.
After that, the typical graph diffusion is performed using the symmetric adjacency matrix in order to get representations that aggregate information from 1 to k-hop neighborhoods.
To ge the final representations, the hidden representaions from 1 to k are summeds and weighted by values $\gamma_k$. These weights are trained jointly with $f_{\theta}$.

As the authors point out, the weights  $\gamma_k$ give th emodel  the ability to adaptively control the contribution of each propagation step and adjust it to the node label pattern, thus adapting to both homophily and etherophily settings. 

Moreover, oversmoothing should be combated by the model assigning less weight to large-step propagation steps whenever they are not beneficial in the training procedure.