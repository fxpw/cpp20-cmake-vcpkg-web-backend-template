cmake_minimum_required(VERSION 2.8...3.28)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED True)

set(CMAKE_BUILD_TYPE ${BUILD_MODE})

set(CMAKE_TOOLCHAIN_FILE ${CMAKE_TOOLCHAIN_FILE} )
set(CMAKE_PREFIX_PATH vcpkg_installed/${VCPKG_TARGET_TRIPLET})

set(CMAKE_C_COMPILER ${CMAKE_C_COMPILER} )
set(CMAKE_CXX_COMPILER ${CMAKE_CXX_COMPILER})

project(${APP_NAME} VERSION 0.1.0 LANGUAGES C CXX)

include_directories(include)

file(GLOB_RECURSE SOURCES "src/*.cpp")

add_executable(${PROJECT_NAME} main.cpp ${SOURCES})

target_include_directories(${PROJECT_NAME} PRIVATE vcpkg_installed/${VCPKG_TARGET_TRIPLET}/include)

find_package(fmt REQUIRED)
find_package(CURL REQUIRED)
find_package(OpenSSL REQUIRED)
find_package(Drogon CONFIG REQUIRED)
target_link_libraries(${PROJECT_NAME} PRIVATE CURL::libcurl fmt::fmt OpenSSL::SSL OpenSSL::Crypto Drogon::Drogon)


