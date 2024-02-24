cmake_minimum_required(VERSION 3.15)
project(Concurrency)

# you should add the third-party libraries first so those
# dependencies get resolved first
add_subdirectory(include)

# sets the C++ version to 17
# TODO: see other ways to set to C++17 (ie. in include/ CMakeLists.txt)
set(CMAKE_CXX_STANDARD 17)

option(BUILD_TESTS "Whether to build tests or not" ON)
option(BUILD_EXAMPLES "Whether to build example or not" ON)

if (BUILD_TESTS)
    message(STATUS "Building tests...")
    add_subdirectory(tests)
endif()

if (BUILD_EXAMPLES)
    message(STATUS "Building examples...")
    add_subdirectory(examples)
endif()