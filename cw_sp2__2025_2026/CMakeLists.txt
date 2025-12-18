# CW SP2 2025-2026 Project

# Collect all source files
file(GLOB_RECURSE CW_SP2_SOURCES
    "src/implementation/cli/*.cpp"
    "src/implementation/generator/*.cpp"
    "src/implementation/lexica/*.cpp"
    "src/implementation/preparer/*.cpp"
    "src/implementation/semantics/*.cpp"
    "src/implementation/syntax/*.cpp"
    "cw.cpp"
)

# Collect all header files
file(GLOB_RECURSE CW_SP2_HEADERS
    "src/include/*.h"
)

add_executable(cw_sp2__2025_2026
    ${CW_SP2_SOURCES}
    ${CW_SP2_HEADERS}
)

target_include_directories(cw_sp2__2025_2026 PRIVATE
    ${CMAKE_CURRENT_SOURCE_DIR}/src/include
    ${CMAKE_CURRENT_SOURCE_DIR}/src/include/cli
    ${CMAKE_CURRENT_SOURCE_DIR}/src/include/generator
    ${CMAKE_CURRENT_SOURCE_DIR}/src/include/lexica
    ${CMAKE_CURRENT_SOURCE_DIR}/src/include/preparer
    ${CMAKE_CURRENT_SOURCE_DIR}/src/include/semantics
    ${CMAKE_CURRENT_SOURCE_DIR}/src/include/syntax
)

target_compile_definitions(cw_sp2__2025_2026 PRIVATE
    _CRT_SECURE_NO_WARNINGS
)

# Set working directory for debugging (Visual Studio)
set_target_properties(cw_sp2__2025_2026 PROPERTIES
    VS_DEBUGGER_WORKING_DIRECTORY "${CMAKE_CURRENT_SOURCE_DIR}"
)

# Install target
install(TARGETS cw_sp2__2025_2026
    RUNTIME DESTINATION bin
)
