# the minimum version of CMake.
cmake_minimum_required(VERSION 3.5.0)
project(p7zip)

set(NATIVERENDER_ROOT_PATH ${CMAKE_CURRENT_SOURCE_DIR})

if(DEFINED PACKAGE_FIND_FILE)
    include(${PACKAGE_FIND_FILE})
endif()

include_directories(${NATIVERENDER_ROOT_PATH}
                    ${NATIVERENDER_ROOT_PATH}/include)

add_library(entry SHARED napi_init.cpp)
target_link_libraries(entry PUBLIC libace_napi.z.so)
add_subdirectory(p7zip-17.05/CPP/7zip/CMAKE/7za)
target_compile_options(7za PRIVATE
    -Wno-c++11-narrowing -Wno-increment-bool -w -fvisibility=hidden -fvisibility-inlines-hidden
    -Ofast)