Limitations with Python 2.6:

- The port should install and run smoothly with Python 2.7 (py27-obspy). 

- With Python 2.6 there seem be some issues, which I assume are not directly related to ObsPy or the port itself. If gcc >=4.5 (variant +gcc45 .. +gcc47) is used to compile scipy (py26-scipy) and py26-obspy, the port would install without problem, but will not be completely functional. 

If you need to install it with Python 2.6,  please use the following procedure:
- install scipy w/ the +gcc44 variant: `sudo port -v install py26-scipy +gcc44` 
 (Note: py26-scipy +gcc47, the default is currently not functional anyway)
- install obspy w/ the +gcc44 variant: `sudo port -v install py26-obspy +gcc44`

The gcc43 would work as well.

In case you encounter any problem do not hesitate to fill a ticket against the port. 