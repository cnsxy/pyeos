add_wast_executable(TARGET test_api_multi_index
  INCLUDE_FOLDERS "${STANDARD_INCLUDE_FOLDERS}"
  LIBRARIES libc++ libc eosiolib
  DESTINATION_FOLDER ${CMAKE_CURRENT_BINARY_DIR}
)

add_library(test_api_multi_index_native SHARED test_api_multi_index.cpp)

target_link_libraries(test_api_multi_index_native PRIVATE eosiolib_native)

target_include_directories(test_api_multi_index_native PRIVATE ${Boost_INCLUDE_DIR}
#   PRIVATE ${CMAKE_SOURCE_DIR}/contracts/libc++/upstream/include
#   PRIVATE ${CMAKE_SOURCE_DIR}/contracts/libc++/include/libc++/upstream/include
#   PRIVATE ${CMAKE_SOURCE_DIR}/contracts/libc++/musl/include/musl/upstream/include
#    PRIVATE ${CMAKE_SOURCE_DIR}/contracts/musl/upstream/include
    PRIVATE ${CMAKE_SOURCE_DIR}/externals/magic_get/include
     PRIVATE ${CMAKE_SOURCE_DIR}/contracts
)


