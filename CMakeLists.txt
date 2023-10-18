cmake_minimum_required (VERSION 3.24)

list(APPEND CMAKE_MODULE_PATH "${CMAKE_CURRENT_SOURCE_DIR}/cmake")
list(APPEND CMAKE_SYSTEM_PREFIX_PATH "${CMAKE_INSTALL_PREFIX}")

project(example.project LANGUAGES C CXX ASM VERSION 1.1.0) # x-release-please-version

set(CMAKE_C_STANDARD 11)
set(CMAKE_C_STANDARD_REQUIRED On)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED On)

option(CMAKE_COMPILE_WARNING_AS_ERROR "Enable warnings-as-error" Off)

include(FetchContent)
FetchContent_Declare(
    mbedtls
    GIT_REPOSITORY https://github.com/Mbed-TLS/mbedtls
    GIT_TAG 1ec69067fa1351427f904362c1221b31538c8b57 # v3.5.0
)

set_directory_properties(PROPERTIES EXCLUDE_FROM_ALL On)

set(DISABLE_PACKAGE_CONFIG_AND_INSTALL On CACHE INTERNAL "")
set(ENABLE_TESTING Off CACHE INTERNAL "")
set(ENABLE_PROGRAMS Off CACHE INTERNAL "")
set(GEN_FILES Off CACHE INTERNAL "")

FetchContent_MakeAvailable(mbedtls)

add_executable(example main.cpp)
