A [copr repository](https://copr.fedoraproject.org/coprs/qulogic/obspy/) is
available that provides packages for ObsPy and its dependencies for the
following distributions:
 * The previous Fedora release (currently 20)
 * The latest Fedora release (currently 21)
 * The next Fedora release (currently 22)
 * Fedora rawhide
 * CentOS/EL 6
 * CentOS/EL 7

On older distributions, the documentation package may not be available, but
documentation may be [accessed online](https://docs.obspy.org/).

To install ObsPy, you must first [enable the repository](#enable-repository),
and then [install the desired package(s)](#install-obspy).

# Enable repository

## Fedora 21+ or 20 with `dnf`

If you're using a version of Linux with `dnf`:

    $ sudo dnf copr enable qulogic/obspy

and you need to have `dnf-plugins-core` installed (it is by default.)

## Fedora 20 with `yum` or CentOS

If you have an older distribution or are not using `dnf`:

    $ sudo yum copr enable qulogic/obspy

and you need to have `yum-plugin-copr` installed.

## Manual

Alternatively, you can manually download a `.repo` file and place it in
`/etc/yum.repos.d/`. These `.repo` files for each distribution can be found
on the [copr Overview page](https://copr.fedoraproject.org/coprs/qulogic/obspy/).

# Install ObsPy

After enabling the repository, you can simple do:

    $ sudo dnf install python3-obspy

or

    $ sudo yum install python3-obspy

If you wish to install Python 2 packages instead, then simply use `python-obspy`
in the command above. There is also a `python-obspy-docs` package for offline
browsing of the documentation (not available for all distributions).