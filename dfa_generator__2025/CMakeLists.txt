cmake_minimum_required(VERSION 3.15)

project(dfa_generator__2025 LANGUAGES CXX)

# Create the executable
add_executable(dfa_generator__2025
    dfa_generator___part_impl.cpp
)

# Set C++ standard
set_PROPERTY(TARGET dfa_generator__2025 PROPERTY CXX_STANDARD 17)
set_PROPERTY(TARGET dfa_generator__2025 PROPERTY CXX_STANDARD_REQUIRED ON)

# Add compiler definitions
target_compile_definitions(dfa_generator__2025 PRIVATE
    _CRT_SECURE_NO_WARNINGS
    WIN32_LEAN_AND_MEAN
    USE_DFA_MINIMIZATION
)

# Set include directories - the built_src is at parent level
target_include_directories(dfa_generator__2025 PRIVATE
    ${CMAKE_CURRENT_SOURCE_DIR}/..
)

# Set working directory for debugging
# For Visual Studio
set_target_properties(dfa_generator__2025 PROPERTIES
    VS_DEBUGGER_WORKING_DIRECTORY "${CMAKE_CURRENT_SOURCE_DIR}"
)

# For VSCode (uses cwd from launch.json, but we set it here for reference)
set_target_properties(dfa_generator__2025 PROPERTIES
    RUNTIME_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/bin"
)

# Install target
install(TARGETS dfa_generator__2025
    RUNTIME DESTINATION bin
)

# Create output directories if they don't exist (custom command)
add_custom_command(TARGET dfa_generator__2025 POST_BUILD
    COMMAND ${CMAKE_COMMAND} -E make_directory "${CMAKE_CURRENT_SOURCE_DIR}/../built_doc"
    COMMAND ${CMAKE_COMMAND} -E make_directory "${CMAKE_CURRENT_SOURCE_DIR}/../built_doc/full_dfa"
    COMMENT "Creating output directories for DFA generator"
)
