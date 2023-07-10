cmake_minimum_required(VERSION 3.8)

project(fdb-bundle)

set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} ${PROJECT_SOURCE_DIR}/lib/ecbuild/cmake)

if(DEFINED ENV{LIBRARY_PATH})
  string(REPLACE ":" ";" LIBRARY_PATH $ENV{LIBRARY_PATH})
  set(CMAKE_LIBRARY_PATH ${CMAKE_LIBRARY_PATH} ${LIBRARY_PATH})
endif()
if(DEFINED ENV{LD_LIBRARY_PATH})
  string(REPLACE ":" ";" LD_LIBRARY_PATH $ENV{LD_LIBRARY_PATH})
  set(CMAKE_LIBRARY_PATH ${CMAKE_LIBRARY_PATH} ${LD_LIBRARY_PATH})
endif()

set(CMAKE_BUILD_TYPE
    Release
    CACHE STRING "Choose the type of build, options are: Debug Release RelWithDebInfo MinSizeRel Profile." FORCE
)

option(ENABLE_AEC "Enable AEC" OFF)
add_subdirectory("${PROJECT_SOURCE_DIR}/lib/eccodes")
add_subdirectory("${PROJECT_SOURCE_DIR}/lib/eckit")
add_subdirectory("${PROJECT_SOURCE_DIR}/lib/metkit")
add_subdirectory("${PROJECT_SOURCE_DIR}/lib/fdb")
