#==============================================================================
# nfx-meta - nfx Libraries Metapackage
#==============================================================================
# A metapackage that locks all nfx library dependencies to tested versions.
# This ensures that all nfx libraries work together correctly.
#
# Usage:
#   FetchContent_Declare(nfx-meta
#       GIT_REPOSITORY https://github.com/nfx-libs/nfx-meta.git
#       GIT_TAG        v1.0.0
#   )
#   FetchContent_MakeAvailable(nfx-meta)
#   target_link_libraries(your-target PRIVATE nfx::meta)
#==============================================================================

cmake_minimum_required(VERSION 3.20)
project(nfx-meta
    VERSION 1.0.0
    DESCRIPTION "nfx libraries metapackage with locked tested versions"
    HOMEPAGE_URL "https://github.com/nfx-libs/nfx-meta"
)

#----------------------------------------------
# Options to enable/disable individual libraries
#----------------------------------------------

option(NFX_META_ENABLE_CONTAINERS       "Enable nfx-containers library"             OFF)
option(NFX_META_ENABLE_CPU              "Enable nfx-cpu library"                    OFF)
option(NFX_META_ENABLE_DATATYPES        "Enable nfx-datatypes library"              OFF)
option(NFX_META_ENABLE_DATETIME         "Enable nfx-datetime library"               OFF)
option(NFX_META_ENABLE_HASHING          "Enable nfx-hashing library"                OFF)
option(NFX_META_ENABLE_JSON             "Enable nfx-json library"                   OFF)
option(NFX_META_ENABLE_RESOURCE         "Enable nfx-resource library"               OFF)
option(NFX_META_ENABLE_SERIALIZATION    "Enable nfx-serialization library"          OFF)
option(NFX_META_ENABLE_STRINGBUILDER    "Enable nfx-stringbuilder library"          OFF)
option(NFX_META_ENABLE_STRINGUTILS      "Enable nfx-stringutils library"            OFF)

option(NFX_META_BUILD_TESTS             "Build tests for enabled libraries"         OFF)
option(NFX_META_BUILD_SAMPLES           "Build samples for enabled libraries"       OFF)
option(NFX_META_BUILD_BENCHMARKS        "Build benchmarks for enabled libraries"    OFF)
option(NFX_META_BUILD_DOCUMENTATION     "Build documentation for enabled libraries" OFF)

option(NFX_META_WITH_JSON_SERIALIZATION "Enable JSON support in serialization"      OFF)

#----------------------------------------------
# Output configuration
#----------------------------------------------

set(_SAVED_CMAKE_REQUIRED_QUIET    ${CMAKE_REQUIRED_QUIET})
set(_SAVED_CMAKE_MESSAGE_LOG_LEVEL ${CMAKE_MESSAGE_LOG_LEVEL})
set(_SAVED_CMAKE_FIND_QUIETLY      ${CMAKE_FIND_QUIETLY})

set(CMAKE_REQUIRED_QUIET    ON     )
set(CMAKE_MESSAGE_LOG_LEVEL VERBOSE)
set(CMAKE_FIND_QUIETLY      ON     )

#----------------------------------------------
# Locked dependency versions
#----------------------------------------------

set(NFX_META_CONTAINERS_VERSION    "0.4.1")
set(NFX_META_CPU_VERSION           "0.1.4")
set(NFX_META_DATATYPES_VERSION     "0.4.0")
set(NFX_META_DATETIME_VERSION      "0.4.2")
set(NFX_META_HASHING_VERSION       "0.2.0")
set(NFX_META_JSON_VERSION          "1.3.4")
set(NFX_META_RESOURCE_VERSION      "1.1.0")
set(NFX_META_SERIALIZATION_VERSION "0.9.1")
set(NFX_META_STRINGBUILDER_VERSION "0.6.0")
set(NFX_META_STRINGUTILS_VERSION   "0.6.2")

#----------------------------------------------
# FetchContent dependencies
#----------------------------------------------

include(FetchContent)

if(DEFINED ENV{CI})
    set(FETCHCONTENT_UPDATES_DISCONNECTED OFF)
else()
    set(FETCHCONTENT_UPDATES_DISCONNECTED ON)
endif()
set(FETCHCONTENT_QUIET OFF)

# --- nfx-containers ---
if(NFX_META_ENABLE_CONTAINERS)
    find_package(nfx-containers QUIET)
    if(NOT nfx-containers_FOUND)
        set(NFX_CONTAINERS_BUILD_TESTS         ${NFX_META_BUILD_TESTS}         CACHE BOOL "Build tests"                 FORCE)
        set(NFX_CONTAINERS_BUILD_SAMPLES       ${NFX_META_BUILD_SAMPLES}       CACHE BOOL "Build samples"               FORCE)
        set(NFX_CONTAINERS_BUILD_BENCHMARKS    ${NFX_META_BUILD_BENCHMARKS}    CACHE BOOL "Build benchmarks"            FORCE)
        set(NFX_CONTAINERS_BUILD_DOCUMENTATION ${NFX_META_BUILD_DOCUMENTATION} CACHE BOOL "Build Doxygen documentation" FORCE)
        set(NFX_CONTAINERS_INSTALL_PROJECT     OFF                             CACHE BOOL "Install project"             FORCE)
        set(NFX_CONTAINERS_PACKAGE_SOURCE      OFF                             CACHE BOOL "Enable source package"       FORCE)
        set(NFX_CONTAINERS_PACKAGE_ARCHIVE     OFF                             CACHE BOOL "Enable archive package"      FORCE)
        set(NFX_CONTAINERS_PACKAGE_DEB         OFF                             CACHE BOOL "Enable DEB package"          FORCE)
        set(NFX_CONTAINERS_PACKAGE_RPM         OFF                             CACHE BOOL "Enable RPM package"          FORCE)
        set(NFX_CONTAINERS_PACKAGE_WIX         OFF                             CACHE BOOL "Enable WIX package"          FORCE)

        FetchContent_Declare(
            nfx-containers
                GIT_REPOSITORY https://github.com/nfx-libs/nfx-containers.git
                GIT_TAG        ${NFX_META_CONTAINERS_VERSION}
                GIT_SHALLOW    TRUE
        )
        FetchContent_MakeAvailable(nfx-containers)
    endif()
endif()

# --- nfx-cpu ---
if(NFX_META_ENABLE_CPU)
    find_package(nfx-cpu QUIET)
    if(NOT nfx-cpu_FOUND)
        set(NFX_CPU_BUILD_TESTS         ${NFX_META_BUILD_TESTS}         CACHE BOOL "Build tests"                 FORCE)
        set(NFX_CPU_BUILD_SAMPLES       ${NFX_META_BUILD_SAMPLES}       CACHE BOOL "Build samples"               FORCE)
        set(NFX_CPU_BUILD_BENCHMARKS    ${NFX_META_BUILD_BENCHMARKS}    CACHE BOOL "Build benchmarks"            FORCE)
        set(NFX_CPU_BUILD_DOCUMENTATION ${NFX_META_BUILD_DOCUMENTATION} CACHE BOOL "Build Doxygen documentation" FORCE)
        set(NFX_CPU_INSTALL_PROJECT     OFF                             CACHE BOOL "Install project"             FORCE)
        set(NFX_CPU_PACKAGE_SOURCE      OFF                             CACHE BOOL "Enable source package"       FORCE)
        set(NFX_CPU_PACKAGE_ARCHIVE     OFF                             CACHE BOOL "Enable archive package"      FORCE)
        set(NFX_CPU_PACKAGE_DEB         OFF                             CACHE BOOL "Enable DEB package"          FORCE)
        set(NFX_CPU_PACKAGE_RPM         OFF                             CACHE BOOL "Enable RPM package"          FORCE)
        set(NFX_CPU_PACKAGE_WIX         OFF                             CACHE BOOL "Enable WIX package"          FORCE)

        FetchContent_Declare(
            nfx-cpu
                GIT_REPOSITORY https://github.com/nfx-libs/nfx-cpu.git
                GIT_TAG        ${NFX_META_CPU_VERSION}
                GIT_SHALLOW    TRUE
        )
        FetchContent_MakeAvailable(nfx-cpu)
    endif()
endif()

# --- nfx-datatypes ---
if(NFX_META_ENABLE_DATATYPES)
    find_package(nfx-datatypes QUIET)
    if(NOT nfx-datatypes_FOUND)
        set(NFX_DATATYPES_BUILD_STATIC        ON                              CACHE BOOL "Build static library"              FORCE)
        set(NFX_DATATYPES_BUILD_SHARED        OFF                             CACHE BOOL "Build shared library"              FORCE)
        set(NFX_DATATYPES_BUILD_TESTS         ${NFX_META_BUILD_TESTS}         CACHE BOOL "Build tests"                       FORCE)
        set(NFX_DATATYPES_BUILD_SAMPLES       ${NFX_META_BUILD_SAMPLES}       CACHE BOOL "Build samples"                     FORCE)
        set(NFX_DATATYPES_BUILD_BENCHMARKS    ${NFX_META_BUILD_BENCHMARKS}    CACHE BOOL "Build benchmarks"                  FORCE)
        set(NFX_DATATYPES_BUILD_DOCUMENTATION ${NFX_META_BUILD_DOCUMENTATION} CACHE BOOL "Build Doxygen documentation"       FORCE)
        set(NFX_DATATYPES_INSTALL_PROJECT     OFF                             CACHE BOOL "Install project"                   FORCE)
        set(NFX_DATATYPES_PACKAGE_SOURCE      OFF                             CACHE BOOL "Enable source package generation"  FORCE)
        set(NFX_DATATYPES_PACKAGE_ARCHIVE     OFF                             CACHE BOOL "Enable TGZ/ZIP package generation" FORCE)
        set(NFX_DATATYPES_PACKAGE_DEB         OFF                             CACHE BOOL "Enable DEB package generation"     FORCE)
        set(NFX_DATATYPES_PACKAGE_RPM         OFF                             CACHE BOOL "Enable RPM package generation"     FORCE)
        set(NFX_DATATYPES_PACKAGE_WIX         OFF                             CACHE BOOL "Enable WiX MSI installer"          FORCE)

        FetchContent_Declare(
            nfx-datatypes
                GIT_REPOSITORY https://github.com/nfx-libs/nfx-datatypes.git
                GIT_TAG        ${NFX_META_DATATYPES_VERSION}
                GIT_SHALLOW    TRUE
        )
        FetchContent_MakeAvailable(nfx-datatypes)
    endif()
endif()

# --- nfx-datetime ---
if(NFX_META_ENABLE_DATETIME)
    find_package(nfx-datetime QUIET)
    if(NOT nfx-datetime_FOUND)
        set(NFX_DATETIME_BUILD_STATIC        ON                              CACHE BOOL "Build static library"              FORCE)
        set(NFX_DATETIME_BUILD_SHARED        OFF                             CACHE BOOL "Build shared library"              FORCE)
        set(NFX_DATETIME_BUILD_TESTS         ${NFX_META_BUILD_TESTS}         CACHE BOOL "Build tests"                       FORCE)
        set(NFX_DATETIME_BUILD_SAMPLES       ${NFX_META_BUILD_SAMPLES}       CACHE BOOL "Build samples"                     FORCE)
        set(NFX_DATETIME_BUILD_BENCHMARKS    ${NFX_META_BUILD_BENCHMARKS}    CACHE BOOL "Build benchmarks"                  FORCE)
        set(NFX_DATETIME_BUILD_DOCUMENTATION ${NFX_META_BUILD_DOCUMENTATION} CACHE BOOL "Build Doxygen documentation"       FORCE)
        set(NFX_DATETIME_INSTALL_PROJECT     OFF                             CACHE BOOL "Install project"                   FORCE)
        set(NFX_DATETIME_PACKAGE_SOURCE      OFF                             CACHE BOOL "Enable source package generation"  FORCE)
        set(NFX_DATETIME_PACKAGE_ARCHIVE     OFF                             CACHE BOOL "Enable TGZ/ZIP package generation" FORCE)
        set(NFX_DATETIME_PACKAGE_DEB         OFF                             CACHE BOOL "Enable DEB package generation"     FORCE)
        set(NFX_DATETIME_PACKAGE_RPM         OFF                             CACHE BOOL "Enable RPM package generation"     FORCE)
        set(NFX_DATETIME_PACKAGE_WIX         OFF                             CACHE BOOL "Enable WiX MSI installer"          FORCE)

        FetchContent_Declare(
            nfx-datetime
                GIT_REPOSITORY https://github.com/nfx-libs/nfx-datetime.git
                GIT_TAG        ${NFX_META_DATETIME_VERSION}
                GIT_SHALLOW    TRUE
        )
        FetchContent_MakeAvailable(nfx-datetime)
    endif()
endif()

# --- nfx-hashing ---
if(NFX_META_ENABLE_HASHING)
    find_package(nfx-hashing QUIET)
    if(NOT nfx-hashing_FOUND)
        set(NFX_HASHING_BUILD_TESTS         ${NFX_META_BUILD_TESTS}         CACHE BOOL "Build tests"                 FORCE)
        set(NFX_HASHING_BUILD_SAMPLES       ${NFX_META_BUILD_SAMPLES}       CACHE BOOL "Build samples"               FORCE)
        set(NFX_HASHING_BUILD_BENCHMARKS    ${NFX_META_BUILD_BENCHMARKS}    CACHE BOOL "Build benchmarks"            FORCE)
        set(NFX_HASHING_BUILD_DOCUMENTATION ${NFX_META_BUILD_DOCUMENTATION} CACHE BOOL "Build Doxygen documentation" FORCE)
        set(NFX_HASHING_INSTALL_PROJECT     OFF                             CACHE BOOL "Install project"             FORCE)
        set(NFX_HASHING_PACKAGE_SOURCE      OFF                             CACHE BOOL "Enable source package"       FORCE)
        set(NFX_HASHING_PACKAGE_ARCHIVE     OFF                             CACHE BOOL "Enable archive package"      FORCE)
        set(NFX_HASHING_PACKAGE_DEB         OFF                             CACHE BOOL "Enable DEB package"          FORCE)
        set(NFX_HASHING_PACKAGE_RPM         OFF                             CACHE BOOL "Enable RPM package"          FORCE)
        set(NFX_HASHING_PACKAGE_WIX         OFF                             CACHE BOOL "Enable WIX package"          FORCE)

        FetchContent_Declare(
            nfx-hashing
                GIT_REPOSITORY https://github.com/nfx-libs/nfx-hashing.git
                GIT_TAG        ${NFX_META_HASHING_VERSION}
                GIT_SHALLOW    TRUE
        )
        FetchContent_MakeAvailable(nfx-hashing)
    endif()
endif()

# --- nfx-json ---
if(NFX_META_ENABLE_JSON)
    find_package(nfx-json QUIET)
    if(NOT nfx-json_FOUND)
        set(NFX_JSON_BUILD_STATIC        ON                              CACHE BOOL "Build static library"        FORCE)
        set(NFX_JSON_BUILD_SHARED        OFF                             CACHE BOOL "Build shared library"        FORCE)
        set(NFX_JSON_BUILD_TESTS         ${NFX_META_BUILD_TESTS}         CACHE BOOL "Build tests"                 FORCE)
        set(NFX_JSON_BUILD_SAMPLES       ${NFX_META_BUILD_SAMPLES}       CACHE BOOL "Build samples"               FORCE)
        set(NFX_JSON_BUILD_BENCHMARKS    ${NFX_META_BUILD_BENCHMARKS}    CACHE BOOL "Build benchmarks"            FORCE)
        set(NFX_JSON_BUILD_DOCUMENTATION ${NFX_META_BUILD_DOCUMENTATION} CACHE BOOL "Build Doxygen documentation" FORCE)
        set(NFX_JSON_INSTALL_PROJECT     OFF                             CACHE BOOL "Install project"             FORCE)
        set(NFX_JSON_PACKAGE_SOURCE      OFF                             CACHE BOOL "Enable source package"       FORCE)
        set(NFX_JSON_PACKAGE_ARCHIVE     OFF                             CACHE BOOL "Enable archive package"      FORCE)
        set(NFX_JSON_PACKAGE_DEB         OFF                             CACHE BOOL "Enable DEB package"          FORCE)
        set(NFX_JSON_PACKAGE_RPM         OFF                             CACHE BOOL "Enable RPM package"          FORCE)
        set(NFX_JSON_PACKAGE_WIX         OFF                             CACHE BOOL "Enable WIX package"          FORCE)

        FetchContent_Declare(
            nfx-json
                GIT_REPOSITORY https://github.com/nfx-libs/nfx-json.git
                GIT_TAG        ${NFX_META_JSON_VERSION}
                GIT_SHALLOW    TRUE
        )
        FetchContent_MakeAvailable(nfx-json)
    endif()
endif()

# --- nfx-resource ---
if(NFX_META_ENABLE_RESOURCE)
    find_package(nfx-resource QUIET)
    if(NOT nfx-resource_FOUND)
        set(NFX_RESOURCE_INSTALL_PROJECT OFF CACHE BOOL "")
        set(NFX_RESOURCE_PACKAGE_SOURCE  OFF CACHE BOOL "")

        FetchContent_Declare(
            nfx-resource
                GIT_REPOSITORY https://github.com/nfx-libs/nfx-resource.git
                GIT_TAG        ${NFX_META_RESOURCE_VERSION}
                GIT_SHALLOW    TRUE
        )
        FetchContent_MakeAvailable(nfx-resource)
    endif()
endif()

# --- nfx-serialization ---
if(NFX_META_ENABLE_SERIALIZATION)
    find_package(nfx-serialization QUIET)
    if(NOT nfx-serialization_FOUND)
        set(NFX_SERIALIZATION_WITH_JSON             ${NFX_META_WITH_JSON_SERIALIZATION}        CACHE BOOL "Enable JSON support"         FORCE)
        set(NFX_SERIALIZATION_BUILD_TESTS           ${NFX_META_BUILD_TESTS}      CACHE BOOL "Build tests"                 FORCE)
        set(NFX_SERIALIZATION_BUILD_EXTENSION_TESTS OFF                          CACHE BOOL "Build extension tests"       FORCE)
        set(NFX_SERIALIZATION_BUILD_SAMPLES         ${NFX_META_BUILD_SAMPLES}    CACHE BOOL "Build samples"               FORCE)
        set(NFX_SERIALIZATION_BUILD_BENCHMARKS      ${NFX_META_BUILD_BENCHMARKS} CACHE BOOL "Build benchmarks"            FORCE)
        set(NFX_SERIALIZATION_BUILD_DOCUMENTATION   ${NFX_META_BUILD_DOCUMENTATION} CACHE BOOL "Build Doxygen documentation" FORCE)
        set(NFX_SERIALIZATION_INSTALL_PROJECT       OFF                          CACHE BOOL "Install project"             FORCE)
        set(NFX_SERIALIZATION_PACKAGE_SOURCE        OFF                          CACHE BOOL "Enable source package"       FORCE)
        set(NFX_SERIALIZATION_PACKAGE_ARCHIVE       OFF                          CACHE BOOL "Enable archive package"      FORCE)
        set(NFX_SERIALIZATION_PACKAGE_DEB           OFF                          CACHE BOOL "Enable DEB package"          FORCE)
        set(NFX_SERIALIZATION_PACKAGE_RPM           OFF                          CACHE BOOL "Enable RPM package"          FORCE)
        set(NFX_SERIALIZATION_PACKAGE_WIX           OFF                          CACHE BOOL "Enable WIX package"          FORCE)

        FetchContent_Declare(
            nfx-serialization
                GIT_REPOSITORY https://github.com/nfx-libs/nfx-serialization.git
                GIT_TAG        ${NFX_META_SERIALIZATION_VERSION}
                GIT_SHALLOW    TRUE
        )
        FetchContent_MakeAvailable(nfx-serialization)
    endif()
endif()

# --- nfx-stringbuilder ---
if(NFX_META_ENABLE_STRINGBUILDER)
    find_package(nfx-stringbuilder QUIET)
    if(NOT nfx-stringbuilder_FOUND)
        set(NFX_STRINGBUILDER_BUILD_STATIC        ON                              CACHE BOOL "Build static library"        FORCE)
        set(NFX_STRINGBUILDER_BUILD_SHARED        OFF                             CACHE BOOL "Build shared library"        FORCE)
        set(NFX_STRINGBUILDER_BUILD_TESTS         ${NFX_META_BUILD_TESTS}         CACHE BOOL "Build tests"                 FORCE)
        set(NFX_STRINGBUILDER_BUILD_SAMPLES       ${NFX_META_BUILD_SAMPLES}       CACHE BOOL "Build samples"               FORCE)
        set(NFX_STRINGBUILDER_BUILD_BENCHMARKS    ${NFX_META_BUILD_BENCHMARKS}    CACHE BOOL "Build benchmarks"            FORCE)
        set(NFX_STRINGBUILDER_BUILD_DOCUMENTATION ${NFX_META_BUILD_DOCUMENTATION} CACHE BOOL "Build Doxygen documentation" FORCE)
        set(NFX_STRINGBUILDER_INSTALL_PROJECT     OFF                             CACHE BOOL "Install project"             FORCE)
        set(NFX_STRINGBUILDER_PACKAGE_SOURCE      OFF                             CACHE BOOL "Enable source package"       FORCE)
        set(NFX_STRINGBUILDER_PACKAGE_ARCHIVE     OFF                             CACHE BOOL "Enable archive package"      FORCE)
        set(NFX_STRINGBUILDER_PACKAGE_DEB         OFF                             CACHE BOOL "Enable DEB package"          FORCE)
        set(NFX_STRINGBUILDER_PACKAGE_RPM         OFF                             CACHE BOOL "Enable RPM package"          FORCE)
        set(NFX_STRINGBUILDER_PACKAGE_WIX         OFF                             CACHE BOOL "Enable WIX package"          FORCE)

        FetchContent_Declare(
            nfx-stringbuilder
                GIT_REPOSITORY https://github.com/nfx-libs/nfx-stringbuilder.git
                GIT_TAG        ${NFX_META_STRINGBUILDER_VERSION}
                GIT_SHALLOW    TRUE
        )
        FetchContent_MakeAvailable(nfx-stringbuilder)
    endif()
endif()

# --- nfx-stringutils ---
if(NFX_META_ENABLE_STRINGUTILS)
    find_package(nfx-stringutils QUIET)
    if(NOT nfx-stringutils_FOUND)
        set(NFX_STRINGUTILS_BUILD_TESTS         ${NFX_META_BUILD_TESTS}         CACHE BOOL "Build tests"                 FORCE)
        set(NFX_STRINGUTILS_BUILD_SAMPLES       ${NFX_META_BUILD_SAMPLES}       CACHE BOOL "Build samples"               FORCE)
        set(NFX_STRINGUTILS_BUILD_BENCHMARKS    ${NFX_META_BUILD_BENCHMARKS}    CACHE BOOL "Build benchmarks"            FORCE)
        set(NFX_STRINGUTILS_BUILD_DOCUMENTATION ${NFX_META_BUILD_DOCUMENTATION} CACHE BOOL "Build Doxygen documentation" FORCE)
        set(NFX_STRINGUTILS_INSTALL_PROJECT     OFF                             CACHE BOOL "Install project"             FORCE)
        set(NFX_STRINGUTILS_PACKAGE_SOURCE      OFF                             CACHE BOOL "Enable source package"       FORCE)
        set(NFX_STRINGUTILS_PACKAGE_ARCHIVE     OFF                             CACHE BOOL "Enable archive package"      FORCE)
        set(NFX_STRINGUTILS_PACKAGE_DEB         OFF                             CACHE BOOL "Enable DEB package"          FORCE)
        set(NFX_STRINGUTILS_PACKAGE_RPM         OFF                             CACHE BOOL "Enable RPM package"          FORCE)
        set(NFX_STRINGUTILS_PACKAGE_WIX         OFF                             CACHE BOOL "Enable WIX package"          FORCE)

        FetchContent_Declare(
            nfx-stringutils
                GIT_REPOSITORY https://github.com/nfx-libs/nfx-stringutils.git
                GIT_TAG        ${NFX_META_STRINGUTILS_VERSION}
                GIT_SHALLOW    TRUE
        )
        FetchContent_MakeAvailable(nfx-stringutils)
    endif()
endif()

#----------------------------------------------
# Create interface library
#----------------------------------------------

add_library(nfx-meta INTERFACE)
add_library(nfx::meta ALIAS nfx-meta)

# Link only enabled libraries
if(NFX_META_ENABLE_CONTAINERS)
    target_link_libraries(nfx-meta INTERFACE nfx-containers::nfx-containers)
endif()
if(NFX_META_ENABLE_CPU)
    target_link_libraries(nfx-meta INTERFACE nfx-cpu::nfx-cpu)
endif()
if(NFX_META_ENABLE_DATATYPES)
    target_link_libraries(nfx-meta INTERFACE nfx-datatypes::static)
endif()
if(NFX_META_ENABLE_DATETIME)
    target_link_libraries(nfx-meta INTERFACE nfx-datetime::static)
endif()
if(NFX_META_ENABLE_HASHING)
    target_link_libraries(nfx-meta INTERFACE nfx-hashing::nfx-hashing)
endif()
if(NFX_META_ENABLE_JSON)
    target_link_libraries(nfx-meta INTERFACE nfx-json::static)
endif()
if(NFX_META_ENABLE_RESOURCE)
    target_link_libraries(nfx-meta INTERFACE nfx::resource)
endif()
if(NFX_META_ENABLE_SERIALIZATION)
    target_link_libraries(nfx-meta INTERFACE nfx-serialization::nfx-serialization)
endif()
if(NFX_META_ENABLE_STRINGBUILDER)
    target_link_libraries(nfx-meta INTERFACE nfx-stringbuilder::static)
endif()
if(NFX_META_ENABLE_STRINGUTILS)
    target_link_libraries(nfx-meta INTERFACE nfx-stringutils::nfx-stringutils)
endif()

#----------------------------------------------
# Installation (optional)
#----------------------------------------------

if(NFX_META_INSTALL_PROJECT)
    include(GNUInstallDirs)
    include(CMakePackageConfigHelpers)

    install(TARGETS nfx-meta
        EXPORT nfx-meta-targets
    )

    install(EXPORT nfx-meta-targets
        FILE nfx-meta-targets.cmake
        NAMESPACE nfx::
        DESTINATION ${CMAKE_INSTALL_LIBDIR}/cmake/nfx-meta
    )

    configure_package_config_file(
        ${CMAKE_CURRENT_SOURCE_DIR}/cmake/nfx-meta-config.cmake.in
        ${CMAKE_CURRENT_BINARY_DIR}/nfx-meta-config.cmake
        INSTALL_DESTINATION ${CMAKE_INSTALL_LIBDIR}/cmake/nfx-meta
    )

    write_basic_package_version_file(
        ${CMAKE_CURRENT_BINARY_DIR}/nfx-meta-config-version.cmake
        VERSION ${PROJECT_VERSION}
        COMPATIBILITY SameMajorVersion
    )

    install(FILES
        ${CMAKE_CURRENT_BINARY_DIR}/nfx-meta-config.cmake
        ${CMAKE_CURRENT_BINARY_DIR}/nfx-meta-config-version.cmake
        DESTINATION ${CMAKE_INSTALL_LIBDIR}/cmake/nfx-meta
    )
endif()

#----------------------------------------------
# Cleanup
#----------------------------------------------

set(CMAKE_REQUIRED_QUIET    ${_SAVED_CMAKE_REQUIRED_QUIET})
set(CMAKE_MESSAGE_LOG_LEVEL ${_SAVED_CMAKE_MESSAGE_LOG_LEVEL})
set(CMAKE_FIND_QUIETLY      ${_SAVED_CMAKE_FIND_QUIETLY})
