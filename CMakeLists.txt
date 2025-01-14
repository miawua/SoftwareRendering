cmake_minimum_required (VERSION 3.18)
project (renderer)

set(HEADERS
    header/tgaimage.h
    header/global.h
    header/algebra.h
    header/model.h
    header/shader.h
    header/rasterization.h
)
set(SOURCES
    src/main.cpp
    src/tgaimage.cpp
    src/model.cpp
    src/shader.cpp
    src/rasterization.cpp
)

include(CheckCXXCompilerFlag)

function(enable_cxx_compiler_flag_if_supported flag)
    string(FIND "${CMAKE_CXX_FLAGS}" "${flag}" flag_already_set)
    if(flag_already_set EQUAL -1)
        check_cxx_compiler_flag("${flag}" flag_supported)
        if(flag_supported)
            set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} ${flag}" PARENT_SCOPE)
        endif()
        unset(flag_supported CACHE)
    endif()
endfunction()

enable_cxx_compiler_flag_if_supported("-Wall")
enable_cxx_compiler_flag_if_supported("-Wextra")
enable_cxx_compiler_flag_if_supported("-pedantic")
enable_cxx_compiler_flag_if_supported("-std=c++17")
enable_cxx_compiler_flag_if_supported("-O3")
# enable_cxx_compiler_flag_if_supported("-fopenmp")

include_directories(${CMAKE_CURRENT_LIST_DIR}/header)

add_executable(${PROJECT_NAME} ${HEADERS} ${SOURCES})