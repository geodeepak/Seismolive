[Homebrew](http://brew.sh/) is a package manager for OS X in the vein of APT (apt-get) on Debian operating systems. It works by providing recipes to install software from source. The advantage is that it is usually very up-to-date and simply works.

To install Homebrew follow the installation instructions on their homepage (make sure the [listed requirements](https://github.com/Homebrew/homebrew/wiki/Installation#requirements) are fulfilled).

### Installing Python, the Scientific Python Stack and other required packages

The `gcc` formula provides the `gfortran` compiler required by NumPy, SciPy, and ObsPy. Also install a non-system, up-to-date, version of Python. `zmq` and `pyqt` are required for IPython notebook and Qt console, respectively.

```bash
$ brew tap Homebrew/python
$ brew update
$ brew install gcc python numpy scipy matplotlib matplotlib-basemap zmq pyqt
```

Make sure that

```bash
$ which pip
```

evaluates to `/usr/local/bin/pip` before continuing. 

### Installing other ObsPy dependencies

Use `pip` to install the remaining ObsPy dependencies and a few must-have packages:

```bash
$ pip install mock flake8 # For obspy-runtests
$ pip install ipython\[all\] # IPython and its main optional dependencies
```

### Installing ObsPy

To install the latest stable version type:

```bash
$ pip install obspy
```

you can than at any point type

```bash
$ pip install --upgrade obspy
```

to update to the latest stable version.

#### Installing the latest master

If you a have a good reason (make sure to have one, otherwise install the latest stable version as described above) to use the latest master from GitHub, you can either use

```bash
$ pip install obspy==dev
```

or checkout out the git repository.

```bash
$ git clone https://github.com/obspy/obspy.git
$ cd obspy
$ pip install .         # for a normal installation
$ pip install -e -v .   # for an editable installation
```

### Testing the installation

To check if everything works as expected you can run ObsPy's included test suite via

```bash
$ obspy-runtests
```

This will run all tests and provides a way to report any potential errors to us. No occurring errors means that you now have a fully working ObsPy installation. Head over to the [Tutorial](http://docs.obspy.org/tutorial/) to learn how to use it.

### IPython HTML Notebook

The above instructions also install a fully working [IPython HTML notebook](http://ipython.org/notebook.html), to launch it type:

```bash
$ ipython notebook 
```

### Additional useful Python Packages

Other useful packages like [pandas](http://pandas.pydata.org/), [requests](http://docs.python-requests.org/en/latest/), [colorama](https://pypi.python.org/pypi/colorama), [SymPy](http://sympy.org/), [scikit-learn](http://scikit-learn.org/), and countless more can be installed with `pip`.