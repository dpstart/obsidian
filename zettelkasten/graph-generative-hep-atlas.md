---
tags: #graph-generative #atlas
---

Core of the problem: collision -> particles fly out -> they leave different marks in the detectors, some only deposit energy in the calorimeter. Multiple layers with complicated geometry.

Output of collision is a cone-shaped stuff.

each graph is particles in a layer. conditioned on initial energy and the angle.

Around 4k points for layer. 4-8 layers. each point has 3 dimensions: 2d position and energy.

deposits withing a single layer are correlated. there is also correlation cross-layer (less)


4k points for layer per layer is a lot. Can we reduce it? if we get only a percentile of the enrgy, we can reduce it a bit. Could also merge together close points with little energy.

inspiration from [[unet]]


how do you recontruct graph? matching?




learn information about "difference" between layers.
EVALUATION METRICS??

---

[[johnny]]'s presentation about [[fast-sim]] methods in [[atlas]]


Prediction from simulation needs accurate modeling of the detector.

Pipeline is

Event generation -> **Detector Simulation** -> Digitisation -> Recontruction -> Analysis

Simulation ([[monte-carlo]]) takes most of the computation, and calorimeter is most of it.

[[geant4]] is used for the full simulation of the detector. Highly accurate. CPU intensive. Need fat simulation with accuracy trade-off.

[[atlas]] calorimeter  is crucial for recontruction of [[jets]] and other stuff. However, geometry is non-trivial, cell sizes vary,  and takes a long time to simulate full interactions in [[geant4]] (O(mins)).


First experiments from [[johnny]]:
* Train a network to approximate showeing in [[geant4]]
* Focus only on photons in a single slice of the calorimeter
* Train the network conditional on photon energy to reproduce shower
* Train on energy deposits in cells from G4 events, then generate new showers

More detailed papers notes at [[deep-generative-hep-atlas-paper]]


