cmake_minimum_required(VERSION 3.10)
project(procc LANGUAGES CXX)

# 使用 C++11
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# 输出目录都在构建目录里
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)

# --------------------------
# 自动拷贝etc，每次 build 都检测更新
# --------------------------
add_custom_command(
        OUTPUT ${CMAKE_BINARY_DIR}/etc
        COMMAND ${CMAKE_COMMAND} -E copy_directory
        ${CMAKE_SOURCE_DIR}/etc ${CMAKE_BINARY_DIR}/etc
        DEPENDS ${CMAKE_SOURCE_DIR}/etc
        COMMENT "Copying etc/ to build directory"
)

add_custom_target(copy_resources ALL
        DEPENDS ${CMAKE_BINARY_DIR}/etc
)

# --------------------------
# 自动生成构建信息文件
# --------------------------
set(VERSION_FILE ${CMAKE_BINARY_DIR}/build_info.txt)
add_custom_command(
        OUTPUT ${VERSION_FILE}
        COMMAND ${CMAKE_COMMAND} -E echo "Project: procc" > ${VERSION_FILE}
        COMMAND ${CMAKE_COMMAND} -E echo "Build Type: ${CMAKE_BUILD_TYPE}" >> ${VERSION_FILE}
        COMMAND ${CMAKE_COMMAND} -E echo "Build Dir: ${CMAKE_BINARY_DIR}" >> ${VERSION_FILE}
        COMMENT "Generating build info file"
)

add_custom_target(generate_build_info ALL
        DEPENDS ${VERSION_FILE}
)

# 包含 src 下的 CMakeLists.txt
add_subdirectory(src)

# 让 procc 可执行文件依赖 copy_resources 和 build_info
add_dependencies(procc copy_resources generate_build_info)
