# SIMPSON 

SIMPSON is a solid state NMR program [[1](#ref1),[2](#ref2)]. According to the
references [[1](#ref1)] this package was released under GPL, but the none of
repositories mentioned in the publications are currently accessible.
This [repository](https://github.com/hjjvandam/simpson) is a best effort attempt
to provide this code in a usable form. This repository was forked from
[Vosegaard's](https://github.com/vosegaard/simpson) but that
one is missing various pieces needed to build and test the code.

SIMMOL is a recommended companion program for setting calculations up [[3](#ref3),[4](#ref4)].

More information is available on the developer's web-site [[5](#ref5)].

# Installation

The code was extended to build and install it with [CMake](gitlab.kitware.com/cmake/cmake).
To build the code successfully a number of dependencies need to be installed:

* MPI

  The Message Passing Interface (MPI) infrastructure is needed to build the code 
  for distributed data parallel execution. Commonly used implementations are
  [OpenMPI](https://github.com/open-mpi/ompi), [MPICH](https://github.com/pmodels/mpich),
  and [MVAPICH](https://mvapich.cse.ohio-state.edu/). Of course if you are using
  a purpose built HPC system there will most likely be a vendor MPI implementation
  installed on the machine. In the latter case it is recommended to use the vendor
  MPI.

* CBLAS

  This library is a C translation of the Basic Linear Algebra Subroutines (BLAS).
  A reference implementation is included in the 
  [LAPACK](https://github.com/Reference-LAPACK/lapack) repository. The reference
  CBLAS implementation is designed with correctness prioritized over speed. 
  For performance reasons you will want to use optimized CBLAS implementations
  such as [OpenBLAS](https://github.com/xianyi/OpenBLAS), or
  [BLIS](https://github.com/flame/blis). In addition there are a number of 
  vendor optimized implementations of which the Intel MKL library is probably
  best known.

* LAPACKE

  This library provide a C API to the Linear Algebra PACKage (LAPACK). LAPACKE
  is included in the [LAPACK](https://github.com/Reference-LAPACK/lapack) repository.

* LAPACK

  As LAPACKE only provides a C API to [LAPACK](https://github.com/Reference-LAPACK/lapack)
  you still need to have LAPACK installed as well. 

* TCL

  The Tool Command Language ([TCL](https://github.com/tcltk/tcl)) is a programming
  language designed to drive software tools. Here it is used to drive the 
  SIMPSON package, i.e. it is the language that SIMPSON "input files" are written in.

* FFTW3

  The Fastest Fourier Transform in the West ([FFTW3](http://fftw.org/)) is, 
  unsurprisingly, a discrete Fourier transform library. It transforms quantities
  represented on a regular grid.

* NFFT

  The Nonequispaced Fast Fourier Transforms ([NFFT](https://github.com/NFFT/nfft))
  is a fast Fourier transform implementation that can exploit non-uniform grids.

After installing these packages you can generate the project files by running
```
   cmake --DCMAKE_PREFIX_PATH=<your-prefix-path> --DCMAKE_INSTALL_PREFIX=<your-prefix-path> -DTCL_INCLUDE_PATH=<directory-where-tcl.h-lives> -DTCL_LIBRARY=<path-to-libtclm.n.so> -H. -Bbuild
```
Here `your-prefix-path` is the prefix you used to install the dependencies that are
listed above. The `path-to-libtclm.n.so` is the full path of the TCL library you want
to link to. In this name `m` stands for the major version number and `n` for the minor
version number, i.e. if you want to use TCL 8.6 then `m=8` and `n=6` and you will be
linking to `<your-library-directory>/libtcl8.6.so`.
This command will generate your project files in the directory `./build`.
For a Linux/Unix system the project files will typically consist of makefiles. In 
that case running
```
   cd build
   make
   make install
```
should build and install SIMPSON.

## References

[<a name="ref1">1</a>] 
    Mads Bak, Jimmy T. Rasmussen, Niels Chr. Nielsen, "SIMPSON: A General Simulation
    Program for Solid-State NMR Spectroscopy", Journal of Magnetic Resonance (2000), Vol. 147, 
    pp. 296-330, doi: [10.1006/jmre.2000.2179](https://doi.org/10.1006/jmre.2000.2179).

[<a name="ref2">2</a>]
    Mads Bak, Jimmy T. Rasmussen, Niels Chr. Nielsen, "SIMPSON: A General Simulation
    Program for Solid-State NMR Spectroscopy", Journal of Magnetic Resonance (2011), Vol. 213, 
    pp. 366-400, doi: [10.1016/j.jmr.2011.09.008](https://doi.org/10.1016/j.jmr.2011.09.008).

[<a name="ref3">3</a>] 
    Mads Bak, Robert Schultz, Thomas Vosegaard, Niels Chr. Nielsen, "Specification and
    Visualization of Anisotropic Interaction Tensors in Polypeptides and Numerical
    Simulations in Biological Solid-State NMR", Journal of Magnetic Resonance (2002), Vol. 154,
    pp. 28-45, doi: [10.1006/jmre.2001.2454](https://doi.org/10.1006/jmre.2001.2454).

[<a name="ref4">4</a>] 
    Thomas Vosegaard, Anders Malmendal, Niels C. Nielsen, "The Flexibility of SIMPSON and 
    SIMMOL for Numerical Simulations in Solid- and Liquid-State NMR Spectroscopy",
    In: N. Müller, P.K. Madhu (eds) Current Developments in Solid State NMR Spectroscopy (2002),
    pp. 75-94, doi: [10.1007/978-3-7091-3715-4_5](https://doi.org/10.1007/978-3-7091-3715-4_5).

[<a name="ref5">5</a>] 
    ["Danish Center for Ultrahigh Field NMR Spectroscopy"](https://inano.au.dk/about/research-centers-and-projects/nmr/software/simpson)
