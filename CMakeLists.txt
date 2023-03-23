cmake_minimum_required(VERSION 3.24)
project(ffenestr)

# https://gitlab.kitware.com/cmake/community/-/wikis/doc/cmake/Useful-Variables
# https://gitlab.kitware.com/cmake/community/-/wikis/doc/tutorials/How-To-Write-Platform-Checks

set(CMAKE_CXX_STANDARD 20)

IF(WIN32)
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} /W4 /WX /wd4068") # really picky warnings, as errors, suppress 'unknown pragma' -- most of the clang-lint stuff
    set(CMAKE_CXX_FLAGS_RELEASE "/O2") # When using MSVC compiler
ELSE()
    set(CMAKE_CXX_FLAGS_DEBUG "${CMAKE_CXX_FLAGS_DEBUG} -O0")
    set(CMAKE_C_FLAGS_RELEASE "${CMAKE_C_FLAGS_DEBUG} -O2")
ENDIF()

message(STATUS "Build type: ${CMAKE_BUILD_TYPE}")

include_directories(.)
#include_directories(src)

IF (WIN32)
    add_executable(ffenestr WIN32 main.cpp fenster.h)
ELSE()
    add_executable(ffenestr main.cpp fenster.h)
ENDIF()


#IF (WIN32)
#    target_link_libraries(ffenestr -luser32 -lgdi32 -lwinmm)
#ENDIF ()