CMAKE_MINIMUM_REQUIRED(VERSION 2.8)

include(RezBuild)
include(ExternalProject)

set(pyside_tools_version ${PYSIDE_TOOLS_VERSION})

set(url_pyside_tools https://github.com/PySide/Tools.git)

set(make_args -j1 VERBOSE=on)

if(${REZ_BUILD_INSTALL})
    set(install_cmd make install ${make_args})
else()
    set(install_cmd "")
endif()

ExternalProject_add(
    pyside_tools
    GIT_REPOSITORY ${url_pyside_tools}
    GIT_TAG ${pyside_tools_version}
    PREFIX pyside_tools
    BUILD_COMMAND make -j1 VERBOSE=on
    CMAKE_ARGS -DCMAKE_INSTALL_PREFIX=${CMAKE_INSTALL_PREFIX}
    INSTALL_COMMAND ${install_cmd}
    BUILD_IN_SOURCE 0
)

rez_install_files(
    cmake/pyside_tools.cmake
    DESTINATION .
)
