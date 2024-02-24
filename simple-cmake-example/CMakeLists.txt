# root CMake should invoke CMakeLists.txt of subdirectories
# to build the targets involved/required in each
# Usually, shouldn't build target explicitly itself

cmake_minimum_required(VERSION 3.15)
project(SimpleCmakeExample)

# build executable based on main.cpp
# anything built in CMake is called a target
# add_executable(main main.cpp)

# adds subdirectory to fan out and build via CMake
# NOTE: moving these around here (ie. to end of file) still allows
# building add_subdirectory(example), so as long as the library used by example
# (simplecmake) in this case, is defined at some point, it should be
# buildable
add_subdirectory(include)
add_subdirectory(src)

# give the option to build the example file (main.cpp)
# creates a variables and fills with initial value, can
# override
# in this case, default value is ON and string is description
option(BUILD_EXAMPLES "Whether or not to build examples" ON)

# if BUILD_EXAMPLES is set to ON, add example as a subdirectory
# as well
if (BUILD_EXAMPLES)
    message(STATUS "Building example...") # display a message when building
    add_subdirectory(example)
endif()
