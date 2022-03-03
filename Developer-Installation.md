This is a companion document to the [contributor guidelines](https://github.com/obspy/obspy/blob/master/CONTRIBUTING.md).

A developer installation of ObsPy will recognize any changes you make locally to the code base. For this you need to install all dependencies of ObsPy. A very easy way to do this **-- and thus highly recommended in may cases --** is to first install ObsPy with Anaconda **in a dedicated, new environment** and then remove the ObsPy package again, leaving the dependencies installed.

Please note: When working in an editable installation and making changes to either any C source code files or making changes to the plugin system (`ENTRY_POINTS` in `setup.py`), you need to subsequently refresh the editable pip installation (do `$ pip install -v -e /path/to/obspy` again) for changes to take effect.

## Installation from source using Anaconda

The easiest easy way to get a working developer installation of ObsPy is via Anaconda. First install the prebuilt, stable ObsPy release package in a fresh, dedicated environment and then just remove ObsPy again - this will leave all dependencies installed (see [[here|Installation via Anaconda]] for more details regarding an installation with `conda`). Example (feel free to use a different environment name):

```bash
# "git" package not needed if already installed in the system
# "c-compiler" package may not be needed if system has a proper C compiler setup
(base) $ conda create -n obspy_dev -c conda-forge python=3.7 obspy git c-compiler
(base) $ conda activate obspy_dev
(obspy_dev) $ conda uninstall --offline --force obspy  # Uninstall without removing dependencies
```

You then want to checkout ObsPy locally with [`git*`](https://git-scm.com/). You also need a C compiler for the subsequent compilation (should be properly set up by the activated Anaconda environment).

    *) N.b.: Making an editable install from an unpacked tarball (as opposed to a git repository clone)
    is possible in the same way, but it lacks the option to output a diff of changes made locally,
    so it is not advisable for a developer installation.

#### Install obspy in [pip's "editable" mode](https://pip.pypa.io/en/stable/reference/pip_install/#editable-installs) 

```bash
$ cd /directory/where/code/lives
# Clone your own ObsPy fork!
$ git clone https://github.com/YOUR_USERNAME/obspy.git
$ cd obspy
# Make sure you branch from the correct base branch! See the
# contributor guidelines for rules on how to choose the correct
# base branch.
$ git checkout master  # Might be different for you
# Make a new branch with your changes.
$ git checkout -b my-new-features  # Choose a sensible branch name!
# The `-e` will only copy a kind of symlink to the `site-packages`
# directory of your activate Python installation. So any changes you
# make to the code base will be reflected when you actually run ObsPy.
# You'll have to rerun this command any time a C source code file or
# entry points of the plugin system in `setup.py` were changed.
$ pip install -v -e .
```

## Installation from source without Anaconda

You should consider using the Anaconda approach above, if at all feasible. Not using Anaconda is for experienced developers familiar with e.g. C compiler setup. You will need a Python 3 installation with the following in place before installing ObsPy with pip editable mode as shown in the above section:

 - pip
 - numpy
 - C compiler
 - git (optional, making an editable installation from an unpacked tar/zipball is possible but much less convenient to track changes made locally or to prepare Pull requests)