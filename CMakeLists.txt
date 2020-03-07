cmake_minimum_required(VERSION 3.12)
project(play-quickjs VERSION 0.1.0 LANGUAGES C CXX)

add_library(quickjs STATIC 
	quickjs.c 
	quickjs.h
	libunicode.c 
	libunicode.h 
	libregexp.c
	libregexp.h
	cutils.c
	cutils.h
)

set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -Wall")
set(CMAKE_C_FLAGS_DEBUG "${CMAKE_C_FLAGS_DEBUG} -g -ggdb")
set(CMAKE_C_FLAGS_RELEASE "${CMAKE_C_FLAGS_RELEASE} -O3 -Wno-array-bounds -Wno-format-truncation")

file(STRINGS "${PROJECT_SOURCE_DIR}/VERSION" CONFIG_VERSION)
target_compile_definitions(quickjs PRIVATE CONFIG_VERSION="${CONFIG_VERSION}")

add_executable(qjs qjs.c)
target_link_libraries(qjs quickjs m)
target_compile_definitions(qjs PRIVATE 
	CONFIG_VERSION="${CONFIG_VERSION}"
)