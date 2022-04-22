# Trilinos

[Trilinos](https://trilinos.org/) is a collection of over [50 self-contained packages](https://trilinos.github.io/packages.html). Configuring and building Trilinos with the right subset of packages is essential to building Peridigm in the next step.

A number of [Trilinos](https://trilinos.org/) packages are required by Peridigm. The Trilinos source code distribution includes the full set of Trilinos packages, each of which may be activated or deactivated using CMake build options, as described below. It is recommended that Makefiles be created by running `cmake` from the command line, as opposed to using the `ccmake` GUI.

Notable required packages from Trilinos are:
* SEACAS
* yaml-cpp

For additional details on obtaining, configuring, and building Trilinos, please visit the [Trilinos website](https://trilinos.github.io).

Below is an example CMake configuration script for Trilinos. Note that the option `-std=c++11` within the `CMAKE_CXX_FLAGS` list is specific to compilers that support C++11 features. A compiler that is C++11 compliant (e.g., GCC 4.7.2 or later) is required for recent versions of Trilinos.

```
#!/bin/bash

MYPREFIX="/home/scott/pkg/trilinos-13-0-1-install" # installation directory
MYSOURCE="/home/scott/pkg/Trilinos-trilinos-release-13-0-1" # trilinos source directory
MYMPI="/usr/lib/x86_64-linux-gnu/openmpi"
MYHDF5="/home/scott/pkg/hdf5-1.10.8-install"
MYNETCDF="/home/scott/pkg/netcdf-c-4.7.4-modified-install"

rm -f CMakeCache.txt

cmake -D CMAKE_INSTALL_PREFIX:PATH="${MYPREFIX}" \
-D MPI_BASE_DIR:PATH="${MYMPI}" \
-D CMAKE_CXX_FLAGS:STRING="-O2 -std=c++11 -pedantic -ftrapv -Wall -Wno-long-long" \
-D CMAKE_BUILD_TYPE:STRING=RELEASE \
-D Trilinos_WARNINGS_AS_ERRORS_FLAGS:STRING="" \
-D Trilinos_ENABLE_ALL_PACKAGES:BOOL=OFF \
-D Trilinos_ENABLE_Teuchos:BOOL=ON \
-D Trilinos_ENABLE_Shards:BOOL=ON \
-D Trilinos_ENABLE_Sacado:BOOL=ON \
-D Trilinos_ENABLE_Epetra:BOOL=ON \
-D Trilinos_ENABLE_EpetraExt:BOOL=ON \
-D Trilinos_ENABLE_Ifpack:BOOL=ON \
-D Trilinos_ENABLE_AztecOO:BOOL=ON \
-D Trilinos_ENABLE_Amesos:BOOL=ON \
-D Trilinos_ENABLE_Anasazi:BOOL=ON \
-D Trilinos_ENABLE_Belos:BOOL=ON \
-D Trilinos_ENABLE_ML:BOOL=ON \
-D Trilinos_ENABLE_Phalanx:BOOL=ON \
-D Trilinos_ENABLE_Intrepid:BOOL=ON \
-D Trilinos_ENABLE_NOX:BOOL=ON \
-D Trilinos_ENABLE_Stratimikos:BOOL=ON \
-D Trilinos_ENABLE_Thyra:BOOL=ON \
-D Trilinos_ENABLE_Rythmos:BOOL=ON \
-D Trilinos_ENABLE_MOOCHO:BOOL=ON \
-D Trilinos_ENABLE_TriKota:BOOL=OFF \
-D Trilinos_ENABLE_Stokhos:BOOL=ON \
-D Trilinos_ENABLE_Zoltan:BOOL=ON \
-D Trilinos_ENABLE_Piro:BOOL=ON \
-D Trilinos_ENABLE_Teko:BOOL=ON \
-D Trilinos_ENABLE_SEACASIoss:BOOL=ON \
-D Trilinos_ENABLE_SEACAS:BOOL=ON \
-D Trilinos_ENABLE_SEACASBlot:BOOL=OFF \
-D Trilinos_ENABLE_Pamgen:BOOL=ON \
-D Trilinos_ENABLE_EXAMPLES:BOOL=OFF \
-D Trilinos_ENABLE_TESTS:BOOL=ON \
-D TPL_ENABLE_HDF5:BOOL=ON \
-D HDF5_INCLUDE_DIRS:PATH="${MYHDF5}/include" \
-D HDF5_LIBRARY_DIRS:PATH="${MYHDF5}/lib" \
-D TPL_ENABLE_Netcdf:BOOL=ON \
-D TPL_Netcdf_Enables_Netcdf4:BOOL=ON \
-D Netcdf_INCLUDE_DIRS:PATH="${MYNETCDF}/include" \
-D Netcdf_LIBRARY_DIRS:PATH="${MYNETCDF}/lib" \
-D TPL_ENABLE_MPI:BOOL=ON \
-D TPL_ENABLE_BLAS:BOOL=ON \
-D TPL_ENABLE_LAPACK:BOOL=ON \
-D TPL_ENABLE_Boost:BOOL=ON \
-D TPL_ENABLE_Matio:BOOL=OFF \
-D TPL_ENABLE_X11:BOOL=OFF \
-D TPL_ENABLE_yaml-cpp:BOOL=ON \
-D CMAKE_VERBOSE_MAKEFILE:BOOL=OFF \
-D Trilinos_VERBOSE_CONFIGURE:BOOL=OFF \
${MYSOURCE}
```

Once Trilinos has been successfully configured, it can be compiled and installed as follows:
````
make -j 8
make install
````
