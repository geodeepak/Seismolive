### Dependencies

ObsPy has a number of dependencies, for the full and up-to-date list go the [[Dependencies Page|Dependencies]].

To install them, please follow the instructions for the operating system of your choice on this wiki. At the end of this page is a list with a couple of possibilities to install the dependencies on different Linux distributions.

ObsPy can only be installed from source if all dependencies have been installed or can be automatically installed during the installation procedure. Most Python dependencies (except NumPy) will be installed automatically during the installation of ObsPy if they are not available.

### On non-root Access

Many institutions don't grant root access to their computers. In that case there are a couple of possibilities:

* **Recommended**: The [[Anaconda|Installation-via-Anaconda]] installer works without root access and is very convenient. 
* Another possibility is to use the provided system Python and install packages on top of it with the help of so called [virtual environments](http://virtualenv.readthedocs.org).
* `pip` can (in most cases) install Python packages locally: `pip install --user PACKAGE`
* Install a complete Python distribution from source. This is for advanced users only but easy enough if you know what you are doing.

### Installing ObsPy

#### Stable Version

Recommended for normal users that do not intend on contributing code to ObsPy. If you have internet access on the machine:

```bash
$ pip install obspy
```

Otherwise download the latest tarball from [PyPi](https://pypi.python.org/pypi/obspy) and type:

```bash
$ pip install obspy-0.x.x.zip
```

##### Fortran Compiler Issues

Sometimes the installation routine attempts to use an incompatible Fortran compiler. f77 is for example not working on RHEL. We recommend to use gfortran as it has proven itsself to work almost everywhere. If you have multiple installed compilers you can force pip (or easy_install, ...) to use a certain compiler:

```bash
$ F77=gfortran pip install obspy
```

#### Development Version

This version is intended for developers or testers of the latest cutting-edge features of ObsPy. Normal users should always install a stable version.

The latest version of ObsPy is available on GitHub. Assuming git is installed you can get it with:

```bash
$ git clone git@github.com:obspy/obspy.git
```

Otherwise a [zip archive](https://github.com/obspy/obspy/archive/master.zip) of the latest development version is also available but not suitable if you plan on modifying ObsPy.

Once you acquired it you can install an editable version of ObsPy with:

```bash
$ cd obspy
$ pip install -e .
```

### Dependencies with Package Managers

*These are possibly not complete and/or up-to-date sets but they should get you started.*

 * Debian/Ubuntu
```bash
      sudo apt-get update
      sudo apt-get install python
      sudo apt-get install python-dev
      sudo apt-get install python-setuptools
      sudo apt-get install python-numpy
      sudo apt-get install python-numpy-dev
      sudo apt-get install python-scipy
      sudo apt-get install python-matplotlib
      sudo apt-get install python-lxml
      sudo apt-get install python-sqlalchemy
      sudo apt-get install python-suds
      sudo apt-get install gfortran
      sudo apt-get install libgfortran3
      sudo apt-get install ipython
```
 * openSUSE
```bash
      sudo zypper update
      sudo zypper install python
      sudo zypper install python-devel
      sudo zypper install python-setuptools
      sudo zypper install python-numpy
      sudo zypper install python-numpy-devel
      sudo zypper install python-scipy
      sudo zypper install python-matplotlib
      sudo zypper install python-matplotlib-tk
      sudo zypper install python-lxml
      sudo zypper install IPython
```
 * Fedora (see also http://vfamilyserver.org/blog/2013/01/installing-obspy-on-fedora-18/)
```bash
      yum install -y python
      yum install -y python-devel
      yum install -y python-setuptools
      yum install -y numpy
      yum install -y scipy
      yum install -y python-matplotlib
      yum install -y python-lxml
      yum install -y python-suds
      yum install -y python-sqlalchemy
      yum install -y gcc-gfortran
```