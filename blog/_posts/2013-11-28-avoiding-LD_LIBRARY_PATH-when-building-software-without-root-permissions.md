---
layout: post
title: "Avoiding LD_LIBRARY_PATH when building software without root permissions"
description: "Preventing library not found errors when building software on systems where you don't have root permissions"
tags: [programming]
---

On a Linux machine, when building software without root permissions, one cannot install libraries into system-wide directories such as `/usr/lib`. This commonly results in error messages such as "cannot open shared object file: No such file or directory". The oft-cited workaround is via the environment variable `LD_LIBRARY_PATH`. This post shows how to avoid having to use `LD_LIBRARY_PATH`.

Suppose that your libraries are installed in `/home/user/lib`. It is possible to embed this search path directly into the executable using  the linker flag `-R`. An example commandline using `gcc` is:

    $ gcc -Wl,-rpath=/home/user/lib -L/home/user/lib ...

This links against libraries in `/home/user/lib` (customise to your actual username) and also embeds that same directory into the binary. No `LD_LIBRARY_PATH` environment variable is needed.

## Using these settings with the Matlab MEX compiler

If a MEX file cannot find a library then you will get an error message such as:

    Invalid MEX-file '...': ...: cannot open shared object file: No such file or directory

To fix this, you need to embed the library search path in your MEX file. MEX compiler settings are read from the `mexopts.sh` script in `~/.matlab/R2013a`. (Adjust the path according to your version of Matlab.)

I inserted the following line to `mexopts.sh`

    LDFLAGS="$LDFLAGS -Wl,-rpath=/home/user/lib -L/home/user/lib"

where `user` stands for my actual username. This is inserted after the line where `LDFLAGS` is defined, because it extends that definition by adding new arguments.
