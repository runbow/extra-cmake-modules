project(extra-cmake-modules)
cmake_minimum_required(VERSION 2.8.12)

# order is important (install dirs before cmake settings)!
set(all_kde_modules
    KDEInstallDirs
    KDECMakeSettings
)

set(ECM_KDE_MODULE_DIR ${CMAKE_CURRENT_SOURCE_DIR}/../../kde-modules)
set(ECM_MODULE_DIR ${CMAKE_CURRENT_SOURCE_DIR}/../../modules)
set(CMAKE_MODULE_PATH "${ECM_KDE_MODULE_DIR}" "${ECM_MODULE_DIR}")

foreach(module ${all_kde_modules})
    message(STATUS "module: ${module}")
    include("${module}")
endforeach()

_repository_name(name "${CMAKE_CURRENT_SOURCE_DIR}/../../")
if (NOT ${name} STREQUAL "extra-cmake-modules")
    message(FATAL_ERROR "Wrong repository name: ${name}, should be 'extra-cmake-modules'")
endif()
add_executable(dummy ../ExecuteKDEModules/main.c)

if(NOT TARGET fetch-translations)
    message(FATAL_ERROR "should have a fetch-translations target")
endif()
