# Image Pattern Generator Project

add_executable(image_pattern_generator
    source.c
    AsmForCode.c
)

set_target_properties(image_pattern_generator PROPERTIES
    LINKER_LANGUAGE C
)

target_compile_definitions(image_pattern_generator PRIVATE
    _CRT_SECURE_NO_WARNINGS
)

# Set working directory for debugging (Visual Studio)
set_target_properties(image_pattern_generator PROPERTIES
    VS_DEBUGGER_WORKING_DIRECTORY "${CMAKE_CURRENT_SOURCE_DIR}"
)

# Install target
install(TARGETS image_pattern_generator
    RUNTIME DESTINATION bin
)
