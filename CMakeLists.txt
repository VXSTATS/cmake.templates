#
# Copyright (C) 10/23/2020 VX APPS <sales@vxapps.com>
#
# This document is property of VX APPS. It is strictly prohibited
# to modify, sell or publish it in any way. In case you have access
# to this document, you are obligated to ensure its nondisclosure.
# Noncompliances will be prosecuted.
#
# Diese Datei ist Eigentum der VX APPS. Jegliche Änderung, Verkauf
# oder andere Verbreitung und Veröffentlichung ist strikt untersagt.
# Falls Sie Zugang zu dieser Datei haben, sind Sie verpflichtet,
# alles in Ihrer Macht stehende für deren Geheimhaltung zu tun.
# Zuwiderhandlungen werden strafrechtlich verfolgt.
#

cmake_minimum_required(VERSION 3.10.0)

project(com.vxstats.qt LANGUAGES CXX)
include(cmake/env.cmake)

add_subdirectory(examples)

# Download and unpack com.vxstats.qt at configure time
configure_file(CMakeLists.txt.in com.vxstats.qt-download/CMakeLists.txt)
execute_process(COMMAND "${CMAKE_COMMAND}" -G "${CMAKE_GENERATOR}" .
    WORKING_DIRECTORY "${CMAKE_BINARY_DIR}/com.vxstats.qt-download"
)
execute_process(COMMAND "${CMAKE_COMMAND}" --build .
    WORKING_DIRECTORY "${CMAKE_BINARY_DIR}/com.vxstats.qt-download"
)

# Prevent com.vxstats.qt from overriding our compiler/linker options
# when building with Visual Studio
set(gtest_force_shared_crt ON CACHE BOOL "" FORCE)

# Add com.vxstats.qt directly to our build. This adds the following targets:
# com.vxstats.qt
add_subdirectory("${CMAKE_BINARY_DIR}/com.vxstats.qt-src"
                 "${CMAKE_BINARY_DIR}/com.vxstats.qt-build"
)
