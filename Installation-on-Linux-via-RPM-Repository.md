A [copr repository](https://copr.fedoraproject.org/coprs/qulogic/obspy/) is
available that provides packages for ObsPy and its dependencies for the
following distributions:
 * The previous Fedora release (currently 22)
 * The latest Fedora release (currently 23)
 * The next Fedora release (currently 24 (when available))
 * Fedora rawhide
 * CentOS/EL 6
 * CentOS/EL 7

On older distributions, the documentation package may not be available, but
documentation may be [accessed online](https://docs.obspy.org/).

To install ObsPy, you must first [enable the repository](#enable-repository),
and then [install the desired package(s)](#install-obspy).

# Enable repository

## Fedora 22+

If you're using a version of Linux with `dnf`:

    $ sudo dnf copr enable qulogic/obspy

and you need to have `dnf-plugins-core` installed (it is by default.)

## CentOS

If you are not using `dnf`:

    $ sudo yum copr enable qulogic/obspy

and you need to have `yum-plugin-copr` installed.

On CentOS, you will need to install the `epel-release` package to obtain
some dependencies from the EPEL repositories.

    $ sudo yum install epel-release

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