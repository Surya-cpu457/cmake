cmake_minimum_required(VERSION 3.10)

# set the project name and version
project(Hello VERSION 1.0)

# specify the C standard
set(CMAKE_C_STANDARD 11)
set(CMAKE_C_STANDARD_REQUIRED True)

# use a toggle feature
set(USE_LIB OFF)

#message
message(STATUS "Compile sources into a library? ${USE_LIB}")

#addding files to srcs
set(scrs hello_file.h hello_file.c)

if(USE_LIB)

#add the lib file
add_library(lib ${scrs})

# add the executable
add_executable(Hello hello.c)

#add target linking file
target_link_libraries(Hello PRIVATE lib)

else()
add_executable(ELHELLO hello.c ${scrs})

endif()