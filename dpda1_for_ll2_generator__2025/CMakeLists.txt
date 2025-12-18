# DPDA1 for LL2 Generator 2025 Project

add_executable(dpda1_for_ll2_generator__2025
    dpda1_for_ll2_generator__2025.cpp
)

target_compile_definitions(dpda1_for_ll2_generator__2025 PRIVATE
    _CRT_SECURE_NO_WARNINGS
)

# Set working directory for debugging (Visual Studio)
set_target_properties(dpda1_for_ll2_generator__2025 PROPERTIES
    VS_DEBUGGER_WORKING_DIRECTORY "${CMAKE_CURRENT_SOURCE_DIR}"
)

# Install target
install(TARGETS dpda1_for_ll2_generator__2025
    RUNTIME DESTINATION bin
)
