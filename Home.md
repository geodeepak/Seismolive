<img class="right" style="width: 60%" src="https://raw.github.com/obspy/website/master/logo/obspy_logo_full_highres.png" />

ObsPy is an open-source project dedicated to provide a **Python framework for processing seismological data**. It provides parsers for common file formats, clients to access data centers and seismological signal processing routines which allow the manipulation of seismological time series.

The goal of the ObsPy project is to facilitate **rapid application development for seismology**.

## Contents

 * [Acknowledging](#acknowledging)
 * [News](#news)
 * [Getting Started](#getting-started)
 * [Installation](#installation)
 * [Stay Informed, Get in Touch!](#stay-informed-get-in-touch)
 * [Documentation](#documentation)
 * [Use Cases / Applications Using ObsPy](#use-cases--applications-using-obspy)
 * [Developer Corner](#developer-corner)

## Acknowledging

Please support the project by acknowledging the use of it. This helps us keep it alive. If you use ObsPy (directly or as a dependency of another package) for work resulting in an academic publication, we would be grateful if one of the following papers is cited:

* <em>M. Beyreuther, R. Barsch, L. Krischer, T. Megies, Y. Behr and J. Wassermann</em> (2010)<br>
  [ObsPy: A Python Toolbox for Seismology](http://www.seismosoc.org/publications/SRL/SRL_81/srl_81-3_es/)<br>
  _SRL_, 81(3), 530-533<br>
  DOI: [10.1785/gssrl.81.3.530](http://dx.doi.org/10.1785/gssrl.81.3.530)
* <em>T. Megies, M. Beyreuther, R. Barsch, L. Krischer, J. Wassermann</em> (2011)<br>
  [ObsPy – What can it do for data centers and observatories?](http://www.annalsofgeophysics.eu/index.php/annals/article/view/4838)<br>
  _Annals Of Geophysics_, 54(1), 47-58<br>
  DOI: [10.4401/ag-4838](http://dx.doi.org/10.4401%2Fag-4838)
* <em>L. Krischer, T. Megies, R. Barsch, M. Beyreuther, T. Lecocq, C. Caudron, J. Wassermann</em> (2015)<br>
  [ObsPy: a bridge for seismology into the scientific Python ecosystem](http://iopscience.iop.org/1749-4699/8/1/014003/)<br>
  _Computational Science & Discovery_, 8(1), 014003<br>
  DOI: [10.1088/1749-4699/8/1/014003](http://dx.doi.org/10.1088/1749-4699/8/1/014003)

You can also cite the used ObsPy version:<br>
[DOIs for released ObsPy versions](https://zenodo.org/search?ln=en&p=obspy&sort=mostrecent) (e.g. for ObsPy 1.2.0: [10.5281/zenodo.3674646](http://dx.doi.org/10.5281/zenodo.3674646))

## News

More details on important news/announcement can be found on [our discourse forum](https://discourse.obspy.org/c/announcements/11) in the future.

##### [Jul 23 2020] ObsPy now on liberapay

ObsPy is now on [liberapay](https://liberapay.com/ObsPy), to raise the funds for our rented server providing some of our services. [Read all the details in our Discourse forum](https://discourse.obspy.org/t/2020-07-23-obspy-now-on-liberapay/994).

##### [Jul 9 2020] ObsPy discourse has landed!

We started our own self-hosted Discourse server for all discussions around ObsPy: https://discourse.obspy.org/

This is real new right now, so we will have to see how it goes, but we feel this might eventually replace the users mailing list. You can login with existing GitHub, Google or Twitter accounts, or create a new user bound to an email address directly on site.

##### [Mar 6 2020] Release of ObsPy 1.2.0

This is a major release with a lot of new features, bug fixes, and general improvements and we strongly recommend all users to update. Follow these link to learn more:

* [[What's New in ObsPy 1.2|What's New in ObsPy 1.2]]
* [Release Including Full Changelog](https://github.com/obspy/obspy/releases/tag/1.2.0)

##### [Feb 17 2019] Release of ObsPy 1.1.1
This is the first bug fix release in the 1.1.x release cycle. It does not change functionality/API but fixes quite a number of bugs resulting in an overall more stable ObsPy package. It is planned to be the only bug fix release for 1.1.x as well as we plan to do the release of 1.2.0 as soon as possible. 

We recommend all users to upgrade through one of the usual channels. Please see the full changelog for all details:

* [Release Including Full Changelog](https://github.com/obspy/obspy/releases/tag/1.1.1)

##### [Oct 27 2017] Release of ObsPy 1.1.0

This is a major release with a lot of new features, bug fixes, and general improvements and we strongly recommend all users to update. Follow these link to learn more:

* [[What's New in ObsPy 1.1|What's New in ObsPy 1.1]]
* [Release Including Full Changelog](https://github.com/obspy/obspy/releases/tag/1.1.0)

##### [Feb 27 2017] Release of ObsPy 1.0.3
This is the third bug fix release in the 1.0.x release cycle. It does not change functionality/API but fixes quite a number of bugs resulting in an overall more stable ObsPy package. It is planned to be the last bug fix release for 1.0.x as well as we plan to do the release of 1.1.0 as soon as possible. 

We recommend all users to upgrade through one of the usual channels. Please see the full changelog for all details:

* [Release Including Full Changelog](https://github.com/obspy/obspy/releases/tag/1.0.3)

##### [Aug 03 2016] Release of ObsPy 1.0.2
This is the second bug fix release in the 1.0 release cycle. It does not change functionality/API but fixes quite a number of bugs resulting in an overall more stable ObsPy package.

We recommend all users to upgrade through one of the usual channels. Please see the full changelog for all details:

* [Release Including Full Changelog](https://github.com/obspy/obspy/releases/tag/1.0.2)

##### [Mar 24 2016] Release of ObsPy 1.0.1
This is the first bug fix release in the 1.0 release cycle. It does not change functionality/API but fixes several bugs in 1.0.0, most notably fixing decryption of encrypted data from requests on restricted data via ArcLink and some bugs when working with SAC headers in the rewritten SAC module.

We recommend all users to upgrade through one of the usual channels. Please see the full changelog for all details:

* [Release Including Full Changelog](https://github.com/obspy/obspy/releases/tag/1.0.1)

##### [Feb 19 2016] Release of ObsPy 1.0.0
This is a big release with significant internal changes, new features, stability improvements, and
much more to prepare ObsPy for future challenges and get rid of accumulated technical debt. It is now stable enough to officially declare it version 1.0. Changes are broad and numerous - follow these links to learn more:

* [[What's New in ObsPy 1.0|What's New in ObsPy 1.0]]
* [Release Including Full Changelog](https://github.com/obspy/obspy/releases/tag/1.0.0)

##### [May 15 2015] Release of ObsPy 0.10.2
ObsPy 0.10.2 is a maintenance release and it contains a number of bug fixes and minor feature improvements so we advise all users to upgrade through one of the usual channels.

* [Release Including Full Changelog](https://github.com/obspy/obspy/releases/tag/0.10.2)

##### [March 20 2015] Release of ObsPy 0.10.1
ObsPy 0.10.1 is once again our biggest release yet with over 2200 single commits from 25 individual contributors!
We strongly encourage all users to update to the new version as it will effectively end support for the 0.9.x line.
Major new features are Python 3 support, a new TauP implementation, Anaconda packages, ...
* [Release Including Full Changelog](https://github.com/obspy/obspy/releases/tag/0.10.1)
* [[What's New in ObsPy 0.10.1|What's New in ObsPy 0.10.1]]


##### [May 4 2014] Release of ObsPy 0.9.2
ObsPy 0.9.2 is a maintenance release and contains the collective bug fixes and minor feature improvements of around 150 commits so we advise all users to upgrade.
* [Release including full changelog](https://github.com/obspy/obspy/releases/tag/0.9.2)

##### [January 9 2014] Release of ObsPy 0.9.0
ObsPy 0.9.0 offers (amongst many other things) two major new features: support for the FDSN webservices and the FDSN StationXML format.
* [Release including full changelog](https://github.com/obspy/obspy/releases/tag/0.9.0)
* [[Migration to ObsPy 0.9.0]]


## Getting Started

The [ObsPy Gallery](http://gallery.obspy.org) and its related [ObsPy Tutorial](http://tutorial.obspy.org) are maybe the best point to get a first impression of what ObsPy is all about. The tutorial is a collection of short example programs with explanations and program output. For help getting started with Python, have a look at this [collection of links to Tutorials](wiki/Python-Tutorials).

ObsPy Tutorial notebooks -- and much more on specific seismology topics -- can also be found on [**Seismo-Live**](http://seismo-live.org/), both as a static preview and as interactively runnable version.

[![Link to Seismo-Live](https://user-images.githubusercontent.com/1842780/75337134-b4310a80-588c-11ea-8ed2-dbabdedaedfc.png)](http://seismo-live.org/)

```python
from obspy import read
st = read()  # load example seismogram
st.filter(type='highpass', freq=3.0)
st = st.select(component='Z')
st.plot()
```

![Example waveform Plot](https://user-images.githubusercontent.com/1842780/75334711-9d88b480-5888-11ea-8bc8-0bfe7021d79e.png)

## Installation

ObsPy is currently [running and tested](http://tests.obspy.org) on Linux (32 and 64 bit), Windows (32 bit and/or 64 bit) and Mac OS X.

ObsPy runs on Python 2.7, 3.5, 3.6, 3.7 and 3.8. We highly recommend and only officially support the latest release of each series. We recommend you use the latest version of python 3 if possible. 

**For individual users we strongly recommend [[Installation via Anaconda|Installation via Anaconda]].**

System administrators can also install system packages (where available, see below).
Detailed information on installing the latest stable version of ObsPy on various operating systems:

* via [Anaconda, a scientific Python distribution](https://docs.continuum.io/anaconda/) (all systems) **(works without root access)**
  * [[normal installation via Anaconda installer|Installation via Anaconda]]
  * [[installation using bundled Anaconda installer|Installation via ObsPy-bundled Anaconda installer]]
* [[Debian/Ubuntu|Installation on Linux via Apt Repository]] via the package manager
* [[Fedora/CentOS|Installation on Linux via RPM Repository]] via the package manager
* Mac OS X via [[Homebrew|Installation on OS X using Homebrew]] or [[MacPorts|Installation on Mac OS X using Macports]]
* Windows from a [[pre-build package (PyPI)|Installation on Windows using a pre-build package (PyPI)]] or from [[source|Installation on Windows From Source]]
* [[FreeBSD|Installation on FreeBSD]] via the package manager
* [[NetBSD|Installation on NetBSD]] via the package manager
* via [[PyPi or from source|Installation via PyPi/from source]], applicable to Linux and OSX
* into an existing [Antelope 5.4 on RHEL/CentOS 6](http://geoffdavis.github.io/blog/2014/08/11/installing-obspy-for-antelope-5-dot-4-on-rhel-slash-centos-6/)
* for a reproducible installation mostly aimed at servers and clusters, have a look at the [Salt formula for ObsPy](https://github.com/obspy/obspy/tree/master/misc/installer/salt-formula)

If you run into problems when following the above installation instructions, you can ask for help in our discourse: https://discourse.obspy.org/c/installation-issues/5

If you intend on making changes to ObsPy or develop for it, read this:
* [[Developer Installation|Developer Installation]]

If you intend on performing parallel processing with Python and Obspy, please read the following:
* [[Notes on Parallel Processing with Python and ObsPy|Notes on Parallel Processing with Python and ObsPy]]

## Stay Informed, Get in Touch!

#### New: [ObsPy Discourse](https://discourse.obspy.org/)

Since July 2020 we also have a discourse at https://discourse.obspy.org/. You can discuss, get in touch with other ObsPy users and ask for help there. We plan this to replace the users mailing list eventually, but this is in it's early stage right now, so we will see where it goes. It also has the complete users mailing list as a read-only category in it, so you can more easily search through older user discussion on there!

#### Mailing Lists

If you are using ObsPy we **strongly recommend** you join the [ [obspy-announcements] ](http://lists.swapbytes.de/listinfo/obspy-announcements) and the [ [obspy-users] ](http://lists.swapbytes.de/listinfo/obspy-users) mailing lists. The **[obspy-announcements]** list will be the place where new additions, important changes and bug fixes will be announced and thus will be very low volume. The **[obspy-users]** list is used to contact other ObsPy users for questions and open discussions.

Please keep **all conversations in English** when using the ObsPy mailing lists, thanks!

To search the users mailing list tell your favorite search engine to only look at results from our archives, using e.g. this search string:

`plot line site:lists.swapbytes.de/archives/obspy-users/`

#### [obspy-announcements]

  * [Subscribe](mailto:obspy-announcements-request@lists.swapbytes.de?subject=subscribe&body=Send%20this%20message%20from%20the%20address%20you%20want%20to%20subscribe.) / [Unsubscribe](mailto:obspy-announcements-request@lists.swapbytes.de?subject=unsubscribe&body=Send%20this%20message%20from%20the%20address%20you%20want%20to%20unsubscribe.)
  * [Browse the archive](http://lists.swapbytes.de/pipermail/obspy-announcements/)

#### [obspy-users]

Note: we might at some point discontinue the users mailing list in favor of the discourse forum, so consider jumping on there right away, if you are new here!

  * [Subscribe](mailto:obspy-users-request@lists.swapbytes.de?subject=subscribe&body=Send%20this%20message%20from%20the%20address%20you%20want%20to%20subscribe.) / [Unsubscribe](mailto:obspy-users-request@lists.swapbytes.de?subject=unsubscribe&body=Send%20this%20message%20from%20the%20address%20you%20want%20to%20unsubscribe.)
  * [Post a message](mailto:users@obspy.org)
  * [Browse the archive](http://lists.swapbytes.de/pipermail/obspy-users/)


#### Follow us on Twitter

For more frequent news and general information on Python in seismology/science, follow us on twitter: **[@obspy](https://twitter.com/obspy)**

There also is a [feed for commits](https://github.com/obspy/obspy/commits/master.atom). To get emails concerning issues make a GitHub login, 'watch' our repository and set up email notifications for your GitHub account.

#### Gitter Chat

You can also get in touch with people in our gitter chat room: https://gitter.im/obspy/obspy

## Documentation

 - for the latest stable release
    - [start page](http://docs.obspy.org)
    - [overview of submodules](http://docs.obspy.org/packages/index.html)
 - [for the current developer version](http://docs.obspy.org/master)
 - [archive for other versions](http://docs.obspy.org/archive)

## Use Cases / Applications Using ObsPy

If you want to showcase and/or discuss your projects built on top of ObsPy, you can now also do so in our Discourse: https://discourse.obspy.org/c/obspy-related-projects/7

Feel free to [add your own project to the list](https://github.com/obspy/obspy/wiki/Home/_edit).
   * [HiPerSeis](https://github.com/GeoscienceAustralia/hiperseis) - High Performance Seismological Tools
   * [ObsPyck](https://github.com/megies/obspyck/wiki)
   * [SeismicHandler](http://www.seismic-handler.org)
   * [SeisHub](https://github.com/barsch/seishub.core)
   * [SeishubExplorer](https://github.com/krischer/SeishubExplorer)
   * [HtoVToolbox](https://github.com/krischer/HtoV-Toolbox)
   * [wavePicker](https://github.com/miili/wavePicker)
   * [Antelope Python moment tensor code](http://eqinfo.ucsd.edu/~rnewman/howtos/antelope/moment_tensor/)
   * [Using ObsPy with py2exe](http://www.geophysique.be/en/2011/08/09/using-obspy-modules-with-py2exe/)
   * [Whisper](https://code-whisper.isterre.fr/)
   * [Wavesdownloader](http://webservices.rm.ingv.it/wavesdownloader/) [(on GitHub)](https://github.com/fabriziobernardi/wavesdownloader)
   * [ADMIRE project](http://www.admire-project.eu/)
   * [pSysmon](http://psysmon.mertl-research.at/doku.php)
   * [ObsPyDMT](https://github.com/kasra-hosseini/obspyDMT)
   * [seedlink plotter](https://github.com/bonaime/seedlink_plotter)
   * [pyTDMT - Python Time Domain Moment Tensor](http://webservices.rm.ingv.it/pyTDMT/) [(on GitHub)](https://github.com/fabriziobernardi/pydmt)
   * [MSNoise - Monitoring Seismic Velocity Changes using Ambient Seismic Noise](http://msnoise.org/) [(on GitHub)](https://github.com/ROBelgium/MSNoise)
   * [Pisces: A practical seismological database library in Python](http://jkmacc-lanl.github.io/pisces/) [(on GitHub)](https://github.com/jkmacc-lanl/pisces)
   * [HASHpy: Python wrapped fork of HASH first motion focal mechanism code](https://github.com/markcwill/hashpy)
   * [waveloc](http://amaggi.github.io/waveloc/index.html) [(on GitHub)](https://github.com/amaggi/rt-waveloc)
   * [scisola](http://students.ceid.upatras.gr/~triantafyl/scisola/) [(on GitHub)](https://github.com/nikosT/scisola)
   * [EQTransformer](https://eqtransformer.readthedocs.io/en/latest/index.html) - AI-based Earthquake Signal Detector and Phase Picker.
   * [instaseis](http://www.instaseis.net) - Instant Global High Frequency Seismograms
   * [LASIF](http://www.lasif.net) - Large-Scale Seismic Inversion Framework
   * [pyflex](http://krischer.github.io/pyflex) - Enhanced port of FLEXWIN
   * [hypoDDpy](https://github.com/krischer/hypoDDpy) - Run hypoDD in a data driven manner.
   * [wfs_input_generator](http://krischer.github.io/wfs_input_generator/) - Generate input files for many waveform solvers directly from data.
   * [rf](https://github.com/trichter/rf) - Calculate receiver functions.
   * [Qopen](https://github.com/trichter/qopen) - Separation of intrinsic and scattering Q by envelope inversion.
   * [EQcorrscan](http://calum-chamberlain.github.io/EQcorrscan/) - Match-filter earthquake detection
   * [PhasePApy](https://github.com/austinholland/PhasePApy) - a Seismic Phase Picker and Associator program package
   * [Jane](https://github.com/krischer/jane) - Document database for Seismology
   * [MouseTrap](http://geo.mff.cuni.cz/~vackar/mouse/) - A module for detecting a special type of disturbance (so called mouse, ping, or fling step) in seismic records.
   * [Lazylyst](https://github.com/AndrewReynen/Lazylyst) - A GUI created for time series review, using a flexible framework for new workflows.
   * [REDPy](https://github.com/ahotovec/REDPy) - A tool for automated detection and analysis of repeating earthquakes in continuous data.
   * [CodaNorm](https://github.com/cormorant/CodaNorm/) - A software package for the body-wave attenuation calculation by the coda-normalization method
   * [ISOLA-ObsPy](http://geo.mff.cuni.cz/~vackar/isola-obspy/) - A seismic source inversion module. Events are described as point sources with centroid moment tensors.
   * [pySW4](https://github.com/shaharkadmiel/pySW4) - Setup, run, post process, and visualize numerical simulations, primarily for SW4.
   * [yam](https://github.com/trichter/yam) - Yet another monitoring tool using correlations of ambient noise.
   * [PyWeed](https://github.com/iris-edu/pyweed) - a cross-platform downloadable app for retrieving event-based seismic data
   * [SeisTomoPy](https://github.com/stephaniedurand/SeisTomoPy) - Fast visualization, comparison and calculations in global tomographic models
   * [Detex](https://github.com/d-chambers/Detex) - A Python package for subspace detection and waveform similarity clustering
   * [pygema](https://github.com/emmaPatagonia/pygema) - Seismic data analysis tool box for volcano monitoring.  Routines includes automatic localization of seismic events,  computation of RSAM and SSAM, magnitude calculation and sql data management.
   * [FAST](https://github.com/stanford-futuredata/FAST) - Unsupervised Large‐Scale Search for Similar Earthquake Signals
   * [Telewavesim](https://paudetseis.github.io/Telewavesim/) - Python software for teleseismic body wave modeling
   * [StDb](https://schaefferaj.github.io/StDb/) - Simple seismic station tools and database generation
   * [RfPy](https://paudetseis.github.io/RfPy/) - Single-station receiver functions and post-processing
   * [SplitPy](https://paudetseis.github.io/SplitPy/) - Teleseismic shear-wave splitting analysis (basic Python translation of [SplitLab](http://splitting.gm.univ-montp2.fr))
   * [OBStools](https://nfsi-canada.github.io/OBStools/) - Python software for processing broadband ocean-bottom seismic data
   * [OrientPy](https://nfsi-canada.github.io/OrientPy/) - Seismic station orientation tools
   * [Ppol](https://gitlab.com/johnrobertscholz/ppol) - P-wave polarization analysis to determine (mis-)orientations of ocean-bottom and terrestrial seismometers.
   * [QuakeMigrate](https://github.com/Ulvetanna/QuakeMigrate) - QuakeMigrate is a Python and C software package that detects and locates seismic events from raw data, using a migration and coalescence based technique
   * [Seisplotjs](http://crotwell.github.io/seisplotjs/) - Javascript seismology library that allows using a web browser as the waveform display for ObsPY 
   * [noisi](https://github.com/lermert/noisi) - A Python tool for ambient noise correlation modeling

#### miscellaneous..

   * https://github.com/ndperezg/taller_obspy
   * https://github.com/dansand/seismic
   * https://github.com/kallstadt-usgs/seisk
   * https://github.com/ovsm-dev/sdp
   * https://github.com/viictorjs/SEG2Py
   * https://github.com/xumi1993/seispy
   * https://github.com/rizac/stream2segment
   * https://github.com/pysit/pysit
   * https://github.com/lizstarin/earthquakemap
   * https://github.com/samhaug/seispy
   * https://github.com/oceanobservatories/mi-instrument
   * https://github.com/echavess/Focal-mechanisms-Pressure-and-Tension-Axis


## Developer Corner

General information on how to contribute to the project can be found [here](https://github.com/obspy/obspy/blob/master/CONTRIBUTING.md).

 * [Style Guide](http://docs.obspy.org/coding_style.html)
 * [Docs or it doesn't exist!](http://lukeplant.me.uk/blog/posts/docs-or-it-doesnt-exist/)
 * [[ObsPy Git Branching Model]]
 * [[Doing a new ObsPy release]]
 * [[Known Python issues]]
 * Performance Tips:
    * [Python](http://wiki.python.org/moin/PythonSpeed/PerformanceTips)
    * [NumPy and ctypes](http://www.scipy.org/Cookbook/Ctypes)
    * [SciPy](http://wiki.scipy.org/PerformancePython)
    * [NumPy Book](http://csc.ucdavis.edu/~chaos/courses/nlp/Software/NumPyBook.pdf)
 * [Testing, Debugging & Profiling](wiki/Testing,-Debugging-&-Profiling)
 * [[Sphinx Documentation]]
 * [Notes on the performed svn to git migration](wiki/Svn-to-git-migration)
 * [[Interesting reading on git, github]]
 * [[Debian packaging]]
 * [[How to: Add a new Submodule]]
 * [[Affiliated Project Guidelines]]
