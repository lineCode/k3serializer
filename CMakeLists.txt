cmake_minimum_required(VERSION 3.5 FATAL_ERROR)
project(k3serializer LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_EXTENSIONS OFF)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

option(BUILD_COVERAGE "Build with Code-Coverage" OFF)
if(BUILD_COVERAGE)
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -g -O0") # debug, no optimisation
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} --coverage") # enabling coverage
    set(CMAKE_CXX_OUTPUT_EXTENSION_REPLACE 1)
endif()

list(APPEND _sources k3serializer.cpp)
add_executable(example example/main.cpp ${_sources})

add_executable(k3_test test/k3serializer_test.cpp ${_sources})
enable_testing()
add_test(
  NAME catch_test
  COMMAND $<TARGET_FILE:k3_test> --success
  )