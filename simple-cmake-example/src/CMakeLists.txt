# This belongs to the same project as
# the root CMakeLists.txt file
project(SimpleCmakeExample)

# aggregates cpp files into a library to use,
# in this case, called simplecmake
add_library(simplecmake SHARED printhello.cpp)

# now, we need to tell where the include files are
# when "libsimplecmake.a" is built, has printhello.cpp source code and
# the printhello.h header file to include from
target_include_directories(
    simplecmake # provide name of target you are specifying the include directories for
    PUBLIC # whoever is linking to this library will get access to the include directories of the library, ie. use <simplecmake/printhello.h>
    # ${CMAKE_CURRENT_SOURCE_DIR} variables tells where the current CMakeLists.txt file is
    ${CMAKE_CURRENT_SOURCE_DIR}/../include/

    # specifies all of the header files used by simplecmake are in going to parent directory then include/ directory
)

