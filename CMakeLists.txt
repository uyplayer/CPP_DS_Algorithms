cmake_minimum_required (VERSION 3.12 FATAL_ERROR)

project(CPP_DS_Algorithms)




# c++ standard
set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)


# set vcpkg environment
set(VCPKG_ROOT "$ENV{vcpkg_root_dir}")
# vcpkg toolchain
SET(CMAKE_TOOLCHAIN_FILE "${VCPKG_ROOT}/scripts/buildsystems/vcpkg.cmake")


# check system information
if (WIN32)
    # windows
    # find package in Windows path
    include_directories("${VCPKG_ROOT}/installed/x64-windows/include")
    link_directories("${VCPKG_ROOT}/installed/x64-windows/lib")
    list(APPEND CMAKE_PREFIX_PATH "${VCPKG_ROOT}/installed/x64-windows")
    # msg log
    message("------------- System version is Windows -------------")
    message("-- vcpkg_DIR: ${VCPKG_ROOT}")
    message("-- vcpkg.cmake dir: ${CMAKE_TOOLCHAIN_FILE}")
    message("-- vcpkg header: ${VCPKG_ROOT}/installed/x64-windows/include")
elseif(UNIX)
    # Linux and macOS msg
    if(APPLE)
        message("------------- System version is macOS -------------")
    else()
        message("------------- System version is Linux -------------")
    endif()
endif()



# add common/include/lib/third_party
include_directories(${PROJECT_SOURCE_DIR}/include)
link_directories(${PROJECT_SOURCE_DIR}/third_party)

# third party framework
find_package(plog REQUIRED)


# add sub dirs
add_subdirectory(cpp_ds_algo_book)
add_subdirectory(tests)

