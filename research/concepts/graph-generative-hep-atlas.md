Topics: #graph-generative 

Core of the problem: collision -> particles fly out -> they leave different marks in the detectors, some only deposit energy in the calorimeter. Multiple layers with complicated geometry.

Output of collision is a cone-shaped stuff.

each graph is particles in a layer. conditioned on initial energy and the angle.

Around 4k points for layer. 4-8 layers. each point has 3 dimensions: 2d position and energy.

deposits withing a single layer are correlated. there is also correlation cross-layer (less)


4k points for layer per layer is a lot. Can we reduce it? if we get only a percentile of the enrgy, we can reduce it a bit. Could also merge together close points with little energy.

inspiration from [[unet]]


how do you recontruct graph? matching?




learn information about "difference" between layers.
EVALUATION METRICS

