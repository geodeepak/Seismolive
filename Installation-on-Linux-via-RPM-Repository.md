A [copr repository](https://copr.fedoraproject.org/coprs/qulogic/obspy/) is
available that provides packages for ObsPy and its dependencies for the
following distributions:
 * The previous Fedora release (currently 24)
 * The latest Fedora release (currently 25)
 * The next Fedora release (currently 26 (when available))
 * Fedora rawhide
 * CentOS/EL 7

A [separate copr repository](https://copr.fedoraproject.org/coprs/qulogic/obspy-el6/)
is available for older repositories:
 * CentOS/EL 6

On older distributions, the documentation package may not be available, but
documentation may be [accessed online](https://docs.obspy.org/).

To install ObsPy, you must first [enable the repository](#enable-repository),
and then [install the desired package(s)](#install-obspy).

# Enable repository

## Fedora 24+

    $ sudo dnf copr enable qulogic/obspy

## CentOS

On CentOS, you will need to install the `epel-release` package to obtain
some dependencies from the EPEL repositories. You also need to have
`yum-plugin-copr` installed.

    $ sudo yum install epel-release yum-plugin-copr

Then enable the correct copr repo as noted below:

### CentOS 6

    $ sudo yum copr enable qulogic/obspy-el6

### CentOS 7

    $ sudo yum copr enable qulogic/obspy

### Manual

Alternatively, you can manually download a `.repo` file and place it in
`/etc/yum.repos.d/`. These `.repo` files for each distribution can be found
on the [copr Overview page](https://copr.fedoraproject.org/coprs/qulogic/obspy/)
or [copr Overview page for EL6](https://copr.fedoraproject.org/coprs/qulogic/obspy-el6/).

# Install ObsPy

After enabling the repository, you can simple do:

## Python 3

Python 3 packages may not be available for CentOS.

    $ sudo dnf install python3-obspy

or

    $ sudo yum install python3-obspy

## Python 2

    $ sudo dnf install python2-obspy

or

    $ sudo yum install python-obspy

## Documentation

For offline browsing of the documentation (not available for all distributions):

    $ sudo dnf install python-obspy-docs

or

    $ sudo yum install python-obspy-docs