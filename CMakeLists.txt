cmake_minimum_required(VERSION 3.10.0)
project(modGTest VERSION 0.0.3 LANGUAGES C CXX)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_EXTENSIONS OFF)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

set(LOCAL_CPP_LIBS "$ENV{LOCAL_CPP_LIBS}")
set(LOCAL_CPP_INCLUDES "$ENV{LOCAL_CPP_INCLUDES}")
set(LOCAL_PROGRAMMING_ROOT "$ENV{LOCAL_PROGRAMMING_ROOT}")
set(LOCAL_CPP_PROJECTS "${LOCAL_PROGRAMMING_ROOT}/Projects/VSCode/C++")
set(LOCAL_CMAKE_MODULES "${LOCAL_PROGRAMMING_ROOT}/Resources/cmake")
include_directories("${LOCAL_CPP_INCLUDES}")

set(THIS_PROJECT "${LOCAL_CPP_PROJECTS}/${CMAKE_PROJECT_NAME}")

include("${LOCAL_CMAKE_MODULES}/gtest.cmake")

include_directories(include)
add_subdirectory(tests)

add_library(${CMAKE_PROJECT_NAME} STATIC ./src/modGTest.cpp)
set_target_properties(${CMAKE_PROJECT_NAME} PROPERTIES 
    ARCHIVE_OUTPUT_DIRECTORY_DEBUG "${CMAKE_BINARY_DIR}/output/lib/debug"
    LIBRARY_OUTPUT_DIRECTORY_DEBUG "${CMAKE_BINARY_DIR}/output/lib/debug"
    RUNTIME_OUTPUT_DIRECTORY_DEBUG "${CMAKE_BINARY_DIR}/output/bin/debug"
    ARCHIVE_OUTPUT_DIRECTORY_RELEASE "${CMAKE_BINARY_DIR}/output/lib/release"
    LIBRARY_OUTPUT_DIRECTORY_RELEASE "${CMAKE_BINARY_DIR}/output/lib/release"
    RUNTIME_OUTPUT_DIRECTORY_RELEASE "${CMAKE_BINARY_DIR}/output/bin/release"
)
target_link_libraries(${CMAKE_PROJECT_NAME} gtest_main)

if (CMAKE_BUILD_TYPE STREQUAL "Release")
    add_custom_command(TARGET ${CMAKE_PROJECT_NAME} POST_BUILD COMMAND ${CMAKE_COMMAND} -E copy_directory  ${THIS_PROJECT}/include/ ${LOCAL_CPP_INCLUDES}/${CMAKE_PROJECT_NAME})
    add_custom_command(TARGET ${CMAKE_PROJECT_NAME} POST_BUILD COMMAND ${CMAKE_COMMAND} -E copy_directory  ${CMAKE_BINARY_DIR}/output/lib/release/ ${LOCAL_CPP_LIBS}/${CMAKE_PROJECT_NAME})
endif()