file(GLOB CRYPT_SOURCES  "upstream/src/crypt/*.c")
file(GLOB CTYPE_SOURCES  "upstream/src/ctype/*.c")
file(GLOB ENV_SOURCES  "upstream/src/env/*.c")
file(GLOB ERRNO_SOURCES  "upstream/src/errno/*.c")
file(GLOB EXIT_SOURCES  "upstream/src/exit/*.c")
file(GLOB LOCALE_SOURCES "upstream/src/locale/*.c")
file(GLOB MATH_SOURCES  "upstream/src/math/*.c")
file(GLOB MBYTE_SOURCES  "upstream/src/multibyte/*.c")
file(GLOB MISC_SOURCES "upstream/src/misc/*.c")
file(GLOB SEARCH_SOURCES "upstream/src/search/*.c")
file(GLOB STDIO_SOURCES "upstream/src/stdio/*.c")
file(GLOB STDLIB_SOURCES "upstream/src/stdlib/*.c")
file(GLOB STRING_SOURCES "upstream/src/string/*.c")
#file(GLOB TIME_SOURCES "upstream/src/time/*.c")
file(GLOB THREAD_SOURCES "upstream/src/thread/*.c") #only for __lock __unlock

set(INTERNAL_SOURCES upstream/src/internal/floatscan.c upstream/src/internal/intscan.c upstream/src/internal/shgetc.c upstream/src/internal/libc.c)

set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -Wno-everything")

file(GLOB HEADERS "${CMAKE_CURRENT_SOURCE_DIR}/upstream/include/*.h"
                  "${CMAKE_CURRENT_SOURCE_DIR}/upstream/src/internal/*.h"
                  "${CMAKE_CURRENT_SOURCE_DIR}/upstream/arch/eos/*.h"
)

add_library(c 
            ${CRYPT_SOURCES} 
            ${CTYPE_SOURCES}
            ${ENV_SOURCES}
            ${ERRNO_SOURCES}
            ${EXIT_SOURCES}
            ${INTERNAL_SOURCES}
            ${LOCALE_SOURCES}
            ${MATH_SOURCES}
            ${MBYTE_SOURCES}
            ${MISC_SOURCES}
            ${SEARCH_SOURCES}
            ${STDIO_SOURCES}
            ${STDLIB_SOURCES}
            ${STRING_SOURCES}
            ${TIME_SOURCES}
            ${THREAD_SOURCES}
            ${HEADERS})

target_include_directories(c
                           PUBLIC "${CMAKE_CURRENT_SOURCE_DIR}/upstream/include"
                                  "${CMAKE_CURRENT_SOURCE_DIR}/upstream/src/internal"
                                  "${CMAKE_CURRENT_SOURCE_DIR}/upstream/src/crypt"
                                  "${CMAKE_CURRENT_SOURCE_DIR}/upstream/arch/eos/"
                                  "${CMAKE_CURRENT_SOURCE_DIR}/../")
