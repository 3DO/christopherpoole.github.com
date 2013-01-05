--- 
layout: minimal_publication
title: A CAD Interface for GEANT4
journal: Australasian Physical and Engineering Sciences in Medicine 
authors: CM Poole, I Cornelius, JV Trapp and CM Langton
file: Poole et al. - A CAD interface for GEANT4.pdf
introduction: Here we describe a technique that allows for CAD models to be directly loaded as geometry without the need for commercial software and intermediate file format conversion.
---

### Abstract
Often CAD models already exist for parts of a geometry being simulated using GEANT4.
Direct import of these CAD models into GEANT4 however,may not be possible and complex components may be diffcult to define via other means.
Solutions that allow for users to work around the limited support in the GEANT4 toolkit for loading predefined CAD geometries have been presented by others, however these solutions require intermediate file format conversion using commercial software.
Here within we describe a technique that allows for CAD models to be directly loaded as geometry without the need for commercial software and intermediate file format conversion.
Robustness of the interface was tested using a set of CAD models of various complexity; for the models used in testing, no import errors were reported and all geometry was found to be navigable by GEANT4.
![](/static/images/geant4_leaf.png)

### Downloads
- The software described in the manuscript is available from the CADMesh project page [here](http://code.google.com/p/cadmesh/).

### Citation

    @article{poole2012cad,
        author={Poole, C.M. and Cornelius, I. and Trapp, J.V. and Langton, C.M.},
        journal={Australasian Physical & Engineering Sciences in Medicine},
        title={A CAD interface for GEANT4},
        year={2012},
        volume={35},
        issue={3},
        pages={329-334},
    }

