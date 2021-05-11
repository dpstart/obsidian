---
topics: #gnn #graphnets 
---

The paper is an exploration of attention in graph neural networks. Moreover, the authors propose to use attention-based, self-supervised link-prediction as an auxiliary task when doing node classification.

Apparently, there is room to improve self-attention mechanism in graph neural networks, as for example GATs have typically showed performance improvements, but the improvements are not consistent across dataset, and it's even clear what graph attention actually learns.

Let's recall that the GAT's attention comes in the form of $a^T[Wh_i||Wh_j]$. In addition to this, the authors investigate dot-product attention, which is in the form $(Wh_i) * (Wh_j)$.

In the proposed self-supervision framework, the attention is based as to predict the presence/absence of edge between node pairs. In essece, it's an auxiliary link prediction task. Here, the authors explore 4 different attention mechanisms: the original one from GAT, dot product attention, scaled dot product, and a mix of dot product and GAT attention.

The final loss is the combination of the cross-entropy on the node labels (for the node classification task), and the self-supervised grapha ttention losses, plus an L2 penalty term.

Given this framework, the authors pose some research question, which I'll summarize here.

1. ** Does graph attention learn label agreement?** The authors here seem to think that, due to oversmoothing in GAT, if an edge exists between nodes with different labels, that it will be hard to distinguish them. Thus, they postulate that 