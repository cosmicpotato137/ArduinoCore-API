cmake_minimum_required(VERSION 3.5)
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)

project(ArduinoCore-API)

include_directories(${CMAKE_CURRENT_SOURCE_DIR})
include_directories(${CMAKE_CURRENT_SOURCE_DIR}/test/include)
include_directories(${CMAKE_CURRENT_SOURCE_DIR}/test/external/catch/v2.13.9/include)

file(GLOB LIB_DUT_SRCS ${CMAKE_CURRENT_SOURCE_DIR}/api/*.cpp)
file(GLOB LIB_TARGET_SRCS ${CMAKE_CURRENT_SOURCE_DIR}/test/src/*.cpp)
set(LIB_TARGET ArduinoCore-API)

add_library(${LIB_TARGET} ${LIB_TARGET_SRCS} ${LIB_DUT_SRCS})

# Testing Project
add_subdirectory(test)
