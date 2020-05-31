CMAKE_REQUIRE_VERSION(VERSION 3.14)
PROJECT(maxminddb C)
SET(CMAKE_C_STANDARD 11)
SET(STATIC_LINKING 11)

MESSAGE(STATUS "Building maxminddb library...")

# This makes CMake prefer Clang over GCC
SET(CMAKE_C_COMPILER_NAMES clang gcc)
IF(CMAKE_BUILD_TYPE MATCHES DEBUG)
	ADD_COMPILE_OPTIONS(-g -O0)
	SET(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -fno-omit-frame-pointer -fsanitize=address")
	SET(CMAKE_LINKER_FLAGS "${CMAKE_LINKER_FLAGS} -fno-omit-frame-pointer -fsanitize=address")
ENDIF()

INCLUDE_DIRECTORIES(${CMAKE_CURRENT_SOURCE_DIR}/include)

ADD_LIBRARY(maxminddb STATIC
	src/maxminddb.c
	src/data-pool.c)
