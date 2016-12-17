cmake_minimum_required(VERSION 2.8)

project(openvr)

include_directories(src headers)
file(GLOB api_source_files
  "src/**.cpp"
)
file(GLOB api_public_header_files
  "headers/*"
)

IF(${CMAKE_SYSTEM_NAME} MATCHES "Darwin")
	add_definitions(-DOSX -DPOSIX)
	set_source_files_properties(
		src/vrcommon/pathtools_public.cpp
		src/vrcommon/vrpathregistry_public.cpp
		PROPERTIES COMPILE_FLAGS "-x objective-c++")
ENDIF(${CMAKE_SYSTEM_NAME} MATCHES "Darwin")

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11")

add_library(openvr_api STATIC ${api_source_files})

install(TARGETS openvr_api DESTINATION lib)
install(FILES ${api_public_header_files} DESTINATION include)
