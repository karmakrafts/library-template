cmake_minimum_required(VERSION 3.18)
project(example LANGUAGES C CXX)

# Include CMake modules in ./cmake/
set(CMAKE_MODULE_PATH "${CMAKE_SOURCE_DIR}/cmake;")
include(cmx)
cmx_include_scripts() # Enable sanitizers on supported platforms and extend compiler warnings

# Library
cmx_add_library(example "${CMAKE_SOURCE_DIR}/src" "${CMAKE_SOURCE_DIR}/include")

# Unit testing
cmx_add_tests(example-tests "${CMAKE_SOURCE_DIR}/test")
target_include_directories(example-tests PRIVATE "${CMAKE_SOURCE_DIR}/include")
target_link_libraries(example-tests PRIVATE example-static)
add_dependencies(example-tests example-static)
