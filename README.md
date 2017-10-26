udt4py
======

libudt4 Python wrapper written with Cython.

Tested with Python 2.7 and Python 3.3 on Linux. In buffer operations bytes,
bytearray and memoryview objects are supported, allowing zero-copy operations.

In order to build the native module, execute:

```bash
python3 setup.py build_ext --inplace
```

In Ubuntu, you will need ``cython3`` package.
To run the tests, execute:

```bash
PYTHONPATH=`pwd` nosetests3 -w tests --tests udt_socket,udt_epoll
```

Example usage:

```python
from udt4py import UDTSocket


if __name__ == "__main__":
    socket = UDTSocket()
    socket.bind("0.0.0.0:7777")
    socket.listen()
    channel = socket.accept()
    msg = bytearray(5)
    channel.recv(msg)
```

Released under Simplified BSD License.
Copyright (c) 2014, Samsung Electronics Co.,Ltd.

# 补充
站在巨人的肩膀上，修改了一下头文件的定义使其支持windows，（Cython不支持在if下cdef，所以改了之后没法再支持linux了），当然epoll没法用了。需要把udt放在include目录下，然后执行
```
python3 setup.py build
```
然后build目录下就会有pyd文件了，拷贝时不要忘了udt.dll文件。