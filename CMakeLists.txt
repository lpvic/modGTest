# CMake initialization
cmake_minimum_required(VERSION 3.10.0)
project(extendedGTest VERSION 0.0.3 LANGUAGES C CXX)

# Set languaje requirements
set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_EXTENSIONS OFF)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# Set common folders
set(LOCAL_CPP_LIBS "$ENV{LOCAL_CPP_LIBS}")
set(LOCAL_CPP_INCLUDES "$ENV{LOCAL_CPP_INCLUDES}")
set(LOCAL_PROGRAMMING_ROOT "$ENV{LOCAL_PROGRAMMING_ROOT}")

set(LOCAL_CPP_PROJECTS "${LOCAL_PROGRAMMING_ROOT}/Projects/VSCode/C++")
set(LOCAL_CMAKE_MODULES "${LOCAL_PROGRAMMING_ROOT}/Resources/cmake/modules")
set(THIS_PROJECT "${LOCAL_CPP_PROJECTS}/${CMAKE_PROJECT_NAME}")
message(STATUS "LOCAL_CPP_PROJECTS=${LOCAL_CPP_PROJECTS}")
message(STATUS "LOCAL_CMAKE_MODULES=${LOCAL_CMAKE_MODULES}")
message(STATUS "THIS_PROJECT=${THIS_PROJECT}")

# Include external libraries
include_directories("${LOCAL_CPP_INCLUDES}")
include_directories("${THIS_PROJECT}/${CMAKE_PROJECT_NAME}")

# Add the cmake folder so the FindSphinx module is found
set(CMAKE_MODULE_PATH ${LOCAL_CMAKE_MODULES} ${CMAKE_MODULE_PATH})

# Add project folders 
add_subdirectory(${CMAKE_PROJECT_NAME})
add_subdirectory(tests)
add_subdirectory(docs)
