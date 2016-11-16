cmake_minimum_required(VERSION 2.8)

project(LASlib)

set(CMAKE_MODULE_PATH "${CMAKE_SOURCE_DIR}/cmake" ${CMAKE_MODULE_PATH})
set(CMAKE_DEBUG_POSTFIX "d")

if(UNIX)
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -O3 -std=c++14")
endif()

file(GLOB header_files inc/*.h inc/*hpp)
file(GLOB source_files src/*.cpp)

include_directories(src)
include_directories(inc)
include_directories(../LASzip/src)

set(files ${header_files} ${source_files} ../LASzip/src/mydefs.hpp)

add_definitions("-DNDEBUG")

add_library(LASlib ${files})

install(TARGETS LASlib
	ARCHIVE DESTINATION lib/
)

install(FILES
		${header_files}
		DESTINATION include_laslib/
)
