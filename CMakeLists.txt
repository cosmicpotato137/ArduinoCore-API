cmake_minimum_required(VERSION 3.5)
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)

project(cross-compile-ArduinoCore-API)

file(GLOB_RECURSE API_SOURCES ${CMAKE_SOURCE_DIR}/api/*.cpp)
file(GLOB_RECURSE API_HEADERS ${CMAKE_SOURCE_DIR}/api/*.h)
file(GLOB_RECURSE MOCK_SOURCES 
    "${CMAKE_SOURCE_DIR}/test/include/*.cpp" 
    "${CMAKE_SOURCE_DIR}/test/external/*.cpp"
)
file(GLOB_RECURSE MOCK_HEADERS 
    "${CMAKE_SOURCE_DIR}/test/include/*.h" 
    "${CMAKE_SOURCE_DIR}/test/external/*.h"
)
add_library(${CMAKE_PROJECT_NAME} 
    ${API_SOURCES}
    ${API_HEADERS}
    ${MOCK_SOURCES}
    ${MOCK_HEADERS}
)

include_directories(
    ${CMAKE_SOURCE_DIR}/test/include
    ${CMAKE_SOURCE_DIR}/api
)

# Testing Project
add_subdirectory(test)
