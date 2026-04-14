cmake_minimum_required(VERSION 3.28)
project(YeetMouseTests)

set(CMAKE_CXX_STANDARD 17)

# Add flags based on build type
if (CMAKE_BUILD_TYPE STREQUAL "Debug")
    message(STATUS "Configuring with debug flags.")
    message(STATUS "Debug build selected. Compiling with debug information and no optimization.")
    add_compile_options(-g -O0)
    add_link_options(-g)
elseif (CMAKE_BUILD_TYPE STREQUAL "Release")
    message(STATUS "Configuring with release flags.")
    message(STATUS "Release build selected. Compiling with full optimization and assertions disabled.")
    add_compile_options(-O3 -DNDEBUG)
else()
    message(STATUS "Configuring with custom build flags.")
    message(STATUS "Custom build type selected. Compiling with debug information and moderate optimization.")
    add_compile_options(-g -O2)
    add_link_options(-g)
endif()

if (CMAKE_SYSTEM_PROCESSOR STREQUAL "ppc64le")
    message(STATUS "Configuring for ppc64le architecture. Adding __ppc64le__ definition.")
    add_compile_definitions(__ppc64le__)
endif()

add_executable(YeetMouseTests main.cpp
        TestManager.cpp
        Tests.cpp
        ../gui/FunctionHelper.cpp
        ../driver/accel_modes.c)

target_compile_definitions(YeetMouseTests PRIVATE TEST_ENV)

target_include_directories(YeetMouseTests PRIVATE
        ${CMAKE_CURRENT_SOURCE_DIR}/..
        ${CMAKE_CURRENT_SOURCE_DIR}/../gui/External
)