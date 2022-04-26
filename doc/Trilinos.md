# Configure, Build, and Install Trilinos

## Overview
[Trilinos](https://trilinos.org/) is a collection of over [50 self-contained packages](https://trilinos.github.io/packages.html). Configuring and building Trilinos with the right subset of packages is essential to building Peridigm in the next step.

A number of [Trilinos](https://trilinos.org/) packages are required by Peridigm. The Trilinos source code distribution includes the full set of Trilinos packages, each of which may be activated or deactivated using CMake build options, as described below. It is recommended that Makefiles be created by running `cmake` from the command line, as opposed to using the `ccmake` GUI.

For additional details on obtaining, configuring, and building Trilinos, please visit the [Trilinos website](https://trilinos.github.io).

## Minimal Trilinos Requirements for Peridigm
Here are all the required Trilinos packages needed for Peridigm:
* Belos
* Epetra
* Epetra
* Ifpack
* NOX
* Sacado
* SEACAS
* SEACASIoss
* Teuchos

The most notable required package above is SEACAS, which is used for input/output in the Exodus file format. 

And here are required TPL elements:
* HDF5
* Netcdf
* MPI
* BLAS
* LAPACK
* yaml-cpp

## Example CMake Configuration of Trilinos
Below is an example CMake configuration script for Trilinos, which **enables everything outlined above** and little else. Note that the option `-std=c++11` within the `CMAKE_CXX_FLAGS` list is specific to compilers that support C++11 features. A compiler that is C++11 compliant (e.g., GCC 4.7.2 or later) is required for recent versions of Trilinos.

```bash
#!/bin/bash

# Replace the following with the correct paths for your system
MYPREFIX="/usr/local/trilinos" # installation directory
MYSOURCE="/home/user1/Trilinos-release" # downloaded trilinos source code directory
MYMPI="/usr/local/mpi"
MYHDF5="/usr/local/HDF5"
MYNETCDF="/usr/local/netcdf"

rm -f CMakeCache.txt

cmake -D CMAKE_INSTALL_PREFIX:PATH="${MYPREFIX}" \
-D CMAKE_CXX_FLAGS:STRING="-O2 -std=c++11 -pedantic -ftrapv -Wall -Wno-long-long" \
-D CMAKE_BUILD_TYPE:STRING=RELEASE \
-D CMAKE_VERBOSE_MAKEFILE:BOOL=OFF \
-D Trilinos_WARNINGS_AS_ERRORS_FLAGS:STRING="" \
-D Trilinos_ENABLE_ALL_PACKAGES:BOOL=OFF \
-D Trilinos_ENABLE_Belos:BOOL=ON \
-D Trilinos_ENABLE_Epetra:BOOL=ON \
-D Trilinos_ENABLE_EpetraExt:BOOL=ON \
-D Trilinos_ENABLE_Ifpack:BOOL=ON \
-D Trilinos_ENABLE_NOX:BOOL=ON \
-D Trilinos_ENABLE_Sacado:BOOL=ON \
-D Trilinos_ENABLE_SEACAS:BOOL=ON \
-D Trilinos_ENABLE_SEACASIoss:BOOL=ON \
-D Trilinos_ENABLE_SEACASBlot:BOOL=OFF \
-D Trilinos_ENABLE_Teuchos:BOOL=ON \
-D Trilinos_ENABLE_EXAMPLES:BOOL=OFF \
-D Trilinos_ENABLE_TESTS:BOOL=ON \
-D Trilinos_VERBOSE_CONFIGURE:BOOL=OFF \
-D TPL_ENABLE_X11:BOOL=OFF \
-D TPL_ENABLE_Matio:BOOL=OFF \
-D TPL_ENABLE_HDF5:BOOL=ON \
-D HDF5_INCLUDE_DIRS:PATH="${MYHDF5}/include" \
-D HDF5_LIBRARY_DIRS:PATH="${MYHDF5}/lib" \
-D TPL_ENABLE_Netcdf:BOOL=ON \
-D Netcdf_INCLUDE_DIRS:PATH="${MYNETCDF}/include" \
-D Netcdf_LIBRARY_DIRS:PATH="${MYNETCDF}/lib" \
-D TPL_ENABLE_MPI:BOOL=ON \
-D MPI_BASE_DIR:PATH="${MYMPI}" \
-D TPL_ENABLE_BLAS:BOOL=ON \
-D TPL_ENABLE_LAPACK:BOOL=ON \
-D TPL_ENABLE_yaml-cpp:BOOL=ON \
${MYSOURCE}
```

## Example Build and Install of Trilinos
Once Trilinos has been successfully configured, it can be compiled and installed as follows:
````
make -j 8
make install
````
