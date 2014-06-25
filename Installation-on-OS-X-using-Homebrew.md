[Homebrew](http://brew.sh/) is a package manager for OS X in the vein of APT (apt-get) on Debian operating systems. It works by providing recipes to install software from source. The advantage is that it is usually very up-to-date and simply works.

To install Homebrew follow the installation instructions on their homepage (make sure the [listed requirements](https://github.com/Homebrew/homebrew/wiki/Installation#requirements) are fulfilled).

### Installing Python and other required packages

The Fortran compiler is required by NumPy, SciPy, and ObsPy; the other libraries are required for lxml, matplotlib, ipython, and basemap. Also install a non-system version of Python.

```bash
$ brew update
$ brew install gfortran libxml2 libxslt freetype python geos zmq pyqt
$ brew link --force freetype
```

Make sure that

```bash
$ which pip
```

evaluates to `/usr/local/bin/pip` before continuing. 

### Installing the Scientific Python Stack and other ObsPy dependencies

Use `pip` to install the remaining ObsPy dependencies and a few must-have packages:

```bash
$ pip install ipython
$ pip install future # For ObsPy >= 0.10
$ pip install numpy
$ pip install scipy
$ pip install matplotlib
$ pip install suds # Only for ObsPy < 0.10
$ pip install suds-jurko # For ObsPy >= 0.10
$ pip install lxml
$ pip install sqlalchemy
$ pip install --allow-external basemap --allow-unverified basemap basemap
$ pip install mock nose flake8
$ pip install pyzmq
$ pip install tornado jinja2
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