cmake_minimum_required(VERSION 3.8)

set(PROJECT_NAME do_time)
project( ${PROJECT_NAME} )

add_library(
    ${PROJECT_NAME} 
    STATIC

    src/do_time.cpp
)

target_include_directories(
    ${PROJECT_NAME}
    PUBLIC
        $<INSTALL_INTERFACE:include>    
        $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
)

target_compile_features(${PROJECT_NAME} PUBLIC cxx_std_11)

if(BUILD_EXAMPLES)

    set(
        EXAMPLE_NAMES 
        eg00_basic
    )
    foreach(EXAMPLE_NAME IN LISTS EXAMPLE_NAMES)
        add_executable(${PROJECT_NAME}_${EXAMPLE_NAME} src/examples/${EXAMPLE_NAME}.cpp)
        target_link_libraries(${PROJECT_NAME}_${EXAMPLE_NAME} ${PROJECT_NAME})
    endforeach()

endif()