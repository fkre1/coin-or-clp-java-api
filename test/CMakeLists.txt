project(CLP_tests)

include(CTest)

if (BUILD_TESTING)
  add_executable(CLPTest CLPTest.cpp)
  target_link_libraries(CLPTest PRIVATE CLPModel catch)
  add_test(NAME CLPTest COMMAND CLPTest)
  configure_file("glp_sirius_test.mps" .)
endif()
