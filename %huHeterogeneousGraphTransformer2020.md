---
topics: #graphtransformers #heterographs #graphnets 
---

This stuff can handle very big heterpgraph, even with a temporal component.


# WHY

Working with [[heterographs]] requires using metapaths, which were usually handcrafter and so require domain knowledge plus don't transfer to different graphs.
Secondly, classical methods assume that different types of nodes/edges share the same feature and representation space, or keep non-sharing weights for either node type or edge type alone.

Their, they don't work with dynamic graphs, and they don't scale to huge graphs.