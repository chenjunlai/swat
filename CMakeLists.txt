cmake_minimum_required(VERSION 2.8)

project(swat Fortran)

set(CPACK_PACKAGE_VERSION_MAJOR 2012)
set(CPACK_PACKAGE_VERSION_MINOR 591)
set(CPACK_PACKAGE_VERSION_PATCH "1")

option(USE_GPROF "Profile the project using gprof" OFF)
if(USE_GPROF)
  message("Adding profiling info for gprof...")
  set(CMAKE_Fortran_FLAGS "${CMAKE_Fortran_FLAGS} -pg")
endif(USE_GPROF)

set(CMAKE_Fortran_FLAGS_COVERAGE "-fprofile-arcs -ftest-coverage")
set(CMAKE_Fortran_FLAGS_LLVM "-fplugin=dragonegg -O4")

add_subdirectory(src)

set(CPACK_GENERATOR "ZIP")

set(CPACK_INSTALL_CMAKE_PROJECTS
  "c:/workspace/swat/build/Release;swat;ALL;/"
  "c:/workspace/swat/build/Debug;swat;ALL;/"
  )
include(CPack)
