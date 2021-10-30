cmake_minimum_required(VERSION 3.20)
project({{cookiecutter.project_name}})

set (CMAKE_EXPORT_COMPILE_COMMANDS ON)
#set(CMAKE_FIND_DEBUG_MODE TRUE)

#find_package(Boost 1.74 REQUIRED COMPONENTS log unit_test_framework)
#include_directories(${Boost_INCLUDE_DIRS})
#link_directories(${Boost_LIBRARY_DIRS})

find_package(Catch2 CONFIG REQUIRED)

include(CMakePrintHelpers)
#cmake_print_variables(CMAKE_MODULE_PATH)

set(CMAKE_CXX_STANDARD 17)

set(SOURCES
        )

add_executable(${PROJECT_NAME} ${SOURCES} main.cpp)

# Include the Source directory so tests can #include ""
include_directories(${PROJECT_SOURCE_DIR})

# Find all unit tests in tests directory
file(GLOB UNIT_TESTS ${PROJECT_SOURCE_DIR}/tests/*.cpp)

add_executable(${PROJECT_NAME}_test ${UNIT_TESTS} ${SOURCES} )

# Link test harness libraries into test executable
target_link_libraries(${PROJECT_NAME}_test PRIVATE Catch2::Catch2)

#configure_file(example.txt example.txt COPYONLY)

enable_testing()
add_test(UnitTests ${PROJECT_NAME}_tests)
