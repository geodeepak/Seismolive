Most machines nowadays have multiple cores and thus performing multiple parallel calculations in parallel is desirable. This is fairly easy to do using Python's [multiprocessing](http://docs.python.org/2/library/multiprocessing.html) module. [joblib](http://packages.python.org/joblib/) also offers a very convenient wrapper around the multiprocessing module that is worth checking out.

`multiprocessing` uses [fork](http://man7.org/linux/man-pages/man2/fork.2.html) to create new processes which unfortunately is not compatible with many implementations of BLAS/LAPACK. NumPy and thus ObsPy rely on them in a number of functions. This incompatibility results in deadlocks and other problems that are nasty to debug.

### How to find out if you are affected?

**Quick and Dirty:** The following example should finish in a couple of seconds. If it does not you have a problem.

```python
#!/usr/bin/env python
# -*- coding: utf-8 -*-
import multiprocessing
import obspy


def process(*args):
    st = obspy.read()
    # Uses problematic BLAS function.
    st.detrend("linear")

p = multiprocessing.Pool(processes=2)
p.map(process, xrange(50))
```

For a more thorough investigation the first step is to find out what BLAS/LAPACK implementation your NumPy and SciPy installations are linked against:

```bash
$ python -c "import numpy; numpy.show_config"
lapack_opt_info:
    libraries = ['openblas', 'openblas']
    library_dirs = ['/usr/local/opt/openblas/lib']
    language = f77
blas_opt_info:
    libraries = ['openblas', 'openblas']
    library_dirs = ['/usr/local/opt/openblas/lib']
    language = f77
openblas_info:
    libraries = ['openblas', 'openblas']
    library_dirs = ['/usr/local/opt/openblas/lib']
    language = f77
blas_mkl_info:
  NOT AVAILABLE
```

The same can be done with SciPy:

```bash
$ python -c "import scipy; scipy.show_config()"
...
```

In this case it links against OpenBLAS.

#### Linked against OpenBLAS
Setting the `OPENBLAS_NUM_THREADS` to `1` solves the problem in this case. This can also be done programmatically as illustrated below.

```bash
$ export OPENBLAS_NUM_THREADS=1
```

#### Linked against Accelerate/vecLib on OSX
There really is no workaround in this case. See also this discussion: http://mail.scipy.org/pipermail/numpy-discussion/2012-August/063589.html

The only option here it to either not use mulitprocessing, restrict it to only one core, or install NumPy linked against some other BLAS implementation.

#### Linked against ATLAS or MKL
There should be no problems with either of those. Most Linux distributions ship with ATLAS thus you are good to go. Otherwise installing ATLAS is an involved multi-hour process and therefore only suitable for specialists. Most commercial scientific Python distributions link against MKL which also avoids the problems. If you have a license you can of course also link against MKL yourself.


### Possible Solutions

#### Install other BLAS/LAPACK implementation
Of course not always suitable. Otherwise there are a lot of installation instructions in the web.

#### Wait for Python 3.4
Python 3.4 will have `forkserver` and `spawn` methods to start new processes. Both should avoid the problem at a slight cost of performance and convenience.

#### Wait until some other software is fixed/adopted

* clang will soon have an OpenMP implementation which should work.
* OpenBLAS might move away from OpenMP to their own thread pool implementation.
* There is a patch in the works that works around this problem for gcc OpenMP.

All of these of course will take a while and even longer until they arrive at downstream users.

#### Use some other form of distributed computing not relying on fork

* [Parallel Python](http://www.parallelpython.com/)
* [IPython Parallel](http://ipython.org/ipython-doc/stable/parallel/)
* [mpi4py](http://mpi4py.scipy.org/) or some other MPI wrapper


#### Some kind of logic to detect the problem and take action

This might be an option if you want other people to use your code. It is based on the example above and should work in all cases.

```python
#!/usr/bin/env python
# -*- coding: utf-8 -*-

# Needs to be done BEFORE numpy is imported! Single threaded performance will
# suffer for certain functions that use parallel BLAS.
import os
os.environ["OPENBLAS_NUM_THREADS"] = "1"

import multiprocessing
import numpy as np
import obspy
import warnings


config_info = str([value for key, value in
                   np.__config__.__dict__.iteritems()
                   if key.endswith("_info")]).lower()

if "accelerate" in config_info or "veclib" in config_info:
    msg = ("NumPy linked against 'Accelerate.framework'. Multiprocessing "
           "will be disabled. See "
           "https://github.com/obspy/obspy/wiki/Notes-on-Parallel-Processing-"
           "with-Python-and-ObsPy for more information.")
    warnings.warn(msg)
    # Disable by replacing with dummy implementation using threads.
    from multiprocessing import dummy
    multiprocessing = dummy  # NOQA


def process(*args):
    st = obspy.read()
    # Uses problematic BLAS function.
    st.detrend("linear")

p = multiprocessing.Pool(processes=2)
p.map(process, xrange(50))
```

### Further information

* https://github.com/xianyi/OpenBLAS/issues/294
* http://gcc.gnu.org/bugzilla/show_bug.cgi?id=60035
* https://github.com/numpy/numpy/issues/654
* https://github.com/numpy/numpy/pull/4194
* https://github.com/celery/celery/issues/1842
* http://mail.scipy.org/pipermail/numpy-discussion/2012-August/063589.html