### Python

Get and run the latest official Python 2.7.x installer from  http://www.python.org/download/ (Python 3.x is NOT supported for now).

The Python binary and the Scripts directory should be set within the system PATH variable. Therefore append the following to the system PATH
```cmd
;C:\path\to\Python2.7;C:\path\to\Python2.7\Scripts
```
See  http://docs.python.org/using/windows.html#excursus-setting-environment-variables for a short tutorial on changing environment variables in Windows.

### C Compiler

Building ObsPy requires a C compiler. ObsPy has been successfully built using the free GNU compiler of the MinGW project (32- and 64-bit) and Microsoft Visual Studio (32- and 64-bit). See also https://github.com/cython/cython/wiki/CythonExtensionsOnWindows#using-windows-sdk-cc-compiler-older-method

### Git Client

In order to check out the latest developer version of ObsPy you need a Git command line client. You may find a binary installers e.g. at http://git-scm.com/downloads.

Please make sure that the directory to the Git client is also included in the PATH settings (for details see step 1), e.g. add
```cmd
;C:\path\to\GitClient\bin;%PATH%
```

### Dependencies

  1. Using pre-compiled executable installers are the easiest way to install the needed packages  NumPy,  SciPy and  matplotlib.
    * The official 32-bit installers are available at:
      *   http://sourceforge.net/projects/numpy/files/
      *   http://sourceforge.net/projects/scipy/files/
      *   http://sourceforge.net/projects/matplotlib/files/matplotlib/
    * or fetch the unofficial Windows 64 bit releases from  http://www.lfd.uci.edu/~gohlke/pythonlibs/ (get the MKL builds for NumPy?).
  2.  ObsPy and further dependencies can be downloaded via pip. pip is already installed if you're using Python 2 >=2.7.9 or Python 3 >=3.4, but you'll need to upgrade pip. Download and run from the windows command line the Python script https://bootstrap.pypa.io/get-pip.py.
      ```
python.exe get-pip.py
      ```
  3.  The following depended Python module are needed. Run from windows command line: 
      ```
pip install lxml sqlalchemy
      ```
  4.  We strongly recommend the enhanced Python shell  IPython which can be obtained via:
      ```
pip install pyreadline ipython
      ```

### ObsPy

Checkout the latest sources using a Git client on command line:
```
git clone https://github.com/obspy/obspy.git /path/to/obspy/src
```

Install ObsPy by running the following command:
```
cd /path/to/obspy/src
python setup.py develop
```
