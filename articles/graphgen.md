---
author:
- Daniele Paliotta
date: March 2021
title: Graph Generative Models
---

The aim of this post is to provide an overview of cthe current state-of-the-art in graph generative modeling, and to explain the most common models along with their strenghts and weaknesses. This post will be updated over time, as new models and techniques are developed for generating high fidelity graphs and for scaling these models wo work with bigger graphs.

# Challenges in Graph Generation

Generating graphs is a challenging task. Firstly, generating graphs is computationally expensive. For a graph of $n$ nodes, there exist $O(n^2)$ possible edges, which means that the number of edges can become huge.
Moreover, unlike the pixels of an image, the nodes in a graph don't follow a predefined order, meaning that they are *permutation-invariant.* As a consequence, an $n$-nodes graoh can be represented in $n!$ different ways, which makes it veeeery hard to capture graph distributions.  

Moreover , graphs are inherently *discrete* structures, where discrete decisions need to be made, for example, when chosing whether to add a new edge between two nodes. 

GraphRNN
========

The GraphRNN framework treats graph generation as a sequential
generation task. This means that the model autoregressively generates a
distribution over the next \"actions\", given the action sequence up to
the current timestep. In this case, the action is the addition of a node
or a edge. The model is hierarchical, with a node-level RNN and an
edge-level RNN. We can define a mapping $f_S$ from graphs to sequences,
where given a graph $G$ with $n$ nodes, and a node ordering $\pi$, the
mapping is defined as

$$S^{\pi} = f_S(G, \pi) = (S_1^{\pi}, ..., S_n^{\pi})$$ Here,
$S_i^{\pi}$ represents the edges between node $\pi(v_i)$ and the
previous nodes. For undirected graphs, it's possible to retrieve the
graph $G$ from this sequence representation. At inference time, it's
then possible to sample $S^{\pi}$ in order to generate a graph. Due to
the sequential nature of $S^\pi$, $p(S^{\pi})$ is modeled by an RNN.
Thus, we have

$$p(S^{\pi}) = \prod_{i=1}^n p(S_i^{\pi} \mid S_1^{\pi}, ..., S_{i-1}^{\pi})$$
and, by modeling this distribution using an RNN, we have

$$\begin{aligned}
    h_i = f_{trans}(h_{i-1}, S_{i-1}^{\pi}) \\
    \theta_i = f_{out}(h_i)
\end{aligned}$$ 

Here, $h_i$ is a vector that encodes the state of the
graph generated so far. $S_{i-1}^{\pi}$ is the adjacency vector for the
previously generated node $i-1$, and $\theta_i$ is the distribution over
the next node's adjacency vector. Note that, in general, $f_trans$ and
$f_out$ can be parametrized by arbitrary neural networks.

GraphRNN Variants
-----------------

The transition function $f_{trans}$ is typically parametrized by a Gated
Recurrent Unit (GRU) network. However, in the original paper, two
different versions of the model are explored, with the difference lying
in the representation of the output function $f_{out}$. The baseline
model, named GraphRNN-S, $f_{out}$ is modeled using a simple multi-layer
perceptron (MLP) with sigmoid activation that shares weights across
timesteps. Thus, the output $\theta_i$ of the model at each timestep is
a vector that represent the probabilties for the edges between node
$v_i$ and previous nodes. The edges are sampled independently according
to a multivariate Bernoulli distribution parametrized by $\theta_i$.

Conversely, the full GraphRNN model implements $f_{out}$ with an
additional RNN, further decomposing $p(S_i^{\pi} \mid S_{<i}^{\pi})$
into

$$p(S_i^{\pi} \mid S_{<i}^{\pi}) = \prod_{j=1}^{i-1}p(S_{i,j}^{\pi} \mid S_{i,<j}^{\pi}, S_{<i}^{\pi})$$
Here, $S_{i,j}^{\pi}$ is a single scalar representing the edge between
node $v_{i+1}$ and node $v_j$ under the ordering $\pi$. From a higher
level, in this setting we have a node-level RNN, represented by
$f_{trans}$. Each iteration of this model implicitly signals the
generation of a new node in the graph, while it's hidden state vector
carries general information about the graph. This hidden state is also
used to initialized the edge-level RNN, which is tasked with modeling
the probablities for the edges of the new node with all previous nodes.

BFS and tractability
--------------------

GraphRNN employs a clever trick in order to not only reduce the number
of sequences to consider when training the model, but also to reduce the
number of edge that need to be predicted at each timestep. The trick
consists in using a BFS ordering of the nodes in the graph. In this way,
instead of training the models on all possible permutations of the
graphs ($O(n!)$), it suffices to train on all possible BFS ordering,
which greatly reduces the number of computations. Moreover, when we
generates graph nodes in a breadth-first way, we know that each new node
can only connect to nodes in its BFS queue (i.e. nodes that are in the
previous \"layer\" of depth in the breadth first sequence). This greatly
reduces the number of edges that need to be generated for each new node.

GRAN
====

The GRAN model generates one block of nodes and associated edges at each
generation step. More specifically, the approach aims at optimizing the
likelihood of the lower triangular part of the adjacency matrix
$A^{\pi}$,

$$p(L^{\pi}) = \prod_{t=1}^T p(L_{b^t}^{\pi} \mid L_{b_1}^{\pi}, ... L_{b_{t-1}}^{\pi})$$

Here, $b_t$ is the set of row indices for the t-th block of $L^{\pi}$,
with a fixed block size B, and $T$ is the number of graph generation
steps (number of nodes divided by size of the block). At each generation
step, GRAN adds B new nodes to the already-generated subgraph, and adds
all possible edges among nodes in the block and with previously
generated nodes. This gives us an augmented graph, and the task at this
point is to only keep the right edges. In GRAN, the generation decision
are made using a GNN instead of a RNN, in order to avoid the long-term
bottleneck issues of RNNs.

Node representation
-------------------

At each generation step $t$, a simple linear mapping is used to compute
hidden representations for the nodes in the already-generated graph:

$$h_{b_i}^0 = WL_{b_i}^{\pi} + b, \forall i < t$$ Here, a block
$L_{b_i}^{\pi}$ is a vector in $\mathbb{R}^{BN}$ given by the
concatenation of the adjacency vector in each block, with B being the
block size, and N being the maximum number of nodes in the generated
graph (the vectors are zero padded for smaller graphs).

GNN with attentive messages
---------------------------

Starting from the initial node representation, the edges associated with
the current block are generated using a GNN. These edges include the
within-block connections as well as the edges linking nodes in the
current block with nodes in the previously generated blocks. Firstly,
the GNN is used to get updated node representations that encode
information about the structure of graph.

For the r-th round of message passing in the GNN, we compute message
vector $m^r_{ij} = f(h_i^r - h_j^r)$ and attention scores
$a_{ij}^r = Sigmoid(g(h_i^r - h_j^r))$, where $\tilde{h_i^r}$ is $h_i^r$
augmented with a B-dimensional binary mask $x_i$ indicating whether node
$i$ is a node from the previous blocks, or if it's part of the new
block. Finally, the update equation for the node representations is

$$h_i^{r+1} = GRU(h_i^r, \sum_{j \in N(i)} a_{ij}^r m_{ij}^r)$$

In short, the node representation is update using a GRU after
aggregating neighbor messages weighted by attention scores. Finally,
both $f$ and $g$ are implemented as multilayer perceptrons.

Output distribution
-------------------

After $R$ rounds of message passing, we get final node representations
for each node. Then, the probability of generating edges in the block
$L^{\pi}_{n_t}$ is modeled as such:

$$\begin{aligned}
        p(L_{b^t}^{\pi} \mid L_{b_1}^{\pi}, ... L_{b_{t-1}}^{\pi}) = \sum_{k=1}^{K} \alpha_k \prod_{i \in b_t} \prod_{1 \leq j \leq i} \theta_{k,i,j}, \\
        \alpha_1, ..., \alpha_K = \text{Softmax} \left(\sum_{i \in b_t. 1 \leq j \leq i} \text{MLP}_{\alpha}\left(h_i^R - h_j^R \right) \right), \\
        \theta_{1,i,j}...,\theta_{K,i,j} = \text{Sigmoid}\left( \text{MLP}_{\theta} \left( h_i^R - h_j^R \right)\right)
    \end{aligned}$$

Node ordering
-------------

You might recall that, with GraphRNN, a BFS ordering was chosen in order
to make the problem tractable. In GRAN, a family of canonical orderings
is chosen. Since each ordering encodes some structural bias about the
graph, in this way the model can consider multiple biases while still
avoiding to run in the intractability of all of the possible node
orderings. Mathematically, the goal is to maximize the log-likelihood
$\log p(G) = \log \sum_{\pi} p(G, \pi)$. The intractability of this is
due to the number of orderings $\pi$ being factorial in the graph size.
As a consequence, the authors limit themselves to a set of canical
orderings $Q$, thus maximizing the following lower bound of the
log-likelihood:

$$\log p(G) = \log \sum_{\pi \in \tilde{Q}} p(G, \pi) = \log \sum_{\pi \in Q}p(A^{\pi})$$
