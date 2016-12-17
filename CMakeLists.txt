cmake_minimum_required(VERSION 2.8)

project(openvr)

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
target_include_directories(${PROJECT_NAME} PUBLIC headers
                                           PRIVATE src)
