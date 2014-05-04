<img class="right" style="width: 60%" src="https://raw.github.com/obspy/website/master/logo/obspy_logo_full_highres.png" />

[![Build Status](https://secure.travis-ci.org/obspy/obspy.png?branch=master)](https://travis-ci.org/obspy/obspy)
[![PEP8 Status](https://www.obspy.org/pep8.png)](http://pep8.obspy.org)
[![Coverage Status](https://coveralls.io/repos/obspy/obspy/badge.png?branch=master)](https://coveralls.io/r/obspy/obspy?branch=master)
[![PyPI Version](https://pypip.in/v/obspy/badge.png)](https://crate.io/packages/obspy/)
[![Downloads](https://pypip.in/d/obspy/badge.png)](https://crate.io/packages/obspy/)

ObsPy is an open-source project dedicated to provide a **Python framework for processing seismological** data. It provides parsers for common file formats, clients to access data centers and seismological signal processing routines which allow the manipulation of seismological time series (see [Beyreuther et al. 2010](http://www.seismosoc.org/publications/SRL/SRL_81/srl_81-3_es/), [Megies et al. 2011](http://www.annalsofgeophysics.eu/index.php/annals/article/view/4838)).

The goal of the ObsPy project is to facilitate **rapid application development for seismology**.

## News
##### [May 4 2014] Release of ObsPy 0.9.2
ObsPy 0.9.2 is a maintenance release and contains the collective bug fixes and minor feature improvements of around 150 commits so we advise all users to upgrade.

Full changelog: https://github.com/obspy/obspy/releases/tag/0.9.2
##### [January 9 2014] Release of ObsPy 0.9.0
ObsPy 0.9.0 offers (amongst many other things) two major new features: support for the FDSN webservices and the FDSN StationXML format.
* [Release including full changelog](../releases/tag/0.9.0)
* [Migration guide to ObsPy 0.9.0](wiki/Migration-to-ObsPy-0.9.0)


## Getting Started

The [ObsPy Gallery](http://gallery.obspy.org) and its related [ObsPy Tutorial](http://tutorial.obspy.org) are maybe the best point to get a first impression of what ObsPy is all about. The tutorial is a collection of short example programs with explanations and program output. For help getting started with Python, have a look at this [collection of links to Tutorials](wiki/Python-Tutorials).

## Installation
ObsPy is currently [running and tested](http://tests.obspy.org) on Linux (32 and 64 bit), Windows XP/Vista/7/8 (32 bit and/or 64 bit) and Mac OS X (32 and 64 bit Intel and untested support for 32 and 64 bit PPC).

These notes describe installing ObsPy on the following platforms:

* [[Linux|Installation on Linux]]
* [[Mac OS X|Installation on Mac OS X]]
* [[Windows|Installation on Windows]]
* [[FreeBSD|Installation on FreeBSD]]

If you intend on performing parallel processing with Python and Obspy, please read the following.
* [[Notes on Parallel Processing with Python and ObsPy|Notes on Parallel Processing with Python and ObsPy]]

## Stay Informed

If you are using ObsPy we **strongly recommend** you to join the [ [obspy-announcements] ](http://lists.obspy.org/listinfo/obspy-announcements) and the [ [obspy-users] ](http://lists.obspy.org/listinfo/obspy-users) mailing lists. The **[obspy-announcements]** list will be the place where new additions, important changes and bug fixes will be announced and thus will be very low volume. The **[obspy-users]** list is used to contact other ObsPy users for questions and open discussions.

#### [obspy-announcements]

  * [Subscribe](mailto:obspy-announcements-request@lists.swapbytes.de?subject=subscribe&body=Send%20this%20message%20from%20the%20address%20you%20want%20to%20subscribe.) / [Unsubscribe](mailto:obspy-announcements-request@lists.swapbytes.de?subject=unsubscribe&body=Send%20this%20message%20from%20the%20address%20you%20want%20to%20unsubscribe.)
  * [Browse the archive](http://lists.obspy.org/pipermail/obspy-announcements/)

#### [obspy-users]

  * [Subscribe](mailto:obspy-users-request@lists.swapbytes.de?subject=subscribe&body=Send%20this%20message%20from%20the%20address%20you%20want%20to%20subscribe.) / [Unsubscribe](mailto:obspy-users-request@lists.swapbytes.de?subject=unsubscribe&body=Send%20this%20message%20from%20the%20address%20you%20want%20to%20unsubscribe.)
  * [Post a message](mailto:users@obspy.org)
  * [Browse the archive](http://lists.obspy.org/pipermail/obspy-users/)

There also is a [feed for commits](https://github.com/obspy/obspy/commits/master.atom). To get emails concerning issues make a GitHub login, 'watch' our repository and set up email notifications for your GitHub account.

## [Documentation](http://docs.obspy.org)
_Note: Documentation for current master snapshot can be found [here](http://docs.obspy.org/master)_

### General packages:
* [obspy.core](http://docs.obspy.org/packages/obspy.core.html) - ObsPy core package, glues the single obspy packages together. Includes support for event data and QuakeML.
* [obspy.imaging](http://docs.obspy.org/packages/obspy.imaging.html) - Imaging spectograms, beachballs and waveforms
* [obspy.realtime](http://docs.obspy.org/packages/obspy.realtime.html) - Extends the ObsPy core classes with real time functionalities (''experimental'')
* [obspy.signal](http://docs.obspy.org/packages/obspy.signal.html) - Filters, triggers, instrument correction, rotation, array analysis, beamforming
* [obspy.station](http://docs.obspy.org/packages/obspy.station.html) - Support for [FDSN StationXML](http://www.fdsn.org/xml/station/) (experimental)
* [obspy.taup](http://docs.obspy.org/packages/obspy.taup.html) - Calculates and visualizes travel times
* [obspy.xseed](http://docs.obspy.org/packages/obspy.xseed.html) - Converter for Dataless SEED, [XML-SEED](http://adsabs.harvard.edu/abs/2004AGUFMSF31B..03T) and SEED RESP files

### Waveform import/export plug-ins:
* [obspy.css](http://docs.obspy.org/master/packages/obspy.css.html) - CSS read support
* [obspy.datamark](http://docs.obspy.org/packages/obspy.datamark.html) - DATAMARK read support
* [obspy.gse2](http://docs.obspy.org/packages/obspy.gse2.html) - GSE2 and GSE1 read and write support
* [obspy.mseed](http://docs.obspy.org/packages/obspy.mseed.html) - MiniSEED read and write support
* [obspy.sac](http://docs.obspy.org/packages/obspy.sac.html) - SAC read and write support
* [obspy.seisan](http://docs.obspy.org/packages/obspy.seisan.html) - SEISAN read support
* [obspy.seg2](http://docs.obspy.org/packages/obspy.seg2.html) - SEG2 read support
* [obspy.segy](http://docs.obspy.org/packages/obspy.segy.html) - SEGY read and write support
* [obspy.sh](http://docs.obspy.org/packages/obspy.sh.html) - Q and ASC read and write support (file formats of [SeismicHandler](http://www.seismic-handler.org))
* [obspy.wav](http://docs.obspy.org/packages/obspy.wav.html) - WAV (audio) read and write support
* [obspy.y](http://docs.obspy.org/packages/obspy.y.html) - Nanometrics Y file format read support (experimental)

### Database or Web service access clients:
* [obspy.arclink](http://docs.obspy.org/packages/obspy.arclink.html) - [ArcLink/WebDC](http://www.webdc.eu) request client
* [obspy.earthworm](http://docs.obspy.org/packages/obspy.earthworm.html) - [Earthworm](http://folkworm.ceri.memphis.edu/ew-doc/) request client
* [obspy.fdsn](http://docs.obspy.org/packages/obspy.fdsn.html) - [FDSN Web services](http://www.fdsn.org/webservices/) request client (experimental)
* [obspy.iris](http://docs.obspy.org/packages/obspy.iris.html) - [IRIS DMC Core Web services](http://www.iris.edu/ws) request client (deprecated since December 2013. Use obspy.fdsn instead.)
* [obspy.neic](http://docs.obspy.org/master/packages/obspy.neic.html) - [NEIC](http://earthquake.usgs.gov/regional/neic/) CWB QueryServer request client (experimental)
* [obspy.neries](http://docs.obspy.org/packages/obspy.neries.html) - [NERIES Seismic Data Portal](http://www.seismicportal.eu/jetspeed/portal/) request client
* [obspy.seedlink](http://docs.obspy.org/packages/obspy.seedlink.html) - [SeedLink](http://www.seiscomp3.org/wiki/doc/applications/seedlink) request client (experimental / not well tested)
* [obspy.seishub](http://docs.obspy.org/packages/obspy.seishub.html) - [SeisHub](https://github.com/barsch/seishub.core) database client

## Use Cases / Applications Using ObsPy

   * [ObsPyck](https://github.com/megies/obspyck/wiki)
   * [SeismicHandler](http://www.seismic-handler.org)
   * [SeisHub](https://github.com/barsch/seishub.core)
   * [SeishubExplorer](https://github.com/krischer/SeishubExplorer)
   * [HtoVToolbox](https://github.com/krischer/HtoV-Toolbox)
   * [StreamPick](https://github.com/miili/StreamPick)
   * [Antelope Python moment tensor code](http://eqinfo.ucsd.edu/~rnewman/howtos/antelope/moment_tensor/)
   * [Running ObsPy in a PiCloud](http://blog.picloud.com/2011/09/26/introducing-environments-run-anything-on-picloud/)
   * [Using ObsPy with py2exe](http://www.geophysique.be/en/2011/08/09/using-obspy-modules-with-py2exe/)
   * [Whisper](http://code-whisper.isterre.fr/html)
   * [Wavesdownloader](http://webservices.rm.ingv.it/wavesdownloader/) [(on GitHub)](https://github.com/fabriziobernardi/wavesdownloader)
   * [ADMIRE project](http://www.admire-project.eu/)
   * [pSysmon](http://www.stefanmertl.com/science/category/software/psysmon/)
   * [MIIC](http://theo1.geo.uni-leipzig.de/wordpress/)
   * [ObsPyDMT](https://github.com/kasra-hosseini/obspyDMT)
   * [seedlink plotter](https://github.com/bonaime/seedlink_plotter)
   * [pyTDMT - Python Time Domain Moment Tensor](http://webservices.rm.ingv.it/pyTDMT/) [(on GitHub)](https://github.com/fabriziobernardi/pydmt)
   * [MSNoise - Monitoring Seismic Velocity Changes using Ambient Seismic Noise](http://msnoise.org/) [(on GitHub)](https://github.com/ROBelgium/MSNoise)
   * [Pisces: A practical seismological database library in Python](http://jkmacc-lanl.github.io/pisces/) [(on GitHub)](https://github.com/jkmacc-lanl/pisces)

## References

  1. Moritz Beyreuther, Robert Barsch, Lion Krischer, Tobias Megies, Yannik Behr and Joachim Wassermann (2010), [ObsPy: A Python Toolbox for Seismology](http://www.seismosoc.org/publications/SRL/SRL_81/srl_81-3_es/), SRL, 81(3), 530-533.
  1. Tobias Megies, Moritz Beyreuther, Robert Barsch, Lion Krischer, Joachim Wassermann (2011), [ObsPy – What can it do for data centers and observatories?](http://www.annalsofgeophysics.eu/index.php/annals/article/view/4838) Annals Of Geophysics, 54(1), 47-58, doi:10.4401/ag-4838.

## Developer Corner

 * [Style Guide](http://docs.obspy.org/coding_style.html)
 * [Docs or it doesn't exist!](http://lukeplant.me.uk/blog/posts/docs-or-it-doesnt-exist/)
 * [[ObsPy Git Branching Model]]
 * [[Known Python issues]]
 * Performance Tips:
    * [Python](http://wiki.python.org/moin/PythonSpeed/PerformanceTips)
    * [NumPy and ctypes](http://www.scipy.org/Cookbook/Ctypes)
    * [SciPy](http://wiki.scipy.org/PerformancePython)
    * [NumPy Book](http://csc.ucdavis.edu/~chaos/courses/nlp/Software/NumPyBook.pdf)
 * [[Testing, Debugging & Profiling]]
 * [[Sphinx Documentation]]
 * [Notes on the performed svn to git migration](wiki/Svn-to-git-migration)
 * [[Interesting reading on git, github]]
 * [[Debian packaging]]
 * [[How to: Add a new Submodule]]
 * [[Anaconda Tips]]