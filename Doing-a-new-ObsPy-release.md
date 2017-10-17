# Doing a New ObsPy Release

Here's a short summary of how to do a new ObsPy release (and properly ;-).

### Make a `"Release X.X.X"` Issue on GitHub

..including the full checklist of TODOs, e.g. copying the initial post from https://github.com/obspy/obspy/issues/1562.

### Check If All Tests Pass Locally

Check that tests work locally on `master` branch, also running all network tests (e.g. `$ obspy-runtests --all`).
It's also a good idea to check that CI is passing tests on current master branch commit (e.g. look up commit status in commit timeline: https://github.com/obspy/obspy/commits/master).

### Make a Source Distribution Zipball and Upload it for Everybody to Test

This should be done
 - using an Anaconda environment that has all ObsPy dependencies
 - but does not have ObsPy installed in it
 - in a "cleanroom" git repository of current master (no untracked files, local changes etc.)

As the cleanroom it's recommended to create a fresh git clone of upstream obspy in `/tmp`:

```bash
$ cd /tmp
$ git clone https://github.com/obspy/obspy obspy-clean
$ cd /tmp/obspy-clean
```

If not done yet, create a git tag for the release, e.g. for a release candidate `6` to version `1.1.0`, and push the tag to the ObsPy upstream repository:

```bash
$ git tag -a '1.1.0rc6' -m '1.1.0rc6'
$ git push --tags
Counting objects: 1, done.
Writing objects: 100% (1/1), 172 bytes | 0 bytes/s, done.
Total 1 (delta 0), reused 0 (delta 0)
To github.com:obspy/obspy
 * [new tag]             1.1.0rc6 -> 1.1.0rc6
```

Now create the source distribution ("sdist") zipball, making sure that file permissions are correct inside the zipball (make sure to use the `python` in an appropriate Python environment like stated above):

```bash
$ umask 0022 && chmod -R a+rX . && python setup.py sdist --format=zip
running sdist
running egg_info
/home/megies/anaconda/envs/default/lib/python2.7/distutils/dist.py:972: UserWarning: 
`build_src` is being run, this may lead to missing
files in your sdist!  You want to use distutils.sdist
instead of the setuptools version:

    from distutils.command.sdist import sdist
    cmdclass={'sdist': sdist}"

See numpy's setup.py or gh-7131 for details.
  cmd_obj.run()
running build_src
build_src
building extension "libgse2_Linux_64bit_py27" sources
building extension "libmseed_Linux_64bit_py27" sources
building extension "libsegy_Linux_64bit_py27" sources
building extension "libsignal_Linux_64bit_py27" sources
building extension "libevresp_Linux_64bit_py27" sources
building extension "libtau_Linux_64bit_py27" sources
building data_files sources
build_src: building npy-pkg config files
creating obspy.egg-info
writing requirements to obspy.egg-info/requires.txt
writing obspy.egg-info/PKG-INFO
writing namespace_packages to obspy.egg-info/namespace_packages.txt
writing top-level names to obspy.egg-info/top_level.txt
writing dependency_links to obspy.egg-info/dependency_links.txt
writing entry points to obspy.egg-info/entry_points.txt
writing manifest file 'obspy.egg-info/SOURCES.txt'
reading manifest file 'obspy.egg-info/SOURCES.txt'
reading manifest template 'MANIFEST.in'
no previously-included directories found matching 'obspy/*/docs'
writing manifest file 'obspy.egg-info/SOURCES.txt'
warning: sdist: standard file not found: should have one of README, README.rst, README.txt

running check
creating obspy-1.1.0rc6
creating obspy-1.1.0rc6/misc
creating obspy-1.1.0rc6/misc/docs
creating obspy-1.1.0rc6/misc/docs/source
creating obspy-1.1.0rc6/misc/docs/source/_ext
creating obspy-1.1.0rc6/misc/docs/source/_ext/autosummary
creating obspy-1.1.0rc6/misc/docs/source/_images
creating obspy-1.1.0rc6/misc/docs/source/_images/expensive_plots
creating obspy-1.1.0rc6/misc/docs/source/_static
[...]
creating obspy-1.1.0rc6/obspy/taup/tests/data
creating obspy-1.1.0rc6/obspy/taup/tests/data/TauP_test_data
creating obspy-1.1.0rc6/obspy/taup/tests/images
copying files to obspy-1.1.0rc6...
copying CHANGELOG.txt -> obspy-1.1.0rc6
copying CONTRIBUTING.md -> obspy-1.1.0rc6
copying CONTRIBUTORS.txt -> obspy-1.1.0rc6
copying LICENSE.txt -> obspy-1.1.0rc6
copying MANIFEST.in -> obspy-1.1.0rc6
[...]
copying obspy/taup/tests/images/traveltimes_many_phases_multiple_degrees.png -> obspy-1.1.0rc6/obspy/taup/tests/images
copying obspy/taup/tests/images/traveltimes_plot_all_False.png -> obspy-1.1.0rc6/obspy/taup/tests/images
Writing obspy-1.1.0rc6/setup.cfg
creating dist
creating 'dist/obspy-1.1.0rc6.zip' and adding 'obspy-1.1.0rc6' to it
adding 'obspy-1.1.0rc6/setup.cfg'
adding 'obspy-1.1.0rc6/PKG-INFO'
adding 'obspy-1.1.0rc6/setup.py'
adding 'obspy-1.1.0rc6/runtests.py'
[...]
adding 'obspy-1.1.0rc6/misc/docs/source/_ext/autosummary/generate.py'
adding 'obspy-1.1.0rc6/misc/docs/source/_ext/autosummary/__init__.py'
removing 'obspy-1.1.0rc6' (and everything under it)
```

This should have created a file `obspy-1.1.0rc6.zip` in subdirectory `sdist/`.
Upload the file as an attachment in a comment in the release issue created in the previous step, and ask others to start testing the release candidate. Also, note down the `SHA256` sum of the zipball, we'll need it when checking conda packaging status:

```bash
$ sha256sum obspy-1.1.0rc6.zip
0a09a198bd48b32b445d9a307202a26d12f8f057a67ee836f483c6a88b423b4e  obspy-1.1.0rc6.zip
```

After uploading, the "cleanroom" obspy clone can be cleaned out again (for more iterations, i.e. pulling in later commits and creating follow-up release candidates) by doing:

```bash
$ # do NOT do this in any of your other git repositories without thinking thrice!!
$ # This will completely delete any local changes, untracked files etc.!!
$ git clean -fdx  # don't do this at $HOME, kids! ;-)
```

### Make Sure Tests Pass for the Release Candidate Zipball

Any testing of the Release Candidate should be done installing the sdist zipball.
Test results for one specific version can be summarized here: http://tests.obspy.org/?version=1.1.0rc6

After going through all the testing outlined below:
 - If some tests still fail, add commits and make a new release candidate and start testing again.
 - If all tests pass, congratulations! You made it through the release cycle alive!

##### Check that tests work locally, also running all network tests

```bash
$ pip uninstall obspy
$ pip install https://github.com/obspy/obspy/files/1391402/obspy-1.1.0rc6.zip
$ obspy-runtests --all  # report test results at the end by confirming with "y"
```

##### Check that docker tests pass

Check that tests pass in all of our docker images (Debians, Ubuntus, Fedora, CentOS, OpenSUSE), adding new images and removing end-of-life distributions as needed (see https://github.com/obspy/obspy/tree/master/misc/docker#release-lifecycle-information)

##### Check that `conda` packaging works

Create a new branch in https://github.com/obspy/obspy-feedstock/ and create a pull request against https://github.com/conda-forge/obspy-feedstock/ (do **not** push to branches in https://github.com/conda-forge/obspy-feedstock/ directly!! All pushes to that repository will result in any packages built successfully being deployed to https://anaconda.org/conda-forge/obspy immediately and automatically). Compare e.g. https://github.com/conda-forge/obspy-feedstock/pull/11 for the process.

##### Check other packaging efforts
 - fedora packaging build system

Currently done by @QuLogic

 - Debian/Ubuntu packaging via docker

This is done creating a release helper branch like here (https://github.com/megies/obspy/tree/deb_1.1.0) and then packaging debs by doing (needs `docker` installed obviously):

```bash
$ cd /path/to/local/obspy/master
$ cd misc/docker
$ ./package_debs.sh -tmegies:deb_1.1.0 debian_8_jessie_armhf
```

### Doing the final release

When everybody is happy about the release candidate, do an sdist zipball with the final release version (e.g. `1.1.0`) and distribute all packaged binaries across all channels (pypi, Anaconda cloud, Debian/Ubuntu apt repo, ...).

**TODO: Add more detailed info on all the package distribution channels..**

**TODO: Add info on how to create the MaxiConda Anaconda+Obspy+Jupyter+... installers via https://github.com/obspy/anaconda-installers**