project(Concurrency)


# FetchContent says fetch content from URL and include it in project
# to be used
include(FetchContent)

# can also use GIT_REPOSITORY here as well if you want to use
# the content of a git repository
# this declares we want the content from the source 
option(DOWNLOAD_EXTRACT_TIMESTAMP ON)
FetchContent_Declare(
    googletest
    URL https://github.com/google/googletest/archive/03597a01ee50ed33e9dfd640b249b4be3799d395.zip
)

# this makes the googletest content available
# FetchContent_MakeAvailable(googletest)

# can use this alternate method also
FetchContent_GetProperties(googletest)
if (NOT googletest_POPULATED)
    # this goes and fetches the actual content
    FetchContent_Populate(googletest)

    # you then include the subdirectory
    add_subdirectory(${googletest_SOURCE_DIR}
        ${googletest_BINARY_DIR} EXCLUDE_FROM_ALL)
    # TODO: look this flag over
    # EXCLUDE_FROM_ALL says exclude this from all my targets
    # in my project
endif()

# Defining and enabling ctests. This is all from the GoogleTest API.
#   https://google.github.io/googletest/quickstart-cmake.html

enable_testing() # to enable ctests

# add test source files as part of executable to run
add_executable(
    tests
    messagebuffer_test.cpp
    workerthread_test.cpp
    threadpool_test.cpp
)

# link the libraries needed for the tests
target_link_libraries(
    tests
    gtest_main # this is pulled in via the FetchContent from earlier
    concurrency # links against concurrency INTERFACE library for testing
)
include(GoogleTest)
gtest_discover_tests(tests)