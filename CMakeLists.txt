cmake_minimum_required(VERSION 3.20)
project(template LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

add_library(template src/template.cpp)
target_include_directories(template PUBLIC include)

enable_testing()
add_executable(template_test tests/test_template.cpp)
target_link_libraries(template_test PRIVATE template)
add_test(NAME template_test COMMAND template_test)
