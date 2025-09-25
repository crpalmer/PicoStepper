cmake_minimum_required(VERSION 3.12)

add_library(picostepper INTERFACE)

target_include_directories(picostepper INTERFACE
        ${CMAKE_CURRENT_LIST_DIR}/src
        ${CMAKE_CURRENT_LIST_DIR}/src/picostepper
        ${CMAKE_CURRENT_LIST_DIR}/src/picostepper/driver
)

target_sources(picostepper INTERFACE
        ${CMAKE_CURRENT_LIST_DIR}/src/picostepper/picostepper.c
)

target_link_libraries(picostepper INTERFACE
        pico_stdlib
        hardware_pio
        hardware_dma
)

# Compile the PIO-programs and include it into the project
pico_generate_pio_header(picostepper ${CMAKE_CURRENT_LIST_DIR}/src/picostepper/driver/four_wire.pio)
pico_generate_pio_header(picostepper ${CMAKE_CURRENT_LIST_DIR}/src/picostepper/driver/two_wire.pio)

