### Python

Get and run the latest official Python (2.7.x or 3.5.x) installer from  http://www.python.org/download/

The Python binary and the Scripts directory should be set within the system PATH variable. Therefore append the following to the system PATH
```cmd
;C:\path\to\Python;C:\path\to\Python\Scripts
```
See  http://docs.python.org/using/windows.html#excursus-setting-environment-variables for a short tutorial on changing environment variables in Windows.

### Dependencies

  1. Using pre-compiled executable installers are the easiest way to install the needed packages  NumPy,  SciPy and  matplotlib.
    * The official 32-bit installers are available at:
      *   http://sourceforge.net/projects/numpy/files/
      *   http://sourceforge.net/projects/scipy/files/
      *   http://sourceforge.net/projects/matplotlib/files/matplotlib/
    * or fetch the unofficial Windows 64 bit releases from  http://www.lfd.uci.edu/~gohlke/pythonlibs/ (get the MKL builds for NumPy?).
  2.  ObsPy and further dependencies can be downloaded via pip. pip is already installed if you're using Python 2 >=2.7.9 or Python 3 >=3.4, but you'll need to upgrade pip. Download and run from the windows command line the Python script https://bootstrap.pypa.io/get-pip.py.

        python.exe get-pip.py

  3.  The following depended Python module are needed. Run from windows command line: 
            
        pip install lxml sqlalchemy

  4.  We strongly recommend the enhanced Python shell  IPython which can be obtained via:
            
        pip install pyreadline ipython

  5. In order to run the whole test suite you will need a few more packages

        pip install flake8 nose mock



### ObsPy

Run on command line:

    pip install obspy


ObsPy may be updated at any time using the -U option:

    pip install -U obspy
