---
layout: minimal_post
title: Using distcc 
published: true 
comments: true
introduction: Distributed compilation is useful for the compilation of very large packages, distcc makes this reasonably straight forwards.
---

For Debian, on your local machine as well as the build nodes:

    sudo apt-get install distcc distcc-pump

On the build nodes:

    distccd --daemon --jobs <n procs> --allow <local machine ip>

Indicate to your local machine where to find the build nodes, IP addresses space separated with options comma separated.
If you are building C++ the `lzo` option is required:

    export DISTCC_HOSTS='<node1 ip>,cpp,lzo <node2 ip>,cpp,lzo'

If you are using CMake for example, you will want to set both `CMAKE_CXX_COMPILER` and `CMAKE_C_COMPILER` to `/usr/lib/distcc/c++` and `/usr/lib/distcc/cc` respectively before configuring your build.
Now you are ready for a distributed build:

    distcc-pump make -j<n procs across all nodes>
    OR
    pump make -j<n procs across all nodes>

## Issues
It seems the package in the Debian repository is not properly configured, and one may encounter this error or similar:

    __________Using distcc-pump from /usr/bin
    __________Using 1 distcc server in pump mode
    /usr/bin/distcc-pump: 1: /usr/bin/distcc-pump: /usr/bin/find_c_extension.sh: not found
    /usr/bin/python: can't open file '/usr/bin/include_server/include_server.py': [Errno 2] No such file or directory
    __________Expected a socket at '/tmp/distcc-pump.dsNg8o/socket'
    __________Could not start distcc-pump include server

To fix, in `/usr/bin/distcc-pump`, aroud line 43 set `include_server`:

    include_server='/usr/lib/pymodules/python2.7/include_server/include_server.py'

