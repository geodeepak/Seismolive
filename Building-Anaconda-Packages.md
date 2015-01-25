1. Download [Anaconda](http://continuum.io/downloads).
2. Install.
3. Checkout latest ObsPy master.
4. cd misc/installer/anaconda

5. Do some setup...

```bash
$ export CONDA_PY=34
```

```bash
$ mkdir -p CONDA_DIR/conda-bld/work
```

On linux:

```bash
$ apt-get install chrpath
```

Repeat for mccabe, flake8, and suds:

6. conda build mccabe
7. conda install "path/to/mccabe"

8. conda build obspy
9 conda install "path/to/obspy"

