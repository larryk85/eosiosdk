cmake_minimum_required(VERSION 3.5)
project(SDK)

add_subdirectory(cppeos)

set(CMAKE_SYSTEM_NAME WebAssembly)
set(triple "wasm32-unknown-unknown-elf")
set(CMAKE_C_COMPILER "${CMAKE_BINARY_DIR}/cppeos/bin/clang")
set(CMAKE_CXX_COMPILER "${CMAKE_BINARY_DIR}/cppeos/bin/clang++")
set(CMAKE_C_COMPILER_TARGET ${triple})
set(CMAKE_CXX_COMPILER_TARGET ${triple})
set(CMAKE_C_FLAGS "--target=wasm32 -nostdlibinc -ffreestanding")
set(CMAKE_CXX_FLAGS "-std=c++14 --target=wasm32 -nostdlibinc -ffreestanding -fno-rtti -fno-exceptions")
set(CMAKE_LINKER "${CMAKE_BINARY_DIR}/cppeos/bin/wasm-ld" CACHE STRING "Linker")

add_subdirectory(musl)
add_subdirectory(libc++)
add_subdirectory(eosiolib)

set(BOOST_INSTALL_DIR "/usr/local/include" CACHE STRING "Boost include directory")

set(STANDARD_INCLUDES "${CMAKE_CURRENT_SOURCE_DIR}/musl/upstream/include"
                      "${CMAKE_CURRENT_SOURCE_DIR}/libc++/upstream/include"
                      "${BOOST_INSTALL_DIR}")

add_subdirectory(hello)
