![Logo](http://i.imgur.com/EnyL91L.png)


It's has been too long but ObsPy 1.1.0 has finally arrived! It is a pretty big release accumulating changes across the code base by 36 unique contributors over the course of over 20 months! Thanks a lot to everyone involved!

In the future we plan to move to smaller, but more frequent, biannual releases.

We recommend all users to upgrade as it, aside from new features, contains a lot of bug fixes and smaller improvements and this release terminates the maintenance of the `1.0.x` line. Additionally there should be no breaking changes (aside the later mentioned now-actually-removed deprecated functions/imports).

This document details significant new features and changes in ObsPy `1.1.0`. The [Full Changelog](#full-changelog) at the end is more comprehensive.

Documentation and resources for this version can (as always) be found at: https://docs.obspy.org

---

## Index

* [Supported Systems](#supported-systems)
* [Updating ObsPy](#updating-obspy)
* [New Deprecations](#new-deprecations)
* [Deprecations are locked and loaded](#deprecations-are-locked-and-loaded)
* [Notable Changes in `obspy.core`](#notable-changes-in-obspycore)
* [NRL (Nominal Response Library) Client](#nrl-nominal-response-library-client)
* [`read_inventory()` support for (X)SEED and RESP files](#read_inventory-support-for-xseed-and-resp-files)
* [New Things Regarding Data Downloading](#new-things-regarding-data-downloading)
* [Quality Control Module](#quality-control-module)
* [New Signal Processing Things](#new-signal-processing-things)
* [Changes in `obspy.taup`](#changes-in-obspytaup)
* [Full Changelog](#full-changelog)

---

### Supported Systems

We officially support the following systems (meaning we test that they work with ObsPy; other versions - especially newer ones, might work, but we cannot guarantee that).

Python modules:

* `Python`: 2.7, 3.4, 3.5, 3.6 (dropped support for Python 3.3)
* `NumPy`: 1.6.2 - 1.13
* `SciPy`: 0.11.0 - 1.0 (minimum SciPy is now 0.11.0)
* `matplotlib`: 1.1.1 - 2.1
* `basemap`: 1.0.2 - 1.1.0

Supported Operating Systems (mostly 32bit and 64bit):

* `Windows`
* `OSX`
* `Linux` (tested with default packages on CentOS/RedHat 7, Debian 7 + 8 + 9, Fedora 25 + 26, openSUSE Leap 42.1 + 42.2, Ubuntu 14.04 + 16.04 + 17.10)
* `Raspberry Pi` (Raspbian Wheezy + Jessie + Stretch)

---

### Updating ObsPy

Updating should be straight-forward. So depending on your installation do

```bash
# Anaconda Python Distribution
$ conda update -c conda-forge obspy
```

```bash
# Generic Python
$ pip install -U obspy
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

* `obspy.io.datamark`: Renamed without deprectation to `obspy.io.win` to match its original name.
* `obspy.io.mseed.util.get_timing_and_data_quality()` is being deprecated and superseded by the `obspy.io.mseed.util.get_flags()` function.

---

### Deprecations are locked and loaded

Remember those pesky little warnings you might have been seeing for the past two years?

```bash
$ python some_obspy_script.py

/Users/lion/workspace/code/obspy/obspy/core/util/deprecation_helpers.py:57: ObsPyDeprecationWarning:
Function 'obspy.readEvents' is deprecated and will stop working with the next ObsPy version.
Please use 'obspy.read_events' instead.

/Users/lion/workspace/code/obspy/obspy/core/util/deprecation_helpers.py:68: ObsPyDeprecationWarning:
Module 'obspy.mseed' is deprecated and will stop working with the next ObsPy version.
Please import module 'obspy.io.mseed' instead.
```

Well - with this release all these deprecations are active, meaning that code that raises these warnings will no longer work and you will have to act on the warnings.

---

## Support for New Data Formats

To further our quest for world domination and the ability to gobble up every seismological data format in existence, this release adds support for or new features to the following file formats:

* **Waveform data formats:**
    * Read support for **Guralp Compressed Format (GCF)** waveform data (see [#1449](https://github.com/obspy/obspy/pull/1449)).
    * Read support for **Reftek 130 (rt130)** waveform data (see [#1433](https://github.com/obspy/obspy/pull/1433)).
    * **Write support for AH (Ad Hoc version 1)** format (see [#1754](https://github.com/obspy/obspy/pull/1754)).
    * Read support for **NNSA KB Core format** waveform data (see [#1332](https://github.com/obspy/obspy/pull/1332)).
    * **Iterative reading of large SEG-Y and SU files** (see [#1400](https://github.com/obspy/obspy/pull/1400)).

*  **Event data formats:**
    * Add **Nordic format (s-file) read/write** (see [#1517](https://github.com/obspy/obspy/pull/1517)).
    * **Read and write support for the SCARDEC catalog** format (see [#1391](https://github.com/obspy/obspy/pull/1391)).
	* **Read support for GSE2.0 bulletin** (see [#1528](https://github.com/obspy/obspy/pull/1528)).
	* **Read and write support for SC3ML event** (see [#1638](https://github.com/obspy/obspy/pull/1638) and [#1848](https://github.com/obspy/obspy/pull/1848)).


* **Station data formats:**
	* **SEED/RESP support for `obspy.read_inventory()`**.
	* **Read support for Arclink Inventory XML** (see [#1539](https://github.com/obspy/obspy/pull/1539)).
	* **Write support for stationtxt format** (see [#1466](https://github.com/obspy/obspy/pull/1466)).
	* **StationXML:**
		* Read and write support for custom tags (see [#1024](https://github.com/obspy/obspy/pull/1024)).
		* Level of detail can be specified during inventory write (see [#1830](https://github.com/obspy/obspy/pull/1830)).

---

### Notable Changes in `obspy.core`

* UTCDateTime is now based on nanosecond integers instead of a UNIX
  timestamp in microseconds (float) - resulting in higher precision and
  support for years 1-9999 (see [#1325](https://github.com/obspy/obspy/pull/1325))

* Event/ResourceIdentifiers are now object aware, meaning even if two
 objects share a `resource_id`, the distinct objects will be returned with
 the `get_referred_object()` method, provided both are still in scope
 (see [#1644](https://github.com/obspy/obspy/pull/1644)).

* `Stream/Trace.write()` can now autodetect file format from file extension
  (see [#1321](https://github.com/obspy/obspy/pull/1321)).

* A trace's `stats.network/station/location/channel` can now also be set in
  one line using a SEED ID string (e.g. `trace.id = "GR.FUR..HHZ"`,
  see [#1439](https://github.com/obspy/obspy/pull/1439)).

* `Stream.rotate(...)` can now also be used to rotate unaligned channels to
 Z-N-E, given an Inventory (see [#1310](https://github.com/obspy/obspy/pull/1310)).

---

### NRL (Nominal Response Library) Client

New client in `obspy.clients.nrl` to access the Nominal Response Library (NRL)
to get ObsPy `Response` objects (see [#1185](https://github.com/obspy/obspy/pull/1185)). Usage example:

```python
>>> from obspy.clients.nrl import NRL
>>> nrl = NRL()
>>> response = nrl.get_response(
...		sensor_keys=['Streckeisen', 'STS-1', '360 seconds'],
...     datalogger_keys=['REF TEK', 'RT 130 & 130-SMA', '1', '200'])
>>> print(response)
Channel Response
    From M/S (Velocity in Meters per Second) to COUNTS (Digital Counts)
    Overall Sensitivity: 1.50991e+09 defined at 0.020 Hz
    10 stages:
        Stage 1: PolesZerosResponseStage from M/S to V, gain: 2400
        Stage 2: ResponseStage from V to V, gain: 1
        Stage 3: CoefficientsTypeResponseStage from V to COUNTS, gain: 629129
        Stage 4: CoefficientsTypeResponseStage from COUNTS to COUNTS, gain: 1
        Stage 5: CoefficientsTypeResponseStage from COUNTS to COUNTS, gain: 1
        Stage 6: CoefficientsTypeResponseStage from COUNTS to COUNTS, gain: 1
        Stage 7: CoefficientsTypeResponseStage from COUNTS to COUNTS, gain: 1
        Stage 8: CoefficientsTypeResponseStage from COUNTS to COUNTS, gain: 1
        Stage 9: CoefficientsTypeResponseStage from COUNTS to COUNTS, gain: 1
        Stage 10: CoefficientsTypeResponseStage from COUNTS to COUNTS, gain: 1
```

---

### `read_inventory()` support for (X)SEED and RESP files

This finally unifies station information and response handling for all file
formats ObsPy can work with. ObsPy can now read (X)SEED and RESP files with
`obpsy.read_inventory()` (see [#1185](https://github.com/obspy/obspy/pull/1185)). A couple of things to note:

* RESP files don't store coordinates. They will thus be set to zero in the
  ObsPy objects.
* Malformed SEED/RESP responses will be interpreted in the way `evalresp`
  interprets them.
* Blockette 60 responses will be converted to their non-dictionary counterparts.

This, amongst other things, makes it a useful tool to convert your legacy data to modern StationXML files.

---

### New Things Regarding Data Downloading

#### FDSNWS Routing Clients

ObsPy now has support for two FDSNWS routing services:

* The [IRIS Federator](https://service.iris.edu/irisws/fedcatalog/docs/1/help/), and
* the [EIDA Routings](http://www.orfeus-eu.org/data/eida/webservices/routing/) service.

They support a similiar interface to the normal FDSN clients, but will query one of the routing services to figure out which data center has what data, before actually downloading the data. Usage example:

```python
>>> from obspy import UTCDateTime
>>> client = RoutingClient("iris-federator")  # Can also be "eida-routing".
>>> st = client.get_waveforms(
...     channel="LHZ", starttime=UTCDateTime(2017, 1, 1),
...     endtime=UTCDateTime(2017, 1, 1, 0, 5), latitude=10,
...     longitude=10, maxradius=25)
>>> print(st)
2 Trace(s) in Stream:
II.MBAR.00.LHZ | 2017-01-01T00:00:00Z - ... | 1.0 Hz, 300 samples
II.MBAR.10.LHZ | 2017-01-01T00:00:00Z - ... | 1.0 Hz, 300 samples
```

#### EIDA Token Authentication

(Experimental) support for [token based authentication](http://geofon.gfz-potsdam.de/waveform/archive/auth/auth-example.php) as implemented by many EIDA nodes (see [#1928](https://github.com/obspy/obspy/pull/1928)).


#### Mass Downloader

* The mass downloader now has `exclude_networks` and `exclude_stations`
 arguments to not download certain pieces of data. (see [#1305](https://github.com/obspy/obspy/pull/1305))
* The mass downloader can now download stations that are part of a given
 inventory object.
* The mass downloader now also works with restricted data. (See [#1350](https://github.com/obspy/obspy/pull/1350))

---

### Quality Control Module

There is a new `obspy.signal.quality_control` module to compute quality metrics from
MiniSEED files (see [#1141](https://github.com/obspy/obspy/pull/1141)). The calculated metrics are in accordance with the [EIDA WF Catalog Service](http://www.orfeus-eu.org/data/eida/webservices/wfcatalog/).

```python
>>> from obspy.signal.quality_control import MSEEDMetadata
>>> mseedqc = MSEEDMetadata(['path/to/file', 'path/to/file2'])
# Calculated metrics are available as
>>> mseedqc.meta
# Serialize to JSON with.
>>> mseedqc.get_json_meta()
```

---

### New Signal Processing Things

* New correlate function for calculating the cross-correlation function
  (new implementation based on Scipy). To calculate the shift of the
  maximum of the cross correlation use xcorr_max. The old xcorr function
  is deprecated but currently still exists (see [#1585](https://github.com/obspy/obspy/pull/1585)).
* New obspy.signal.regression module to compute linear regressions, with or
  without weights, with or without allowing for an intercept.
  (see [#1716](https://github.com/obspy/obspy/pull/1716), [#1747](https://github.com/obspy/obspy/pull/1747))
* add new plotting capabilities to PPSD (temporal variations per frequency
  and spectrogram-like plot) and also make underlying processed PSDs
  available via `PPSD.psd_values` property (see [#1327](https://github.com/obspy/obspy/pull/1327))

---

###  Changes in `obspy.taup`

* Add obspy.taup.taup_geo.calc_dist_azi, a function to return the distance,
  azimuth and backazimuth for a source - receiver pair. (see [#1538](https://github.com/obspy/obspy/pull/1538))
* Fixing calculations through very small regional models. (see [#1761](https://github.com/obspy/obspy/pull/1761))
* Updated ray path plot method, added travel time plot method, and wrapper
  functions for both ray path and travel time plotting. (see [#1501](https://github.com/obspy/obspy/pull/1501), [#1877](https://github.com/obspy/obspy/pull/1877))

---

### Full Changelog

```
master: (doi: 10.5281/zenodo.165135)
 - General:
   * Read support for Guralp Compressed Format (GCF) waveform data,
     obspy.io.gcf (see #1449)
   * Read support for Reftek 130 (rt130) waveform data,
     obspy.io.reftek (see #1433)
   * Add Nordic format (s-file) read/write (see #1517)
   * Read and write support for events in the SCARDEC catlogue format
     (see #1391).
   * Write support for AH (Ad Hoc version 1) format (see #1754)
   * Client to access the Nominal Response Library (NRL) (see #1185).
   * `obspy.read_inventory()` can now read dataless SEED and RESP files
     (see #1185).
   * change version number scheme for scenarios when no official version number
     can be determined (see #1889 and #1916)
   * Support for the IRIS Federator and EIDAWS FDSNWS web routing services
     (see #1779 and #1919).
 - obspy.core:
   * UTCDateTime is now based on nanoseconds (long) instead of a unix
     timestamp in microseconds (float) - resulting in higher precision and
     support for years 1-9999 (see #1325)
   * Ensure that Trace.data is always C-contiguous in memory (see #1732)
   * Event/ResourceIdentifier is now object aware, meaning even if two
     objects share a resource_id the distinct objects will be returned with
     the get_referred_object method provided both are still in scope. If one
     of the objects gets garbage collected, however, a warning will be issued
     and the behavior will be the same as before (see #1644).
   * Better error message when attempting to write invalid QuakeML resource
     ids (see #1699).
   * Stream/Trace.write() can now autodetect file format from file extension
     (see #1321).
   * New convenience property `.matplotlib_date` for `UTCDateTime` objects to
     get matplotlib datetime float representation (which can be used in
     time-based matplotlib axes, e.g. by Stream.plot(); see #1339).
   * Trace.times() has new options `type` and `reftime` to support fetching an
     array of sampletimes in various different timing varieties ("relative":
     the old default, float relative to trace starttime or `reftime` in
     seconds; "utcdatetime": absolute times as UTCDateTime objects;
     "timestamp": array of float POSIX timestamps, compare
     `UTCDateTime.timestamp`; "matplotlib": array of float matplotlib dates,
     useful for plotting on matplotlib time axes; see #1307)
   * A trace's stats.network/station/location/channel can now also be set in
     one line using a SEED ID string (e.g. `trace.id = "GR.FUR..HHZ"`,
     see #1439).
   * Instrument correction for response list stages originating from inventory
     objects (see #1514).
   * `Stream.rotate(...)` can now also be used to rotate unaligned channels to
     Z-N-E, given an Inventory (see #1310)
   * Non finite floats (NaN, inf, -inf) can now no longer be set for all
     event objects (see #1597).
   * Instrument responses can now also be calculated for a given list of
     frequencies (see #1598).
   * Order of extra tags for event type classes serialized to QuakeML can now
     be controlled by using an OrderedDict (see #1617)
   * Bode plots can now optionally plot the phase in degrees (see #1763).
   * `Stream.select()` now also works on the component level if channels only
     have one letter (see #1847).
 - obspy.clients.earthworm:
   * Much faster trace unpacking (see #1762).
 - obspy.clients.fdsn:
   * empty SEED codes (e.g. ``network=''``) will now be properly sent to the
     server as options and not omitted, which led to wildcard matching (for
     details see #1578)
   * The mass downloader now has `exclude_networks` and `exclude_stations`
     arguments to not download certain pieces of data. (see #1305)
   * The mass downloader can now download stations that are part of a given
     inventory object.
   * The mass downloader now also works with restricted data. (See #1350)
   * No data (HTTP 204) responses now raise `FDSNNoDataException` rather than
     the more general `FDSNException`.
   * Fixing cross implementation of bulk waveform and station requests (see
     #1685).
   * Adding mappings for the TEXNET (see #1852) and the ICGC (see #1902)
     services.
   * Support for the non-standard EIDA token authentication (see #1928).
 - obspy.imaging:
   * The functionality behind the `obspy-scan` command line script has been
     refactored into a `Scanner` class so that it can be reused in custom
     workflows. (see #1444)
 - obspy.imaging.cm:
   * new colormap: viridis_white. This is a modification of viridis that
     goes to white instead of yellow but remains perceptually uniform. It
     is especially useful for printing when an image should merge with the
     white background.
 - obspy.imaging.waveform:
   * Support for filling the wiggles when plotting sections (horizontal and
     vertical, see #1445).
 - obspy.io.arclink:
    * Read support for Arclink Inventory XML (see #1539)
 - obspy.io.ascii:
    * Custom formatting of sample values when writing SLIST and TSPAIR.
 - obspy.io.datamark:
    * Renamed without deprectation to obspy.io.win to match its original name.
      Datamark is a datalogger, saving the WIN format.
 - obspy.io.gse2:
    * Read support for GSE2.0 bulletin (see #1528)
 - obspy.io.nlloc:
    * Also parse author information and COMMENT line (see #1484)
    * Fix reading hypocenter files created by NonLinLoc versions of the 6.0.x
      beta branch (see #1760 and #1783)
 - obspy.io.quakeml:
    * Read and write support for nested custom tags (see #1463)
    * Fix some minor bugs that could lead to empty stub elements, e.g. like
      empty MomentTensor when reading and later writing again a QuakeML file
      with a FocalMechanism but no MomentTensor, potentially resulting in
      QuakeML files that breach the QuakeML schema (see #1896)
 - obspy.io.seiscomp:
    * Read and write support for SC3ML event (see #1638 and #1848)
    * Fix bug where files with arbitrary publicIDs and files with missing
      depth, latitude, longitude, or elevation tags could not be read
      (see #1817)
 - obspy.io.stationtxt:
    * Write support for stationtxt format (see #1466)
 - obspy.io.stationxml:
    * Read and write support for custom tags (see #1024)
    * No longer add the (unused) time zone field to StationXML datetimes to
      follow the example of big data centers. (see #1572)
    * Level of detail can be specified during inventory write (see #1830)
      using the level keyword (one of: network, station, channel, response).
    * Skip empty and incomplete channels during reading (see #1839, #1840).
 - obspy.io.segy:
    * Fixing an issue when comparing two still packed SEG-Y trace headers
      (see #1735).
    * Iterative reading of large SEG-Y and SU files with
      `obspy.io.segy.segy.iread_segy` and `obspy.io.segy.segy.iread_su`.
      (see #1400).
    * Write correct revision number (see #1737).
    * Textual headers will now always contain the file revision number and the
      end header mark if nothing else exists at these positions (see #1738).
    * The SEG-Y format detection now also checks the format version number
      (see #1781).
    * Enable reading SEG-Y files that have day of year 0 in trace header
      (see #1722).
    * Write textual file headers also if given as a text string
      (see #1811, #1813).
 - obspy.io.css:
   * Read support for NNSA KB Core format waveform data. (see #1332)
 - obspy.io.mseed:
   * New generic get_flags() utility function able to retrieve statistics
     about all fixed header flags and the timing quality. This makes the
     get_timing_and_data_quality() function obsolete which is thus
     deprecated and will be removed with the next release. The get_flags()
     function is also much faster. (see #1141)
   * Always hook up the libmseed logging to its Python counterpart to avoid
     some rare segfaults. (see #1658)
   * Update to libmseed v2.19.4 (see #1703, #1780).
   * Correctly read MiniSEED files with a data offset of 48 bytes (see #1540).
   * InternalMSEEDReadingError now called InternalMSEEDError and
     InternalMSEEDReadingWarning now called InternalMSEEDWarning as both
     can now also be raised in non-reading contexts (see #1658).
   * Should no-longer segfault with arbitrarily truncated files (see #1728).
   * Will now raise an exception when attempting to directly read mini-SEED
     files larger than 2048 MiB (#1746).
   * `.stats.mseed` attributes are no longer per-file but per-trace where
     applicable (see #1782).
   * `get_record_information()` - Don't fail if the word order is invalid.
 - obspy.io.nlloc:
   * Set preferred origin of event (see #1570)
 - obspy.io.nordic:
   * Add Nordic format (s-file) read/write (see #1517)
 - obspy.io.win:
   * see obspy.io.datamark.
 - obspy.io.xseed:
   * Added azimuth and dip to the get_coordinates() function. (see #1315)
   * Fixing some issues with the get_resp() output on Python 3 (see #1748).
   * Can now also parse RESP files (see #1185).
   * Can transform responses in the Parser object to ObsPy Inventory objects
     (see #1185).
 - obspy.scripts:
   * obspy-scan command line script now also plots and prints overlaps
     alongside gaps (see #1366)
   * obspy-plot now has option to disable min/max plot (see #1583)
 - obspy.signal:
   * fixed a bug in calibration.rel_calib_stack (resulting amplitude response
     had wrong scaling if using non-default "overlap_fraction", see #1821)
   * fixed a bug in coincidence_trigger() with event templates. when a template
     with mismatching SEED ID was encountered all following (potentially valid)
     templates were skipped as well (see #1850)
   * New obspy.signal.quality_control module to compute quality metrics from
     MiniSEED files. (see #1141)
   * New correlate function for calculating the cross-correlation function
     (new implementation based on Scipy).
     To calculate the shift of the maximum of the cross correlation use
     xcorr_max. The old xcorr function is deprecated but currently still
     exists (see #1585).
   * New obspy.signal.regression module to compute linear regressions, with or
     without weights, with or without allowing for an intercept. (see #1716,
     #1747)
   * add new plotting capabilities to PPSD (temporal variations per frequency
     and spectrogram-like plot) and also make underlying processed PSDs
     available via `PPSD.psd_values` property (see #1327)
   * Fixed bug in `rotate2zne()` for non-orthogonal configurations
     (see #1913, #1927).
 - obspy.taup:
   * Add obspy.taup.taup_geo.calc_dist_azi, a function to return the distance,
     azimuth and backazimuth for a source - receiver pair. (see #1538)
   * Fixing calculations through very small regional models. (see #1761)
   * Updated ray path plot method, added travel time plot method, and wrapper
     functions for both ray path and travel time plotting. (see #1501, #1877)
```
