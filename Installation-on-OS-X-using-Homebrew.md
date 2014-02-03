[Homebrew](http://brew.sh/) a is package manager for OS X in the vein of APT (apt-get) on Debian operating systems. It works by providing recipes to install software from source. The advantage is that it is usually very up-to-date and simply works.

Before installing Homebrew you will need to install a compiler as OS X does not ship with one by default. You can get one by either installing [Xcode through the App Store](https://itunes.apple.com/en/app/xcode/id497799835?mt=12) (Warning: huge download and installation) or by installing the [Command Line Tools](https://developer.apple.com/downloads/) from Apple. You must be in possession of an Apple account for both options.

Installing Homebrew is then simply a manner of pasting the following line in a terminal:

```bash
ruby -e "$(curl -fsSL https://raw.github.com/Homebrew/homebrew/go/install)"
```

You will then want to put the Homebrew directory at the very top of your `$PATH` variable. One possibiliy of doing this is appending the following line to your `~/.bash_profile` file.

```bash
export PATH=/usr/local/bin:$PATH
```

You are now ready to use Homebrew by first utilizing it to install Python.

### Installing Additional Dependencies

ObsPy requires a Fortran compiler and furthermore lxml requires two XML libraries and matplotlib sometimes does not work with the freetype library shipping with OS X. To install all the requirements use

```bash
$ brew install gfortran libxml2 libxslt freetype
$ brew link --force freetype  # You can also try to install matplotlib with the OS X provided version
```

### Installing Python

```bash
$ brew install python
```

This command will also install `distribute` and `pip`, both invaluable tools for managing Python installations.

Now make sure that

```bash
$ which pip
```

evaluate to `/usr/local/bin/pip` and use it to install [virtualenv](http://www.virtualenv.org/).

virtualenv provides functionality to create virtual Python environment that do not interfere with each other. This guide will install ObsPy and dependencies to a virtualenv. To create a virtual environment, again make sure that 

```bash
$ virtualenv --system-site-packages  # Do NOT forget the system-site-packages
```

evaluates to `/usr/local/bin/virtualenv` and execute

```bash
$ virtualenv obspy_virtualenv
```

The argument is the folder where the environment is installed to. You can choose any one you like. Once it is done, activate it via

```bash
$ source obspy_virtualenv/bin/activate
```

Your prompt will change to reflect the current virtual environment. To leave it, simply type `deactivate`. If you always want to use that virtualenv, you can place the activation command in your `~/.bash_profile`.

### Installing the Scientific Python Stack

You can use `pip` to install the remaining ObsPy dependencies and must-haves. Installing them all in one go usually does not work for some reason.

```bash
$ pip install ipython
$ pip install numpy
$ pip install scipy
$ pip install matplotlib
$ pip install suds
$ pip install lxml
$ pip install sqlalchemy
```

### Installing ObsPy

To install the latest stable version, simply type

```bash
$ pip install obspy
```

you can than at any point type

```bash
$ pip install --upgrade obspy
```

to update to the latest stable version.

#### Installing the latest master

If you a have a good reason (make sure to have one, otherwise install the latest stable version as described above) to use the latest master from Github, you can either use

```bash
$ pip install obspy==dev
```

or checkout out our git repository and install it from there.

```bash
$ git clone https://github.com/obspy/obspy.git
$ cd obspy
$ pip install .         # for a normal installation
$ pip install -e . -v    # for a developers installation
```

### Testing the installation

To check if everything works as expected you can run ObsPy's included test suite via

```bash
$ obspy-runtests
```

This will run all tests and provides a way to report any potential errors to us. No occurring errors means that you now have a fully working ObsPy installation. Head over to the [Tutorial](http://docs.obspy.org/tutorial/) to learn how to use it.

### Additional useful Python Packages

This section describes the installation of some more potentially useful Python packages.

#### IPython HTML Notebook

The [IPyton HTML Notebook](http://ipython.org/notebook.html) is web-based interactive environment to run Python (and thus ObsPy) combining code execution, text, mathematics, plots and more. Definitely worth a try.

It requires ZMQ, which can be installed via

```bash
$ brew install zmq
```

Install some more Python dependencies with

```bash
$ pip install pyzmq
$ pip install tornado
$ pip install jinja2
```

You should now be able to type

```bash
$ ipython notebook --pylab=inline
```

which drops you in a browser ready for action.

#### Basemap

The [basemap package](http://matplotlib.org/basemap/) is an add-on for matplotlib giving you the possibility to plot maps similar to GMT. It currently cannot be installed via `pip` so it must be installed from source. Use Homebrew to install a dependency

```bash
$ brew install geos
```

then download the latest source version from their homepage and 

```bash
$ tar -xzf basemap-1.x.x.tar.gz
$ cd basemap-1.x.x
$ pip install .
```

#### Qt Bindings

Two sets of Python bindings for the Qt cross-platform application and UI framework are in existence. Both are (except for some licensing issues) virtually identical from a usage perspective. Thankfully that arduous task is greatly simplified by utilizing Homebrew once again.

[PySide](http://qt-project.org/wiki/PySide) can simply be installed with the help of `pip` and Homebrew:

```bash
$ /usr/local/bin/pip install sphinx
$ brew install pyside
```

This might take a while so grab a coffee or lunch.

Installing [PyQt](http://www.riverbankcomputing.com/software/pyqt) is also rather simple.

```bash
$ brew install pyqt
```

This will also take a while.

#### Other packages

Other useful packages like [pandas](http://pandas.pydata.org/), [requests](http://docs.python-requests.org/en/latest/), [colorama](https://pypi.python.org/pypi/colorama), [SymPy](http://sympy.org/), [scikit-learn](http://scikit-learn.org/), and countless more can be installed with `pip`.