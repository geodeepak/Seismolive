[Anaconda](https://store.continuum.io/cshop/anaconda/) is a scientific Python installation shipping with essentially all needed packages. Install it according to the instructions on their homepage. Use Version 2.7 for ObsPy < 0.10, for later versions you can also use Python 3.4. Make sure the `conda` and `pip` commands point to the Anaconda installation.

### C and Fortran compilers

To install ObsPy you need a C and a Fortran compiler (does not apply on Windows). On Linux use the package management system of your distribution, on OS X best use Homebrew or MacPorts. Package names are potentially `gcc` and `gfortran`.

### Install some additional packages via Anaconda

```bash
$ conda install nose mock basemap flake8 sqlalchemy
```

### Install remaining packages via pip

```bash
$ pip install suds  # For ObsPy < 0.10
$ pip install suds-jurko  # For ObsPy >= 0.10
$ pip install obspy
```

Run the test suite to assure everything works correctly.

```bash
$ obspy-runtests
```