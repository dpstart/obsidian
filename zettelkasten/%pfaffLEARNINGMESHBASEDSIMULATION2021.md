---
topics: #graphnets #gnn #mesh
---

Here the authors introduce MeshGraphNets, a framework for learning mesh-based simulations using graph neural networks.
These simulations allow modelling of complex physical systems, such as cloth, fluid dynamics, and air flow.

The original simulation meshes are represented by a set of mesh nodes and edges. Each node is associated with a coordinate in mesh space, and with the value of the quantity that the system is modelling. Some systems, called *Lagrangian*, are also endowed with a 3D so-called *world-space* coordinate for the nodes.


The proposed model first  translates the mesh represantion into a multigraph, with the Lagrangian systems having additional"word"edges to enable interactions that might be local in 3D space but non-local in mesh space. These edges are created by spatial proximity.

In the graph, positional features are encoded in the edges. The initial features for both nodes and edges are then encoeed with simple MPLs, and that passed though several layers of message-passing.

![[Screenshot 2021-05-11 at 15.08.15.png]]


The latent node features for the nodes are finally translated by a decoder MLP into output features $p_i$. These features are interpreted as derivatives of the system quantitiy that we are modelling, so that they can be used to update the state of the system at the next timestep.

The resulting simulations, which can be seen [here](https://sites.google.com/view/meshgraphnets), tend o run 1-2 orders of magnitude faster that the simulations they were trained on.