This is a companion document to the [contributor guidelines](https://github.com/obspy/obspy/blob/master/CONTRIBUTING.md).

A developer installation of ObsPy will recognize any changes you make to the code base. For this you need to install all dependencies of ObsPy. A very easy way to do this is to first install ObsPy with Anaconda and then just remove ObsPy again - this will leave all dependencies installed (see [[here|Installation via Anaconda]] for more details regarding an installation with `conda`). Example (feel free to use a different environment name):

```bash
$ conda create -n obspy_dev python=3.6  # Use a new Python version for development!
$ source activate obspy_dev
$ conda install -c conda-forge obspy
$ conda uninstall obspy
```

You then need to checkout ObsPy with git. Make sure you have git installed - you'll also need a C compiler for the subsequent compilation.

### Install obspy in [pip's "editable" mode](https://pip.pypa.io/en/stable/reference/pip_install/#editable-installs) 

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