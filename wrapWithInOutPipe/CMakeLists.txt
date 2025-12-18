# Wrap With InOutPipe Project

add_executable(wrapWithInOutPipe
    wrapper.c
)

set_target_properties(wrapWithInOutPipe PROPERTIES
    LINKER_LANGUAGE C
)

target_compile_definitions(wrapWithInOutPipe PRIVATE
    _CRT_SECURE_NO_WARNINGS
)

# Set working directory for debugging (Visual Studio)
set_target_properties(wrapWithInOutPipe PROPERTIES
    VS_DEBUGGER_WORKING_DIRECTORY "${CMAKE_CURRENT_SOURCE_DIR}"
)

# Install target
install(TARGETS wrapWithInOutPipe
    RUNTIME DESTINATION bin
)
