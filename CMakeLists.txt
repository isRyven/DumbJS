cmake_minimum_required(VERSION 3.12)
project(dumbjs VERSION 0.1.0 LANGUAGES C)

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
