###  Installing MacPorts

There are several options to install MacPorts, but I recommend to use the _Mac OS X Installer_ which is probably the standard approach. All authoritative details on installing MacPorts are found [here](http://www.macports.org/install.php). 

1. Install _Xcode_ from _Apple Developer Connection_. The version to install will depend on your OSX version and the required components are specified on MacPorts' [website](http://www.macports.org/install.php). 
1. Accept the License Terms, if Xcode 4 and later was installed.
1. Install MacPorts and add `/opt/local/bin` & `/opt/local/sbin` to your path.
1. I recommend to run `sudo port -v selfupdate` before you start installing ports.

### Installing ObsPy

Once MacPorts is available on your system, installing ObsPy and all dependencies is as easy as executing the following command:

    sudo port install py27-obspy

The port should install and run smoothly with Python 2.7 (`py27-obspy`), but some limitations apply to Python 2.6. In case you encounter any problem do not hesitate to fill a ticket against the port. 

### Limitations with Python 2.6 (on 31/07/2013):

With Python 2.6 there seem be some issues, which I assume are not directly related to ObsPy or the port itself. If gcc >=4.5 (variants: `+gcc45`, `+gcc46` & `+gcc47`) is used to compile `py26-scipy` and `py26-obspy`, the port would install without problem, but will not be completely functional. 

If for some reason you need to install ObsPy with Python 2.6, use the `+gcc44` variant for both `py26-scipy`  and `py26-obspy`. The `+gcc43` variant works as well. The default variant `py26-scipy +gcc47` is currently not functional. The procedure to use is the following:

    sudo port -v install py26-scipy +gcc44 
    sudo port -v install py26-obspy +gcc44