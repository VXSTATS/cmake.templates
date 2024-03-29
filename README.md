# CMake Templates
Use an external CMake project inside your own project.

## External Project Template
Create a external project template, with the project as CMakeLists.txt.in:
```cmake
cmake_minimum_required(VERSION 3.10.0)

project(com.vxstats.qt-download NONE)

include(ExternalProject)
ExternalProject_Add(com.vxstats.qt
    GIT_REPOSITORY git@github.com:VXSTATS/com.vxstats.qt.git
    GIT_TAG master
    SOURCE_DIR "${CMAKE_BINARY_DIR}/com.vxstats.qt-src"
    BINARY_DIR "${CMAKE_BINARY_DIR}/com.vxstats.qt-build"
    CONFIGURE_COMMAND ""
    BUILD_COMMAND ""
    INSTALL_COMMAND ""
    TEST_COMMAND ""
)
```

## Include template
Generate and use the template inside your CMake project:
```cmake
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
```

## Support
If you have issues, please let us know and ask for support@vxstats.com to solve your needs.
