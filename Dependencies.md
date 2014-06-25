ObsPy has a number of dependencies that need to be available when installing from source.

##### Dependencies required before installation

* C and Fortran compilers
* A supported version of Python
* NumPy

##### Dependencies that will be installed during the setup if not available

* future (for ObsPy >= 0.10)
* scipy
* matplotlib
* lxml
* sqlalchemy
* suds (for ObsPy < 0.10)
* suds-jurko (for ObsPy >= 0.10)
* argparse (for ObsPy > 0.10 and Python 2.6)

##### Optional, but recommended dependencies

* basemap

##### Additional dependencies required/optional for running the test suite
* flake8
* mock (for ObsPy > 0.10 and Python < 3.3)
* nose
* pyimgur (for ObsPy >= 0.10)