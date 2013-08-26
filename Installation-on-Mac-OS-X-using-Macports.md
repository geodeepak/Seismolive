###  Installing MacPorts

There are several options to install MacPorts, but I recommend to use the _Mac OS X Installer_ which is probably the standard approach. All authoritative details on installing MacPorts are found [here](http://www.macports.org/install.php). 

Here a summary of the necessary steps:
1. Install _Xcode_ from _Apple Developer Connection_. The version to install will depend on your OSX version and the required components are specified on MacPorts' [website](http://www.macports.org/install.php). 
1. Accept the License Terms, if Xcode 4 and later was installed.
1. Install MacPorts and add `/opt/local/bin` & `/opt/local/sbin` to your path.
1. I recommend to run `sudo port -v selfupdate` before you start installing ports.

### Installing ObsPy

Once MacPorts is available on your system, installing ObsPy and all dependencies is as easy as executing the following command:

    sudo port install py27-obspy

This will install ObsPy as a site-package of Macport's version of Python 2.7 interpreter `py27-obspy`. All required dependencies are installed as well. If for some reason you need to install ObsPy for the Python 2.6 interpreter the port is `py26-obspy`. As with other packages as well, you could have both versions installed at the same time.

### Limitations with Python 2.6: 
(updated on 26/08/2013)

ObsPy now should work fine on most systems, both with Python 2.6 and Python 2.7. Just be sure to use an updated ports repository, so be sure to run `sudo port -v selfupdate` before installation.

The only limitation I am currently aware of is on Mac OS X 10.5 (Leopard), where the `py26-obspy` port would build and install, but does not pass all runtime tests.
