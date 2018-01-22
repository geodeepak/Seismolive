![Logo](http://i.imgur.com/EnyL91L.png)


***NOT YET RELEASED - THIS DOCUMENT IS WORK IN PROGRESS!!***

This document details significant new features and changes in ObsPy `1.2.0`. The [Full Changelog](#full-changelog) at the end is more comprehensive.

Documentation and resources for this version can (as always) be found at: https://docs.obspy.org

---

> Aside from the occasional change and new feature, there **never was any formal funding** for ObsPy and it has been developed by enthusiastic volunteers, mostly from academia. If you use ObsPy, please consider [acknowledging](https://github.com/obspy/obspy/wiki#acknowledging) us so we can justify investing time into it.

---


---

## Index

...

---

### Supported Systems

We officially support the following systems (meaning we test that they work with ObsPy; other versions - especially newer ones, might work, but we cannot guarantee that).

Python modules:

* `Python`: 2.7, 3.4, 3.5, 3.6
* `NumPy`: 1.6.2 - 1.14
* `SciPy`: 0.11.0 - 1.0
* `matplotlib`: 1.1.1 - 2.1
* `basemap`: 1.0.2 - 1.1.0

Supported Operating Systems (mostly 32bit and 64bit):

* `Windows`
* `OSX`
* `Linux` (tested with default packages on CentOS/RedHat 7, Debian 7 + 8 + 9, Fedora 25 + 26, openSUSE Leap 42.2 + 42.3, Ubuntu 14.04 + 16.04 + 17.04 + 17.10)
* `Raspberry Pi` (Raspbian Wheezy + Jessie + Stretch)

---

### Updating ObsPy

Updating should be straight-forward. So depending on your installation do


```bash
# Generic Python
#
# For the first time we also have binary wheels for Linux and OSX so
# this now also works without a compiler.
$ pip install -U obspy
```

```bash
# Anaconda Python Distribution
# `conda install -c obspy obspy` is no longer supported for most platforms!
$ conda update -c conda-forge obspy
```

```bash
# Debian/Ubuntu
# add debs.obspy.org to your /etc/apt/sources.list first
$ apt-get update
$ apt-get upgrade python-obspy  # and/or python3-obspy
```

or whatever your package manager of choice needs to be told to update a package.

---

### New Deprecations
 * The `'domain'` keyword in the correlate function is deprecated in favor of the new `'method'` keyword to stay compatible with new SciPy versions.
...

### New Signal Processing Things

 * New `correlate_template()` function with 'full' normalization useful for template matching.


---