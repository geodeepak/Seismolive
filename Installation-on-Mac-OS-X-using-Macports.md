###  Installing MacPorts

There are several options to install MacPorts, but I recommend to use the _Mac OS X Installer_ which is probably the standard approach. All authoritative details on installing MacPorts are found [here](http://www.macports.org/install.php). Here a summary of the necessary steps:

1. Install _Xcode_ from _Apple Developer Connection_ or _Mac App Store_. The version to install will depend on your _OS X_ version. Note that for recent _XCode_ (4.3+) you will need to install the _command line tools_ explicitly. 
1. Accept the License Terms, if Xcode 4 or later was installed. All steps to setup _XCode_ correctly are found on MacPorts' [website](http://www.macports.org/install.php). 
1. Install MacPorts and add `/opt/local/bin` & `/opt/local/sbin` to your path.
1. I recommend to run `sudo port -v selfupdate` before you start installing new ports.


### Installing ObsPy

Once MacPorts is available on your system, installing ObsPy and all dependencies is as easy as executing the following command:

    sudo port install py27-obspy

This will install ObsPy as a site-package of Macport's version of Python 2.7 interpreter `py27-obspy`. All required dependencies are installed as well. If for some reason you need to install ObsPy for the Python 2.6 interpreter the port to use is `py26-obspy`. As with other packages as well, you could have both versions installed at the same time.

