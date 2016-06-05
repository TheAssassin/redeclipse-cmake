# CMake configuration for Red Eclipse

This CMake configuration can be used to build Red Eclipse. It is a drop-in
replacement for the existing Makefile.

## General usage instructions

This guide was written on and for building on some Linux distribution.

First, grab a copy of enet's CMake configuration (hint: it's the file
`CMakeLists.txt` in its [Github repository](https://github.com/lsalzman/enet/))
and put it into `src/enet/`.

Then you can put this repository's `CMakeLists.txt` into `src/`. Now you're
almost ready to compile Red Eclipse.

To keep your repository clean (i.e. not have any compiled binaries next to the
source files) you are strongly encouraged to create a separate directory for
the build itself. A pragmatic name would be `build`.

Change to your copy of Red Eclipse, then go into the `src/` directory and
create a directory `build` (`cd src && mkdir build`). Then run CMake to create
a Makefile (this is the default behaviour on Linux systems - note that you
can also create IDE project files and configurations for other build systems
with CMake) by running `cmake ..` in `src/build/`. Now you're ready to build
the project. Just run `make` (or `make -j<number of cpus>` to decrease
build time by compiling multiple files concurrently).

You can use the following set of commands (maybe by pasting them into a script)
that contains all the steps to build Red Eclipse:

```
cd src/
mkdir -p build/
cmake ..
make -j$(cat /proc/cpuinfo  | grep processor | wc -l)
```

If you want to clean up your environment (maybe if you change the CMake
configuration and the project configuration is broken afterwards), just remove
the build directory (`rm -rf [src/]build/`) and rerun the commands to
create a CMake configuration and build the software.


## About

The CMake configuration provided by this repository uses
[pkg-config](https://www.freedesktop.org/wiki/Software/pkg-config/) to
configure library dependencies such as SDL2. This makes cross compilation to
other systems (e.g. OS X, Windows) easier as most cross compiling toolchains
provide their own pkg-config executables.

The CMake configuration currently supports almost all the functionality the
original Makefile provides, except for the installation commands (this is work
in progress though).
