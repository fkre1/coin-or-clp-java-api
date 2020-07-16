# coin-or-illp-api

ILP solver API for FragTree computation using the coin-or library

## dependencies
- `gfortran` for coin-or
- `jdk` for Java Native Interface (JNI) libraries

## compile

``` shell
mkdir build
cd build
cmake ..
cmake --build . --target install
```
test with

``` shell
cd test
ctest
```

To compile without testing, replace `cmake ..` with `cmake -DBUILD_TESTING=0 ..`
### target-specific compilation

#### Windows

Windows libraries can be compiled with MSYS2 for 32 and 64 bit on the
same machine.

Run these commands in the MSYS2 MinGW 32/64bit (depending on the
desired target architecture: "32" or "64" as `TARGET_ARCH`):

``` shell
mkdir build
cd build
cmake -G "MSYS Makefiles" -DTARGET_ARCH=$TARGET_ARCH ..
cmake --build . --target install
```

Notes:
- coinor libraries might have to be compiled beforehand (also in the MSYS2
  MinGW 32/64bit shell).
- `TARGET_ARCH` ensures that the compiled libraries will be put into
  the correct install directory
- `CLPModel was not found in this scope`: if compilation fails due to
  this error, all references to CLPModel.hpp have to be changed to
  CLPModel.h (for unknown reasons, the header extension has to be *.h
  on Windows; this might also apply to OSX!)

#### Linux

Ensure that the dependencies are installed, then just use the commands
listed at the top.


#### OSX

Additional dependencies like `cmake` might have to be installed (e.g.,
via `homebrew`, see [coin-or
README](api/extern/coinor/README.md)). Changing references from
CLPModel.hpp to CLPModel.h might also be required (see above under "Windows").

Otherwise, compile as stated at the top.

As linking under OSX creates absolute paths for dependencies, these
have to be adapted for deploying CLPModelWrapper. This can be achieved
by copying required dependencies into the [resource
folder](src/main/resources/native/osx/) and using the [`int`
script](mac_utils/int).
