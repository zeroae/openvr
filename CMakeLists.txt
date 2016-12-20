cmake_minimum_required(VERSION 2.8)

project(openvr C CXX)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

set(CPP_FILES
	src/openvr_api_public.cpp
	src/jsoncpp.cpp
	src/vrcommon/dirtools_public.cpp
	src/vrcommon/envvartools_public.cpp
	src/vrcommon/pathtools_public.cpp
	src/vrcommon/sharedlibtools_public.cpp
	src/vrcommon/hmderrors_public.cpp
	src/vrcommon/vrpathregistry_public.cpp
	src/vrcommon/strtools_public.cpp
	src/vrcommon/vrpathregistry_public.cpp)

#OpenVR needs to be built in SHARED mode at the moment.
#Investigate these links to submit a pull-request for handling both
# - https://cmake.org/cmake/help/v2.8.8/cmake.html#module:GenerateExportHeader
# - https://cmake.org/Wiki/BuildingWinDLL

add_library(${PROJECT_NAME} SHARED ${CPP_FILES})
target_include_directories(${PROJECT_NAME} PUBLIC headers
                                           PRIVATE src src/vrcommon)

install(TARGETS ${PROJECT_NAME} 
	LIBRARY DESTINATION "lib"
	ARCHIVE DESTINATION "lib/static"
	RUNTIME DESTINATION "bin")
