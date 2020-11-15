cmake_minimum_required(VERSION 3.10.0)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall")

set(CMAKE_CXX_CPPLINT "cpplint;--filter=-legal/copyright,-build/include")

file(GLOB app_src "*.cpp" "*.hpp" "*.hxx" "*.cxx" "*.h++" "*.c++" )
add_executable(tdd_cpp_exe ${app_src})
