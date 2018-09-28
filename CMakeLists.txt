# CMake required version
cmake_minimum_required(VERSION 3.1)

# "Only interpret if() arguments as variables or keywords when unquoted."
cmake_policy(SET CMP0054 NEW)

project(lz4)

# Build docs
option(LZ4_BUILD_STATIC "Build lz4 static" ON)

SET(LZ_SRCS
	lib/xxhash.c
	lib/lz4.c
	lib/lz4hc.c
	lib/lz4frame.c
)

SET(LZ_EXPORTS
	lib/dll/liblz4.def
)

if (LZ4_BUILD_STATIC)
	add_library(lz4 ${LZ_SRCS})
else()
	add_library(lz4 ${LZ_SRCS} ${LZ_EXPORTS})
endif()

target_include_directories(lz4 PUBLIC lib)
