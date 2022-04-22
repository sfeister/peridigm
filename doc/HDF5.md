## Install Parallel HDF5
[HDF5](https://www.hdfgroup.org/solutions/hdf5) libraries are required by NetCDF and the SEACAS Trilinos package. HDF5 should be configured with the `--enable-parallel` option.

If you choose to use a package manager to install the HDF5 libraries rather than building from source, make sure you install **parallel HDF5** - not the more typical serial HDF5.

An example build process for [HDF5](https://www.hdfgroup.org/solutions/hdf5):

````
# Set environment variables for MPI compilers
export CC=mpicc
export CXX=mpicxx
export FC=mpif90
export F77=mpif77

# Configure HDF5
./configure --prefix=/usr/local/HDF5 --enable-parallel

# Make and install HDF5
make -j 4
make install
````
