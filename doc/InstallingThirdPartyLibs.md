# Installing Third-Party Packages and Libraries

The build process for Peridigm requires a number of third-party tools and libraries, configured in their typical fashion. You can either build and install these libraries yourself, or install the development files using your operating system package manager.

---

* C/C++ compiler, such as [gcc](https://gcc.gnu.org/) or intel compilers
* [CMake](https://cmake.org/) (used when building Trilinos and Peridigm)
* MPI (both binaries and libraries), such as OpenMPI or MPICH (used when building HDF5, NetCDF, Trilinos, and Peridigm)
* [BLAS](http://www.netlib.org/blas/) (used when building Trilinos)
* [LAPACK](http://www.netlib.org/lapack/) (used when building Trilinos)
* [yaml-cpp](https://github.com/jbeder/yaml-cpp) (used when building Trilinos)
* [python2](https://www.python.org/) (used only for testing purposes at the end of the build process)

Once you have all these tools and libraries installed your system, make sure the binaries, shared libraries, and headers for these are all locatable in your default paths. (For example, the binaries are in your PATH, the includes are in your CPATH, and the libs are in your LD_LIBRARY_PATH).
