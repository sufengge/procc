add_library(procc_lib
        Basic_Grammar.cpp
        constant.cpp
        data_type.cpp
        exegesis.cpp
        variable_scope.cpp
        variable_type.cpp
)

target_include_directories(procc_lib PUBLIC ${CMAKE_SOURCE_DIR}/include)
add_executable(procc main.cpp)
target_link_libraries(procc PRIVATE procc_lib)
target_compile_options(procc PRIVATE -Wall -O2)
target_compile_options(procc_lib PRIVATE -Wall -O2)
