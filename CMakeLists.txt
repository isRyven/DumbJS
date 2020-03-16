cmake_minimum_required(VERSION 3.12)
project(dumbjs VERSION 0.1.0 LANGUAGES C)

option(DUMBJS_EXAMPLES "Build DumbJS examples" OFF)

set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -Wall")
set(CMAKE_C_FLAGS_DEBUG "${CMAKE_C_FLAGS_DEBUG} -g -ggdb")
set(CMAKE_C_FLAGS_RELEASE "${CMAKE_C_FLAGS_RELEASE} -O2 -flto -Wno-array-bounds -Wno-format-truncation")

add_library(dumbjs STATIC 
	quickjs.c 
	quickjs.h
	libunicode.c 
	libunicode.h 
	libregexp.c
	libregexp.h
	cutils.c
	cutils.h
)

add_library(dumbjs_h INTERFACE)
target_include_directories(dumbjs_h INTERFACE "${CMAKE_CURRENT_SOURCE_DIR}")
target_link_libraries(dumbjs m dumbjs_h)

if(DUMBJS_EXAMPLES AND (PROJECT_SOURCE_DIR STREQUAL CMAKE_SOURCE_DIR))
	message(STATUS "Building DumbJS examples")
	add_subdirectory(examples)
endif()
