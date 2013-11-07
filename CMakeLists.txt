# Minumum build script for building the Tuvok library needed for Tuvok Commandline UVF converter

cmake_minimum_required( VERSION 2.8 )
project( TuvokDataConverter )
list( APPEND CMAKE_MODULE_PATH ${CMAKE_SOURCE_DIR}/CMake )
if( NOT BUILDYARD )
  include( Buildyard )
  return( )
endif( )

include(Common)
include(InstallFiles)
include(FindPackages)

if(NOT CMAKE_BUILD_TYPE)
  set(CMAKE_BUILD_TYPE RelWithDebInfo CACHE STRING
      "Choose the type of build, options are: None Debug Release RelWithDebInfo." FORCE)
endif(NOT CMAKE_BUILD_TYPE)

if( ${CMAKE_COMPILER_IS_GNUCXX} )
  set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS}")
  set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++0x -fno-strict-aliasing" )
endif( ${CMAKE_COMPILER_IS_GNUCXX} )

include_directories( ${TUVOK_INCLUDE_DIR}
                     ${TUVOK_INCLUDE_DIR}/exception
                     ${TUVOKCMDLINECONVERTER_SOURCE}
                     ${TUVOKCMDLINECONVERTER_SOURCE}/DebugOut 
                     ${QT_INCLUDE_DIR} )

set( TUVOKDATACONVERTER_SOURCES  ${CMAKE_SOURCE_DIR}/main.cpp
                                 ${CMAKE_SOURCE_DIR}/DebugOut/HRConsoleOut.cpp )


add_executable( TuvokDataConverter ${TUVOKDATACONVERTER_SOURCES} )
target_link_libraries ( TuvokDataConverter ${TUVOK_LIBRARY} )
install( TARGETS TuvokDataConverter RUNTIME DESTINATION bin )
