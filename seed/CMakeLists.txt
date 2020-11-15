cmake_minimum_required(VERSION 3.10.0)
project(tdd_fizzbuzz_cpp VERSION 0.1.0 LANGUAGES CXX)

include(CTest)
enable_testing()

add_subdirectory(src)
add_subdirectory(unit_test)
