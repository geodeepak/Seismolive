###  Installing MacPorts ###

If you have not already installed MacPorts, you need first do this before installing ObsPy. There are several options to install MacPorts, but I recommend to use the _Mac OS X Installer_ which is probably the standard approach. All authoritative details on installing MacPorts can be found [here](http://www.macports.org/install.php). Summary of the necessary steps:

1. Install _Xcode_ from _Apple Developer Connection_ or _Mac App Store_. The version to install will depend on your _OS X_ version. Note that for recent _XCode_ (notable 4.3 and later) you will need to install the _command line tools_ explicitly. 
1. Accept the License Terms, if Xcode 4 or later was installed. All steps to setup XCode correctly are found on MacPorts' [website](http://www.macports.org/install.php). 
1. Install MacPorts and add `/opt/local/bin` & `/opt/local/sbin` to your path.
1. I recommend to run `sudo port -v selfupdate` before you start installing any new ports.


### Installing ObsPy ###

Once MacPorts is correctly deployed on your system, installing ObsPy and all dependencies is as easy as executing the following command:

    sudo port install py27-obspy

This will install ObsPy (port `py27-obspy`) as one of the `site-packages` of the Python 2.7 interpreter provided by MacPorts (port `python27`). It is a distinct instance of Python and independent of the system's version. All required dependencies are installed automatically. You need to use MacPort's Python interpreter, which is usually located in `/opt/local/bin/python2.7`, to be able to import the ObsPy package. You can make this Python instance your default interpreter by executing:

    sudo port select python python27

Hint: MacPorts avoids any changes to your OS X base system, therefore this selection is implemented by creating symbolic links in `opt/local/bin`. In order to ensure the selection is effective, your search path variable `$PATH` should be set in a way to give precedence to directory `/opt/local/bin`.

If for some reason you prefer to install ObsPy against the Python 2.6 interpreter, the corresponding port is `py26-obspy`. You can have both versions installed at the same time.


### Upgrading your ObsPy ###

When a new version of ObsPy becomes available via Macports, you can use the following sequences to update your Macports based ObsPy installation:

    sudo port selfupdate
    sudo port upgrade py27-obspy

The old version is only deactivated, so you could switch back in case you find it useful. If you prefer to clean up your system, remove the old version by executing:

    sudo port uninstall py27-obspy and inactive
