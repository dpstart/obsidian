Topics: #graphnets #equivariance
Link: https://arxiv.org/abs/2102.09844v1


## What

[[EGNN]]s. Learn [[graphnets]] equivariant to rotations, translations, reflections and permutation. Supposed to not require expesive higher-order representations in intermediate leyers, and scaling to high-dimensional spaces.

## Why
Inductive bayes are needed. Inductive biases can exploit simmetries. E.g. translation equivariance in CNNs and permutation equivariance in GNNs.

Many problems also exhibit 3D translation and rotation simmetries, such as [[point-clouds]], 3D molecular structures and [[n-body]] particle simuations. Related work on this uses higher-order representations for intermediate network layers, and the computation requires expensive stuff. Addionally, often the data is restricted to scalar values and 3D vectors.

## How

The layer is called [[EGCL]].  Condider graph with feature node embeddings $h_i$ and also a n-dimensional coordinate $x_i$ associated with each of the nodes. The model will preserve equivariance to rotations and translations on these set of coordinates $x_i$, and will also preserve equivariance to permutation on the set of nodes V just like a normal GNN.

Consicely, $h^{l+1}, x^{l+1} = ECGL[h^l, x^l, edges]$.

## And?
SOTA results in modelling dynamical systems, [[representation-learning]] in [[graph-autoencoders]], prediction of molecular properties in [[QM9]] dataset.