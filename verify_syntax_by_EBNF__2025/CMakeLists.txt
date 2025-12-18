# Verify Syntax by EBNF 2025 Project

add_executable(verify_syntax_by_EBNF__2025
    one_file__x86_Debug.cpp
)

target_compile_definitions(verify_syntax_by_EBNF__2025 PRIVATE
    _CRT_SECURE_NO_WARNINGS
)

# Set working directory for debugging (Visual Studio)
set_target_properties(verify_syntax_by_EBNF__2025 PROPERTIES
    VS_DEBUGGER_WORKING_DIRECTORY "${CMAKE_CURRENT_SOURCE_DIR}"
)

# Install target
install(TARGETS verify_syntax_by_EBNF__2025
    RUNTIME DESTINATION bin
)
