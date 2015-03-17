![Logo](http://i.imgur.com/EnyL91L.png)

ObsPy 0.10.0 is once again our biggest release yet with over 2200 single commits from 25 individual contributors. Great work everyone!

We strongly encourage all users to update to the new version as it will effectively end support for the 0.9.x line.

---

> Aside from the occasional change and new feature, there never was any formal funding for ObsPy and it has been developed by enthusiastic volunteers. If you use ObsPy, please make sure to properly [acknowledge](https://github.com/obspy/obspy/wiki#acknowledging) us so we can justify investing time into it.

---


## Major New Features

This section highlights the main new features; the full changelog including a long list of other changes is at the end of this post. Make sure to check it out!

### Python 3 Support

ObsPy now supports Python 3.3 and 3.4 in addition to the existing support of Python 2 - all from a single code base! The Python ecosystem is now in a state where Python 3 is slowly becoming the recommended Python version. If you start a new project or script, give Python 3 a shot!

### Anaconda Support

With all the changes in the new ObsPy version we are finally able to offer (Ana)conda packages for all platforms and Python versions. This might seem small but this is a huge time and problem saver when installing ObsPy and other scientific Python packages. Thus this is now the recommended way to install ObsPy. You only need to download Anaconda/Miniconda and then you can simply install ObsPy including all dependencies by running:

```bash
$ conda install -c obspy obspy
```

### New TauP implementation

We replaced the old `ttimes` wrapper with a port of the Java TauP toolkit. Aside from finally getting rid of Fortran in our code base this also comes with a slew of new features like the calculation of arbitrary seismic body wave phases including ray paths and pierce points. Checkout the [documentation](http://docs.obspy.org/packages/obspy.taup.html) and the [tutorial](http://docs.obspy.org/tutorial/code_snippets/travel_time.html) for more details.

![TauP](http://i.imgur.com/V9MpXja.png)

### New Formats

ObsPy's biggest draw has always been its unified and comprehensive file format support. We therefore happily welcome a bunch of new formats into our growing family:

| Format   | Description                                                                               |
|----------|-------------------------------------------------------------------------------------------|
| AH       | Read support for the Ad Hoc waveform format of the Lamont-Doherty Geological Observatory. |
| CNV      | Write support for the CNV event summary format used by the VELEST program.                |
| NDK      | Read support for the NDK files distributed by the GCMT project.                           |
| Datamark | Read support for the DataMark waveform format.                                            |
| NLLOC    | Read/Write support for the NonLinLoc file formats.                                        |
| PDAS     | Read support for PDAS waveform files.                                                     |
| ZMAP     | Read/Write support for ZMAP event file format.                                            |


### Fully LGPLv3 licensed Code

This is the first release where all code is officially under the LGPLv3 license.

### Supported Platforms

ObsPy 0.10.0 is compatible with Python `2.6`, `2.7`, `3.3`, and `3.4` and `numpy >= 1.4.0` and `scipy >= 0.7.2`.

We officially support (meaning we test on these platforms; it will likely work on others as well):

* Anaconda on all platforms (Linux 32bit/64bit, OSX, and Windows 32bit/64bit)
* Official Python for Windows from python.org
* OSX Homebrew and MacPorts
* CentOS 6 and 7 (and by extension RHEL 6 and 7)
* Debian 6 (Squeeze), 7 (Wheezy), and 8 (Jessie)
* Fedora 20 and 21
* OpenSUSE 13.1 and 13.2
* Ubuntu 12.04, 14.04, and 14.10

The next major ObsPy Release (ObsPy 0.11.0) will drop support for 

* `Python < 2.7`
* `matplotlib < 1.1`
* `numpy < 1.6`
* `scipy < 0.10`

so make sure to update your system in due time if you run one of these old versions.

## Migration Guide

Code that runs without any warnings on ObsPy 0.9.2 should continue to work just fine under ObsPy 0.10.0. If you update from an even older version you might have to adjust the `Stream/Trace.taper()` calls to the new syntax:

```python
st.taper(max_percentage=0.05, type="hann")
```

## Contributors

Thanks a bunch to everyone who made this possible! Contributors responsible for the changes in 0.10.0 in alphabetical order:

* Benjamin Sullivan
* Bernhard Morgenstern
* Claudio Satriano
* Elliott Sales de Andrade
* Emanuel Antunes
* Henri Martin
* Joachim Wassermann
* John Leeman
* Laura Ermert
* Leonardo Uieda
* Lion Krischer
* Lukas Heiniger
* Marc Grunberg
* Marius Isken
* Mark Williams
* Mortiz Beyreuther
* Nicolas Rothenhäusler
* Paul Kaeufl
* Robert Barsch
* Sébastien Bonaimé
* sfieux
* Thomas Lecocq
* Tobias Megies
* Tommaso Fabbri
* Yannik Behr


## Full Changelog

- Highlights:
  * Python3 support
  * anaconda support
  * New formats: AH, CNV, NDK, Datamark, NLLOC, PDAS, ZMAP
  * ObsPy licensed under LGPL v3.0 now as a whole.
- General:
  * Support for Python 3.3 and 3.4 in addition to 2.6 and 2.7
  * ObsPy licensed under LGPL v3.0 now as a whole.
  * More generic processing history for most Stream and Trace methods.
  * Now requires NumPy >= 1.4.0
  * Now requires SciPy >= 0.7.2
  * Tested compatibility with most major Linux distributions still receiving updates.
  * The next major obspy release (0.11) will drop support for:
    * Python < 2.7
    * matplotlib < 1.1
    * numpy < 1.6
    * scipy < 0.10
- obspy.ah
  * New submodule for reading the AH (Ad Hoc) waveform format
- obspy.kinemetrics
  * New submodule for reading the Kinemetrics EVT waveform format
- obspy.arclink:
  * add support for Poles and Zeros type "B" (Analog, Hz), see #899
- obspy.core:
  * Preview waveform plot improved: interactive updating of ticks and ticklabels, correct ticklabels for sub-minute zoom level (#657)
  * fixed a problem with UTCDateTime with timestamps of far future dates (larger than 2038, often seen in StationXML end dates, see #805)
  * Support for basic custom namespace tags in QuakeML I/O (see #454) 
  * `interpolate()` method for Stream/Trace objects.
  * Dictionary values added to an AttribDict will now be converted to an AttribDict.
  * Removed custom OrderedDict backport for Python 2.6. Now relies on the one provided by the future package.
  * Renamed 'type' argument to 'method' in the Trace.differentiate() method.
  * Renamed 'type' argument to 'method' in the Trace.integrate() method. Additionally, several broken alternate methods have been removed.
  * new plugins for NonLinLoc formats for readEvents() and Catalog/Event.write() (see obspy.nlloc and #900)
  * The wrap_long_string utility function is deprecated. Users may use the textwrap module which provides similar functionality.
  * new plugin for CNV event format (used by VELEST) for Catalog/Event.write() (see obspy.cnv and #905)
  * better customizable control during merging traces with sub-sample shift of sampling points (see #980)
- obspy.cnv:
  * new plugin to write CNV event files (used by VELEST) from Catalog/Event objects. (see #905)
- obspy.css:
  * Support for little-endian binary and ASCII files (see #881).
  * Support exporting Inventory objects to CSS relations.
- obspy.fdsn:
  * WADL files are cached per Python process.
  * Bulk station downloading using POST requests.
  * Support for FDSNWS 1.1, e.g. the `matchtimeseries` parameter for the station service.
- obspy.imaging:
  * Maintain beach ball aspect ratio through optional axes argument (see #734)
  * Refactored Catalog.plot() into helper routine `obspy.imaging.maps.plot_basemap()` (see #753).
  * The projections of Catalog.plot() have been modified slightly to provide equal-area projections:
    * The `"cyl"` projection is now named `"global"`. It is now the Mollweide projection.
    * The '"local"` projection now uses the Albers Equal Area projection.
- obspy.mseed:
  * Support for reading and writing all encodings supported by libmseed.
  * proper error reporting while reading
  * `details=True` when reading will now write to `Trace.stats.mseed.blkt1001.timing_quality` instead of `Trace.stats.mseed.timing_quality`.
  * The timing quality will now also be written to a file if it is set.
  * Non-existing values when reading with `details=True` will now be set to `False` instead of `-1`.
  * New utility function `obspy.mseed.util.set_flags_in_fixed_header()` giving the ability to overwrite flags in the fixed header of existing MiniSEED files.
  * The sequence number of the first record of each Trace can now be specified when writing MiniSEED files.
  * `obspy-mseed-recordanalyzer`:
      - Bugfix: when specifying an out-of-bounds record number, information about the last record in the file was displayed (see #957). Now a proper error message is shown and the command line script exits with non-zero exit code.
      - Faster reading of a single record header
      - Added option "-a" to print information of all records
  * upgrade to libmseed 2.15
- obspy.ndk:
  * New submodule able to read NDK files from the Global CMT project.
- obspy.neries:
  * The whole module is deprecated and will be removed with the next major release. To access EMSC event data please use the obspy.fdsn client (use `Client(base_url='NERIES', ...)`), for access to ORFEUS waveform data please use the obspy.fdsn client (use `Client(base_url='ORFEUS', ...)`) and for travel times please use obspy.taup.
- obspy.nlloc:
  * new plugins to write NonLinLoc Phase observations files from Catalog/Event objects and to read NonLinLoc Hypocenter-Phase file into Catalog/Event objects. (see #900)
- obspy.pdas:
  * read support for PDAS waveform files
- obspy.sac:
  * New `byteorder` option for writing sac files to disk.
  * Can now read/write from/to file-like objects like io.BytesIO and open files.
- obspy.seedlink:
  * bugfix: INFO responses from the IRIS ringserver are now parsed correctly (see #807)
  * New submodule `easyseedlink` providing an easier way to create SeedLink clients
  * New `Client` class providing a basic seedlink client for individual requests of finite time windows (i.e. non-continuous programs)
  * Fix memory leak in `SLClient` (MiniSEED record leak in packet parser, see #918)
- obspy.seisan:
  * bugfix the actual data were misaligned by one
- obspy.seishub:
  * use specified timeout in all requests to server (see #786)
  * Helper method `Client.event.getEvents()` to fetch a `Catalog` object from a seishub server of version 1.4.0 or higher.
- obspy.signal:
  * Increased performance of PPSD plotting.
  * Interpolating methods. Wrappers around routines from scipy and a custom `weighted average slopes` method from Wiggins 1976.
  * PPSD has new methods to extract mean and mode of the histogram by frequency (see #804)
  * PPSD: water level in instrument correction can now be specified by user on PPSD initialization
  * New polarization analysis methods: flinn, vidale, pm
- obspy.station:
  * add plotting methods (response/bode, location maps) to Inventory/Station/Channel/Response objects (see #750)
  * add `get_coordinates()` method to inventory and network objects (see #740)
  * read/write support for DataAvailability tags in StationXML files.
  * write support for SACPZ ASCII representation of channel responses.
- obspy.xseed:
  * add support for Poles and Zeros type "B" (Analog, Hz), see #899
- obspy.zmap:
  * New module which adds ZMAP read/write support
- obspy.taup:
  * replaced fortran implementation through much more powerfull python port of java taup. This enabled us to drop all fortan code, which simplifies releases and builds tremendously.
- scripts:
  * All scripts now require argparse instead of optparse.
  * All scripts now accept -V or --version to print version information.
  * obspy-dataless2xseed: -v and --version options are renamed to -x and --xml-version to not conflict with above option.
  * obspy-indexer: Options have been modified or amended slightly:
    * --data is a new alias to -d.
    * --db-uri is a new alias to -u.
    * --log is a new alias to -l.
    * --poll-interval is a new alias to -i.
    * --recent is a new alias to -r.
    * -a is a new alias to --all-files.
    * -f is a new alias to --force-reindex.
    * -H is a new alias to --host.
    * -p is a new alias to --port.
    * --check_duplicates is renamed to --check-duplicates.
    * --drop_database is renamed to --drop-database.
    * --mapping_file is renamed to --mapping-file.
    * --run_once is renamed to --run-once.
  * obspy-mopad: Options have been modified or amended slightly:
    * convert subcommand:
      * No changes.
    * decompose subcommand:
      * --input_system is renamed to --input-system.
      * --output_system is renamed to --output-system.
    * gmt subcommand:
      * --show_1fp is renamed to --show-1fp.
      * --show_isotropic_part is renamed to --show-isotropic-part.
    * plot subcommand:
      * --basis_vectors is renamed to --basis-vectors.
      * --full_sphere is renamed to --full-sphere.
      * --input_system is renamed to --input-system.
      * --lines_only is renamed to --lines-only.
      * --output_file is renamed to --output-file.
      * --pa_system is renamed to --pa-system.
      * --pressure_colour is renamed to --pressure-colour.
      * --show1fp is renamed to --show-1fp.
      * --show_isotropic_part is renamed to --show-isotropic-part.
      * --tension_colour is renamed to --tension-colour.
  * obspy-plot: --format option is accepted as an alias of -f.
  * obspy-print: Options have been modified or amended slightly:
    * --format is a new alias of -f.
    * --nomerge is renamed to --no-merge.
  * obspy-runtests: -a option is accepted as an alias of --all.
  * obspy-scan: Options have been modified or amended slightly:
    * --endtime is renamed to --end-time.
    * --event-times is renamed to --event-time. --event-time may be specified multiple times.
    * --ids is renamed to --id. --id may be specified multiple times.
    * --nox is renamed to --no-x.
    * --nogaps is renamed to --no-gaps.
    * --starttime is renamed to --start-time.
