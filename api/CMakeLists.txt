project(CLPapi)

# cmake flags/requirements
set(CMAKE_EXPORT_COMPILE_COMMANDS ON) # for IDEs
set(CMAKE_POSITION_INDEPENDENT_CODE ON) # for compiling shared lib
cmake_minimum_required (VERSION 3.5)
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# determine host platform
if (CMAKE_HOST_WIN32)
  set(WINDOWS 1)
elseif(CMAKE_HOST_APPLE)
  set(MACOS 1)
elseif(CMAKE_HOST_UNIX)
  set(LINUX 1)
endif()

set(COIN_LIB_HINTS
  extern/coinor/platforms/win/dist/lib
  extern/coinor/platforms/linux/dist/lib
  extern/coinor/platforms/macos/dist/lib)

# coin files
find_library(CLP_COINUTILS CoinUtils HINTS ${COIN_LIB_HINTS})
find_library(CLP_OSI Osi HINTS ${COIN_LIB_HINTS})
find_library(CLP_OSICLP OsiClp HINTS ${COIN_LIB_HINTS})
find_library(CLP_CLP Clp HINTS ${COIN_LIB_HINTS})
include_directories(extern/coinor/dist/include/coin)

add_subdirectory(extern/catch)
add_subdirectory(src)
add_subdirectory(test)
