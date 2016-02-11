![Logo](http://i.imgur.com/EnyL91L.png)


### Rewritten SAC module

The ObsPy SAC plugin has been rewritten, resulting in two changes in `obspy.read` and `Stream/Trace.write` using SAC files, and significant changes in the lower-level handling.  

**Changes in `obspy.read`**

1. The new SAC module will preserve the original `iztype` and reference time (if found in `Trace.stats.sac`), thus also preserving any existing relative time headers (e.g. travel-time picks).  This better supports round-trip SAC file processing.  The previous SAC module generally produced `iztype = ib` SAC files without checking the previous header `iztype`, which had the possibility of producing invalid relative time headers.  
2. `obspy.read` does not put unset SAC headers into `trace.stats.sac` unless `debug_headers=True` is set.  This is a change in default behavior.

**`SACTrace` replaces `SacIO`**

The recommended way of reading and writing SAC files is still using `obspy.read`, but users of `obspy.sac.SacIO` will need to be aware of changes.  The old `obspy.sac.sacio` has be rewritten and recycled into a new `obspy.io.sac` subpackage, and the old `SacIO` class is replaced by the `SACTrace` class, which provides a simplified I/O interface and more flexible reference time and relative-time header handling.

The previous `SacIO` I/O methods, `ReadSacFile`, `ReadSacHeader`, `ReadSacXY`, `ReadSacXYHeader`, `WriteSacBinary`, `WriteSacHeader`, and `WriteSacXY` are replaced by just two methods: `SACTrace.read` and `SACTrace.write`.  Reading and writing of header-only vs. full-file, ASCII vs. binary, and big vs little-endian byte order are controlled by keywords in these two methods.  Additionally, producing a `SACTrace` instance from a file does not require initializing an empty class instance first, as was required by `SacIO`.

```python
from obspy.io.sac import SACTrace

# read from a binary file
sac = SACTrace.read(filename)

# read or write header only
sac = SACTrace.read(filename, headonly=True)
sac.write(filename, headonly=True)

# read from an ASCII file, write a big-endian binary SAC file
sac = SACTrace.read(filename, ascii=True)
sac.write(filename, byteorder='big')
```

The new `SACTrace` class also has more flexible reference time and relative time header handling.  In `SACTrace`, the SAC reference time (a combination of `nzyear`, `nzjday`, `nzhour`, `nzmin`, `nzsec`, and `nzmsec`) can be accessed and manipulated through the `SACTrace.reftime` attribute (property), which is a `UTCDateTime` instance.  The reference time (or any of the relative time headers) can be modified by adding/subtracting seconds, or by setting it to a new `UTCDateTime` instance entirely.  Any changes to `reftime` will be reflected in the "nz" time headers, and will trigger corresponding changes in the relative time headers `a, e, f, t0-t9` such that they stay correctly referenced in absolute time.

```python
sac = SACTrace(nzyear=2000, nzjday=1, nzhour=0, nzmin=0, nzsec=0, nzmsec=0,
               t1=23.5, data=numpy.arange(100))
sac.reftime, sac.b, sac.e, sac.t1
# (2000-01-01T00:00:00.000000Z, 0.0, 99.0, 23.5)

# Move reference time by relative seconds, relative time headers are preserved.
sac.reftime -= 2.5
sac.reftime, sac.b, sac.e, sac.t1
# (1999-12-31T23:59:57.500000Z, 2.5, 101.5, 26.0)

# Set reference time to new absolute time, relative time headers are preserved.
sac.reftime = UTCDateTime(2000, 1, 1, 0, 2, 0, 0)
sac.reftime, sac.b, sac.e, sac.t1
# (2000-01-01T00:02:00.000000Z, -120.0, -21.0, -96.5)
```

Additionally, manually changing the `iztype` header will similarly preserve the absolute referencing of relative time headers.
