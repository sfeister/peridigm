# Modify, Build, and Install NetCDF

[NetCDF](https://github.com/Unidata/netcdf-c/releases), built with reference to parallel HDF5, is required by the Trilinos SEACAS package. Prior to compiling NetCDF, it is recommended that you modify the source code as described below to better support 
large-scale Peridigm simulations.

## Modify the NetCDF-C Source Code
After downloading the [NetCDF-C source code](https://github.com/Unidata/netcdf-c/releases), modify the following `#define` statements in the `netcdf.h` file. This file is located in the `include` directory of the NetCDF-C source code.  Change the values to match what is given below.

```bash
#define NC_MAX_DIMS 65536                                                                                                    
#define NC_MAX_ATTRS 8192                                                                                      
#define NC_MAX_VARS 524288                                                                                                    
#define NC_MAX_NAME 256                                                                                                      
#define NC_MAX_VAR_DIMS 8   
```

## Build the Modified Version of NetCDF

An example build process for [NetCDF](https://github.com/Unidata/netcdf-c/releases):

```bash
# Set environment variables for MPI compilers
export CC=mpicc
export CXX=mpicxx
export FC=mpif90
export F77=mpif77
```

```bash
# (As needed) Include paths to HDF5 and MPI Libraries (mpi.h, in particular)
# Below, replace the [...] with your own, correct paths.
export CFLAGS="-I/[...]/[...]/hdf5[...]/include -I/[...]/[...]/mpi[...]/include"
export LDFLAGS="-L/[...]/[...]/hdf5[...]/lib"
```

```bash
# Configure NetCDF
./configure --prefix=/usr/local/netcdf --enable-parallel--enable-netcdf-4 --disable-v2 --disable-fsync --disable-dap
```

```bash
# Make, test, and install NetCDF
make -j 8
make check
make install
```
