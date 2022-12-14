We use the [future](http://python-future.org/) library and only support python >= 3.3. The motivation for Python 3 is best summarized in this [article](http://python-notes.curiousefficiency.org/en/latest/python3/questions_and_answers.html). [Porting-to-python-3](http://lucumr.pocoo.org/2013/5/21/porting-to-python-3-redux/) is a nice description how to support python 3 via a single code base.

### str vs. bytes
On Python 3 strings are now internally Unicode, bytes are their encoded representation (see e.g. this brilliant [video](http://pyvideo.org/video/948/pragmatic-unicode-or-how-do-i-stop-the-pain)).

[lxml](http://lxml.de) can deal with strings and bytes but treats them differently. Strings must not have an xml encoding declaration - it will raise otherwise. Bytes on the other hand can, and probably should (otherwise it defaults to utf-8) have an encoding declaration, see also [lxml FAQ](http://lxml.de/FAQ.html#why-can-t-lxml-parse-my-xml-from-unicode-strings).

The idea is to to represent raw content like waveforms, XML files or URL request by bytes and BytesIO. We internally convert them to Unicode / str such that the user of the library, will only deal with strings (e.g. `Trace.stats`).

### hasattr
Python 3 `hasattr()` expects an `AttributeError` no `KeyError` to be raised if the attribute is not found. Thus in order to allow `hasattr()` of an `AttribDict`, `__getattr__` must raise an `AttributeError` instead of an `KeyError`. This was not the case in the past. This change affects many places in our code and might also break some third party code.

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
In contrast to Python 2 dictionaries are now really arbitrary order and the order changes often between test runs. `sorted` is here your friend.

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
It's pretty simple: _always_ use `str`, unless communicating externally, because you should use a definite encoding. In other words, all file reading should be decoded (either through the text mode, or loading binary and decoding manually) and all file writing should be encoded. Python 2 allows you to be a bit lazy and mix the two; Python 3 does not.

The typical pitfall is: Our tests are reading bytes but not decoding them, and the writes in the new code are not encoding the strings to bytes.

A single code base bytes and str support for python 2 and 3 is quite a challenge. The following examples shows how the following python 3 decode encode can work with python 2:

#### python 3
```python
>>> byte = b'b\xc3\xa4h'
>>> print(byte.decode())
b??h
>>> string = "b??h"
>>> print(string.encode())
b'b\xc3\xa4h'
```

#### python 2 (python 3 compatible via future library)
See also the future package [str](http://python-future.org/str_object.html?highlight=decode#str), [bytes](http://python-future.org/what_else.html?highlight=decode#bytes) documentation. However, quite a few external libraries cannot deal with these types from the future package.
```python
>>> from __future__ import print_function
>>> from future.builtins import str, bytes
>>> byte = bytes(b'b\xc3\xa4h')
>>> print(byte.decode())
b??h
>>> string = str(u"b??h")
b'b\xc3\xa4h'
```

#### python 2 (python 3 compatible via 'utf-8' argument)
This is quite similar to the ipython's [py3compat](https://github.com/ipython/ipython/blob/master/IPython/utils/py3compat.py#L20) and the method of the old [#203 pull request](https://github.com/obspy/obspy/pull/203/files#diff-bc24580f1745d517c0153521a8f6570fR32)
```python
>>> from __future__ import print_function
>>> byte = b'b\xc3\xa4h'
>>> print(byte.decode('utf-8'))
b??h
>>> string = u"b??h"
>>> string.encode('utf-8')
'b\xc3\xa4h'
```

