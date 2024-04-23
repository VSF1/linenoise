cmake_minimum_required (VERSION 2.9)
project (LINENOISE DESCRIPTION "A shell library")

if(CMAKE_BUILD_TYPE)
    message("Building ${CMAKE_BUILD_TYPE} build.")
elseif(NOT CMAKE_BUILD_TYPE)
    message(FATAL_ERROR "No build type specified. Use -DCMAKE_BUILD_TYPE=[DEBUG|RELEASE] to specify.")
endif(CMAKE_BUILD_TYPE)

# set the version of our library
# MAJOR, is significant breaking changes, MINOR, is when we might have changed signatures of existing functions, PATCH, is just bug fixes and no breaking changes
set(LINENOISE_VERSION_MAJOR 1)
set(LINENOISE_VERSION_MINOR 0)
set(LINENOISE_VERSION_PATCH 1)
set(LINENOISE_VERSION_STRING ${LINENOISE_VERSION_MAJOR}.${LINENOISE_VERSION_MINOR}.${LINENOISE_VERSION_PATCH})

file(GLOB LINENOISE_SOURCE_FILES "linenoise.c")
file(GLOB LINENOISE_HEADER_FILES "linenoise.h")

set(LINENOISE_SOURCES ${LINENOISE_SOURCE_FILES})
set(LINENOISE_HEADERS ${LINENOISE_HEADER_FILES})

# where the library will be built to
set(LIBRARY_OUTPUT_PATH ${PROJECT_BINARY_DIR}/libs)

add_library(linenoise SHARED ${LINENOISE_SOURCES} ${LINENOISE_HEADERS})
target_link_libraries(linenoise)

target_include_directories(linenoise PUBLIC ".")
# sets the shared library version
# http://cmake.3232098.n2.nabble.com/Version-in-name-of-shared-library-td7581530.html
set_target_properties(linenoise PROPERTIES VERSION ${LINENOISE_VERSION_STRING} SOVERSION ${LINENOISE_VERSION_MAJOR})
set_target_properties(linenoise PROPERTIES LINKER_LANGUAGE C)
