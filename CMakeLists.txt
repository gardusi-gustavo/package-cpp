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

# Imported algorithms: one executable per reference file, one compile-only
# object target per solution, and one executable for the template.
file(GLOB_RECURSE ALGO_REFERENCE CONFIGURE_DEPENDS
  "${CMAKE_CURRENT_SOURCE_DIR}/src/algorithms/reference/*.cpp")
foreach(src IN LISTS ALGO_REFERENCE)
  file(RELATIVE_PATH rel "${CMAKE_CURRENT_SOURCE_DIR}/src/algorithms" "${src}")
  string(REPLACE "/" "_" target "${rel}")
  string(REPLACE ".cpp" "" target "${target}")
  add_executable(algo_ref_${target} "${src}")
  target_include_directories(algo_ref_${target} PRIVATE
    "${CMAKE_CURRENT_SOURCE_DIR}/src/algorithms")
  add_test(NAME algo_ref_${target} COMMAND algo_ref_${target})
endforeach()

file(GLOB_RECURSE ALGO_SOLUTIONS CONFIGURE_DEPENDS
  "${CMAKE_CURRENT_SOURCE_DIR}/src/algorithms/solutions/*.cpp")
foreach(src IN LISTS ALGO_SOLUTIONS)
  file(RELATIVE_PATH rel "${CMAKE_CURRENT_SOURCE_DIR}/src/algorithms" "${src}")
  string(REPLACE "/" "_" target "${rel}")
  string(REPLACE ".cpp" "" target "${target}")
  add_library(algo_sol_${target} OBJECT "${src}")
  target_include_directories(algo_sol_${target} PRIVATE
    "${CMAKE_CURRENT_SOURCE_DIR}/src/algorithms")
endforeach()

file(GLOB_RECURSE ALGO_TEMPLATES CONFIGURE_DEPENDS
  "${CMAKE_CURRENT_SOURCE_DIR}/src/algorithms/templates/*.cpp")
foreach(src IN LISTS ALGO_TEMPLATES)
  file(RELATIVE_PATH rel "${CMAKE_CURRENT_SOURCE_DIR}/src/algorithms" "${src}")
  string(REPLACE "/" "_" target "${rel}")
  string(REPLACE ".cpp" "" target "${target}")
  add_executable(algo_tpl_${target} "${src}")
  target_include_directories(algo_tpl_${target} PRIVATE
    "${CMAKE_CURRENT_SOURCE_DIR}/src/algorithms")
  add_test(NAME algo_tpl_${target} COMMAND algo_tpl_${target})
endforeach()
