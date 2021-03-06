set(PYTHON3 "LD_LIBRARY_PATH=${CMAKE_SOURCE_DIR}/externals/python;${CMAKE_SOURCE_DIR}/externals/python/dist/bin/python3")

add_custom_command(
    OUTPUT ${CMAKE_CURRENT_SOURCE_DIR}/vm_cpython.wrap.cpp
    COMMAND ${PYTHON3} -m cython --cplus ${CMAKE_CURRENT_SOURCE_DIR}/vm_cpython.pyx -o ${CMAKE_CURRENT_SOURCE_DIR}/vm_cpython.wrap.cpp
    DEPENDS ${CMAKE_CURRENT_SOURCE_DIR}/vm_cpython.pyx
)

add_library(vm_cpython SHARED 
            vm_cpython.wrap.cpp
            vm_cpython.cpp
            )

target_link_libraries(vm_cpython PRIVATE vmapi4python python3)

target_include_directories(vm_cpython PRIVATE ${Boost_INCLUDE_DIR}
#   PRIVATE ${CMAKE_SOURCE_DIR}/contracts/libc++/upstream/include
#   PRIVATE ${CMAKE_SOURCE_DIR}/contracts/libc++/include/libc++/upstream/include
#   PRIVATE ${CMAKE_SOURCE_DIR}/contracts/libc++/musl/include/musl/upstream/include
#    PRIVATE ${CMAKE_SOURCE_DIR}/contracts/musl/upstream/include
    PRIVATE ${CMAKE_SOURCE_DIR}/externals/magic_get/include
    PRIVATE ${CMAKE_BINARY_DIR}/libraries/appbase/include
    PUBLIC ${CMAKE_SOURCE_DIR}/libraries/chainbase/include
    PUBLIC ${CMAKE_SOURCE_DIR}/libraries/softfloat/source/include

    PUBLIC ${CMAKE_SOURCE_DIR}/externals/python/Include
    PUBLIC ${CMAKE_SOURCE_DIR}/externals/python

    PRIVATE ${CMAKE_BINARY_DIR}/libraries/fc/include
#    PRIVATE ${CMAKE_BINARY_DIR}/libraries/chain/include
    PRIVATE ${CMAKE_SOURCE_DIR}/contracts
)

