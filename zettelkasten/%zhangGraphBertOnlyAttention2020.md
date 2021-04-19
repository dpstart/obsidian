topics: #graphnets #transformers #graphtransformers #graphbert

### Why

Overreliance of graphnets on links leads to issues such as *suspended animation* and *oversmoothing*. Moreover, it impedes strong parallelization within the graph, which becomes increasingly important as graphs grow larger.

This model doesn't uses link information, also allowing unsupervised pre-training and fine-tuning/transfer to different graph datasets.


### How

#### Linkless subgraph batching

GraphBERT works on linkless subgraph. That is, subgraphs are linked from the input graphs, and links batched, with the edges being completely ignored by the model. This allows strong parallelization across the subgraphs.

For sampling the subgraph, a *top-k intimacy* approach is used. More specifically, an intimiacy matrix **S** is computed, measuring some kind of relationship between nodes. After that, given a starting nodes, other nodes are added to the subgraph based on the relative intimacy. In the top-k setting, the *k* nodes which exhibit the highest intimiacy with the initial node are sampled. 

The intimacy matrix is defined based on the [[pagerank]] algorithm. 


#### Input embeddings

The nodes in the sampled subgraphs here are ordered according to the intimacy value with the initial node. After this ios done, the input vectors are first embedded in a feature vecor. After that, three separate embeddings are fused into the represantion, in order to add positional and structural information about the graph, as the model is trained without any edge information and wouldn't otherwise be able to exploit the graph structure.

##### Weisfeiler-Lehman Absolute Role Embedding

The Weisfeiler-Lehman ([[WL]]) algorithms is a procedure originally developed to solve the [[graph isomorphism]] problem. That is, decide whether two graphs have the same structure. To do so, the algorithms assings label to nodes based on their structural role in the graph data.

For GraphBERT, the WL labels are computed for each nodes, and based on that, a positional embedding is computed based on the reciped from the original transformer:


#####  Intimacy based Relative Positional Embedding

The WL encoding captures global nodes structural information. Contrarily, the intimacy-based encoding allows to extract local information in the sampled subgraph based on the order of the node list (recall that nodes represantations are sorted by intimacy score, with the initial node being at position 0).

In order to compute the intimacy-based embeddings, the same formula for the WL embeddings is now applyed to a position index assigned to each node, which encode the "closeness" to the initial node.


##### Hop based Relative Distance Embedding
The hop-based encoding is dependent on the relative distance in hops between each node in the subgraph and the initial node. This is however computed on the initial graph.

#### Transformer encoder

The war vector embeddings, and the positional encodings, are summed to buld the inital node represantion. This is then fed to a standard transformer encoder.
The difference from the original transformer here is that we only want to computed the represantion for the central node in the subgraph. Thus, a final *Fusion* step will average the  represantion of all nodes , which defines the final state of the target nodes. 


#### Pre-Training
GraphBERT is pretrained with two tasks: node attribute reconstuction, and graph structure recovery.

##### Node Raw Attribute Reconstruction

Once we have the final represantion for the target nodes, this task simply consists in adding a fully-connected layer to reconstruct the original node attributes.

##### Graph Structure Recovery
This task is used to capture graph structure information. The idea is the following: given two learned node represantion, we can use the cosine similarity between the vectors to approximate some notion of similarity between the nodes. In this case, we want the cosine similarity between the represantion to be close to the intimacy score.


#### Fine-tuning/Transfer

##### Node classification
We can simply add a fully connected layer with a softmax on top, and fine-tune the entire network for the classification task.


### Results

The model is only evaluated on citation datasets. These are **Cora**, **Citeseer**, and **PubMed**.

* For node classification, GraphBERT outperforms most existing models on this datasets. It's also interesting that the performance doesn't degrade with deeper models. I guess this makes sense because it doesn't use message passing/signal diffusion.

* The model works best when all three encodings are added to the initial embeddings. Still, the positional embeddings don't give huge improvements over only using the raw input features.


### What's next
