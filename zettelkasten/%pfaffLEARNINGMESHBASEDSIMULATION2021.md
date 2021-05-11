---
topics: #graphnets #gnn #mesh
---

Here the authors introduce MeshGraphNets, a framework for learning mesh-based simulations using graph neural networks.
These simulations allow modelling of complex physical systems, such as cloth, fluid dynamics, and air flow.

The original simulation meshes are represented by a set of mesh nodes and edges. Each node is associated with a coordinate in mesh space, and with the value of the quantity that the system is modelling. Some systems, called *Lagrangian*, are also endowed with a 3D so-called *world-space* coordinate for the nodes.


The proposed model first  translates the mesh represantion into a multigraph, with the Lagrangian systems having additional edges 

![[Screenshot 2021-05-11 at 15.08.15.png]]