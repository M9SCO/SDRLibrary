cmake_minimum_required(VERSION 3.3.1)

PROJECT( "rtlSdrAndroid" C )

ADD_SUBDIRECTORY(librtlsdr)

FILE ( GLOB_RECURSE SOURCES_LIB "src/*.c" )

SET ( CMAKE_C_FLAGS         "-Wall" )
SET ( CMAKE_C_FLAGS_DEBUG   "-g -DDEBUG")
SET ( CMAKE_C_FLAGS_RELEASE "-O1 -DNDEBUG" ) # Keep optimization low to reduce random libusb crashes

FIND_LIBRARY( LOG_LIB log )

ADD_LIBRARY( ${PROJECT_NAME} SHARED ${SOURCES_LIB} )
TARGET_INCLUDE_DIRECTORIES( ${PROJECT_NAME} PRIVATE include )
TARGET_LINK_LIBRARIES( ${PROJECT_NAME} ${LOG_LIB} librtlsdr )