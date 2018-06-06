#file(GLOB ABI_FILES "*.abi")
#configure_file("${ABI_FILES}" "${CMAKE_CURRENT_BINARY_DIR}" COPYONLY)

add_executable( hello hello.cpp )

target_include_directories(hello PUBLIC ${STANDARD_INCLUDES})
target_link_libraries(hello PRIVATE c c++ eosio)
