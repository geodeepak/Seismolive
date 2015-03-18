<img class="right" style="width: 60%" src="https://raw.github.com/obspy/website/master/logo/obspy_logo_full_highres.png" />

ObsPy is an open-source project dedicated to provide a **Python framework for processing seismological** data. It provides parsers for common file formats, clients to access data centers and seismological signal processing routines which allow the manipulation of seismological time series.

The goal of the ObsPy project is to facilitate **rapid application development for seismology**.

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

Alternatively you can also directly cite the used ObsPy version:<br>
[DOIs for released ObsPy versions](https://zenodo.org/search?ln=en&p=obspy&action_search=) (e.g. for ObsPy 0.9.2: [10.5281/zenodo.10648](http://dx.doi.org/10.5281/zenodo.10648))

## News
##### [May 4 2014] Release of ObsPy 0.9.2
ObsPy 0.9.2 is a maintenance release and contains the collective bug fixes and minor feature improvements of around 150 commits so we advise all users to upgrade.
* [Release including full changelog](../releases/tag/0.9.2)

##### [January 9 2014] Release of ObsPy 0.9.0
ObsPy 0.9.0 offers (amongst many other things) two major new features: support for the FDSN webservices and the FDSN StationXML format.
* [Release including full changelog](../releases/tag/0.9.0)
* [Migration guide to ObsPy 0.9.0](wiki/Migration-to-ObsPy-0.9.0)


## Getting Started

The [ObsPy Gallery](http://gallery.obspy.org) and its related [ObsPy Tutorial](http://tutorial.obspy.org) are maybe the best point to get a first impression of what ObsPy is all about. The tutorial is a collection of short example programs with explanations and program output. For help getting started with Python, have a look at this [collection of links to Tutorials](wiki/Python-Tutorials).

## Installation

ObsPy is currently [running and tested](http://tests.obspy.org) on Linux (32 and 64 bit), Windows XP/Vista/7/8 (32 bit and/or 64 bit) and Mac OS X.

Detailed information on installing the latest stable version of ObsPy on various operating systems:

* via [[Anaconda|Installation via Anaconda]], a scientific Python distribution (all systems) **(works without root access)**
  * Installation information for [MESS 2015](https://www.geophysik.uni-muenchen.de/MESS): see [[here|Installation via Anaconda for MESS]]
* [[Debian/Ubuntu|Installation on Linux via Apt Repository]] via the package manager
* [[Fedora/CentOS|Installation on Linux via RPM Repository]] via the package manager
* Mac OS X via [[Homebrew|Installation on OS X using Homebrew]] or [[MacPorts|Installation on Mac OS X using Macports]]
* Windows from a [[pre-build package (PyPI)|Installation on Windows using a pre-build package (PyPI)]] or from [[source|Installation on Windows From Source]]
* [[FreeBSD|Installation on FreeBSD]] via the package manager
* via [[PyPi or from source|Installation via PyPi/from source]], applicable to Linux and OSX
* for a reproducible installation mostly aimed at servers and clusters, have a look at the [Salt formula for ObsPy](https://github.com/obspy/obspy/tree/master/misc/installer/salt-formula)

If you intend on performing parallel processing with Python and Obspy, please read the following:
* [[Notes on Parallel Processing with Python and ObsPy|Notes on Parallel Processing with Python and ObsPy]]

## Stay Informed

If you are using ObsPy we **strongly recommend** you join the [ [obspy-announcements] ](http://lists.obspy.org/listinfo/obspy-announcements) and the [ [obspy-users] ](http://lists.obspy.org/listinfo/obspy-users) mailing lists. The **[obspy-announcements]** list will be the place where new additions, important changes and bug fixes will be announced and thus will be very low volume. The **[obspy-users]** list is used to contact other ObsPy users for questions and open discussions.


#### [obspy-announcements]

  * [Subscribe](mailto:obspy-announcements-request@lists.swapbytes.de?subject=subscribe&body=Send%20this%20message%20from%20the%20address%20you%20want%20to%20subscribe.) / [Unsubscribe](mailto:obspy-announcements-request@lists.swapbytes.de?subject=unsubscribe&body=Send%20this%20message%20from%20the%20address%20you%20want%20to%20unsubscribe.)
  * [Browse the archive](http://lists.obspy.org/pipermail/obspy-announcements/)

#### [obspy-users]

  * [Subscribe](mailto:obspy-users-request@lists.swapbytes.de?subject=subscribe&body=Send%20this%20message%20from%20the%20address%20you%20want%20to%20subscribe.) / [Unsubscribe](mailto:obspy-users-request@lists.swapbytes.de?subject=unsubscribe&body=Send%20this%20message%20from%20the%20address%20you%20want%20to%20unsubscribe.)
  * [Post a message](mailto:users@obspy.org)
  * [Browse the archive](http://lists.obspy.org/pipermail/obspy-users/)


#### Follow us on Twitter

For more frequent news and general information on Python in seismology/science, follow us on twitter: **[@obspy](https://twitter.com/obspy)**

There also is a [feed for commits](https://github.com/obspy/obspy/commits/master.atom). To get emails concerning issues make a GitHub login, 'watch' our repository and set up email notifications for your GitHub account.

## Documentation

 - for the latest stable release
    - [start page](http://docs.obspy.org)
    - [overview of submodules](http://docs.obspy.org/packages/index.html)
 - [for the current developer version](http://docs.obspy.org/master)

## Use Cases / Applications Using ObsPy

   * [ObsPyck](https://github.com/megies/obspyck/wiki)
   * [SeismicHandler](http://www.seismic-handler.org)
   * [SeisHub](https://github.com/barsch/seishub.core)
   * [SeishubExplorer](https://github.com/krischer/SeishubExplorer)
   * [HtoVToolbox](https://github.com/krischer/HtoV-Toolbox)
   * [wavePicker](https://github.com/miili/wavePicker)
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
   * [HASHpy: Python wrapped fork of HASH first motion focal mechanism code](https://github.com/markcwill/hashpy)
   * [waveloc](http://amaggi.github.io/waveloc/index.html) [(on GitHub)](https://github.com/amaggi/rt-waveloc)
   * [scisola](http://students.ceid.upatras.gr/~triantafyl/scisola/) [(on GitHub)](https://github.com/nikosT/scisola)

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