[Anaconda](https://store.continuum.io/cshop/anaconda/) (you can also use [Miniconda](http://conda.pydata.org/miniconda.html) for a smaller footprint) is a scientific Python installation shipping with essentially all needed packages. Install it according to the instructions on their homepage. You can use any Anaconda Python version. An **Anaconda Python installation is completely separate** from any existing system wide or user space Python installation, so **Anaconda can be tested without the fear of breaking an existing installation**.

**Anaconda works on most systems without root access!**

 * [Install Anaconda following the instructions on their site](https://www.continuum.io/downloads)

 * Add the `conda-forge` channel (for 32bit Linux packages also add `obspy` channel) to your Anaconda configuration (see [conda docs reagarding channels](https://conda.io/docs/channels.html)):

```bash
$ conda config --add channels conda-forge
```

 * **We strongly recommend to work with separate Anaconda environments, and especially not use the special ``root`` environment** (that is used for all `conda` commands and environment manipulations, package installations etc.) for anything besides updating the `conda` package itself (if necessary):

```bash
$ conda create -n obspy python=2.7   # or e.g. python=3.5
$ source activate obspy
(obspy) $ 
```

 * Install pre-compiled [ObsPy conda package from Anaconda cloud](https://anaconda.org/obspy/obspy) with:

```bash
(obspy) $ conda install obspy
```

#### Updating

```bash
(obspy) $ conda update obspy
```

or (if you did not add the `conda-forge` channel to your default channels):

```bash
(obspy) $ conda update -c conda-forge obspy
```

Try to stick to **only using `conda` package manager to install packages whenever possible!** Other tools like `pip` (or even its outdated `easy_install` predecessor) should really only be used for Python packages that are not packaged by Anaconda (search for available pre-packaged versions first doing `conda search <package_name>` -- or if it's not available in the default channel doing `anaconda search -t conda <package_name>`). And even when needing to install a package from source using `pip` it is a good idea to at least install the package's dependencies via `conda` beforehand.

#### Troubleshooting:

 * Windows users might have to add `conda-forge` channel to have `basemap` packages available (see [ContinuumIO/anaconda-issues#757](https://github.com/ContinuumIO/anaconda-issues/issues/757))
 * If you have problems, be sure to check out the [Troubleshooting page of Anaconda](http://conda.pydata.org/docs/troubleshooting.html)
 * Especially **beware of mixing in Python packages from outside the environment**, not handled/installed by the `conda` package manager. This is usually unwanted and coming from older (and way more sloppy) Python installations and **bound to bring forth very unexpected and hard to debug behavior and errors**. This can happen outside of anaconda's control by..
   * having [`PYTHONPATH` and `PYTHONHOME` environment variables](http://conda.pydata.org/docs/troubleshooting.html#resolution-for-python-packages-make-sure-you-do-not-have-pythonpath-or-pythonhome-set) set, or (less common) by..
   * having [Python modules in specific user space locations which Python looks for](http://conda.pydata.org/docs/troubleshooting.html#resolution-for-python-packages-remove-any-site-specific-directories)

#### Tip:

Versions of packages can be fixed by [pinning in Anaconda](http://conda.pydata.org/docs/faq.html#pinning-packages) (e.g. so that certain packages stay on same version even when updating packages that depend on them). It can be a good idea to pin the installed numpy version as many packages are compiled against a certain numpy version and only update numpy deliberately. Also, ObsPy major version can be fixed in the same way to keep an Anaconda environment on the a fixed version, e.g.:

(Note: Recent `conda` version >=4.0 has significant improvements and properly takes numpy dependent packages into account when trying to update numpy, so pinning numpy is not as important anymore with an updated `conda` package)

```
numpy 1.10.*
matplotlib 1.5.*
basemap 1.0.*
obspy 1.0.*
```

#### Example:

This example shows how to set up a separate anaconda environment (after anaconda installation) for the old ObsPy version 0.10.2 (assuming a Python2 installation):

 * add our obspy Anaconda channel (only needs to be done once after Anaconda installation)

```bash
$ conda config --add channels obspy
```

 * create separate, bare environment with name "obspy0.10"

```bash
$ conda create -n obspy0.10 python=2.7
Fetching package metadata: ........
Solving package specifications: ...........

Package plan for installation in environment /home/megies/anaconda/envs/obspy0.10:

The following NEW packages will be INSTALLED:

    openssl:    1.0.2g-0     
    pip:        8.1.1-py27_0 
    python:     2.7.11-0     
    readline:   6.2-2        
    setuptools: 20.3-py27_0  
    sqlite:     3.9.2-0      
    tk:         8.5.18-0     
    wheel:      0.29.0-py27_0
    zlib:       1.2.8-0      

Proceed ([y]/n)? y

Extracting packages ...
[      COMPLETE      ]|######################################| 100%
Linking packages ...
[      COMPLETE      ]|######################################| 100%
#
# To activate this environment, use:
# $ source activate obspy0.10
#
# To deactivate this environment, use:
# $ source deactivate
#
```

 * activate environment for use in this terminal

```bash
$ source activate obspy0.10
discarding /path/to/anaconda/bin from PATH
prepending /path/to/anaconda/envs/obspy0.10/bin to PATH
(obspy0.10)$ which python  # just to illustrate which python is in use now
/path/to/anaconda/envs/obspy0.10/bin/python
```

 * set desired version numbers by pinning in environment (create new text file "pinned" in correct folder, see above)

```
# contents of /path/to/anaconda/envs/obspy0.10/conda-meta/pinned:
python 2.7.*
numpy 1.10.*
matplotlib 1.5.*
basemap 1.0.*
obspy 0.10.*
```

 * now install obspy and dependencies

```bash
(obspy0.10)$ conda install obspy
Fetching package metadata: ........
Solving package specifications: ...........

Package plan for installation in environment /home/megies/anaconda/envs/obspy0.10:

The following packages will be downloaded:

    package                    |            build
    ---------------------------|-----------------
    libgfortran-3.0            |                0         261 KB
    future-0.15.2              |           py27_0         616 KB
    numpy-1.9.3                |           py27_2         5.7 MB
    pytz-2016.2                |           py27_0         176 KB
    lxml-3.6.0                 |           py27_0         2.8 MB
    python-dateutil-2.5.1      |           py27_0         235 KB
    scipy-0.17.0               |       np19py27_2        29.9 MB
    ------------------------------------------------------------
                                           Total:        39.7 MB

The following NEW packages will be INSTALLED:

    basemap:         1.0.7-np19py27_0 
    cairo:           1.12.18-6        
    flake8:          2.5.1-py27_0     
    fontconfig:      2.11.1-5         
    freetype:        2.5.5-0          
    funcsigs:        0.4-py27_0       
    future:          0.15.2-py27_0    
    geos:            3.3.3-0          
    libgfortran:     3.0-0            
    libpng:          1.6.17-0         
    libxml2:         2.9.2-0          
    libxslt:         1.1.28-0         
    lxml:            3.6.0-py27_0     
    matplotlib:      1.4.3-np19py27_2 
    mccabe:          0.3.1-py27_0     
    mkl:             11.3.1-0         
    mock:            1.3.0-py27_0     
    numpy:           1.9.3-py27_2     
    obspy:           0.10.2-np19py27_0
    pbr:             1.3.0-py27_0     
    pep8:            1.7.0-py27_0     
    pixman:          0.32.6-0         
    py2cairo:        1.10.0-py27_2    
    pyflakes:        1.1.0-py27_0     
    pyparsing:       2.0.3-py27_0     
    pyqt:            4.11.4-py27_1    
    python-dateutil: 2.5.1-py27_0     
    pytz:            2016.2-py27_0    
    qt:              4.8.7-1          
    scipy:           0.17.0-np19py27_2
    sip:             4.16.9-py27_0    
    six:             1.10.0-py27_0    
    sqlalchemy:      1.0.12-py27_0    

Proceed ([y]/n)? 

Fetching packages ...
libgfortran-3. 100% |######################################| Time: 0:00:00 442.02 kB/s
future-0.15.2- 100% |######################################| Time: 0:00:00 756.18 kB/s
numpy-1.9.3-py 100% |######################################| Time: 0:00:04   1.40 MB/s
pytz-2016.2-py 100% |######################################| Time: 0:00:00 356.89 kB/s
lxml-3.6.0-py2 100% |######################################| Time: 0:00:03 793.42 kB/s
python-dateuti 100% |######################################| Time: 0:00:00 473.91 kB/s
scipy-0.17.0-n 100% |######################################| Time: 0:00:20   1.54 MB/s
Extracting packages ...
[      COMPLETE      ]|######################################| 100%
Linking packages ...
[      COMPLETE      ]|######################################| 100%
```

 * done!

### Test your Installation

Run the test suite to assure everything works correctly.

```bash
$ obspy-runtests
```

### Offline installation

For installation of Anaconda including ObsPy in an offline environment, see http://lists.swapbytes.de/archives/obspy-users/2017-February/002298.html