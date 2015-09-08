# Minumum build script for building the Tuvok library needed for Tuvok Commandline UVF converter

cmake_minimum_required(VERSION 2.8 FATAL_ERROR)
project(TuvokDataConverter)

list(APPEND CMAKE_MODULE_PATH ${PROJECT_SOURCE_DIR}/CMake
  ${CMAKE_SOURCE_DIR}/CMake/common)

set(VERSION_MAJOR "0")
set(VERSION_MINOR "1")
set(VERSION_PATCH "0")
set(VERSION_ABI 1)

include(GitExternal)
include(Common)

common_package(Tuvok REQUIRED)
common_package(Boost REQUIRED COMPONENTS program_options)

include_directories( ${TUVOK_INCLUDE_DIR}
                     ${TUVOK_INCLUDE_DIR}/exception
                     ${TUVOKCMDLINECONVERTER_SOURCE}
                     ${TUVOKCMDLINECONVERTER_SOURCE}/DebugOut 
                     ${QT_INCLUDE_DIR} )

set( TUVOKDATACONVERTER_SOURCES  ${CMAKE_SOURCE_DIR}/main.cpp
                                 ${CMAKE_SOURCE_DIR}/DebugOut/HRConsoleOut.cpp )


add_executable( TuvokDataConverter ${TUVOKDATACONVERTER_SOURCES} )
target_link_libraries ( TuvokDataConverter ${TUVOK_LIBRARY}  
  ${Boost_PROGRAM_OPTIONS_LIBRARY})
install( TARGETS TuvokDataConverter RUNTIME DESTINATION bin )
