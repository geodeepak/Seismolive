![Logo](http://i.imgur.com/EnyL91L.png)


***NOT YET RELEASED - THIS DOCUMENT IS WORK IN PROGRESS!!***

This document details significant new features and changes in ObsPy `1.2.0`. The [Full Changelog](#full-changelog) at the end is more comprehensive. This release is based on around 50 individual contributors over the course of 15 months since the last major release `1.1.0`.

Documentation and resources for this version can (as always) be found at: https://docs.obspy.org

---

> Aside from the occasional change and new feature, there **never was any formal funding** for ObsPy and it has been developed by enthusiastic volunteers, mostly from academia. If you use ObsPy, please consider [acknowledging](https://github.com/obspy/obspy/wiki#acknowledging) us so we can justify investing time into it.

Work on this release was in parts and among others supported by the following
institutions/companies and grants (in alphabetical order):
 - Earthquake Commision of New Zealand (EQC), grant 18/753
 - École et Observatoire des Sciences de la Terre - Université de Strasbourg
 - ETH Zürich
 - Friedrich-Schiller-Universität Jena
 - Geoscience Australia
 - Incorporated Research Institutions for Seismology (IRIS), NSF (SAGE) award
   :: EAR-1851048
 - Institut de Physique du Globe de Strasbourg
 - Institut de Physique du Globe de Paris
 - Institutions for Seismology (IRIS) through the PASSCAL Instrument Center at
   New Mexico Tech. The facilities of the IRIS Consortium are supported by the
   National Science Foundation under Cooperative Agreement EAR-1261681 and the
   DOE National Nuclear Security Administration.
 - Istituto Nazionale di Geofisica e Vulcanologia, Osservatorio Etneo (Italy),
   Allegato B2 DPC-INGV 2012-2021 Task 10
 - Ludwig-Maximilians-Universität München
 - National Institute for Occupational Safety and Health
 - Royal Netherlands Meteorological Institute (KNMI)
 - School of Geography, Environment and Earth Sciences, Victoria University of
   Wellington
 - The European Union’s Horizon 2020 research and innovation programme under
   the ChEESE project, grant agreement No. 823844
 - The Royal Observatory of Belgium
 - U.S. Geological Survey


---

## Index

* [Supported Systems](#supported-systems)
* [Updating ObsPy](#updating-obspy)
* [Farewell Python2](#farewell-python2)
* [New Deprecations](#new-deprecations)
* [New Signal Processing Things](#new-signal-processing-things)
* [Notable Changes in obspy.core](#notable-changes-in-obspycore) 
* [Additional Support for Nordic Format](#additional-support-for-nordic-format)
* [Miscellaneous Notable Bug Fixes and Improvements](#miscellaneous-notable-bug-fixes-and-improvements)
* [Full Changelog](#full-changelog)

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

### Farewell Python2

ObsPy `1.2.0` will be the last version to support both Python 2 and 3. Right after the release all Python 2 compatibility will be removed from `master` branch. New features after `1.2.0` will only be released with Python 3 support. Please consider switching all your production code relying on ObsPy to Python 3 as soon as possible.

---

### New Deprecations
 * The `'domain'` keyword in the correlate function is deprecated in favor of the new `'method'` keyword to stay compatible with new SciPy versions.
* `obspy.core.UTCDateTime`: Deprecation warnings now occur when comparing attributes outside init or comparing different precisions.
* `obspy.core.convert_id_to_quakeml_uri`: Is being deprecated and replaced by `ResourceIdentifier` (see [#2303] (https://github.com/obspy/obspy/pull2303)) 
* `obspy.core.get_quakemk_uri` is being deprecated and replaced by `obspy.core.get_quakemk_uri_str`.

---

### New Signal Processing Things

 * New `correlate_template()` function with 'full' normalization useful for template matching.


---
### Notable Changes in obspy.core

* StationXML support has now been changed to versions 1.1 (see [#2510](https://github.com/obspy/obspy/pull/2510)) 

* Wildcard support for url and `read_inventory` was implemented (see [#2326] (https://github.com/obspy/obspy/pull/2326)).

* Support for selecting inventory with geographic locations was added (see [#2515] (https://github.com/obspy/obspy/pull/2515)).

---

### Additional Support for Nordic Format

The ability to read and write focal mechanisms as well as moment tensors in Nordic format was added.  It is also possible to convert between covariance matrix uncertainty to a confidence ellipsoid using `obspy.io.nordic.core.xyz_to_confidence_ellipsoid` as well as in the other direction using `obspy.io.nordic.core.confidence_ellipsoid_to_xyz`.  

---

###  Miscellaneous Notable Bug Fixes and Improvements 
* `obspy.signal.polarization` fixed an issue when selecting Z/N/E from a given trace (see [#2365] (https://github.com/obspy/obspy/pull/2365)).
* `obspy.signal.PPSD` fixed the check for whether new slices should be added or they would be unwanted duplicated data (see [#2229] (https://github.com/obspy/obspy/pull/2229)).
 
---

### Full Changelog

```
1.2.0: (doi: 10.5281/zenodo.3674646)
- obspy.core:
   * inventory objects have been adapted to StationXML 1.1 for details on
     changes see #2510 and
     https://github.com/FDSN/StationXML/blob/master/Changes.md
   * Fixed import of custom plugins (see #2423)
   * Fixed "==" comparison for Stream and Trace which was very slow in case of
     traces with >1e6 samples (see #2377)
   * Added almost_equal method for Stream and Trace classes (see #2286).
   * Casting FDSN identifiers to strings upon setting in the stats dictionary
     (see #1997).
   * UTCDateTime objects will now always evaluate equal if their string
     representations are equal (see #2049).
   * UTCDateTime objects now issue depreciation warnings when setting any
     attributes outside of init, or comparing UTCDateTime objects with
     different precisions (see #2077).
   * UTCDateTime objects can now accept hour, minute, second, and microsecond
     values greater than their normal limits by setting the strict keyword
     argument to False (see #2232).
   * fixed UTCDateTime(..., julday=366) for non-leap years. This was returning
     January 1st of the next year in case of non-leap years being used. Now it
     properly raises an out-of-bounds ValueError (see #2369)
   * When reading StationXML/SC3ML, make sure to properly read empty string
     fields as empty strings instead of "None" (see #2519 and #2527)
   * better ISO8601 detection for UTCDateTime objects and UTCDateTime(...,
     iso8601=False) now completely disables ISO8601 handling (see #2447)
   * Added replace method to UTCDateTime class (see #2077).
   * Added remove method to Inventory class (see #2088).
   * Added id property to WaveformStreamID (see #2131).
   * Added __str__ and _repr_pretty_ method for Comment class (see #2115)
   * Added __eq__ to QuantityError so empty instances equal None (see #2185).
   * Reworked the event scoped resource identifiers for the event classes
     hopefully fixing all edge-cases (see #2091).
   * Added a hook to allow users to customize finding objects for
     resource_ids which are not found via the normal means (see #2279).
   * Calling Stream.write(...) on an empty stream will now raise an
     ObsPyException consistently across all I/O plugins (see #2201)
   * Stream.get_gaps() will now properly report gaps within Traces that
     have masked arrays (i.e. Traces that have been merged without a fill
     value, see #2299 and #2300).
   * Added copy method to Inventory class (see #2322).
   * The Response.recalculate_overall_sensitivity() method now accepts integers
     (see #2338, #2343).
   * Added wildcard and url support to read_inventory (see #2326).
   * Modified stream.get_gaps() to deal with overlaps correctly (see #1403)
   * Added option "label_epoch_dates" to Inventory/Network.plot_response() to
     optionally add channel epoch start/end dates to legend labels (see #2309)
   * Deprecated the convert_id_to_quakeml_uri, regenerate_uuid, and
     get_quakeml_uri methods of the ResourceIdentifier class (see #2303).
   * Added get_quakeml_uri_str and get_quakeml_id methods to the
     ResourceIdentifier class (see #2303).
   * New method to create response objects directly from poles and zeros (see
     #1962).
   * Added Stream.stack method (see #2440).
   * Added a component field to the Stats object which allows to get and set
     the last character of the SEED channel (see #2484).
   * Fixed a bug in Stream.plot(type='section', reftime=..., ...) that caused
     wrong relative start times of traces relative to given reftime (see #2493)
   * Fixed a Windows-specific path case issue in a helper function that returns
     a list of untracked files in the git repository (see #2296)
   * Fix a bug that was causing an exception being raised in `Response.plot()`
     because a float was being passed down to numpy.linspace as length of array
     (see #2533)
   * Geographic select of inventory/network/station (see #2515)
 - obspy.clients.fdsn:
   * Add new `_discover_services` boolean flag to the Client, which allows the
     Client to skip the initial services query at instantiation.  This can
     reduce the load on service providers, but skips checks against unsupported
     query parameters.
   * Adding more location codes to the default priority list in the mass
     downloader (see #2155, #2159).
   * The mass downloader now raises a warning if all channels from a station
     have been deselected due to the default location priorities setting. This
     is a pure usability improvement as it has been confusing users
     (see #2159).
   * make sure that streams fetched via FDSN are properly trimmed to user
     requested times if data center serves additional data around the start/end
     (see #1887, #2298)
   * fix a problem that could spam subprocesses that were not closed in routed
     clients (see #2342 and #2344)
   * make it possible to use signed EIDA tokens and also skip token validation
     completely (see #2297)
   * adding a mapping for RASPISHAKE
 - obspy.clients.neic:
   * properly use specified timeout value (see #2450)
 - obspy.clients.seishub:
   * Properly handle fetching poles and zeros in presence of multiple metadata
     files for a given station (see #2411)
 - obspy.clients.seedlink:
   * add method "get_info()" to fetch information on what
     networks/stations/locations/channels are served by the seedlink server
     (see #2405)
   * "get_waveforms()" can now be used with '*' and '?' wildcards in any part
     of requested SEED ID, i.e. network, station, location and channel (see
     #2405)
 - obspy.clients.iris:
   * results of distaz method are now returned as native floats (see #2499)
 - obspy.geodetics:
   * new utility function `inside_geobounds()` to check whether an object is
     inside a geographic bound (see #2515)
 - obspy.imaging:
   * obspy-scan can now be used with wildcarded SEED IDs when specifying what
     to plot after scanning data (see #2227)
   * fix a problem in Scanner when loading npz on Python3 that was written on
     Python2 (see #2413)
   * fix an issue that could make small landmasses not get plotted in basemap
     plots (see #2471, #2477)
   * Fixed a bug in Stream.plot(type='section', reftime=..., ...) that caused
     wrong relative start times of traces relative to given reftime (see #2493)
 - obspy.io:
    * added read support for receiver gather format v. 1.6 (see #2070)
    * added read support for FOCMEC 'out' and 'lst' files (see #2156)
    * added read support for HypoDD 'pha' files (see #2378)
 - obspy.io.arclink:
   * Accommodate change in SeisComP3 publicID delimiter from '#' to '/' in
     ArclinkXML (see #2552)
 - obspy.io.dmx:
   * Add read support for INGV's DMX format (see #2452)
 - obspy.io.gcf:
   * Fixes Python 3.8 compatibility of GCF reader. (see #2505)
 - obspy.io.mseed:
   * Fix a bug resulting in an infinite loop when trying to read a FullSEED
     file without any data records (see #2534 and #2535)
   * Add ability to write int64 data to mseed if it can safely be downcast
     to int32 data, otherwise raises ObsPyMSEEDError. (see #2356)
   * The recordanalyzer can now detect calibration blockettes 300, 310,
     and 320 (see #2370).
   * Can now write zero sampling-rate traces. (see #2488, 2509)
 - obspy.io.nordic:
   * Add ability to read and write focal mechanisms and moment tensor
     information. (see #1924)
   * Add explicit warnings regarding unsupported sections of Nordic files.
   * Fix mapping of magnitude-types between MS to S and Ms to s.
   * Output preferred origin when writing to Nordic format instead of using
     the first origin (see #2195)
   * Include high-accuracy phase-pick reading and writing - high-accuracy is
     now the default phase-writing format, a boolean flag `high_accuracy`
     has been added to turn this off. (see #2351 and #2348)
   * Allow long-phase names (both reading and writing) - longer than 4 char.
     (see #2351)
   * Include AIN as takeoff-angle when reading and writing nordic files
     (see #2404).
   * Add error ellipses and read high-accuracy hypocenter lines (see #2451)
   * Fix the incorrect handling of events missing pick evaluation information
     (see #2520)
 - obspy.io.reftek:
   * Implement reading reftek encodings '16' and '32' (uncompressed data,
     16/32bit integers, see #2058 and #2059)
 - obspy.io.rg16:
   * implement module to read waveforms and headers from fcnt format (see #2265).
   * Fix reading when start+endtime are inside one data packet (see #2485).
 - obspy.io.seg2:
   * Handle data format code 3 trace data (#2022, #2385).
   * Improve parsing of free-form entries (#2385).
   * Fix non-native endian data loading (#2385).
 - obspy.io.segy:
   * show nice error message when trying to write a trace with too many samples
     in it (see #2358, #1393)
 - obspy.io.seiscomp:
   * Very large performance improvement reading large sc3ml inventory files by
     pre-indexing sensors, dataloggers and responses and reducing lxml calls
     (see #2296).
   * When reading StationXML/SC3ML, make sure to properly read empty string
     fields as empty strings instead of "None" (see #2519 and #2527)
 - obspy.io.stationxml:
   * When reading StationXML/SC3ML, make sure to properly read empty string
     fields as empty strings instead of "None" (see #2519 and #2527)
   * inventory objects have been adapted to StationXML 1.1 for details on
     changes see #2510 and
     https://github.com/FDSN/StationXML/blob/master/Changes.md
 - obspy.io.quakeml:
   * Allow writing invalid ids but raise a warning
     (see #2104, #2090, #2093, #1872).
   * Skip invalid enumeration values during reading but raise a warning.
     (see #2106, #2098, #2095)
   * Catalogs with empty event description objects can be round-tripped (see
     #2339, #2340).
   * Correctly handle QuakeML native namespaces (if they are not matching the
     document root's namespace) as custom namespaces and parse them into
     `.extra` (see #2466)
 - obspy.io.sac:
   * Fix bug writing inventory with SOH channels to SACPZ (see #2200).
 - obspy.io.segy:
   * Raise nicer error messages when header packing fails (see #2194, #2196).
 - obspy.io.seiscomp:
   * Adding support for SC3ML 0.10 (see #2024).
   * Update xsl to allow conversion of amplitude picks not associated with
     origins (see #2273).
 - obspy.io.sh:
   * Add read support for SeismicHandler EVT event files (see #2109)
 - obspy.io.shapefile:
   * Add possibility to add custom database columns when writing catalog or
     inventory objects to shapefile (see #2012 and #2305)
 - obspy.io.xseed:
   * Ability to parse SEED files with extra newlines between blockettes
     (see #2383)
 - obspy.signal.trigger:
    * fix a bug in AR picker (see #2157)
    * option to return Baer-Kradolfer characteristic function from pk_mbaer
      function added (see #2341)
 - obspy.signal.polarization:
   * Fix an issue in selecting Z/N/E traces from given stream (see #2365)
 - obspy.signal.PPSD:
   * Changed numpy-based serialization as to not require pickling (see #2424).
   * Fixed exact trace cutting for PSD segments (see #2040).
   * Timestamp representations internally and in npz I/O were changed to use
     integer nanosecond POSIX timestamps to avoid any potential floating point
     inaccuracies and since this is also what UTCDateTime is based on nowadays
     (see #2045).
   * Fixed the check for new PSD slices whether they should be added or whether
     they would add unwanted duplicated data (see #2229).
   * Fix `period_lim` option when `xaxis_frequency=True` (see #2246).
   * Added `allow_pickle` parameter to `PPSD.add_npz` and `PPSD.load_npz` and
     set its default to `False` (see #2457).
   * Added representation of earthquake models from Clinton & Heaton (2002) in
     'plot()' method using option 'show_earthquakes' (see #2455).
 - obspy.signal.cross_correlation:
   * Add new `correlate_template()` function with 'full' normalization option,
     required for correlations in template-matching
     (see #2035 and #2042).
   * 'domain' parameter in correlate function is deprecated in favour of new
     'method' parameter to be consistent with recent SciPy versions
     (see #2042).
   * Add `correlate_stream_template()` and `correlation_detector()`
     functions to detect events based on template matching (see #2315)
 - obspy.taup:
   * fix cycling through colors in ray path plots (see #2470, #2478)
   * fix a floating point issue on IBM machines (see #2559, #2560)
```
