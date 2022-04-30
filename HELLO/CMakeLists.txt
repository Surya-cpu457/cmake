cmake_minimum_required(VERSION 3.10)

# set the project name and version
project(Hello VERSION 1.0)

# specify the C standard
set(CMAKE_C_STANDARD 11)
set(CMAKE_C_STANDARD_REQUIRED True)

# add the executable
add_executable(Hello hello.c)