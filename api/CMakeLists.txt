project(CLPapi)

# cmake flags/requirements
set(CMAKE_EXPORT_COMPILE_COMMANDS ON) # for IDEs
set(CMAKE_POSITION_INDEPENDENT_CODE ON) # for compiling shared lib
cmake_minimum_required (VERSION 3.5)
set(CMAKE_CXX_FLAGS "-fpermissive") # DEBUG, remove later
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
# determine architecture
if (CMAKE_SYSTEM_PROCESSOR STREQUAL "x86_64")
  set (TARGET_ARCH "64")
elseif (CMAKE_SYSTEM_PROCESSOR STREQUAL "x86"
    OR CMAKE_SYSTEM_PROCESSOR STREQUAL "i386"
    OR CMAKE_SYSTEM_PROCESSOR STREQUAL "i686")
  set (TARGET_ARCH "32")
endif()

set(COIN_LIB_HINTS
  extern/coinor/dist/lib        # locally built libraries
  extern/coinor/platforms/win/dist/lib
  extern/coinor/platforms/macos/dist/lib
  extern/coinor/platforms/linux/dist/lib)

# coin files
find_library(CLP_COINUTILS NAMES CoinUtils libCoinUtils.lib Coi HINTS ${COIN_LIB_HINTS})
find_library(CLP_OSI NAMES Osi libOsi.lib HINTS ${COIN_LIB_HINTS})
find_library(CLP_OSICLP NAMES OsiClp libOsiClp.lib HINTS ${COIN_LIB_HINTS})
find_library(CLP_CLP NAMES Clp libClp.lib HINTS ${COIN_LIB_HINTS})
if (WINDOWS)
  find_library(CLP_COINGLPK NAMES coinglpk HINTS ${COIN_LIB_HINTS})
  find_library(CLP_COINMUMPS NAMES coinmumps HINTS ${COIN_LIB_HINTS})
  find_library(CLP_COINBLAS NAMES coinblas HINTS ${COIN_LIB_HINTS})
  find_library(CLP_COINMETIS NAMES coinmetis HINTS ${COIN_LIB_HINTS})
  find_library(CLP_COINLAPACK NAMES coinlapack HINTS ${COIN_LIB_HINTS})
  find_library(GFORTRAN NAMES gfortran libgfortran-5.dll)
  find_library(BZ2 NAMES bz2 libbz2-1.dll)
  find_library(ZSTD NAMES zstd libzstd.dll)
  find_library(GMP NAMES gmp)
endif()
include_directories(extern/coinor/dist/include/coin)

add_subdirectory(extern/catch)
add_subdirectory(src)
add_subdirectory(test)
