cmake_minimum_required(VERSION 3.8)

set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} ${CMAKE_SOURCE_DIR}/lib/ecbuild/cmake)

project(fdb-bundle)

include(ExternalProject)

externalproject_add(
  eccodes
  SOURCE_DIR ${CMAKE_SOURCE_DIR}/lib/eccodes
  INSTALL_COMMAND ""
)
externalproject_get_property(eccodes BINARY_DIR)
set(eccodes_ROOT ${BINARY_DIR})

externalproject_add(
  eckit
  SOURCE_DIR ${CMAKE_SOURCE_DIR}/lib/eckit
  INSTALL_COMMAND ""
)
externalproject_get_property(eckit BINARY_DIR)
set(eckit_ROOT ${BINARY_DIR})

externalproject_add(
  metkit
  SOURCE_DIR ${CMAKE_SOURCE_DIR}/lib/metkit
  INSTALL_COMMAND ""
  DEPENDS eccodes eckit
  CMAKE_ARGS -Deccodes_ROOT=${eccodes_ROOT} -Deckit_ROOT=${eckit_ROOT}
)
externalproject_get_property(metkit BINARY_DIR)
set(metkit_ROOT ${BINARY_DIR})

externalproject_add(
  fdb
  SOURCE_DIR ${CMAKE_SOURCE_DIR}/lib/fdb
  INSTALL_COMMAND ""
  DEPENDS eccodes eckit metkit
  CMAKE_ARGS -Deccodes_ROOT=${eccodes_ROOT} -Deckit_ROOT=${eckit_ROOT} -Dmetkit_ROOT=${metkit_ROOT}
)
