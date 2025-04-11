# SPDX-License-Identifier: LGPL-2.1-or-later

include_directories(${CMAKE_CURRENT_SOURCE_DIR}/..)
include_directories(${CMAKE_CURRENT_SOURCE_DIR}/include)
include_directories(${CMAKE_CURRENT_SOURCE_DIR}/external/catch/v2.13.9/include)


set(TEST_SRCS
  src/CanMsg/test_CanMsg.cpp
  src/CanMsg/test_CanMsg_CopyCtor.cpp
  src/CanMsg/test_CanExtendedId.cpp
  src/CanMsg/test_CanStandardId.cpp
  src/CanMsg/test_isExtendedId.cpp
  src/CanMsg/test_isStandardId.cpp
  src/CanMsg/test_operator_assignment.cpp
  src/CanMsg/test_printTo.cpp
  src/CanMsgRingbuffer/test_available.cpp
  src/Common/test_makeWord.cpp
  src/Common/test_map.cpp
  src/Common/test_max.cpp
  src/Common/test_min.cpp
  src/IPAddress/test_toString.cpp
  src/IPAddress/test_fromString.cpp
  src/IPAddress/test_fromString6.cpp
  src/IPAddress/test_IPAddress.cpp
  src/IPAddress/test_IPAddress6.cpp
  src/IPAddress/test_operator_assignment.cpp
  src/IPAddress/test_operator_comparison.cpp
  src/IPAddress/test_operator_comparison6.cpp
  src/IPAddress/test_operator_parentheses.cpp
  src/IPAddress/test_operator_parentheses6.cpp
  src/IPAddress/test_printTo.cpp
  src/IPAddress/test_printTo6.cpp
  src/Print/test_clearWriteError.cpp
  src/Print/test_getWriteError.cpp
  src/Print/test_print.cpp
  src/Print/test_println.cpp
  src/Print/test_availableForWrite.cpp
  src/Ringbuffer/test_available.cpp
  src/Ringbuffer/test_availableForStore.cpp
  src/Ringbuffer/test_clear.cpp
  src/Ringbuffer/test_isFull.cpp
  src/Ringbuffer/test_peek.cpp
  src/Ringbuffer/test_read_char.cpp
  src/Ringbuffer/test_store_char.cpp
  src/Stream/test_find.cpp
  src/Stream/test_findUntil.cpp
  src/Stream/test_getTimeout.cpp
  src/Stream/test_parseFloat.cpp
  src/Stream/test_parseInt.cpp
  src/Stream/test_readBytes.cpp
  src/Stream/test_readBytesUntil.cpp
  src/Stream/test_readString.cpp
  src/Stream/test_readStringUntil.cpp
  src/Stream/test_setTimeout.cpp
  src/String/test_concat.cpp
  src/String/test_operators.cpp
  src/String/test_compareTo.cpp
  src/String/test_comparisonFunc.cpp
  src/String/test_characterAccessFunc.cpp
  src/String/test_substring.cpp
  src/String/test_indexOf.cpp
  src/String/test_lastIndexOf.cpp
  src/String/test_length.cpp
  src/String/test_move.cpp
  src/String/test_remove.cpp
  src/String/test_replace.cpp
  src/String/test_String.cpp
  src/String/test_toDouble.cpp
  src/String/test_toFloat.cpp
  src/String/test_toInt.cpp
  src/String/test_toLowerCase.cpp
  src/String/test_toUpperCase.cpp
  src/String/test_trim.cpp
  src/WCharacter/test_isAscii.cpp
  src/WCharacter/test_isControl.cpp
  src/WCharacter/test_isDigit.cpp
  src/WCharacter/test_isHexadecimalDigit.cpp
  src/WCharacter/test_isLowerCase.cpp
  src/WCharacter/test_isPunct.cpp
  src/WCharacter/test_isSpace.cpp
  src/WCharacter/test_isUpperCase.cpp
  src/WCharacter/test_isWhitespace.cpp
  src/WCharacter/test_toAscii.cpp
)


add_compile_definitions(HOST)
add_compile_options(-Wall -Wextra -Wpedantic -Werror)
add_compile_options(-Wno-cast-function-type)

set(CMAKE_C_FLAGS   "${CMAKE_C_FLAGS} --coverage")
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} --coverage -Wno-deprecated-copy")

if(CMAKE_CXX_COMPILER_ID STREQUAL "GNU")
  message(STATUS "Using GCC compiler")
  execute_process(
    COMMAND ${CMAKE_CXX_COMPILER} -dumpversion
    OUTPUT_VARIABLE GCC_VERSION_STRING
    OUTPUT_STRIP_TRAILING_WHITESPACE
  )
  message(STATUS "GCC version: ${GCC_VERSION_STRING}")
  string(REPLACE "." ";" VERSION_LIST ${GCC_VERSION_STRING})
  list(GET VERSION_LIST 0 GCC_VERSION_MAJOR)
  add_compile_definitions(GCC_VERSION=${GCC_VERSION_MAJOR})
endif()


# Add the test executable
set(TEST_TARGET test-ArduinoCore-API)
add_executable(
  ${TEST_TARGET}
  ${TEST_SRCS}
)

target_link_libraries(${TEST_TARGET} PUBLIC
  ${LIB_TARGET}
  -lgcov
)
target_link_directories(${TEST_TARGET} PUBLIC
  ${CMAKE_BINARY_DIR}/lib
)
