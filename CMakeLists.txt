cmake_minimum_required(VERSION 3.5)
project(SDK)

include(ClangExternalProject.txt)

set(CMAKE_SYSTEM_NAME WebAssembly)
set(WASM_ROOT "${CMAKE_BINARY_DIR}/EosioClang-prefix/src/EosioClang-build/bin")

set(CMAKE_C_COMPILER "${WASM_ROOT}/clang")
set(CMAKE_CXX_COMPILER "${WASM_ROOT}/clang++")
set(TRIPLE "wasm32-unknown-unknown-elf")

set(CMAKE_C_COMPILER_TARGET ${TRIPLE})
set(CMAKE_CXX_COMPILER_TARGET ${TRIPLE})
set(CMAKE_C_FLAGS "--target=wasm32 -O3 -nostdlib -nostdlibinc -ffreestanding")
set(CMAKE_CXX_FLAGS "-std=c++14 -O3 --target=wasm32 -nostdlib -ffreestanding -fno-rtti -fno-exceptions")

set(WASM_LINKER "${WASM_ROOT}/wasm-ld")
set(WASM_IMPORTS "${CMAKE_CURRENT_SOURCE_DIR}/eosio.imports")

set(CMAKE_CXX_LINK_EXECUTABLE "${WASM_LINKER} <LINK_FLAGS> <OBJECTS> -o <TARGET> <LINK_LIBRARIES>")

set(CMAKE_AR "${WASM_ROOT}/llvm-ar" CACHE PATH "ar" FORCE)
set(CMAKE_RANLIB "${WASM_ROOT}/llvm-ranlib" CACHE PATH "ranlib" FORCE)

set(CMAKE_EXE_LINKER_FLAGS "--allow-undefined-file=${WASM_IMPORTS} -e apply -stack-first")

set(BOOST_INSTALL_DIR "/usr/local/include" CACHE STRING "Boost include directory")

set(STANDARD_INCLUDES "${CMAKE_CURRENT_SOURCE_DIR}/libc++/upstream/include" "${CMAKE_CURRENT_SOURCE_DIR}/musl/upstream/include"
                      "${BOOST_INSTALL_DIR}")

set(STANDARD_LIBS c++ c eosio)

add_subdirectory(libraries)
#add_subdirectory(musl)
#add_subdirectory(libc++)
#add_subdirectory(eosiolib)

add_subdirectory(hello)
#add_subdirectory(exchange)
