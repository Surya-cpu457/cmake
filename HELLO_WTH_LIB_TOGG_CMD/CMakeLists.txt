cmake_minimum_required(VERSION 3.10)

# set the project name and version
project(Hello VERSION 2.0)

# specify the C standard
set(CMAKE_C_STANDARD 11)
set(CMAKE_C_STANDARD_REQUIRED True)

# use a toggle feature
option(USE_LIB "Compile source into library?" OFF)

#message
message(STATUS "Compile sources into a library? ${USE_LIB}")

include(CMakeDependentOption)
# second option depends on the value of the first
cmake_dependent_option(
  MAKE_STATIC_LIBRARY "Compile sources into a static library" OFF
  "USE_LIB" ON
  )

# third option depends on the value of the first
cmake_dependent_option(
  MAKE_SHARED_LIBRARY "Compile sources into a shared library" OFF
  "USE_LIB" ON
  )

set(CMAKE_WINDOWS_EXPORT_ALL_SYMBOLS ON)


#addding files to srcs
set(scrs hello_file.h hello_file.c)

if(USE_LIB)
  message(STATUS "Compile sources into a STATIC library? ${MAKE_STATIC_LIBRARY}")
  message(STATUS "Compile sources into a SHARED library? ${MAKE_SHARED_LIBRARY}")

  if(MAKE_SHARED_LIBRARY)
  #add the lib file
  add_library(lib SHARED ${scrs})
  
  # add the executable
  add_executable(SHHello hello.c)
  
  #add target linking file
  target_link_libraries(SHHello PRIVATE lib)
  endif()

  if(MAKE_STATIC_LIBRARY)
  #add the lib file
  add_library(lib STATIC ${scrs})
  
  # add the executable
  add_executable(STHello hello.c)
  
  #add target linking file
  target_link_libraries(STHello PRIVATE lib)
  endif()

else()
add_executable(NLHELLO hello.c ${scrs})

endif()