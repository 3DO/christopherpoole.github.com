---
layout: minimal_post
title: Compiling and installing the GEANT4 Python bindings 
comments: True
introduction: Python bindings for GEANT4 are not compiled and installed out of the box. This is a quick rundown on setting everything up.
---

## Dependencies
* [GEANT4](http://geant4.org/), version 9.6 as of writing
* [Boost.Python](http://www.boost.org/doc/libs/1_53_0/libs/python/doc/)
* [Python](http://www.python.org/)

## Installation
Install GEANT4 in the [usual way](http://geant4.web.cern.ch/geant4/UserDocumentation/UsersGuides/InstallationGuide/html/ch02.html#sect.UnixBuildAndInstall) using `cmake`; I find using `cmake-gui` a bit easier for configuration:

    $> mkdir geant4.9.6_build
    $> cd geant4.9.6_build
    $> cmake-gui ../geant4.9.6

Select any options you feel you need to, click 'Configure' followed by 'Generate' and exit `cmake-gui`.

    $> make -j8
    $> sudo make install

Now we have to compile and install the actual Python bindings.
As far as I know this does not yet use `cmake` so we have to fall back to the old `gmake` method.

    $> export G4INSTALL=/path/to/geant4/installation/geant4.9.6
    $> cd $G4INSTALL/share/Geant4-9.6.0/geant4make
    $> source geant4make.sh

Before we go back to the GEANT4 source directory we have to create a symlink so the Python wrapping configure script finds the GEANT4 libraries (if you are on a 64bit machine):

    $> cd $G4INSTALL
    $> sudo ln -s lib lib64

Back in the GEANT4 source directory:

    $> cd environments/g4py
    $> ./configure linux64 --prefix=$G4INSTALL/python --with-g4install-dir=$G4INSTALL
    $> make -j8
    $> sudo make install
    $> export PYTHONPATH=$PYTHONPATH:$G4INSTALL/python/lib

That should do the trick:

    $> python -c "import Geant4, g4py"

    *************************************************************
     Geant4 version Name: geant4-09-06    (30-November-2012)
                          Copyright : Geant4 Collaboration
                          Reference : NIM A 506 (2003), 250-303
                                WWW : http://cern.ch/geant4
    *************************************************************
    
    Visualization Manager instantiating with verbosity "warnings (3)"...
    
    $>     

On where to go from here, have a look [g4lib](https://github.com/christopherpoole/g4lib), boiler plate for getting going with Python and GEANT4.
    
