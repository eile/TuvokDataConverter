# Minumum build script for building the Tuvok library needed for Volume Renderer

cmake_minimum_required(VERSION 2.8)
project( TuvokCmdLineConverter )

list(APPEND CMAKE_MODULE_PATH ${CMAKE_SOURCE_DIR}/CMakeLocal)
find_package( TuvokLibrary REQUIRED )

if(NOT CMAKE_BUILD_TYPE)
  set(CMAKE_BUILD_TYPE RelWithDebInfo CACHE STRING
      "Choose the type of build, options are: None Debug Release RelWithDebInfo." FORCE)
endif(NOT CMAKE_BUILD_TYPE)

if( ${CMAKE_COMPILER_IS_GNUCXX} )
  set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS}")
  set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++0x -fno-strict-aliasing" )
endif( ${CMAKE_COMPILER_IS_GNUCXX} )


include_directories( ${TUVOK_INCLUDE_DIR} 
                     ${TUVOKCMDLINECONVERTER_SOURCE}
                     ${TUVOKCMDLINECONVERTER_SOURCE}/DebugOut 
                     ${QT_INCLUDE_DIR} )

set( TUVOKCMDLINECONVERTER_SOURCES  ${TUVOKCMDLINECONVERTER_DIR}/main.cpp
                                    ${TUVOKCMDLINECONVERTER_DIR}/DebugOut/HRConsoleOut.cpp )


add_executable( TuvokCmdLineConverter ${TUVOKCMDLINECONVERTER_SOURCES} )
target_link_libraries ( TuvokCmdLineConverter ${TUVOK_LIBRARY} ) 
install( TARGETS TuvokCmdLineConverter EXECUTABLE DESTINATION bin )

