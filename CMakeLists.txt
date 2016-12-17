cmake_minimum_required(VERSION 2.8)

project(openvr)

include_directories(src headers)
file(GLOB CPP_FILES
  "src/**.cpp"
)

IF(${CMAKE_SYSTEM_NAME} MATCHES "Darwin")
	add_definitions(-DOSX -DPOSIX)
	set_source_files_properties(
		src/vrcommon/pathtools_public.cpp
		src/vrcommon/vrpathregistry_public.cpp
		PROPERTIES COMPILE_FLAGS "-x objective-c++")
ENDIF(${CMAKE_SYSTEM_NAME} MATCHES "Darwin")

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11")

add_library(${PROJECT_NAME} STATIC ${CPP_FILES})

# Expose Projects's public includes to other projects through 
# cache variable
set (${PROJECT_NAME}_INCLUDE_DIRS ${PROJECT_SOURCE_DIR}/headers
	CACHE INTERNAL "${PROJECT_NAME}: Include Directories" FORCE)
