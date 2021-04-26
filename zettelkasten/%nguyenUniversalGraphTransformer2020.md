---
topics: #graphtransformers #graphnets

---

For each node, sample a number of neighbors and input to networks. At each training batch, the number of neighbors sampled is different. After that, it's a basi transformers.

To obtain the final representation, the vectors across the laters are concatenated.

To get the final graph embedding, all the final emeddings of the nodes are summed.


Differences from [[%dwivediGeneralizationTransformerNetworks2021]]:
-	no edge features, no sparse connecivity bias.
-	Layer norm instead of batch norm
-	concatenation across layers.
-	Tested on different datasets.

Differences from [[%zhangGraphBertOnlyAttention2020]]:

- Seems rather similar as the linkledd subgraph is fed
- No positional encoding, which is actually very important in graphbert.

Differences from [[%yunGraphTransformerNetworks2020]]
- That work was focused on heterographs.