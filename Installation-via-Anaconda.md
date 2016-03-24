[Anaconda](https://store.continuum.io/cshop/anaconda/) (you can also use [Miniconda](http://conda.pydata.org/miniconda.html) for a smaller footprint) is a scientific Python installation shipping with essentially all needed packages. Install it according to the instructions on their homepage. You can use any Anaconda Python version.

**Anaconda works on most systems without root access!**

 * [Install Anaconda following the instructions on their site](https://www.continuum.io/downloads)

 * Add our channel to your Anaconda configuration:

```bash
conda config --add channels obspy
```

 * Install pre-compiled [ObsPy conda package from Anaconda cloud](https://anaconda.org/obspy/obspy) with:

```bash
$ conda install obspy
```

#### Tip:

Versions of packages can be fixed by [pinning in Anaconda](http://conda.pydata.org/docs/faq.html#pinning-packages) (e.g. so that certain packages stay on same version even when updating packages that depend on them). It can be a good idea to pin the installed numpy version as many packages are compiled against a certain numpy version and only update numpy deliberately. Also, ObsPy major version can be fixed in the same way to keep an Anaconda environment on the a fixed version, e.g.:

```
numpy 1.10.*
matplotlib 1.5.*
basemap 1.0.*
obspy 1.0.*
```

#### Example:

This example shows how to set up a separate anaconda environment (after anaconda installation) for the old ObsPy version 0.10.2 (assuming a Python2 installation and assuming obspy channel was added -- see above):

 * create separate, bare environment with name "obspy0.10"

```bash
$ conda create -n obspy0.10 python=2.7
```

 * activate environment for use in this terminal

```bash
$ source activate obspy0.10
(obspy0.10)$ 
```

 * set desired version numbers by pinning in environment (create new text file "pinned" in correct folder, see above)

```
# contents of /path/to/anaconda/envs/obspy0.10/conda-meta/pinned:
python 2.7.*
numpy 1.9.*
matplotlib 1.5.*
basemap 1.0.*
obspy 0.10.*
```

 * now install obspy and dependencies

```bash
(obspy0.10)$ conda install obspy
```

 * done!

### Test your Installation

Run the test suite to assure everything works correctly.

```bash
$ obspy-runtests
```