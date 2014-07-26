[Anaconda](https://store.continuum.io/cshop/anaconda/) (you can also use [Miniconda](http://conda.pydata.org/miniconda.html) for a smaller footprint) is a scientific Python installation shipping with essentially all needed packages. Install it according to the instructions on their homepage. Use Version 2.7 for ObsPy < 0.10, for later versions you can also use Python 3.4. Make sure the `conda` and `pip` commands point to the Anaconda installation.

**Anaconda works on most systems without root access!**

### Fortran compiler

To install ObsPy you currently need a C and a Fortran compiler (does not apply on Windows). A C compiler should already be available or, in the case of OSX, is a requirement for the package managers. On Linux use the package management system of your distribution, on OS X best use [Homebrew](http://brew.sh/) or [MacPorts](http://www.macports.org/). The package name is potentially `gfortran`, e.g.

```bash
# Debian and Ubuntu (derivates)
$ sudo apt-get install gfortran

# CentOS/RedHat/Fedora
$ sudo yum install gcc-gfortran

# (Open)SUSE
$ sudo zypper install gcc-fortran

# OSX with Homebrew
$ brew install gcc
```


### Install obspy

```bash
$ pip install obspy
```


### Additional packages

These two packages are missing from the default Anaconda distribution. `flake8` is needed for running the tests and `basemap` is an optional dependency for plotting data on maps.

```bash
$ conda install flake8 basemap
```


### Test your Installation

Run the test suite to assure everything works correctly.

```bash
$ obspy-runtests
```