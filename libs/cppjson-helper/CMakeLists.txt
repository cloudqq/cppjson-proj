cmake_minimum_required(VERSION 3.17)

project(cppjson-helper)

configure_file(CMakeLists.txt.in jsoncpp-download/CMakeLists.txt)
execute_process(COMMAND ${CMAKE_COMMAND} -G "${CMAKE_GENERATOR}" .
        RESULT_VARIABLE result
        WORKING_DIRECTORY ${CMAKE_CURRENT_BINARY_DIR}/jsoncpp-download)
if(result)
    message(FATAL_ERROR "CMake step for jsoncpp failed: ${result}")
endif()

execute_process(COMMAND ${CMAKE_COMMAND} --build .
        RESULT_VARIABLE result
        WORKING_DIRECTORY ${CMAKE_CURRENT_BINARY_DIR}/jsoncpp-download)
if(result)
    message(FATAL_ERROR "Build step for jsoncpp failed: ${result}")
endif()

add_subdirectory(${CMAKE_CURRENT_BINARY_DIR}/jsoncpp-src
        ${CMAKE_CURRENT_BINARY_DIR}/jsoncpp-build
        EXCLUDE_FROM_ALL )


#message(${jsoncpp_INCLUDE_DIR})