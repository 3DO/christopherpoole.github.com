---
layout: minimal_publication 
title: Faster Monte Carlo Simulation of Radiotherapy Geometries 
school: Queensland University of Technology
journal: PhD Thesis by Published Papers
file: Poole - Faster Monte Carlo simulation of radiotherapy geometries.pdf
---

### Abstract

Using Monte Carlo simulation for radiotherapy dose calculation can provide more accurate results when compared to the analytical methods usually found in modern treatment planning systems, especially in regions with a high degree of inhomogeneity.
These more accurate results acquired using Monte Carlo simulation however, often require orders of magnitude more calculation time so as to attain high precision, thereby reducing its utility within the clinical environment.
This work aims to improve the utility of Monte Carlo simulation within the clinical environment by developing techniques which enable faster Monte Carlo simulation of radiotherapy geometries.
This is achieved principally through the use new high performance computing environments and simpler alternative, yet equivalent representations of complex geometries.

Firstly the use of cloud computing technology and it application to radiotherapy dose calculation is demonstrated.
As with other super-computer like environments, the time to complete a simulation decreases as \( 1/n \) with increasing \( n \) cloud based computers performing the calculation in parallel.
Unlike traditional super computer infrastructure however, there is no initial outlay of cost, only modest ongoing usage fees; the simulations described in the following are performed using this cloud computing technology.
The definition of geometry within the chosen Monte Carlo simulation environment - Geometry & Tracking 4 (GEANT4) in this case - is also addressed in this work.
At the simulation implementation level, a new computer aided design interface is presented for use with GEANT4 enabling direct coupling between manufactured parts and their equivalent in the simulation environment, which is of particular importance when defining linear accelerator treatment head geometry.
Further, a new technique for navigating tessellated or meshed geometries is described, allowing for up to 3 orders of magnitude performance improvement with the use of tetrahedral meshes in place of complex triangular surface meshes.
The technique has application in the definition of both mechanical parts in a geometry as well as patient geometry.

Static patient CT datasets like those found in typical radiotherapy treatment plans are often very large and present a significant performance penalty on a Monte Carlo simulation.
By extracting the regions of interest in a radiotherapy treatment plan, and representing them in a mesh based form similar to those used in computer aided design, the above mentioned optimisation techniques can be used so as to reduce the time required to navigation the patient geometry in the simulation environment.
Results presented in this work show that these equivalent yet much simplified patient geometry representations enable significant performance improvements over simulations that consider raw CT datasets alone.
Furthermore, this mesh based representation allows for direct manipulation of the geometry enabling motion augmentation for time dependant dose calculation for example.
Finally, an experimental dosimetry technique is described which allows the validation of time dependant Monte Carlo simulation, like the ones made possible by the afore mentioned patient geometry definition.
A bespoke organic plastic scintillator dose rate meter is embedded in a gel dosimeter thereby enabling simultaneous 3D dose distribution and dose rate measurement.

This work demonstrates the effectiveness of applying alternative and equivalent geometry definitions to complex geometries for the purposes of Monte Carlo simulation performance improvement.
Additionally, these alternative geometry definitions allow for manipulations to be performed on otherwise static and rigid geometry.

### Published Papers
- [A CAD interface for GEANT4](/A-CAD-interface-for-GEANT4)
- [Fast tessellated solid navigation in GEANT4](/Fast-tessellated-solid-navigation-in-GEANT4)
- [A hybrid radiation detector for simultaneous spatial and temporal dosimetry](/A-hybrid-radiation-detector-for-simultaneous-spatial-and-temporal-dosimetry)
- [Radiotherapy Monte Carlo simulation using cloud computing technology](/Radiotherapy-Monte-Carlo-simulation-using-cloud-computing-technology)

### Citation
    
    @phdthesis{
        author = {Poole, C. M.},
        title = {Faster Monte Carlo Simulation of Radiotherapy Geometries},
        school = {Queensland University of Technology},
        year = {2012}
    }

