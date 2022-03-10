![Logo](http://i.imgur.com/EnyL91L.png)

# WORK IN PROGRESS: THIS IS JUST A TEMPLATE FOR UPCOMING RELEASE RIGHT NOW

### UPDATE
ObsPy ... has been released to fix an installation issue with version ... that is exclusive to the installation with `pip` or from source and with the newest versions of setuptools installed, see https://github.com/obspy/obspy/releases/tag/....

---

This document details significant new features and changes in ObsPy `X.X.0` (DOI for this version: `10.5281/zenodo.XXXXXXX`). The [Full Changelog](#full-changelog) at the end is more comprehensive. This release is based on around XXX individual contributors over the course of the last XXX years since the last major release `XXXX`.

Documentation and resources for this version can (as always) be found at: https://docs.obspy.org

---

> Aside from the occasional change and new feature, there **never was any formal funding** for ObsPy and it has been developed by enthusiastic volunteers, mostly from academia. If you use ObsPy, please consider [acknowledging](https://github.com/obspy/obspy/wiki#acknowledging) us so we can justify investing time into it.

Work on this release was in parts and among others supported by the following
institutions/companies and grants (in alphabetical order):
 - ...
 - ...
 - (fill in from changelog)


---

## Index

* [Supported Systems](#supported-systems)
* [Updating ObsPy](#updating-obspy)
* [Farewell Python2](#farewell-python2)
* [Backwards Incompatible / Breaking Changes](#backwards-incompatible---breaking-changes)
* [New Deprecations](#new-deprecations)
* [New Signal Processing Things](#new-signal-processing-things)
* [Notable Changes in Core Packages](#notable-changes-in-core-packages) 
* [Additional Reading Support](#additional-reading-support)
* [Miscellaneous Notable Bug Fixes and Improvements](#miscellaneous-notable-bug-fixes-and-improvements)
* [Full Changelog](#full-changelog)

---

### Supported Systems

We officially support the following systems (meaning we test that they work with ObsPy; other versions - especially newer ones, might work, but we cannot guarantee that).

Python modules:

* `Python`: 3.7, 3.8
* `NumPy`: >=1.15.0
* `SciPy`: >=1.0.0
* `matplotlib`: >=3.2.0

Supported Operating Systems (mostly 32bit and 64bit):

* `Windows`
* `OSX`
* `Linux` (tested with default packages on CentOS/RedHat 7 + 8, Debian 8 + 9 + 10, Fedora 30 + 31, openSUSE Leap 15.1, Ubuntu 14.04 + 16.04 + 18.04)
* `Raspberry Pi` (Raspbian 8 + 9 + 10)

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

### Backwards Incompatible / Breaking Changes

 * ...

---

### New Deprecations
 * ...
 * ...

---

### New Signal Processing Things

 * ...
 * ...

---

### Notable Changes in Core Packages

 * ...
 * ...

---

### Additional Reading Support 

 * ...
 * ...


###  Miscellaneous Notable Bug Fixes and Improvements 
 * ...
 * ...
 
---

### Full Changelog

```
X.X.0: (doi: ...)
 - obspy.core:
   * ...
   * ...
```
