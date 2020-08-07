project(CLPWrapper CXX)

find_package(JNI REQUIRED)
set(CLPModel_HEADER "CLPModel.hpp")
if (WINDOWS)
  find_package(ZLIB REQUIRED)
  # if .hpp on windows: "not defined in this scope" errors
  set(CLPModel_HEADER "CLPModel.h")
endif()

add_library(CLPModel STATIC CLPModel.cpp ${CLPModel_HEADER})
add_library(CLPModelWrapper_JNI SHARED CLPModelWrapper_JNI.cpp)
if(WINDOWS)
  # no lib as prefix for windows DLL, so java's loadLibrary recognizes it
  set_target_properties(CLPModelWrapper_JNI PROPERTIES PREFIX "")
endif()
target_include_directories(CLPModelWrapper_JNI PUBLIC ${JNI_INCLUDE_DIRS})
target_include_directories(CLPModel PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})
target_link_libraries(CLPModel PUBLIC
  # definitely needed CLP libraries
  ${CLP_CLP} ${CLP_OSICLP} ${CLP_OSI} ${CLP_COINUTILS}
  # auxiliary libraries, needed by windows
  ${CLP_COINGLPK} ${CLP_COINLAPACK} ${CLP_COINMUMPS}
  ${CLP_COINBLAS} ${CLP_COINMETIS}
  # system libraries, needed by windows
  ${GFORTRAN} ${BZ2} ${ZLIB_LIBRARIES} ${GMP})
target_link_libraries(CLPModelWrapper_JNI PRIVATE CLPModel ${JNI_LIBRARIES})

# install for maven packaging
set(CMAKE_INSTALL_PREFIX "${PROJECT_SOURCE_DIR}/../build/")
set(MAVEN_PATH "native")
if(WINDOWS)
  # only the libCLPModelWrapper_JNI.dll is needed
  # install (DIRECTORY "${PROJECT_SOURCE_DIR}/../platforms/win"
  #   DESTINATION "${CMAKE_INSTALL_PREFIX}${MAVEN_PATH}/win${TARGET_ARCH}")
  install (TARGETS CLPModelWrapper_JNI DESTINATION
    "${CMAKE_INSTALL_PREFIX}${MAVEN_PATH}/w${TARGET_ARCH}")
elseif(LINUX)
  # dependencies needed (NOTE: copy manually!)
  # install (DIRECTORY "${PROJECT_SOURCE_DIR}/../platforms/linux" DESTINATION
  #   "${CMAKE_INSTALL_PREFIX}${MAVEN_PATH}/linux${TARGET_ARCH}")
  install (TARGETS CLPModel CLPModelWrapper_JNI DESTINATION
    "${CMAKE_INSTALL_PREFIX}${MAVEN_PATH}/l${TARGET_ARCH}")
elseif(MACOS)
  # dependencies needed (NOTE: copy manually!)
  # # ${TARGET_ARCH} probably doesn't work
  # install (DIRECTORY "${PROJECT_SOURCE_DIR}/../platforms/macos"
  #   DESTINATION "${CMAKE_INSTALL_PREFIX}${MAVEN_PATH}/macos")
  install (TARGETS CLPModel CLPModelWrapper_JNI DESTINATION
    "${CMAKE_INSTALL_PREFIX}${MAVEN_PATH}/osx")
endif()
