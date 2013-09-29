Protocol Buffers - Google's data interchange format
Copyright 2008 Google Inc.
http://code.google.com/apis/protocolbuffers/

CMake - C++ Installation - Unix / MacOSX / Windows
=======================

To build and install the C++ Protocol Buffer runtime and the Protocol
Buffer compiler (protoc) execute the following:

  $ mkdir build
  $ cd build
  $ cmake ../
  $ cmake --build .


Binary Compatibility Warning
============================

Due to the nature of C++, it is unlikely that any two versions of the
Protocol Buffers C++ runtime libraries will have compatible ABIs.
That is, if you linked an executable against an older version of
libprotobuf, it is unlikely to work with a newer version without
re-compiling.  This problem, when it occurs, will normally be detected
immediately on startup of your app.  Still, you may want to consider
using static linkage.

Java and Python Installation
============================

The Java and Python runtime libraries for Protocol Buffers are located
in the java and python directories.  See the README file in each
directory for more information on how to compile and install them.
Note that both of them require you to first install the Protocol
Buffer compiler (protoc), which is part of the C++ package.

Usage
=====

The complete documentation for Protocol Buffers is available via the
web at:

  http://code.google.com/apis/protocolbuffers/
