![Logo](http://i.imgur.com/EnyL91L.png)

This document details significant new features and changes in ObsPy `1.3.0` (DOI for this version: `10.5281/zenodo.6327346`). The [Full Changelog](#full-changelog) at the end is more comprehensive. This release is based on around **TODO** individual contributors over the course of the last 2 years since the last major release `1.2.0`.

Documentation and resources for this version can (as always) be found at: https://docs.obspy.org

---

> Aside from the occasional change and new feature, there **never was any formal funding** for ObsPy and it has been developed by enthusiastic volunteers, mostly from academia. If you use ObsPy, please consider [acknowledging](https://github.com/obspy/obspy/wiki#acknowledging) us so we can justify investing time into it.

---

## Index

* [Supported Systems](#supported-systems)
* [Updating ObsPy](#updating-obspy)
* [Farewell Python2](#farewell-python2)
* [New Deprecations](#new-deprecations)
* [New Signal Processing Things](#new-signal-processing-things)
* [Notable Changes in Core Packages](#notable-changes-in-core-packages) 
* [Additional Support for Nordic Format](#additional-support-for-nordic-format)
* [Additional Reading Support](#additional-reading-support)
* [Miscellaneous Notable Bug Fixes and Improvements](#miscellaneous-notable-bug-fixes-and-improvements)
* [Full Changelog](#full-changelog)

---

### Supported Systems

We officially support the following systems (meaning we test that they work with ObsPy; other versions - especially newer ones, might work, but we cannot guarantee that, upper boundary is basically versions available through `conda-forge` at time of release).

Python modules:

* `Python`: 3.7, 3.8, 3.9 and 3.10
* `NumPy`: 1.15.0 - 1.22.3
* `SciPy`: 1.0.0 - 1.8.0
* `matplotlib`: 3.2.0 - 3.5.1
* `basemap`: **not supported anymore**
* `cartopy`: 0.20.x -

Supported Operating Systems:

* `Windows`
* `OSX`
* `Linux`
* `Raspberry Pi`

See [test reports for version 1.3.0](https://tests.obspy.org/?version=1.3.0).

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

..or whatever your package manager of choice needs to be told to update a package.

---

### Farewell Python2

ObsPy `1.2.x` were the last versions to support both Python 2 and 3. Starting with version `1.3.0` all releases are Python 3 only.

### Backwards Incompatible / Breaking Changes

 * The deprecated `xcorr` cross correlation was removed. Please use the `correlate` or `correlate_template` functions which return the full cross correlation function. To determine the shift of the maximum in the cross correlation function use the `xcorr_max` function. Migration of old code:
```
    Old: maxshift, ccval = xcorr(a, b, shift)
    New: cc = correlate(a, b, shift)
         maxshift, ccval = xcorr_max(cc)

    Old: _, _, cc = xcorr(a, b, shift, full_xcorr=True)
    New: cc = correlate(a, b, shift)
```

---

### New Deprecations
 * ...

---

### New Signal Processing Things

 *...

---

### Notable Changes in Core Packages

* ...


### Additional Reading Support 

 * ...


###  Miscellaneous Notable Bug Fixes and Improvements 
* ...
 
---

### Full Changelog

```
1.3.0 (doi: 10.5281/zenodo.6327346)
===================================

Changes:
 - obspy.*
   * no more support for Python 2 (see #2577)
   * added python 3.9 and 3.10 tests for all platforms,
     minimal supported python version is 3.7 (#2925, #2489)
   * removed os.path calls with pathlib library calls (see #2751).
   * rewrote CI tests to make use of cache (see #2936)
   * removed individual logging configurations in Obspy, logging can be
     configured by the user, see documentation of Pythons logging module,
     only the FDSN mass downloader automatically configures logging as before,
     but this behavior can be turned off now. The loglevel keywords are
     therefore deprecated and have no effect anymore (see #2720)
   * refactored obspy-runtest to use pytest and modified several command
     line arguments, required to disable image comparisons (see #2489)
   * removed calls to deprecated NumPy functionality (see #2949, #2981)
   * cleaned the documentation, build process, and docstrings (see #2662, #2954)
   * refactored and modernized setup.py (see #2422)
 - scripts:
   * SDS report: try to be faster on slow filesystems (see #3009)
 - obspy.core:
   * speed up import of obspy core functions (see #2758)
   * read_inventory(): add "level" option to read files faster when less level
     of detail is needed. currently only implemented for StationXML reading
     (see #2759)
   * add option to suppress evalresp sensitivity mismatch warning when removing
     instrument response (see #2677)
   * round magnitudes in Catalog/Event string representation to one decimal
     (see #2742)
   * add support for pathlib.Path objects in read(), read_inventory() and
     read_events() functions (see #2743)
   * add a "DEF" option (default units) to Inventory.plot_response() and
     Trace.remove_response() (see #2806)
   * stream.select(): circumvent wildcard-matching when called with a trace-id
     without wildcards for quicker trace selection.
   * Inventory addition now consistently uses shallow copies (#2675, #2694)
   * removed obsolete wrapper around numpy.loadtxt causing import error with
     numpy 1.22 (see #2912, #2913)
   * fix iso8601 regex for issue #2868 to cope with day 360 properly
   * fix crash when resampling very short traces (see #2926)
   * response list stages: do not raise an exception if response calculation
     involves extrapolation outside of frequency range defined by the response
     list stage but rather only show a warning. raising an exception is the
     safe route but it also prevents valid calculations as it is up to the user
     to make sure that signal spectrum is properly suppressed in those
     frequency ranges outside of the valid response information (see #2988)
   * fix a bug while checking for valid URI syntax when setting identifiers on
     inventory type objects (see #2905)
 - obspy.clients.arclink:
   * submodule removed completely, since ArcLink was officially deprecated and
     deactivated on all big datacenters years ago (see #2994)
 - obspy.clients.fdsn:
   * introduce fine-grained FDSN client exceptions (see #2653, #2964)
   * support for "eventtype" parameter in get_events(), as specified in version
     1.2 of the FDSN event web service (see #2780)
   * Hostnames with hyphens and long TLDs are no longer rejected as invalid
     FDSN server URLs (#2878)
   * add URL mapping for IRISPH5, IESDMC, GEOFON (alternative to GFZ)
     (see #2739, #2932)
   * update RESIF URL mapping to use http and add RESIFPH5 (see #2938)
 - obspy.clients.filesystem:
   * add get_waveforms_bulk() method to SDS client (see #2616, #2626)
   * SDS client get_latency(): make one internal check optional which can be a
     massive speedup on slow filesystems (see #3009)
 - obspy.clients.seedlink:
   * basic client: properly terminate after finished get_info() request (see
     #2996)
 - obspy.imaging:
   * fix section plot in case of a single trace only (see #2764)
   * removed basemap, now only cartopy is supported for maps (see #2961)
   * fix day plot when passed a small interval (see #2967)
 - obspy.clients.filesystem.tsindex:
   * improvements to leap second file setup and other small fixes (see #2776)
 - obspy.clients.seedlink:
   * Fix a bug in basic client when printing debug output (see #2734)
 - obspy.clients.seishub:
   * added deprecation message
 - obspy.db:
   * added deprecation message
   * removed from default test suite
 - obspy.io
   * add support to resolve the SEED id of picks for nlloc hyp files and
     nordic files, refactor the same functionality for SeismicHandler evt
     and HypoDD pha files. Some parameter names therefore changed in the
     latter, but former parameter names are still supported (see #2251)
 - obspy.io.css:
   * open CSS waveforms even if gzip-compressed (see #2736)
 - obspy.io.gse2:
   * When reading GSE2 bulletins, station magnitudes now include waveform IDs
     and have associated station magnitude contributions (see #2718)
 - obspy.io.hypodd
   * add PHA write support (see #2687)
   * add read support for horizontal and vertical origin uncertainty (see #2687)
 - obspy.io.kinemetrics:
   * adds the ``apply_calib`` argument to the ``read_evt`` method to allow
     obtaining the raw data bits stored in the evt file (see #2582), note this
     changes the default (wrong!) behaviour, by default the data returned will
     be the NOT corrected ones. When passing ``apply_calib=True``, the
     calibration factor will be used.
 - obspy.io.nordic:
   * add read and write support for New Nordic format (see #2814)
   * fix bug where negative magnitudes were not read properly
   * fix bug where empty hours / minutes / seconds were not read as zero
   * fix bug where lat/lon-errors were read as lon/lat
   * fix bug where origin-error was written with RMS rather than time_error
   * for reading picks in Old Nordic format, set network code to None
     (was 'NA' previously)
   * stop writing waveform-file link to a DUMMY-file by default
   * add support for I/O of apparent velocity / horizontal slowness
   * add support for writing of multiple origins
   * add event-type mapping between Nordic and Obspy/Quakeml (do not fully
     match)
   * read pick-weight as pick.extra.nordic_pick_weight (was arrival.time_weight)
     and read finalweight into arrival.time_weight (or backazmiuth_weight)
     instead.
 - obspy.io.reftek:
   * enable reading data with floating point sampling rates like low sampling
     rate state-of-health channels (see #2678)
   * fix reading data in '16' and '32' encodings, when packets do not use
     the fixed maximum amount of available number of samples per data packet
     (see #2678)
   * properly take into account native system byteorder, should fix reading
     rt130 data on big endian systems (see #2678)
 - obspy.io.seiscomp:
   * Add support for SC3ML 0.11 and 0.12, dropped support for SC3ML < 0.6
     (see #2284).
   * Add support for custom tags (see #2284).
 - obspy.io.sh:
   * fix appending traces to existing Q file (see #2870)
 - obspy.io.xseed:
   * fix a bug reading SEED blockettes 48 and 58 which was likely never
     encountered (see #2668)
   * Properly read a given value of 0.0 in station elevation and not replace it
     with bogus value (see #2763)
 - obspy.signal.array_analysis
   * fixed an issue in array_processing function returning wrong times
     for matplotlib versions >= 3.3 due to the epoch change in matplotlib
     (see #2723)
 - obspy.signal.cross_correlation:
   * Remove deprecated xcorr function, remove deprecated domain keyword
     argument in correlate function (see #1979)
 - obspy.signal.spectral_estimation.PPSD:
   * Added special handling option for infrasound data and global infrasound
     noise models for plotting (see #2740)
   * Replaced use of deprecated Matplotlib functionality (see #2951)
 - obspy.signal.trigger:
   * Improved clarity and speed of several STA/LTA triggers methods, namely
     classic_sta_lta_py, z_detector, and recursive_sta_lta_py (see #2892)
   * Added simple AIC method by Maeda (1985)
```
