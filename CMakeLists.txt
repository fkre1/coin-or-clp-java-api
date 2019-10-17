project(CLPapi)

# cmake flags/requirements
set(CMAKE_EXPORT_COMPILE_COMMANDS ON) # for IDEs
set(CMAKE_POSITION_INDEPENDENT_CODE ON) # for compiling shared lib
cmake_minimum_required (VERSION 3.5)
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# coin files
find_library(CLP_COINUTILS CoinUtils HINTS extern/coinor/dist/lib)
find_library(CLP_OSI Osi HINTS extern/coinor/dist/lib)
find_library(CLP_OSICLP OsiClp HINTS extern/coinor/dist/lib)
find_library(CLP_CLP Clp HINTS extern/coinor/dist/lib)
include_directories(extern/coinor/dist/include/coin)

add_subdirectory(extern/catch)
add_subdirectory(src)
add_subdirectory(test)
