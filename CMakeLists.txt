CMAKE_MINIMUM_REQUIRED(VERSION 2.8) 

PROJECT(libQingStor)

SET(CMAKE_VERBOSE_MAKEFILE ON CACHE STRING "Verbose build." FORCE)

SET(CMAKE_MODULE_PATH "${CMAKE_CURRENT_SOURCE_DIR}/CMake" ${CMAKE_MODULE_PATH})

INCLUDE(Functions)
INCLUDE(Options)

IF (WIN32) 
	INCLUDE(ExternalProject)
	ADD_DEFINITIONS(-DWIN32)
ELSE ()
	FIND_PACKAGE(OpenSSL REQUIRED)
	FIND_PACKAGE(Curl REQUIRED)	
	OPTION (INSTALL_SDK_HEADERS "Request installation of headers." ON)
ENDIF()  

# add preprocesser macro
ADD_DEFINITIONS(-DCURL_STATICLIB)
ADD_DEFINITIONS(-DYAML_DECLARE_STATIC)

IF (WIN32) 
ADD_SUBDIRECTORY(3rdparty) 
ENDIF() 
ADD_SUBDIRECTORY(src lib)




