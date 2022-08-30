add_executable(flash_nuke
        nuke.c
        )

target_link_libraries(flash_nuke
        pico_stdlib
        hardware_flash
        )

if ("${CMAKE_GENERATOR}" STREQUAL "IAR Embedded Workbench for Arm")
# No support for binary type "no_flash" with IAR, so use "copy_to_ram" instead.
pico_set_binary_type(flash_nuke copy_to_ram)
else()
# It doesn't make sense to run this program from flash. Always build a
# RAM-only binary.
pico_set_binary_type(flash_nuke no_flash)
endif()

pico_add_extra_outputs(flash_nuke)

# add url via pico_set_program_url
example_auto_set_url(flash_nuke)

