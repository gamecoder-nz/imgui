cmake_minimum_required(VERSION 3.23)
project(Imgui)
set(CMAKE_CONFIGURATION_TYPES Debug;Release)

file(GLOB SRC *.cpp)
file(GLOB BACKEND_SRC backends/imgui_impl_bgfx.cpp backends/imgui_impl_sdl2.cpp)

add_library(Imgui ${SRC} ${BACKEND_SRC})

include_directories(./)
include_directories(../bgfx/include)
include_directories(../bx/include)
include_directories(../sdl/include)

if(MSVC)
    include_directories(../bx/include/compat/msvc)
    target_compile_options(Imgui PUBLIC "/Zc:__cplusplus")
endif()
set(CMAKE_CXX_FLAGS_DEBUG "${CMAKE_CXX_FLAGS_DEBUG} -DBX_CONFIG_DEBUG=1")
set(CMAKE_CXX_FLAGS_RELEASE "${CMAKE_CXX_FLAGS_DEBUG} -DBX_CONFIG_DEBUG=0")
