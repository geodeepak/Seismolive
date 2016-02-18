![Logo](http://i.imgur.com/EnyL91L.png)

ObsPy has been in developed since 2008 and we now declare it stable enough to be called `1.0`. It is a big release with significant internal changes, new features, stability improvements, and much more to prepare ObsPy for future challenges and get rid of accumulated technical debt.

We strongly encourage all users to update to the new version as it will effectively end support for the `0.10.x` line.

---

> Aside from the occasional change and new feature, there never was any formal funding for ObsPy and it has been developed by enthusiastic volunteers. If you use ObsPy, please make sure to properly [acknowledge](https://github.com/obspy/obspy/wiki#acknowledging) us so we can justify investing time into it.

---


### Supported Systems

We officially support (meaning we test that they work with ObsPy; other versions - especially newer ones, might work, but we cannot guarantee that) the following systems.

Python modules: 

* `Python`: 2.7, 3.3, 3.4, 3.5 (we dropped support for 2.6 but added support for 3.5)
* `numpy`: 1.6 - 1.10 (minimum numpy is now 1.6)
* `scipy`: 0.9 - 0.17 (minimum scipy is now 0.9)
* `matplotlib`: 1.1 - 1.5
* `basemap`: 1.0.2 - 1.0.7

Supported Operating Systems (mostly 32bit and 64bit):

* `Windows` 
* `OSX`
* `Linux` (tested with default packages on CentOS/RedHat 7, Debian 7 + 8, Fedora 22 + 23, openSUSE 13.2 + Leap 42.1, Ubuntu 12.04 + 14.04 + 15.10)
* `Raspberry Pi`

### New Internal Structure

Over the years ObsPy has accumulated some cruft and technical debt. In this release we massively restructured ObsPy to ease maintenance to be able to tackle future challenges. A side effect of all these changes is that it might affect you - our users. We took great care to minimize these effects: **Everything that worked with ObsPy 0.10.2 should still work with ObsPy 1.0.0 but you might get a lot of warnings. Please adjust your code so no more warnings are raised so it will work with future ObsPy versions.**.

ObsPy is now structured as follows:

* `obspy.clients`: All modules retrieving data from the web or other resources.
* `obspy.core`: Core classes which are also restructured to yield smaller and more maintainable files.
* `obspy.io`: All modules reading and writing files in various formats.
* `obspy.geodetics`: Geographic utilities.
* `obspy.realtime`: Features for realtime seismogram analysis.
* `obspy.signal`: All signal processing functions and classes.
* `obspy.taup`: Theoretical arrival times using the tau-p method.

For example a script might yield the following output:

```bash
$ python some_obspy_script.py

/Users/lion/workspace/code/obspy/obspy/core/util/deprecation_helpers.py:57: ObsPyDeprecationWarning:
Function 'obspy.readEvents' is deprecated and will stop working with the next ObsPy version.
Please use 'obspy.read_events' instead.

/Users/lion/workspace/code/obspy/obspy/core/util/deprecation_helpers.py:68: ObsPyDeprecationWarning:
Module 'obspy.mseed' is deprecated and will stop working with the next ObsPy version.
Please import module 'obspy.io.mseed'instead.
```

Thus you should change

1. `obspy.readEvents()` to `obspy.read_events()`
2. `obspy.mseed` to `obspy.io.mseed`

and your code will continue to work with future ObsPy versions.

### Support for New Data Formats

ObsPy gained support for a few new data formats. They can be read by just using the normal `obspy.read()`, `obspy.read_events()`, and `obspy.read_inventory()` functions.

* **Support for additional waveform data formats:**
  - Read support for the ASCII format for waveforms from the K-NET and KiK-net strong-motion seismograph networks. See [documentation](http://docs.obspy.org/packages/obspy.io.nied.html).
* **Support for additional event data formats:**
  - CMTSOLUTION files used by many waveform solvers. See [documentation](http://docs.obspy.org/packages/obspy.io.cmtsolution.html).
  - ESRI shapefile write support, useful in GIS applications See [documentation](http://docs.obspy.org/packages/obspy.io.shapefile.html).
* **Support for additional station data format:**
  - The FDSN web service station text format can now be read. See [documentation](http://docs.obspy.org/packages/obspy.io.stationtxt.html).
  - Read support for the NIED's moment tensor TEXT format. See [documentation](http://docs.obspy.org/packages/obspy.io.nied.html).


### New Clients

With `1.0.0` ObsPy gained support for a couple of new local and remote data sources.

* **SDS file system structure**: The `obspy.clients.filesystem` module has a client to read data from SDS directory structure. Very useful for observatories. See [documentation](http://docs.obspy.org/packages/obspy.clients.filesystem.html)
* **Syngine**: The `obspy.clients.syngine` modules grants access to the [IRIS Syngine]() service. See [documentation](http://docs.obspy.org/packages/obspy.clients.syngine.html).
* Additionally we removed the old `obspy.neries` client. The same data can still be accessed with the `obspy.clients.fdsn` client.


### Mass Downloader for FDSN Web Services

ObsPy now contains a module to download and integrate data from any number of FDSN web services at once. Users only have to describe the geographic domain and what they want to download and it does it for them. If you routinely download data - check it out: http://docs.obspy.org/packages/autogen/obspy.clients.fdsn.mass_downloader.html

The following picture shows a possible domain restriction to only download data from within Germany:

<img src="https://raw.githubusercontent.com/wiki/obspy/obspy/images/mass_downloader_domain.png" width=70%>


### New Fancy Event Plots

If an event has moment tensors it can now be plotted in some fancy ways:

```python
from obspy import read_events
cat = read_events("/path/to/CMTSOLUTION")
ev = cat[0]
ev.plot()
```

<img src="https://raw.githubusercontent.com/wiki/obspy/obspy/images/fancy_event.png" width=70%>

If you have mayavi installed you can even get interactive three dimensional radiation patterns:

```python
ev.plot(kind="mayavi")
```

<img src="https://raw.githubusercontent.com/wiki/obspy/obspy/images/mayavi_radiation_pattern.png" width=70%>



### Rewritten SAC Module

The ObsPy SAC plugin has been rewritten, resulting in two changes in `obspy.read` and `Stream/Trace.write` using SAC files, and significant changes in the lower-level handling.  

**Changes in `obspy.read`**

1. The new SAC module will preserve the original `iztype` and reference time (if found in `Trace.stats.sac`), thus also preserving any existing relative time headers (e.g. travel-time picks).  This better supports round-trip SAC file processing.  The previous SAC module generally produced `iztype = ib` SAC files without checking the previous header `iztype`, which had the possibility of producing invalid relative time headers.  
2. `obspy.read` does not put unset SAC headers into `trace.stats.sac` unless `debug_headers=True` is set.  This is a change in default behavior.

**`SACTrace` replaces `SacIO`**

The recommended way of reading and writing SAC files is still using `obspy.read`, but users of `obspy.sac.SacIO` will need to be aware of changes.  The old `obspy.sac.sacio` has be rewritten and recycled into a new `obspy.io.sac` subpackage, and the old `SacIO` class is replaced by the `SACTrace` class, which provides a simplified I/O interface and more flexible reference time and relative-time header handling.

The previous `SacIO` I/O methods, `ReadSacFile`, `ReadSacHeader`, `ReadSacXY`, `ReadSacXYHeader`, `WriteSacBinary`, `WriteSacHeader`, and `WriteSacXY` are replaced by just two methods: `SACTrace.read` and `SACTrace.write`.  Reading and writing of header-only vs. full-file, ASCII vs. binary, and big vs little-endian byte order are controlled by keywords in these two methods.  Additionally, producing a `SACTrace` instance from a file does not require initializing an empty class instance first, as was required by `SacIO`.

```python
from obspy.io.sac import SACTrace

# read from a binary file
sac = SACTrace.read(filename)

# read or write header only
sac = SACTrace.read(filename, headonly=True)
sac.write(filename, headonly=True)

# read from an ASCII file, write a big-endian binary SAC file
sac = SACTrace.read(filename, ascii=True)
sac.write(filename, byteorder='big')
```

The new `SACTrace` class also has more flexible reference time and relative time header handling.  In `SACTrace`, the SAC reference time (a combination of `nzyear`, `nzjday`, `nzhour`, `nzmin`, `nzsec`, and `nzmsec`) can be accessed and manipulated through the `SACTrace.reftime` attribute (property), which is a `UTCDateTime` instance.  The reference time (or any of the relative time headers) can be modified by adding/subtracting seconds, or by setting it to a new `UTCDateTime` instance entirely.  Any changes to `reftime` will be reflected in the "nz" time headers, and will trigger corresponding changes in the relative time headers `a, e, f, t0-t9` such that they stay correctly referenced in absolute time.

```python
sac = SACTrace(nzyear=2000, nzjday=1, nzhour=0, nzmin=0, nzsec=0, nzmsec=0,
               t1=23.5, data=numpy.arange(100))
sac.reftime, sac.b, sac.e, sac.t1
# (2000-01-01T00:00:00.000000Z, 0.0, 99.0, 23.5)

# Move reference time by relative seconds, relative time headers are preserved.
sac.reftime -= 2.5
sac.reftime, sac.b, sac.e, sac.t1
# (1999-12-31T23:59:57.500000Z, 2.5, 101.5, 26.0)

# Set reference time to new absolute time, relative time headers are preserved.
sac.reftime = UTCDateTime(2000, 1, 1, 0, 2, 0, 0)
sac.reftime, sac.b, sac.e, sac.t1
# (2000-01-01T00:02:00.000000Z, -120.0, -21.0, -96.5)
```

Additionally, manually changing the `iztype` header will similarly preserve the absolute referencing of relative time headers.
