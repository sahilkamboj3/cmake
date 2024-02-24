# This belongs to the same project as
# the root CMakeLists.txt file
project(SimpleCmakeExample)

# main is the name of the executable and
# main.cpp is the source cpp file
add_executable(main main.cpp)

target_link_libraries(
    main
    PRIVATE 
    simplecmake
)