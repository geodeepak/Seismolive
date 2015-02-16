# Installation of Anaconda Python/ObsPy for MESS



Please go to http://continuum.io/downloads, download and run the Anaconda installer for Python 2.7:

[[images/anaconda.png]]

**Note:** On Mac/Linux, at the end of installation please confirm `"yes"` when asked if Anaconda Python should be prepended to your `PATH` environment variable.

### Fortran compiler

To install ObsPy you currently need a C and a Fortran compiler (does not apply on Windows*). A C compiler should already be available or, in the case of OSX, is a requirement for the package managers. On Linux use the package management system of your distribution, on OS X best use [Homebrew](http://brew.sh/) or [MacPorts](http://www.macports.org/). The package name is potentially `gfortran`, e.g.

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
*Anaconda for Windows ships with C and Fortran compilers, however compiling on a 64bit Windows may require a small patch by changing line no. 331 in ```AnacondaInstallDir\Lib\site-packages\numpy\distutils\fcompiler\gnu.py```
to ```pass #raise NotImplementedError("Only MS compiler supported with gfortran on win64")```.

### Additional packages

These two packages are missing from the default Anaconda distribution. `flake8` is needed for running the tests and `basemap` is an optional dependency for plotting data on maps.

```bash
$ conda install flake8 basemap
```


### Install ObsPy

After successful installation of the Anaconda Python Environment please install ObsPy:

**Windows**:
Click `Start` > `Programs` > `Anaconda` > `Anaconda Command Prompt`..

**Mac/Linux**:
Open a terminal..

Then type the following command:
```bash
easy_install obspy==0.9.2
```

After successful installation you should be able to start the IPython Notebook (from inside the Anaconda Command Prompt or Terminal)..

```bash
ipython notebook
```

The IPython Notebook should open in a new browser window or tab:

[[images/ipython_notebook_server.png]]

Click on `"New Notebook"`, type in the following commands and run the command cell (either click on arrow symbol or type CTRL-Enter).

[[images/ipython_notebook_import_obspy.png]]