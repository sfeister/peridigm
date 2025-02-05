# Install Standard Third-Party Tools and Libraries

The build process for Peridigm requires a number of third-party tools and libraries to be configured, built, and installed.

The tools and libraries below do not need to be customized in their builds - a standard build is sufficient. You can either build and install these tools and libraries yourself from source, or install them using your operating system's package manager.

---

Tools:
* C/C++ compiler, such as [gcc](https://gcc.gnu.org/) or Intel's [icc](https://www.intel.com/content/www/us/en/develop/documentation/cpp-compiler-developer-guide-and-reference/top.html)
* [CMake](https://cmake.org/) (used when building Trilinos and Peridigm)
* [python2](https://www.python.org/) (used only for testing purposes at the end of the build process)

Libraries:
* MPI, such as [OpenMPI](https://www.open-mpi.org/) or [MPICH](https://www.mpich.org/) (binaries and libraries are used when building HDF5, NetCDF, Trilinos, and Peridigm)
* [BLAS](http://www.netlib.org/blas/) (used when building Trilinos)
* [LAPACK](http://www.netlib.org/lapack/) (used when building Trilinos)
* [yaml-cpp](https://github.com/jbeder/yaml-cpp) (used when building Trilinos)

Make sure paths to the relevant binaries, shared libraries, and headers for these tools and libraries are locatable for the next build steps.
