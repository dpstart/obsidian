Topics: #graphnets 

One of the main issues with [[graphnet]] is the *bottleneck* issue: GNNs struggle to propagate information between distant nodes in the graph.  This paper introduces this issue as the *over-squashing* problem, since the network is not able to compress exponentially-growing information into fixed-sized vectors.

As a result, traditional GNNs perform poorly when the prediction task depends on long-range interaction. Moreover, it is shown that GNNs that absorm incoming edges equally, such as [[GCN]] and [[GIN]], are more subsceptible to this issue than [[GAT]] of [[GGNN]].

In most literature, GNNs were observed not to benefit from more than a few layers. The common explaantion for this is [[oversmoothing]]: node representations become indistinguishable when the number of layers increases. For long-range task, however, the paper hypothesizes that the explanation for the limited perfomance lies in [[oversquashing]].

In fact, the bottleneck issue here is very similar to the issue for seq2seq models, which typically suffer from a bottleneck issue in the decoder when attention is not used, since the receptive field of a ndoe grows linearly with the number of steps. 

For graph, the issue is strictly worse, since the number of nodes that fall in the receptive field of a target node grows exponentially with the number of message-passing steps.

The *problem radius* here is defined as a useful measure for defining the problem, and it correponds to the prioblem's required range of interaction. 

