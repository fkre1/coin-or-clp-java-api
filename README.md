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
cmake --build .
```
test with

``` shell
cd test
ctest
```

To compile without testing, replace `cmake ..` with `cmake -DBUILD_TESTING=0 ..`
