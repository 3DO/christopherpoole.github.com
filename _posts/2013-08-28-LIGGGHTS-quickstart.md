---
layout: minimal_post
title: LIGGGHTS quickstart installation guide 
comments: True
introduction: LIGGGHTS is an enhanced version of LAMMPS (a molecular dynamics simulator) for discrete element method particle simulation.
---

If you want LAMMPS, install LIGGGHTS instead, it is considerably easier.
However, all of the required information is not in one place, it is scattered in random PDF files.

## Dependencies
* [LIGGGHTS](http://cfdem.dcs-computing.com/?q=OpenSourceDEM), [LAMMPS](http://lammps.sandia.gov/) comes with it
* [FFTW](http://www.fftw.org/)
* [OpenMPI](http://www.open-mpi.org/)

## Installation
FFTW and OpenMPI are probably in the packaging repository for your system, check there first, otherwise follow the instructions on the project pages.
Pleasingly the LIGGGHTS code and a mirror of the current version of LAMMPS is maintained on the [CFDEMproject](https://github.com/CFDEMproject) github page:

    $> git clone https://github.com/CFDEMproject/LIGGGHTS-PUBLIC LIGGGHTS
    $> cd LIGGGHTS/src
    $> make

This will list a vast array of preconfigured build targets and environments.
Here we choose the standard LAMMPS packages and exclude the ones that require special attention or are targeted for advanced use:

    $> make yes-standard no-poems no-reax no-meam no-kim no-gpu

If you are on a multi-core desktop or seek to run the code on a cluster, choose `openmpi`:

    $> make openmpi 

else you can build the serial/single process option:

    $> make serial

There is not an installation target so for the time being the official guide suggests a symbolic link:

    $> sudo ln -s /<absolute path to src>/LIGGGHTS/src/lmp_openmpi /usr/bin/liggghts

or for the serial version:
    
    $> sudo ln -s /<absolute path to src>/LIGGGHTS/src/lmp_serial /usr/bin/liggghts

## Running the examples
Both the LAMMPS and LIGGGHTS examples are very instructive.
The LAMMPS examples/tutorials can be found here:

    LIGGGHTS/examples/LAMMPS

likewise, the LIGGGHTS specific examples/tutorials can be found here:

    LIGGGHTS/examples/LIGGGHTS/Tutorials_public/

Running the LIGGGHTS `meshGran` example looks like this:

    $> cd LIGGGHTS/examples/LIGGGHTS/Tutorials_public/meshGran
    $> liggghts < in.meshGran

For both the `serial` and `openmpi` builds this will run on a single core/thread.
For multiple cores/threads `mpirun` needs to be invoked and the number of processors set explicitly:

    $> mpirun -n 4 liggghts < in.meshGran


