cmake_minimum_required(VERSION 3.2)

project(asio_usage)

include(${CMAKE_BINARY_DIR}/conanbuildinfo.cmake) 
conan_basic_setup(TARGETS)

add_executable(server async_tcp_echo_server.cpp)
add_executable(client blocking_tcp_echo_client.cpp)

set_target_properties(
	server
    client
PROPERTIES
    CXX_STANDARD 20
    CXX_STANDARD_REQUIRED ON
)

target_link_libraries(server PRIVATE
    CONAN_PKG::asio
)
target_link_libraries(client PRIVATE
    CONAN_PKG::asio
)

if (MSVC)
    target_compile_options(server PRIVATE
        /W4 /MD
    )
    target_compile_options(client PRIVATE
        /W4 /MD
    )

else ()
    target_compile_options(server PRIVATE
        -Wall -Wextra -pedantic -Werror
    )
    target_compile_options(client PRIVATE
        -Wall -Wextra -pedantic -Werror
    )
endif()


