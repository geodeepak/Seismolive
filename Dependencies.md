ObsPy has a number of dependencies that need to be available when installing from source.

##### Dependencies required before installation

* C compiler
* A supported version of Python
* NumPy

##### Dependencies that will be installed during the setup if not available

* future
* scipy
* matplotlib
* lxml
* sqlalchemy
* suds-jurko (for obspy.neries)
* argparse (for Python < 2.7)

##### Optional, but recommended dependencies

* basemap

##### Additional dependencies required/optional for running the test suite
* flake8
* mock (for Python < 3.3)
* nose
* pyimgur