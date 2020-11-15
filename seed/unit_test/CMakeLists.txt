cmake_minimum_required(VERSION 3.10.0)
SET(CMAKE_PREFIX_PATH "/mingw64" ${CMAKE_PREFIX_PATH})
find_package(GTest REQUIRED)
include(GoogleTest)
include_directories( ./ ../src  ${GTEST_INCLUDE_DIRS})

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall")

file(GLOB all_src "*.cpp" "*.hpp" "*.hxx" "*.cxx" "*.h++" "*.c++" "../src/*.cpp" "../src/*.hpp" "../src/*.hxx" "../src/*.cxx" "../src/*.h++" "../src/*.c++" )
set(unit_test_src)
foreach(f ${all_src})
    if(NOT f MATCHES "main.cpp")
        list(APPEND unit_test_src ${f})
    endif()
endforeach()

add_executable(unit_test ${unit_test_src})

target_link_libraries(unit_test gtest gtest_main pthread)

gtest_discover_tests(unit_test)

set(CMAKE_BUILD_TYPE "Debug")

list(APPEND CMAKE_MODULE_PATH "${CMAKE_SOURCE_DIR}/cmake")
include(CodeCoverage)

append_coverage_compiler_flags()

setup_target_for_coverage_gcovr_html(
    NAME unit_test_coverage_html                # New target name
    EXECUTABLE unit_test --gtest_output=xml     # Executable in PROJECT_BINARY_DIR
    DEPENDENCIES unit_test                      # Dependencies to build first
    EXCLUDE "/usr/*" "/mingw64/" "mingw32/" "${PROJECT_SOURCE_DIR}/unit_test/"
    NO_DEMANGLE                                 # Don't demngle C++ symbols
                                                #  even if c++filt is found
    )

setup_target_for_coverage_gcovr(
    NAME unit_test_coverage                     # New target name
    EXECUTABLE unit_test --gtest_output=xml     # Executable in PROJECT_BINARY_DIR
    #EXECUTABLE ctest     # Executable in PROJECT_BINARY_DIR
    DEPENDENCIES unit_test                      # Dependencies to build first
    EXCLUDE "/usr/*" "/mingw64/" "/mingw32/" "${PROJECT_SOURCE_DIR}/unit_test/"
    NO_DEMANGLE                                 # Don't demngle C++ symbols
                                                #  even if c++filt is found
    )

