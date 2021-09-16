cmake_minimum_required(VERSION 3.16)

project(connect)

include(${CMAKE_CURRENT_SOURCE_DIR}/cmake/FindWayland.cmake)

function(dump_cmake_variables)
    get_cmake_property(_variableNames VARIABLES)
    list (SORT _variableNames)
    foreach (_variableName ${_variableNames})
        if (ARGV0)
            unset(MATCHED)
            string(REGEX MATCH ${ARGV0} MATCHED ${_variableName})
            if (NOT MATCHED)
                continue()
            endif()
        endif()
        message(STATUS "${_variableName}=${${_variableName}}")
    endforeach()
endfunction()

include_directories(WAYLAND_CLIENT_INCLUDE_DIR)

add_executable(${PROJECT_NAME} connect.c)

target_link_libraries(${PROJECT_NAME} PUBLIC ${WAYLAND_CLIENT_LIBRARIES})