[Anaconda](https://store.continuum.io/cshop/anaconda/) (you can also use [Miniconda](http://conda.pydata.org/miniconda.html) for a smaller footprint) is a scientific Python installation shipping with essentially all needed packages. Install it according to the instructions on their homepage. You can use any Anaconda Python version.

**Anaconda works on most systems without root access!**

 * Install Anaconda following the instructions on their site

 * Add our channel to your Anaconda configuration:

```bash
conda config --add channels obspy
```

 * Install pre-compiled [ObsPy conda package from Anaconda cloud](https://anaconda.org/obspy/obspy) with:

```bash
$ conda install obspy
```


### Test your Installation

Run the test suite to assure everything works correctly.

```bash
$ obspy-runtests
```