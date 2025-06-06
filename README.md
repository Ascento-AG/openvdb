### openvdb

This repository provides a wrapper ament package for the [OpenVDB](https://github.com/AcademySoftwareFoundation/openvdb) library.
Linking to this package is more convenient that compiling the source code, since this  requires a machine with more that 16GB of memory.

There is binary availables for different ubuntu distributios. Unfortunately these are not up to date, and for Ubuntu20.04LTS belong to a too old version.

These binaries have been built for arm and x64 architectures on a Linux machine.
The header files have been copied over together with the corresponding shared library. The static library has not been added here, since we often just used the shared libary and its size is prohibitive (>100Mb). The downside is that 
all dependencies must be met. 

See the first row (OpenVDB Core) in the [dependencies table](https://www.openvdb.org/documentation/doxygen/dependencies.html) to check all requirements.

🚨 **Important Notice**

This repository is not actively maintained and is intended for internal use only. While it wraps functionality from a third-party library licensed under the Apache License 2.0, it was not designed or developed with the intention of being a public open-source project.
We appreciate your interest, but please be aware that we do not currently plan to support external contributions or ongoing community maintenance.
