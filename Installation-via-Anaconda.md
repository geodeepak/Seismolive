[Anaconda](https://store.continuum.io/cshop/anaconda/) is a scientific Python installation shipping with essentially all needed packages. Install it according to the instructions on their homepage. Use Version 2.7 for ObsPy < 0.10, for later versions you can also use Python 3.4. Make sure the `conda` and `pip` commands point to the Anaconda installation.

**Anaconda works without root access!**

### C and Fortran compilers

To install ObsPy you need a C and a Fortran compiler (does not apply on Windows). On Linux use the package management system of your distribution, on OS X best use Homebrew or MacPorts. Package names are potentially `gcc` and `gfortran`.

### Install flake8 and basemap

These two packages are missing from the default Anaconda distribution.

```bash
$ conda install flake8 basemap
```

### Install obspy

```bash
$ pip install obspy
```

Run the test suite to assure everything works correctly.

```bash
$ obspy-runtests
```