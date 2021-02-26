Topics: #graphvae #graph-generartive

Graphs are hard to generate because of their discrete structure. Learning in a step-by-step, kinda autoregressive way requires discrete decisions. 

Solution: output a probabilistic, fully-connected graph of a predefined maximum size. (I feel already like this is gonna be inefficient for big graphs).

Existence of nodes and edges is modeled as independent random variables.