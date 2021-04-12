Topics: #graphnets 

One of the main issues with [[graphnet]] is the *bottleneck* issue: GNNs struggle to propagate information between distant nodes in the graph.  This paper introduces this issue as the *over-squashing* problem, since the network is not able to compress exponentially-growing information into fixed-sized vectors.

As a result, traditional GNNs perform poorly when the prediction task depends on long-range interaction. Moreover, it is shown that GNNs that absorm incoming edges equally, such as [[GCN]] and [[GIN]], are more subsceptible to this issue than [[GAT]] of [[GGNN]].

In most literature, GNNs were observed not to benefit from more than a few layers. The common explaantion for this is [[oversmoothing]]: node representations become indistinguishable when the number of layers increases. For long-range task, however, the paper hypothesizes that the explanation for the limited perfomance lies in [[oversquashing]].

In fact, the bottleneck issue here is very similar to the issue for seq2seq models, which typically suffer from a bottleneck issue in the decoder when attention is not used, since the receptive field of a ndoe grows linearly with the number of steps. 

For graph, the issue is strictly worse, since the number of nodes that fall in the receptive field of a target node grows exponentially with the number of message-passing steps.

The *problem radius* here is defined as a useful measure for defining the problem, and it correponds to the prioblem's required range of interaction. Clearly, this is typically unknown in advance, and is usually approximated empirially by tuning the number of layers.

When a prediciton problem as a problem radius $r$, the GNN muyst have as many layers $K$ as $r$. Howeverly, since the number of nodes in the receptive field grows exponentially with $K$, the network need to squash an exponentially-growing amount of intomation into a fixed-size vector, and so crucial messages might fail to reach thei distant destinations, and the model would learn only short-ranged signals fromt he training data and fail to generalize at test time.

The authors show the NEIGHBORMATCH task a toy task that exhibits the need for long-range interactions between nodes.


Examples of tasks that require long-range interaction appear in the prediciton fo chemical properties of molecules, which might depend on the combination of atoms that reside on opposite sides of the molecule.

On the toy dataset, it is shown that, even if enogh layers are built into the network, the models underfit when the number of layers increases. The GAT and GGNN fails later that GCN and GIN. this difference can be exaplined by the neighbor aggregation computation. GCN and GIN aggregate all neighbors before combining them with the target node's representation. Thus they must compress the information flowing from all the leaves into a single vector, and only afterwars interact with the target node's own representation. In contrast, GAT uses attention to weight incoming messages given tha target node's representation. At the last layer only, the tatget node can ignore the irrelevant incoming edge, and absorb only the relevant edge.


A question posed is: if all GNNs have reached low training accuracy, how do these GNN models usually fit the training data in public datasets of long-range problems? The hypothesis is that they overfiit short-range signals and artifacts from the training set, rather that learning the long-range information that was sqashed in the bottleneck. Thus, they generalize poorly at test time.


Simple solution: Adding a fully-adjacent (FA) layer in the last layer.
