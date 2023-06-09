cmake_minimum_required(VERSION 3.2.0)
project(qhttpengine)

set(PROJECT_NAME "QHttpEngine")
set(PROJECT_DESCRIPTION "Simple and secure HTTP server for Qt applications")
set(PROJECT_AUTHOR "Nathan Osman")
set(PROJECT_URL "https://github.com/nitroshare/qhttpengine")

set(PROJECT_VERSION_MAJOR 1)
set(PROJECT_VERSION_MINOR 0)
set(PROJECT_VERSION_PATCH 1)
set(PROJECT_VERSION ${PROJECT_VERSION_MAJOR}.${PROJECT_VERSION_MINOR}.${PROJECT_VERSION_PATCH})

# Build a shared library by default
option(BUILD_SHARED_LIBS "Build QHttpEngine as a shared library" ON)

set(BIN_INSTALL_DIR bin CACHE STRING "Binary runtime installation directory relative to the install prefix")
set(LIB_INSTALL_DIR lib CACHE STRING "Library installation directory relative to the install prefix")
set(INCLUDE_INSTALL_DIR include CACHE STRING "Header installation directory relative to the install prefix")

set(DOC_INSTALL_DIR share/doc/qhttpengine CACHE STRING "Documentation installation directory relative to the install prefix")
set(EXAMPLES_INSTALL_DIR "${LIB_INSTALL_DIR}/qhttpengine/examples" CACHE STRING "Examples installation directory relative to the install prefix")

find_package(Qt6Network 5.4 REQUIRED)

set(CMAKE_AUTOMOC ON)

add_subdirectory(src)

option(BUILD_DOC "Build Doxygen documentation" OFF)
if(BUILD_DOC)
    find_package(Doxygen REQUIRED)
    add_subdirectory(doc)
endif()

option(BUILD_EXAMPLES "Build the example applications" OFF)
if(BUILD_EXAMPLES)
    add_subdirectory(examples)
endif()

option(BUILD_TESTS "Build the test suite" OFF)
if(BUILD_TESTS)
    find_package(Qt6Test 5.4 REQUIRED)
    enable_testing()
    add_subdirectory(tests)
endif()

set(CPACK_PACKAGE_INSTALL_DIRECTORY "${PROJECT_NAME}")
set(CPACK_PACKAGE_VENDOR "${PROJECT_AUTHOR}")
set(CPACK_PACKAGE_VERSION_MAJOR ${PROJECT_VERSION_MAJOR})
set(CPACK_PACKAGE_VERSION_MINOR ${PROJECT_VERSION_MINOR})
set(CPACK_PACKAGE_VERSION_PATCH ${PROJECT_VERSION_PATCH})

set(CPACK_COMPONENT_DOCUMENTATION_DISPLAY_NAME "Documentation")
set(CPACK_COMPONENT_DOCUMENTATION_DESCRIPTION "Documentation generated for the library")
set(CPACK_COMPONENT_EXAMPLES_DISPLAY_NAME "Examples")
set(CPACK_COMPONENT_EXAMPLES_DESCRIPTION "Sample applications using the library")

include(CPack)
