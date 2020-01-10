For installation add the ObsPy apt repository to your package manager by adding the following line to the file `/etc/apt/sources.list` (needs root privileges):
ObsPy is packed for all Debian and Ubuntu releases which are still officially supported.
Replace `$CODENAME` with the  codename of your [Debian](http://en.wikipedia.org/wiki/Debian#Releases)/[Ubuntu](http://en.wikipedia.org/wiki/Ubuntu_releases) release.

```sources.list
deb http://deb.obspy.org $CODENAME main
```

For example for Debian stretch put this in your `/etc/apt/sources.list` file:

```sources.list
deb http://deb.obspy.org stretch main
```

Currently supported releases are (see http://deb.obspy.org/pool/main/p/python-obspy/ for the most up-to-date list of current packages):

 * [Debian](https://www.debian.org/releases/):
    - wheezy *(i386, amd64, [armv6l](http://www.raspbian.org/))*
    - jessie *(i386, amd64, [armv6l](http://www.raspbian.org/))*
    - stretch *(i386, amd64, [armv6l](http://www.raspbian.org/))*
    - buster *(i386, amd64, [armv6l](http://www.raspbian.org/))*
 * [Ubuntu](https://wiki.ubuntu.com/Releases):
    - trusty *(i386, amd64)*
    - xenial *(i386, amd64)*
    - bionic *(i386, amd64)*
 * [Raspbian wheezy, jessie, stretch and buster (hard-float, armv6l)](http://www.raspbian.org/)

If you are unsure about the codename of your installation you can use the following command to display it:

```bash
lsb_release -cs
```

Next you need to import the ObsPy gnupg key so that apt is able to check the integrity of the downloaded packages. The following command needs to be executed only once:

```bash
$ wget --quiet -O - https://raw.github.com/obspy/obspy/master/misc/debian/public.key | sudo apt-key add -
```

To install ObsPy including all dependencies:

```bash
$ sudo apt-get update
$ # python3 package only available for newer Debian/Ubuntu releases
$ sudo apt-get install python-obspy python3-obspy
```

If you want to uninstall ObsPy and all unneeded dependencies just do:

```bash
$ sudo apt-get remove python-obspy python3-obspy
```

For newer Debian (starting with "jessie") and Ubuntu (starting with "trusty") releases, `python3-obspy` package will be available. Furthermore data and image files only needed to run ObsPy's test suites are contained in a separate package `python-obspy-dbg` which can be opted-out when installing with e.g. `aptitude install -R python-obspy`.