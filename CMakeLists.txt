cmake_minimum_required(VERSION 3.12)

# Pull in SDK (must be before project)
include($ENV{PICO_SDK_PATH}/external/pico_sdk_import.cmake)
include($ENV{PICO_EXTRAS_PATH}/external/pico_extras_import.cmake)
include($ENV{PIMORONI_PICO_PATH}/pimoroni_pico_import.cmake)

project(pico_life C CXX ASM)
set(CMAKE_C_STANDARD 11)
set(CMAKE_CXX_STANDARD 17)

# Avoid issues with old SDK version and check it explicitly
if (PICO_SDK_VERSION_STRING VERSION_LESS "1.3.0")
    message(FATAL_ERROR "Raspberry Pi Pico SDK version 1.3.0 (or later) required. Your version is ${PICO_SDK_VERSION_STRING}")
endif()

# Initialize the SDK
pico_sdk_init()

# Recommended options for Pico
add_compile_options(-Wall
    -Wno-format          # int != int32_t as far as the compiler is concerned because gcc has int32_t as long int
    -Wno-unused-function # we have some for the docs that aren't called
)

if (CMAKE_C_COMPILER_ID STREQUAL "GNU")
    add_compile_options(-Wno-maybe-uninitialized)
endif()

# Main program definition
add_executable(pico_life
    src/main.cpp
)

target_include_directories(pico_life PRIVATE
    ${CMAKE_CURRENT_LIST_DIR}/src
)

# Include required libraries from Pimoroni SDK
include($ENV{PIMORONI_PICO_PATH}/libraries/pico_graphics/pico_graphics.cmake)
include($ENV{PIMORONI_PICO_PATH}/libraries/cosmic_unicorn/cosmic_unicorn.cmake)

# Pull in everything together
target_link_libraries(pico_life
    pico_stdlib
    hardware_pio
    hardware_adc
    hardware_dma
    pico_graphics
    cosmic_unicorn
)
pico_enable_stdio_usb(pico_life 1)

# create map/bin/hex file etc.
pico_add_extra_outputs(pico_life)
