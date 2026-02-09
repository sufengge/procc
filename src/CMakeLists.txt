cmake_minimum_required(VERSION 3.10)

project(procc LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# 头文件目录
include_directories(${CMAKE_SOURCE_DIR}/../include)

# 可执行文件输出到 bin
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/../bin)

add_executable(procc
        main.cpp
        Basic_Grammar.cpp
        constant.cpp
        data_type.cpp
        exegesis.cpp
        variable_scope.cpp
        variable_type.cpp
)
