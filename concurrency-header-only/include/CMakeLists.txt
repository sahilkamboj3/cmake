project(Concurrency)

# assumes package is already installed on the system
#   (ie. fetch from our system)
# if can't find the package, fails the build
find_package(Boost REQUIRED)

add_library(
    concurrency
    INTERFACE # defines the library as header-only (essentially don't have source files)
    # shouldn't specify header arguments here, do with target_sources() function - only needed for
    #   INTERFACE library (aka. this is only for header-only library, doesn't apply for PUBLIC/PRIVATE if
    #   your library is private for some reason)
)

# this adds the header files into the concurrency library to be used
target_sources(concurrency
    INTERFACE
    concurrency/messagebuffer.h
    concurrency/threadpool.h
    concurrency/workerthread.h
)

# this specifies the include/ files the user can use and include/import
# in their code when using the library
target_include_directories(
    concurrency
    INTERFACE
    ${CMAKE_CURRENT_SOURCE_DIR}
)

# want to link against Boost interface
target_link_libraries(
    concurrency
    INTERFACE # defines the library as header-only (essentially don't have source files)
    pthread # emulates "-L pthread" to link against pthread for threading libraries
    Boost::boost # defines the ::boost target that we want
)