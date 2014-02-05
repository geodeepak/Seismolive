### App

The easiest way to install ObsPy under Mac is to use the fully self contained OSX Application of ObsPy and all its dependencies. No need to install anything else, just this one application. This is great for acquiring a fully working ObsPy environment very quickly. It might prove problematic to install additional modules if your OS X version and the one where the app has been compiled on differ too much. In that case please consider one of the options presented below.

  * [[OSX Application|Installation on Mac with OSX Application]]

### MacPorts

A very convenient method to install ObsPy on various versions of Mac OS X and Python, along with a large choice other Python packages is though the MacPorts Projects package management system (http://www.macports.org). This is especially true for users already using MacPorts. Not-yet-users of MacPorts are encouraged to give it a try! The method via MacPorts would install all dependencies and ObsPy either from a pre-compiled binary package or from source. Here the details:

  * [[Installation using MacPorts|Installation on Mac OS X using MacPorts]]

### Homebrew

Another package manager for OS X is [Homebrew](http://brew.sh/). It provides recipes for many different codes and usually compiles them during the installation. This is probably the most work from all alternatives presented here but arguably also the most flexible one.

 * [[Installation using Homebrew|Installation on OS X using Homebrew]]

### Notes on multiprocessing on OSX

NumPy usually links against some BLAS and LAPACK implementation in order to speed up some routines. Per default it will, on OSX, link against Apple's `Accelerate.framework` consisting of `Accelerate` and `vecLib`. These are highly optimized but will break in combination with Python's `multiprocessing` module or any other use of `os.fork` if a function from `numpy.linalg` is called. A simple linear detrend from within ObsPy will already trigger this.

The same holds true, when linking against OpenBLAS. A solution would be to link against LAPACK but installing that can be very hard.

The recommendation right now is to either wait for Python 3.4 which includes some different ways of spawning processes, avoid using the numpy.linalg package (almost impossible when using ObsPy), or use some other parallel processing packages that does not make use of `os.fork` like the ipython clusters or pp.
