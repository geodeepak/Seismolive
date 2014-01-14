We use the [future](http://python-future.org/) library and only support python >= 3.3. The motivation for Python 3 is best summarized in this [article](http://python-notes.curiousefficiency.org/en/latest/python3/questions_and_answers.html)

### str vs. bytes
On Python 3 strings are now internally utf-8, bytes are their ascii representation (see e.g. this brilliant [video](http://pyvideo.org/video/948/pragmatic-unicode-or-how-do-i-stop-the-pain)).

[lxml](http://lxml.de) can deal with strings and bytes but treats them differently. Strings must not have an xml encoding declaration - it will raise otherwise. Bytes on the other hand can, and probably should (otherwise it defaults to utf-8) have an encoding declaration, see also [lxml FAQ](http://lxml.de/FAQ.html#why-can-t-lxml-parse-my-xml-from-unicode-strings).

The idea is to internally make the natural choice to represent raw content like waveforms, XML files or URL request by bytes and BytesIO. We internally convert them to utf-8 / str such that the user of the library, will only deal with strings (e.g. `Trace.stats`).

### hastattr
Python 3 `hasattr()` expects an `AttributeError` no `KeyError` to be raised if the attribute is not found. Thus in order to allow `hasattr()` of an `AttribDict`, `__getattr__` must raise an `AttributeError` instead of an `KeyError`. This was not the case in the past. This change effects many places in our code and might also break some third party code.

### doctests, unicode prefix
Doctests are a pain to maintain for a python 2 and python 3 compatible code base. The problem is that the python 3 aware `str` / the compatibility `future.builtins.str` will result in:
```python
# python 3
>>> from future.builtins import str
>>> str("hello")
>>> "hello"
```
```python
# python 2
>>> from future.builtins import str
>>> str("hello")
>>> u"hello"
```

Thus there is a "u" prefix in python2 which will cause the doctests to fail. Solutions range from trying to use print everywhere, use `#doctest: +ELLIPSIS` (e.g. ..."hello"), or just skipping the test. They are all quite awful. 

### arbitrary order dictionaries
In contrast to Python 2 dictionaries are now really arbitrary order and the order changes often between test runs. `sorted` is here your frind.

### accessing single characters in byte strings
```python
In [11]: s = b"hallo"

In [12]: s[3]  # intuitively I expect "l"
Out[12]: 108

In [13]: chr(s[3])
Out[13]: 'l'

In [14]: s[3:4]   # I often used this
Out[14]: b'l'
```

### native_str
Some libraries have troubles with `future.builtins.str` for a single code base python 2 and 3 support. For these cases, `native_str` is your friend, e.g.:
```python
np.ctypeslib.ndpointer(dtype='int32', ndim=1, flags=native_str('C_CONTIGUOUS'))
```

### decode and encode
A single code base bytes and str support for python 2 and 3 is quite a challenge. The following examples shows how the following the following python 3 decode encode can work with python 2:

#### python 3
```python
>>> byte = b'b\xc3\xa4h'
>>> print(byte.decode())
bäh
>>> string = "bäh"
>>> print(string.encode())
b'b\xc3\xa4h'
```

#### python 2 (python 3 compatible via future library)
See also the future package [str](http://python-future.org/str_object.html?highlight=decode#str), (bytes)[http://python-future.org/what_else.html?highlight=decode#bytes] documentation. However, quite a few external libraries cannot deal with these types from the future package.
```python
>>> from __future__ import print_function
>>> from future.builtins import str, bytes
>>> byte = bytes(b'b\xc3\xa4h')
>>> print(byte.decode())
bäh
>>> string = str(u"bäh")
b'b\xc3\xa4h'
```

#### python 2 (python 3 compatible via 'utf-8' argument)
This is quite similar to the ipython's [py3compat](https://github.com/ipython/ipython/blob/master/IPython/utils/py3compat.py#L20) and the method of the old [#203 pull request](https://github.com/obspy/obspy/pull/203/files#diff-bc24580f1745d517c0153521a8f6570fR32)
```python
>>> from __future__ import print_function
>>> byte = b'b\xc3\xa4h'
>>> print(byte.decode('utf-8'))
bäh
>>> string = u"bäh"
>>> string.encode('utf-8')
'b\xc3\xa4h'
```

