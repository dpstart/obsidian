Topics: #graph-generative #atlas
Link: https://cds.cern.ch/record/2630433/files/ATL-SOFT-PUB-2018-001.pdf


## What

Use of [[deep-generative-models]]  ([[GAN]]s + [[VAE]]s) from simulationg showers in the  [[atlas]] detector. Goal: [[fast-calorimeter-simulation]].

The paper is the first applications of this models to fast simulation of the calorimeter response. The study focuses on showers for photons over a range of energies in the central region of the calorimeter.

## Why

Full simulation is slow and presents a bottleneck in the simuation pipeline. [[fast-calorimeter-simulation]] now relies on techniques based on thousands of indvidual parametrizations of the calorimeter response in the longitudinal and transverse direction given  a single particle's energy and pseudorapidity. 

## How

VAE: The objective function is augmented with additional terms related to the total energy deposition of a particle and the fraction of energy depositived in each calorimeter layer.

GAN: [[wgan]] is used.

## And?

Due to stochastic nature of shower development, no individual shower can be compared. Instead, the comparison is made between significant distrubution used during the event reconstruction and particle identification, such as total energy, energy deposited in each layer, and relative distribution of energies in the cells.

Note: the sum of simulated energies may evceed the trugh particle eneergy. Energy conservation is not taught to the model.

Results on energy deposits are good for most of the energy but bad in the tails.