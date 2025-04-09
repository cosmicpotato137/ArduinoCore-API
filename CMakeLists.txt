cmake_minimum_required(VERSION 3.5)
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)

project(cross-compiled-ArduinoCore-API)

include_directories(${CMAKE_SOURCE_DIR})
include_directories(${CMAKE_SOURCE_DIR}/test/include)
include_directories(${CMAKE_SOURCE_DIR}/test/external/catch/v2.13.9/include)

set(LIB_DUT_SRCS
  api/CanMsg.cpp
  api/CanMsgRingbuffer.cpp
  api/Common.cpp
  api/IPAddress.cpp
  api/String.cpp
  api/Stream.cpp
  api/Print.cpp
)

set(LIB_TARGET_SRCS
  test/src/main.cpp
  test/src/dtostrf.cpp
  test/src/itoa.cpp
  test/src/MillisFake.cpp
  test/src/PrintMock.cpp
  test/src/StreamMock.cpp
  ${LIB_DUT_SRCS}
)

set(LIB_TARGET ${CMAKE_PROJECT_NAME})

add_library(LIB_TARGET ${LIB_TARGET_SRCS})

# Testing Project
add_subdirectory(test)
