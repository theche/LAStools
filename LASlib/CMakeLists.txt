cmake_minimum_required(VERSION 2.8)

project(LASlib)

set(CMAKE_MODULE_PATH "${CMAKE_SOURCE_DIR}/cmake" ${CMAKE_MODULE_PATH})
set(CMAKE_DEBUG_POSTFIX "d")

if(UNIX)
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -O3 -std=c++14")
endif()

file(GLOB header_files inc/*.h inc/*hpp)
file(GLOB source_files src/*.cpp)

set(header_files_laszip 
	../LASzip/src/laszip.hpp 
	../LASzip/src/lasreadpoint.hpp
	../LASzip/src/lasreaditemcompressed_v1.hpp 
	../LASzip/src/lasreaditemcompressed_v2.hpp
	../LASzip/src/laswritepoint.hpp 
	../LASzip/src/laswriteitemcompressed_v1.hpp
	../LASzip/src/laswriteitemcompressed_v2.hpp 
	../LASzip/src/integercompressor.hpp
	../LASzip/src/arithmeticdecoder.hpp 
	../LASzip/src/arithmeticencoder.hpp
	../LASzip/src/arithmeticmodel.hpp 
	../LASzip/src/lasindex.hpp
	../LASzip/src/lasquadtree.hpp 
	../LASzip/src/lasinterval.hpp
	)
set(source_files_laszip 
	../LASzip/src/laszip.cpp 
	../LASzip/src/lasreadpoint.cpp
	../LASzip/src/lasreaditemcompressed_v1.cpp 
	../LASzip/src/lasreaditemcompressed_v2.cpp
	../LASzip/src/laswritepoint.cpp 
	../LASzip/src/laswriteitemcompressed_v1.cpp
	../LASzip/src/laswriteitemcompressed_v2.cpp 
	../LASzip/src/integercompressor.cpp
	../LASzip/src/arithmeticdecoder.cpp 
	../LASzip/src/arithmeticencoder.cpp
	../LASzip/src/arithmeticmodel.cpp 
	../LASzip/src/lasindex.cpp
	../LASzip/src/lasquadtree.cpp 
	../LASzip/src/lasinterval.cpp
	)

include_directories(src)
include_directories(inc)
include_directories(../LASzip/src)

set(files ${header_files} ${source_files} ${header_files_laszip} ${source_files_laszip})

add_definitions("-DNDEBUG")

add_library(LASlib ${files})

install(TARGETS LASlib
	ARCHIVE DESTINATION lib/
)

install(FILES
		${header_files}
		DESTINATION include_laslib/
)
