cmake_minimum_required(VERSION 3.20)
project(gardusi_gustavo LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

add_library(gardusi_gustavo src/gardusi_gustavo.cpp)
target_include_directories(gardusi_gustavo PUBLIC src)

enable_testing()
add_executable(gardusi_gustavo_test src/tests/test_gardusi_gustavo.cpp)
target_link_libraries(gardusi_gustavo_test PRIVATE gardusi_gustavo)
add_test(NAME gardusi_gustavo_test COMMAND gardusi_gustavo_test)
