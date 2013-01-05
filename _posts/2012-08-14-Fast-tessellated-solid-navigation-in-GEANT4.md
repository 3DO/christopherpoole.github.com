--- 
layout: minimal_publication
title: Fast tessellated solid Navigation in GEANT4
journal: IEEE Transations on Nuclear Science
authors: CM Poole, I Cornelius, JV Trapp and CM Langton
file: Poole et al. - Fast tessellated solid navigation in GEANT4.pdf
icon: /static/images/pelvis_tet.png
---

### Abstract
Navigation through tessellated solids in GEANT4 can degrade computational performance, especially if the tessellated solid is large and is comprised of many facets.
Redefining a tessellated solid as a mesh of tetrahedra is common in other computational techniques such as finite element analysis as computations need only consider local tetrahedrons rather than the tessellated solid as a whole.
Here within we describe a technique that allows for automatic tetrahedral meshing of tessellated solids in GEANT4 and the subsequent loading of these meshes as assembly volumes; loading nested tessellated solids and tetrahedral meshes is also examined.
As the technique makes the geometry suitable for automatic optimisation using smartvoxels, navigation through a simple tessellated volume has been found to be more than two orders of magnitude faster than that through the equivalent tessellated solid.
Speed increases of more than two orders of magnitude were also observed for a more complex tessellated solid with voids and concavities.
The technique was benchmarked for geometry load time, simulation run time and memory usage. Source code enabling the described functionality in GEANT4 has been made freely available on the Internet.

![](/static/images/pelvis_tet.png)

### Downloads
- The software described in the manuscript is available from the CADMesh project page [here](http://code.google.com/p/cadmesh/).

### Citation

    @article{poole2012fast, 
        author={Poole, C. M. and Cornelius, I. and Trapp, J. V. and Langton, C. M.}, 
        journal={Nuclear Science, IEEE Transactions on},
        title={Fast Tessellated Solid Navigation in GEANT4}, 
        year={2012}, 
        month={August}, 
        volume={59}, 
        number={4}, 
        pages={1695 -1701}, 
    }


