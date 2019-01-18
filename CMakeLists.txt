cmake_minimum_required(VERSION 3.1)
if(NOT CMAKE_BUILD_TYPE)
    message("Using default build type: Release")
    set(CMAKE_BUILD_TYPE Release CACHE STRING "" FORCE)
endif()
project(ALPSCoreParapack CXX)

option(BUILD_SHARED_LIBS "Build shared libraries" ON)

# RPATH fix
set(CMAKE_INSTALL_RPATH_USE_LINK_PATH TRUE)
if(${CMAKE_SYSTEM_NAME} MATCHES "Darwin")
 set(CMAKE_INSTALL_NAME_DIR "${CMAKE_INSTALL_PREFIX}/lib")
else()
 set(CMAKE_INSTALL_RPATH "${CMAKE_INSTALL_PREFIX}/lib")
endif()

#policy update CMP0042
if(APPLE)
  set(CMAKE_MACOSX_RPATH ON)
endif()

# ALPSCore
find_package(ALPSCore REQUIRED)

# Google Test
set(GOOGLETEST_VERSION 1)
add_subdirectory(googletest)
include_directories(googletest/include)
enable_testing()

# add_subdirectory(src)
# add_subdirectory(test)
