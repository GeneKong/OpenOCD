cmake_minimum_required (VERSION 3.0)
project (OpenOCD)

INCLUDE (CheckIncludeFiles)
SET(OPENOCD_VERSION 0.10.0)

include(config.cmake)

find_path(LIBUSB1_INCLUDE_DIR libusb.h
	HINTS ${CMAKE_SYSTEM_INCLUDE_PATH} D:/mingw/include
	PATH_SUFFIXES libusb-1.0)
	
find_path(HIDAPI_INCLUDE_DIR hidapi.h
	HINTS ${CMAKE_SYSTEM_INCLUDE_PATH} D:/mingw/include
	PATH_SUFFIXES hidapi)
	
add_definitions(-DHAVE_CONFIG_H -DPKGDATADIR="../../share/openocd" -DBINDIR="../../bin" -D__USE_MINGW_ANSI_STDIO=1)
include_directories(${CMAKE_CURRENT_BINARY_DIR} ${LIBUSB1_INCLUDE_DIR} ${HIDAPI_INCLUDE_DIR} D:/mingw/include D:/MinGW/i686-w64-mingw32/include)
set(CMAKE_C_FLAGS "-std=gnu99")

add_subdirectory(jimtcl-cmake)
add_subdirectory(src)

INSTALL(DIRECTORY tcl/ DESTINATION share/openocd/scripts)
INSTALL(DIRECTORY contrib DESTINATION share/openocd)
